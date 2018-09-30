---

theme : "black"
transition : "default"

---

# システムプログラミング言語 Rust

---

## システムプログラミング言語？

- 優れた実行効率、少ない資源
- 彽レイヤ操作可能
- ネイティブバイナリ
- GCは許容しない

--

### つまり・・・

--

### システムプログラミング言語では

- OSカーネル、デバイスドライバなどが書ける
- IOT、組み込み向けMPUにも使用可能
  - Cortex-M、AVRなど
- 高いパフォーマンスが求められる基板層向け
- リアルタイム性が高いアクションゲームにも

---

### プログラミング言語のトレンド

<small>

- ネイティブ言語
  - C/C++ <!-- .element: class="fragment highlight-red" data-fragment-index="1" -->
  - Rust  <!-- .element: class="fragment highlight-red" data-fragment-index="2" -->
  - Go
  - Swift/Objective-C
  - Pascal
  - D
  - Haskel
  - OCaml
  - Common Lisp


- VM(JIT)系
  - JVM
    - Java, Clojure, Scalar
  - CLR(Mono)
    - C#, F#
  - BEAM
    - Erlang


- スクリプト言語
  - Javascript
  - Ruby
  - Python
  - Perl
  - Lua

</small>

--

## ようするにC/C++の後継言語がなかった。

# Rustの誕生

---

## Rustの特徴

- ゼロコスト抽象化
- ムーブセマンティクス <!-- .element: class="fragment highlight-red" data-fragment-index="1" -->
- 保証されたメモリ安全性 <!-- .element: class="fragment highlight-red" data-fragment-index="1" -->
- データ競合のないスレッド <!-- .element: class="fragment highlight-red" data-fragment-index="1" -->
- トレイトによるジェネリクス <!-- .element: class="fragment highlight-red" data-fragment-index="1" -->
- パターンマッチング <!-- .element: class="fragment highlight-red" data-fragment-index="1" -->
- 型推論 <!-- .element: class="fragment highlight-red" data-fragment-index="1" -->
- 最小限のランタイム
- 効率的なCバインディング

<small>（[公式サイト](https://www.rust-lang.org/ja-JP/index.html)より）</small>

---

## 実際使用してみての印象

--

### 実際使用してみての印象 (1/4)

- C言語系手続き型言語の皮を被った別パラダイムの言語
  - Haskel, OCamlの影響が強い？

- Haskel, OCamlは仕事ではちょっと･･･、でもRustなら･･･

--

### 実際使用してみての印象 (2/4)

- コンパイル時にできるだけ問題を解消
  - コンパイルを通すのに一苦労
  - コード生成だけでなく強力な静的解析
  - エラーメッセージは親切でわかりやすい

- - -
- コンパイルが通れば･･･
  - メモリーリーク、資源解放忘れがない
  - メモリー破壊がない
  - スレッド間のデータ競合がない

　

### つまり安心！！

--

### 実際使用してみての印象 (3/4)

- 型が厳密、型推論が強力、寿命管理が厳密
- Genericsが強力、多用
  - C++のような一部の変態向けではない
- 省略省略(構文糖）多め、'?'記法など
- 文(Statement)よりも式(Expression)指向
- パターンマッチ便利

--

### 実際使用してみての印象 (4/4)

- Cargo 便利
  - Batteries included
- 処理系が一つなのは何気にありがたい(vs C++)
- 実質 nightly build が標準
- 枯れてない言語なので情報が錯綜しがち
