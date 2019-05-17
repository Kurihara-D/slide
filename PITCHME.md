## RubyKaigi2019  
### @福岡  

---

## Agenda
- PatternMatching
- RubyKaigiについての感想

---
## pattern matching is...?

- Extend case expression for pattern matching

```ruby
case [1, [2, 3, 4]]
in [1, [2, a, b]]
  puts a #=> 3
  puts b #=> 4
end
```
---
## 特徴
- 構造をチェックして、マッチした際に変数にデータがバインドされる
- 一致するパターンが見つかるまで上から順番に実行される
- 一致するパターンがない且つelse句がない場合はNoMatchingPatternErrorがraiseされる
---
## 既存の変数をパターンとして扱いたいよね
---
## こんな感じ？
```ruby
a = 2
case 1
in a
  puts a
end
#=> ???
```
---
# #=> 1
---
## Use ^
```ruby
a = 2
case 1
in ^a
  puts a
end
#=> NoMatchingPatternError
```
Note:
- Elixirのパターンマッチングのようにピン演算子を使えばcase内のスコープに入れられます
---
## 使いどころ(?)
- ArrayやHashの構造チェック(順番や型もチェックしてくれる)
- JSONのパターンマッチ

--- 
## Array
```rubyは良さげ
case [1, 2, 3]
in [3, 2, 1]
in [2, 3, 1]
in [1, 3, 2]
end
#=> NoMatchingPatternError

```

---
## JSON
```json
{
  "foo": "bar",
  "items": [
    {
      "key1": 1,
      "key2": 2
    }
  ]
}
```

```ruby
json = JSON.parse(json, symbolize_names: true)
case json
in {foo: "bar", items: [{key1: 1, key2: var}]}
  puts var #=> 2
end
```
Note:
- マッチしたときに値を取り出して何かするときとか、そういうときに使えそう

---
### PatternMatchingまとめ
- APIのレスポンス(JSON)を処理する時とか使えそう
- HashやArrayの構造をチェックした上でそれらの値を扱う場面では簡潔にかける
Note:
- 他にも使いどころはあると思うけど
---
### まとめ
- Rubyのコア部分の話がほぼメイン
- Rails6で導入されるオートローダー`ZeitWerk`は期待
- 静的型チェックは賛否両論ある(Stripe社のSorbetは良さげ)

Note:
- Rubyぽくはないよね・・・・
---

#### 告知
- 本日20:00~
  - ログの取扱についての勉強会
- 5/23(木) 19:00~
  - Vue, React, Elm 品評会
Note:
- team-kでは定期的に勉強会を開催しているので興味がある方は#dev_comi(ch)に参加してください！
