---
title: "Haskell勉強してみた"
emoji: "📑"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["haskell"]
published: false
---

# 概要

すごいHaskellを読んでHaskellに入門したので、学んだことをまとめています。
オブジェクト指向型言語との比較のために筆者がよく使用している、`javascript`, `python`との比較も記載しています。

# 対象読者

- オブジェクト指向型言語の基本を理解しているが、関数型言語がわからない方。

# 関数

## 前置関数

haskellのほとんどの関数は前置関数らしい。

関数名を書いて、スペースで区切られた引数を書く。

例えば2つの引数を受け取って小さい値を返す`min`関数は以下の通り。

```haskell
min 2 3
```

多くの言語では以下のように呼び出す。

```javascript
min(1,2)
```

## 中置関数

「中置」と記載があるように2つの引数の間に記載して使用する。(他の言語の演算子と同じ)

```haskell
1 * 2
```

```javascript
1 * 3
```

また、先置関数の場合でも引数が2つの場合、その関数をバッククォートで囲うことで中置関数と同じように使うことができます。

```haskell
5 div 3
```


## 呼び出しの順序

関数の呼び出しはすべての演算の中で最も高い優先度になるようです。

以下はjavascriptとhaskellでそれぞれ同じように解釈される式です。
見比べてみましょう。

```javascript
succ(9) + max(5, 4) + 1
```

```haskell
succ 9 + max 5 4 + 1
```

優先して処理させたい場合、`()`で囲む必要があります

```haskell
succ 9 + max 5 ( 4 + 3 )
-- 17
```


## 関数の定義

簡単な関数を定義するのは以下のように記載します。
ここでもjavascriptとの比較を載せておきます。

```haskell
doubleMe x = x * 2
```

```javascript
function doubleMe(x) {
  return x * 2
}
```

# リスト

haskellのリストは1つの型を複数個格納できます。
javascriptなどでは1つの配列に文字が入れたり、数字を入れたりすることが可能ですが、haskellではできません。

```haskell
let numbers = [4,8,12,16,20]
```


```javascript
const numbers = [4,8,12,16,20]
```

## 連結

haskellでは`++`演算子を用いてリストの結合を行います。
また、haskellでは"hello"のような文字列は文字のリストと同じで、++による結合が行なえます。

```haskell
[1,2,3,4] ++ [5,6,7,8]
-- [1,2,3,4,5,6,7,8]
```

```javascript
[1,2,3,4].concat([5,6,7,8])
```

また、先頭に単一の要素を追加する場合は`:`を使うことができます。

```haskell
0:[1,2,3,4,5]
-- [0,1,2,3,4,5]
```

## 要素へのアクセス

リストの要素を先頭からの位置で取得したい場合は、`!!`演算子を使用します。
また、添字は0から始まります。

```haskell
[1,2,3,4,5,6] !! 0
-- 1
```

## 簡単なリスト操作の関数

### `head`
先頭の要素を返す。

```haskell
head [1,2,3,4,5]
-- 1
```

### `tail`
先頭の要素を除いた残りの`tail`の部分を返す。

```haskell
tail [1,2,3,4,5]
-- [2,3,4,5]
```

### `last`
末尾の要素を返す。

```haskell
last [1,2,3,4,5]
-- 5
```

### `init`
末尾の要素を除いた残りの`init`の部分を返す。

```haskell
init [1,2,3,4,5]
-- [1,2,3,4]
```

`head`, `tail`, `last`, `init`は空の配列を渡すとエラーになるため注意する必要がある。（コンパイル時にチェックできない）

### `null`

リストが空の場合は`true`, 空ではない場合は`false`を返す。

```haskell
null [1,2,3]
-- False

null []
-- True
```

### `reverse`

リストを逆順にしたものを返す。

```haskell
reverse [1,2,3,4,5]
-- [5,4,3,2,1]
```

### `take`

数とリストを受け取り、先頭から指定された数の要素を取り出したリストを返す。

```haskell
take 2 [1,2,3]
-- [1,2]
```

### `drop`

数とリストを受け取り、先頭から指定された数を削除したリストを返す。

```haskell
drop 3 [1,2,3,4,5,6,7]
-- [4,5,6,7]
```

### `maximum`, `minimum`

maximum -> 順番が定義された要素からなるリストを受け取り、その中で最大の要素を返す。
minimum -> 順番が定義された要素からなるリストを受け取り、その中で最小の要素を返す。

```haskell
maximum [1,2,3,4,5,6,7]
-- 7
minimum [1,2,3,4,5,6,7]
-- 1
```

### `sum`, `product`

sum -> 数のリストを受け取り、それらの和を返す。
product -> 数のリストを受け取り、それらの積を返す。

```haskell
sum [1,2,3,4,5]
-- 15
product [1,2,3,4,5]
-- 120
```

## レンジ(range)

列挙で要素の組み合わせでリストを作成することができます。
以下はpythonとhaskellで1から20までのすべての自然数のリストを作るコードです。

```haskell
[1..20]
-- [1,2,3,4,5,6,7,8,9,10,11,12,13,14,15,16,17,18,19,20]
```

```python
list(range(1,21))
-- [1,2,3,4,5,6,7,8,9,10,11,12,13,14,15,16,17,18,19,20]
```

アルファベットについても列挙することができます

```haskell
['a'..'z']
-- "abcdefghijklmnopqrstuvwxyz"
```


### 増分(ステップ)の指定
何も指定していない場合1ずつ増えていきますが、最初の要素と2つ目の要素をカンマで区切って上限を指定することで、増分を指定することができます。

以下は2から20までの偶数を列挙するコードです。


```haskell
[2,4..20]
-- [2,4,6,8,10,12,14,16,18,20]
```

## リストの生成

上限を指定しないことで、レンジを使って無限リストを生成することもできます。
(haskellが遅延評価のため、要素が必要になったら計算するので可能)


```haskell
let l = [1..] -- 1から1ずつ増えていくリストを無限の要素作る
take 10 l -- 10要素分必要になったため、10要素分計算して表示している
-- [1,2,3,4,5,6,7,8,9,10]
```

### リストを作成できる関数

#### `cycle`

リストを受け取り、要素を無限に繰り返したリストを返す。

```haskell
take 10 (cycle [1,2,3])
-- [1,2,3,1,2,3,1,2,3,1]
```

#### `repeat`

1つの要素を受け取り、その要素のみを無限に繰り返したリストを返す。

```haskell
take 10 (repeat 5)
-- [5,5,5,5,5]
```

#### `replicate`
リストの長さと複製する要素を受け取り、その要素をリストの長さ分繰り返したリストを返す。

```haskell
replicate 3 10
-- [10,10,10]
```

### リスト内包表記

リスト内包表記はリストのフィルタリング、変換、組み合わせを行う方法です。
以下のコードを例に説明します。

```haskell
[x * 2 | x <- [1..10]]
-- [2,4,6,8,10,12,14,16,18,20]
```

`x <- [1..10]`の部分はリストから要素を取り出してxが受け取っているという意味です。([1..10]の各要素をxに束縛しているとも言える)
`|`より前の部分`x * 2`は、取り出した値に対して、どのようなリストを作りたいか指定しています。
この場合だと`take 10 [2,4..]`と同じことをしていて、読みにくくなっているように見えます。
しかし、複雑な処理をしたい場合に輝きます。
 
 例えば、1から10までの要素で2倍した値が10以上のものからなるリストが欲しい場合は以下のように記述します。
 このように、条件(述語)を使用してリストを間引くことをフィルターするといいます。(javascriptやpythonも同名の関数がある)

 ```haskell
 [x * 2 | x <- [1..10], x * 2 >= 10]
 -- [10,12,14,16,18,20]
 ```

10以上のすべての奇数をBANG!に置き換え、10以下のすべての奇数をBOOM!に置き換える内包表記を使用した関数を以下に記載します。


```haskell
-- odd関数は数字を受け取り、奇数であればTrue、そうでなければFalseを返す。
boombangs xs = [ if x < 10 then "BOOM!" else "BANG!" | x <- xs, odd x ]
```

述語は複数含めることができます。
以下は1から30の自然数のうち、3の倍数かつ20以上のリストを取得しています。

```haskell
[ x | x <- [1..30], x `mod` 3 == 0, x > 20 ]
```

述語だけではなく、複数のリストから値を取り出す事もできます。
複数のリストから値を取り出した場合、それらのリストの要素のすべての組み合わせがリストに反映されます。

```haskell
[ x + y | x <- [1..10] | y <- [10,100,1000]]
-- [11,101,1001,12,102,1002,13,103,1003,14,104,1004,15,105,1005,16,106,1006,17,107,1007,18,108,1008,19,109,1009,20,110,1010]
```

# タプル

複数の違う方の要素を格納して、1つの値にするために使用されます。

以下のような特徴があります。

- タプルはカッコで囲み、要素をカンマで区切って表現する
  - `(1,2,3)`
- 複数の違う型の要素を格納できる
  - `(1, "hello")`
- 長さが固定
  - 要素を追加したい場合は、別途関数を書かないといけない

## ペアを使う

値を格納するのに
