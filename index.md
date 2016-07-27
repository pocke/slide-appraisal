# Appraisalを<br>使ってみた話

2016/07/27 [Shinjuku.rb #39](https://shinjukurb.doorkeeper.jp/events/49357)

---

# だれこれ

---

<img style="width: 20%; border-radius: 50%" alt="ほにゃー" src="pocke.svg">

## Masataka Kuwabara (a.k.a. pocke)

- Actcat Inc.
- PORT Inc.


---

# こんなこと<br>ありませんか?



---



Gemのテストをする際

複数の依存バージョンでテストを行いたい

---


# たとえば


---

## mi

https://github.com/pocke/mi

鋭意開発中


---



Rails用

マイグレーションファイルジェネレータ



```sh
$ bin/rails g mi users +email:string
```

↓

```ruby
class AddEmailToUsers < ActiveRecord::Migration
	def change
		add_column :users, :email, :string
	end
end
```

---

Rails 4系、5系両方サポートしたい!

↓

4系、5系両方でテストしたい!

↓

どうやろう…

---

## そこで

---


# Appraisal

---



## Appraisal


> A Ruby library for testing your library against different versions of dependencies.
>
> https://github.com/thoughtbot/appraisal

みんな大好きthoughtbot製


---

# こう使う

---

### gemfileに依存を書いて…

```
spec.add_development_dependency 'appraisal'
```


---

### `Appraisals`というファイルを作成して…

```ruby
appraise 'rails40' do
  gem 'rails', '~> 4.0.0'
end

appraise 'rails41' do
  gem 'rails', '~> 4.1.0'
end

appraise 'rails42' do
  gem 'rails', '~> 4.2.0'
end

appraise 'rails50' do
  gem 'rails', '~> 5.0.0'
end
```

---

### インストール!

```sh
$ appraisal install
```

---

### テストを実行!

```sh
$ bundle exec appraisal rspec
# 4つのRailsのバージョンでテストが実行されるデモ
```


---

# まとめ

---

ちょろっとコードを書けば

依存Gemのバージョンを切り替えてテストが出来る!


---

### 詳しくは

[Rails 4, 5 両方対応のGemをTravisでテストした話 - pockestrap](http://pocke.hatenablog.com/entry/2016/07/11/105900)


---

# Discuss

---

- テストに使っている便利Gemある?
  - Appraisalみたいなテスト環境系
  - rspec-power_assertみたいな便利テスト系

- 複数RubyバージョンをサポートするGemの開発
  - guardを使うと2.2未満使えない問題
  - 2.2.2未満はActive Support 5系使えない問題
  - 個人的に知りたい!
