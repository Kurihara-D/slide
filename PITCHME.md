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
## ざっくり特徴
- 多重代入のように見えるが構造をチェックしている
- 一致するパターンが見つかるまで上から順番に実行される
  - 一致するパターンがない場合はNoMatchingPatternError
---
## 既存の変数をパターンとして扱いたいよね
---
## こんな感じ？
```ruby
a = 2
case 1
in a
  puts a #=> ???
end
```
---
# #=> 1
---
## Like Elixir
- use ^  

```ruby
a = 2
case 1
in ^a
  puts a
end
#=> NoMatchingPatternError
```
---
## ユースケース
- JSONのパターンマッチ
- ArrayやHashの構造チェック(順番や型もチェックしてくれる)
---
## JSON
```json
{
  "foo": "bar",
  "hoge": [
    {
      "fuga": 1,
      "weei": 2
    }
  ]
}
```

```ruby
json = JSON.parse(json, symbolize_names: true)
case json
in {foo: "bar", hoge: [{fuga: 1, weei: var}]}
  puts var #=> 2
end
```
--- 
## Array
```ruby
case [1, 2, 3]
in [3, 2, 1]
in [2, 3, 1]
in [1, 3, 2]
end
#=> NoMatchingPatternError

```

