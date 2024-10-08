---
title: 演算子と式
summary: 式は、AliceScriptにおけるもっとも重要かつ基本的な要素です。
date : 2021-12-25
---

AliceScriptにおいて、ほとんどのものは ==**式**== で記述されます。
AliceScriptでは式を、値を返すものすべてと定義します。
ここでは式を値があるものすべてと定義します。

AliceScriptにおける式のもっとも単純な形を次に示します。

```cs title="AliceScript"
1 + 1;
```

数学と同じですね。
この例では、`1+1`の計算を行っています。ここで、`1`は、明らかに`1`という値です。言い換えると`1`は`1`という値を表す式なのです。 このようにコード中に直接書かれた値のことを、==リテラル== と呼びます。

式の多くの使い道は、式の結果をどこかへ代入することです。
次の例をご覧ください。

```cs title="AliceScript"
var a = 1 + 1;
```

この例では、先ほどの計算結果を変数`a`に定義して代入しています。
この代入の後、変数`a`は、`2`になります。
このように何かの値に代入すると、**[代入文](../statement.md)** となります。
AliceScriptで変数を定義したり代入する方法について詳しく知るには、[変数](../variable.md)を参照してください。

ここでの`+`は加算演算子という演算子です。
AliceScriptにはさまざまな演算子が存在し、それらは以下のグループに分類できます。

- [代入演算子](./assignment-operator.md)
- [算術演算子](./arithmetic-operators.md)
- [関係演算子](./relational-operators.md)
- [論理演算子](./logical-operators.md)
- [ビット演算子](./bitwise-operators.md)
- [文字列演算子](./string-operators.md)
- [型演算子](./type-operators.md)
- [new演算子](./new-operator.md)

## 文と式の違い

AliceScriptには、==文== と ==式== の異なるふたつのコード概念があります。それぞれの違いは次の通りです。

- **式**は必ずなんらかの有効な値を返します
- **文**は常に[Void](../../api/void/index.md)を返します。文は0つ以上の有効な式から成り立ちます。

歴史的な事情から、文を式の中に含めること自体はできます。例えば、以下のコードは正常に機能します。

```cs title="AliceScript"
"ABC" + (var a = 2)
```

ただし、可読性を下げるため文を式の中に含めるべきではありません。

## 複合代入
多くの算術演算子は、複合代入をサポートします。算術演算子を`op`と置いた場合、次のふたつの式は同じ意味を持ちます。

```cs title="AliceScript"
x op= y;
```

```cs title="AliceScript"
x = x op y;
```

## 演算子の優先順位
すべての演算子には、優先順位があります。
たとえば、$1 + 2 \times 3$という式がある場合、$+$よりも$\times$の方が先に計算するようなものです。次の例では、乗算が加算よりも優先順位が高いため、先に乗算が行われます。

```cs title="AliceScript"
var a = 1 + 2 * 3;
print(7);
```

演算の順序を変更するには、かっこを使用します。

```cs title="AliceScript"
var a = (1 + 2) * 3;
print(9);
```

次の表は、演算子を優先順位の高い順に並べたものです。同じ行内の演算子の優先順位は同じです。

|優先順位|演算子|
|---|---|
|14|`++`、`--`|
|13|`**`|
|12|`*`、`/`、`%`|
|11|`+`、`-`|
|10|`<<`、`>>`|
|9|`<`、`>`、`<=`、`>=`|
|8|`==`、`!=`|
|7|`&`|
|6|`^`|
|5|`|`|
|4|`&&`|
|3|`||`|
|2|`??`|
|1|`=`|

## デリゲートの組み合わせ
左辺と右辺の両方がデリゲート型の場合、左辺のデリゲートと右辺のデリゲートが結合された新しいデリゲートが返されます。次に例を示します。

```cs title="AliceScript"
var del1 = ()=>{
  print("Hello");
};
var del2 = ()=>{
  print("World");
};

var del = del1 + del2;
del.Invoke();
//出力:Hello
//    World
```

## ラムダ演算子
ラムダ演算子(`=>`)は、ラムダ式中で、左側の引数指定部と右側の式本体をわけるために使用します。[ラムダ式](../../api/delegate/index.md)を参照してください。
