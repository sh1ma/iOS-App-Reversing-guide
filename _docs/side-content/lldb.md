---
title: lldbの使い方
---

# LLDB

このページでは、lldbの使い方について詳しく説明します。(iOSデバイスのプロセスにアタッチするまでの手順は別ページで紹介します)

また、アセンブリが読めない方は[ARMアセンブリ](/iOS-App-Reversing-guide/docs/side-content/arm-assembly)のページを先に学ぶことをオススメします。

この記事では

- ある程度ARMアセンブリについて理解している
- lldbの基本的な使い方(ブレークポイントコマンド、ディスアセンブルコマンド等)は理解している
- [xia0LLDB](https://github.com/4ch12dy/xia0LLDB)プラグインがインストール済み

として進めていきます。

基本的な使い方は[lldb cheat sheet](https://www.nesono.com/sites/default/files/lldb%20cheat%20sheet.pdf)で学ぶと良いでしょう。

また、わからないコマンドは`help`で詳しい情報を確認することが出来ます。

例えば`register read`がわからなければ

```
help register read
```

とすることで詳しい情報を確認できます。

## シチュエーション別コマンド集


### `$x8 == 10`のときだけブレークしたい。

```
b 0x1111 # Breakpoint 1
br mod -c "$x8 == 10" 1
```


### 逆アセンブラで見つけたアドレスにブレークポイントを置きたい

```
image dump sections Twitter # "Twitter"の部分はアプリの実行ファイル名
```

以下のように出力されると思います。

![](https://kov4l3nko.github.io/blog/2016-04-27-debugging-ios-binaries-with-lldb/viber-image-section-dump.png)

> https://kov4l3nko.github.io/blog/2016-04-27-debugging-ios-binaries-with-lldb/#aslrより引用

```
<__TEXT addressの始端> - <__PAGEZERO addressの終端>
```

を計算します。この場合以下のようにします。

```
p/x 0x0000000100058000-0x0000000100000000 # result: 0x0000000000058000
```

Hopperの示す関数のアドレスが`0x1234`の場合、`0x1234+0x0000000000058000`をすることで実際のアドレスを求めることが出来ます。

いちいちこんなことをしていては面倒なので素直に[xia0LLDB](https://github.com/4ch12dy/xia0LLDB)の`xbr`コマンドを使いましょう。

```
xbr 0x1234
```

とすれば、自動で計算をされた位置にブレークポイントを張ってくれます。


### 現在いるアドレスから任意のアドレスに移動したい

`0x1212`に移動したければ、

```
thread jump -a 0x1212
```

とすることで移動できます。


### サブルーチンから呼び出し元にすぐに戻りたい

```
thread return
```

とすれば返り値無しで戻る事ができます。

返り値を設定したい場合は

```
thread return 1
```

といったようにすれば良いでしょう。


### ブレークする度に任意の情報を表示したい

ブレークする度にレジスタを表示したいとします。その場合は

```
(lldb) target stop-hook add
Enter your stop hook command(s).  Type 'DONE' to end.
> register read
Stop hook #1 added.
```

このようにすればブレークする度にレジスタが表示されます。