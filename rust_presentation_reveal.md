---

theme : "black"
transition : "default"

<style type="text/css">
  .reveal h1,
  .reveal h2,
  .reveal h3,
  .reveal h4,
  .reveal h5,
  .reveal h6 {
    text-transform: none;
  }
</style>

---

# システムプログラミング言語 Rust

---

- 森本篤 @ Cyllista
  - 業務ではC++とPython
  - Rust歴は2ヶ月ぐらい
  - 学習用の題材: レイトレ本の C++ -> Rust に移植

<div style="text-align:center;">
  <img src="book-rt.jpg">
</div>

---

### Rustはこんな言語

~~~rust
fn main() {
    let s1 = String::from("hello");

    let (s2, len) = calculate_length(s1);

    println!("The length of '{}' is {}.", s2, len);
}

fn calculate_length(s: String) -> (String, usize) {
    let length = s.len(); // len() returns the length of a String

    (s, length)
}
~~~

---

## Rustは速度、安全性、並行性の3つのゴールにフォーカスしたシステムプログラミング言語です。 

<small>（[公式サイト](https://www.rust-lang.org/ja-JP/index.html)より）</small>

--

## システムプログラミング言語？

- 優れた実行効率、少ない資源、フットプリント
- 彽レイヤ操作可能
- リソースに対する透明性
- ネイティブバイナリ
- GCを持たない！ <!-- .element: class="fragment highlight-red" data-fragment-index="1" -->

--

### つまり・・・

--

### システムプログラミング言語では

- OSカーネル、デバイスドライバなどが書ける
- IOT、組み込み向けMPUにも使用可能
  - Cortex-M、AVRなど
- 高いパフォーマンスが求められる基板層向け
- リアルタイム性が高いアクションゲームにも
  - ゲーム機は実質組み込み系

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

## 何十年も！

# Rustの爆誕！

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

<small>（[公式サイト](https://www.rust-lang.org/ja-JP/index.html)より）</small>

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

- 精神的安心がえられる！
  - メモリーリーク、資源解放忘れがない
  - メモリー破壊がない
  - スレッド間のデータ競合がない

Note:
Pythonつらい。

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
  - ビルドシステム、
  - パッケージマネジャー
    - 実質: "Batteries included"
  - ユニットテスト、プロファイリング
- 処理系が一つなのは何気にありがたい(vs C/C++)
- 実質 nightly build が標準
- 枯れてない言語なので情報が錯綜しがち
  - Stable版が6週間毎にリリースされる

---

## 特徴的な言語機能

---

## Rustの値

- 値は以下の特徴を持つ
  - 厳格な型
  - 所有権 or 借用
  - 可変性（デフォルトでimmutable）
  - 寿命
  - トレイト

--

### 所有権の例

~~~rust
fn say(msg: String) {
    println!("I wanna say: {}", msg);
}

fn main() {
    let m = String::from("hello");
    say(m);
    say(m);  // error!
}
~~~

Note:


---

## Trait

（特徴、特性）

--

### Trait

- GoのInterfaceに似ている
- Traitをつけるとトレイトが要求するメソッドを割り当てる
- 標準型を含め、struct, enumの任意の型に後からでもつけられる
- Generic関数の制約に用いることもできる

~~~rust
impl<T> [T] {
  fn sort(&mut self) where T: Ord { ... }
~~~

note:
C++と比べるとずいぶん便利

--

### 標準で用意されている代表的なTrait

- Debug
- Copy
- Clone
- Drop
- Default
- Hash
- Eq, PartialEq
- Ord, PartialOrd
- std::ops::add, ...

---

### ポリモーフィズム

- Traitを用いてポリモーフィズムが実現できる
  - 静的ディスパッチ -> Generics
  - 動的ディスパッチ -> Trait Object or Boxing

- - - 

静的・動的はC++みたいに関数実装時に"virtual/non-virtual"を選択する必要はなく、呼び出し時に選択できる。  
（C++メソッドの定義時に決まってしまう）

--

### 静的ディスパッチ

- 静的はコンパイル時に呼び出し先が決定する
  - 動的よりも軽量なので可能であれば静的で
- Genericsと聞くとC++は抵抗があるが、Rustのそれは使いやすい
- Traitで受け入れる型に制約をつけられる

--

### 動的ディスパッチ

- Trait Object、もしくはBoxingを行うことで可能
- Fat Pointer（オブジェクトとvptrのペア）を呼び出し時に生成
- オブジェクト自身にvptrを持つC++よりも効率的

Note:

- Generics vs Trite object
- Fat pointer

---

### 列挙体(enum)

- enumは値を保持できる

~~~rust
enum Shape {
	Circle(Point, f64),
	Rectangle(Point, Point)
}

fn area(sh: Shape) -> f64 {
    match sh {
        Shape::Circle(_, size) => PI * size * size,
        Shape::Rectangle(Point { x, y }, Point { x: x2, y: y2 }) => (x2 - x) * (y - y2)
    }
}
~~~

--

### エラーハンドリング

- エラーハンドリングにはenumが用いられる
- Result(Ok<T>, Err<E>), Option(Some(T), None)
- '?'文法でif-errorチェックが簡便に書ける

~~~rust
fn read_content(fname: &String) -> io::Result<Vec<u8>> {
    let mut f = File::open(fname)?;
    let mut buffer = Vec::new();
    f.read_to_end(&mut buffer)?;
    Ok(buffer)
}

fn main() {
    match read_content("foo.txt") {
        Ok(s) => { println!("content size: {}", s.len()) },
        Err(e) => { println!("error: {}", e) },
    }
}
~~~

---

## まとめ

- やっぱり"難しい系"の言語
- アマチュアのおもちゃではなく玄人向けツール
- でも、敷居は下がってきている
- 既存の手続き型OOP言語の外に出たい人は是非！

---

# end
