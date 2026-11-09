# Dr Quine

## English

Programs that output the same text as their own source code, known as quines. Implemented in C, x86-64 assembly, and Go.

There are three forms: print the source to the terminal, save it as another source file, or repeatedly generate and run copies while decreasing a counter. Compare the generated text with the original to check the replication.

### Programs

| Program | Behavior |
| --- | --- |
| Colleen | Print its source code to standard output |
| Grace | Create a `Grace_kid` file containing the same source |
| Sully | Generate, compile, and run copies from `Sully_5` through `Sully_0` |

### Build and run

Requires GNU Make and the tools for the chosen language. C needs a C compiler; assembly needs Linux x86-64, NASM, and a C compiler (`gcc` is used when running Sully); Go needs Go.

From the repository root, build the desired language:

```sh
make -C C
make -C ASM
make -C Go
```

C example:

```sh
cd C
./Colleen          # Print the source
./Grace            # Create Grace_kid.c
./Sully            # Generate the chain from Sully_5.c to Sully_0.c
```

Run the same program names inside `ASM/` or `Go/` for those versions. Their generated sources use `.s` and `.go`, respectively.

### Verification

In `C/`, compare Colleen's output and Grace's generated file with their original sources. No output from `diff` means they match.

```sh
./Colleen | diff - Colleen.c
./Grace
diff Grace.c Grace_kid.c
```

### Implementation

- C: reconstructs the source using format strings, newlines, quotes, and the format string itself.
- Assembly: uses relative addressing and PLT function calls for PIE linking.
- Go: uses `fmt`'s `%q` to quote and escape source strings.

## 日本語

実行すると、自分を記述したソースコードと同じテキストを出力するプログラムです。このようなプログラムを「クワイン」と呼びます。C・アセンブリ（x86-64）・Goの3言語で実装しています。

画面にコードを表示する版、別のソースファイルとして保存する版、番号を減らしながら複製を生成・実行する版の3種類があります。出力と元のファイルを比較して、自己複製できているか確認できます。

### プログラム

| プログラム | 動作 |
| --- | --- |
| Colleen | 自分のソースコードを標準出力にそのまま出力する |
| Grace | 自分のソースコードと同じ内容の `Grace_kid` ファイルを生成する |
| Sully | カウンタを減らしながら複製 `Sully_5` 〜 `Sully_0` を生成・コンパイル・実行する |

### ビルドと実行

GNU Make と、実行する言語の処理系が必要です。C版はCコンパイラ、ASM版は Linux x86-64・NASM・Cコンパイラ（Sully の実行には `gcc`）、Go版は Go を使用します。

リポジトリ直下で、使う言語のビルドコマンドを実行します。

```sh
make -C C
make -C ASM
make -C Go
```

実行例（C版）：

```sh
cd C
./Colleen          # ソースコードを標準出力に表示
./Grace            # Grace_kid.c を生成
./Sully            # Sully_5.c から Sully_0.c まで連鎖
```

ASM版・Go版も各言語ディレクトリで同名のプログラムを実行します。生成されるソースの拡張子は、それぞれ `.s`・`.go` です。

### 検証

Cディレクトリで、Colleen の出力と Grace の生成ファイルを元のソースと比較できます。差分がなければ何も表示されません。

```sh
./Colleen | diff - Colleen.c
./Grace
diff Grace.c Grace_kid.c
```

### 実装メモ

- C版：書式文字列に改行・引用符・文字列自身を埋め込み、ソースを再現します。
- ASM版：相対アドレス参照と PLT 経由の関数呼び出しで、PIE リンクに対応しています。
- Go版：`fmt` の `%q` でソース文字列を引用・エスケープします。
