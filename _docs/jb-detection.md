---
title: 様々な脱獄検知とそれらの回避
---

# 様々な脱獄検知とそれらの回避

## ここで学べること

- 脱獄検知の手法
- それらの回避策を発見するためのアプローチ方法

## 脱獄検知とは

その名の通り、脱獄を検知する技術です。多くのアプリケーションが(主にチートを防ぐ目的で)導入しています。開発者が個人的に行うものから商用に開発されている高度なものまで様々なバリエーションがありますが、手法はほとんどの場合で単純ですが、これらに難読化等の技術が組み合わさることにより、回避することが困難になります。
検知手法は以下のように大別されます。

- 脱獄環境でのみ生成されるファイルの存在確認
- 通常ではアクセスできないファイルへのアクセスの試行
- `cydia://`などの URL スキームが開けるかどうかのチェック
- その他システムコールを用いた検知

次のセクションでは、これらを回避する手法を見ていきましょう。

## 検知を回避する手法

検知する方法が変われば回避する方法も変わっていきます。
でもそれなら何故脱獄検知を回避する Tweak は存在するのでしょう？検知手法はアプリごとに違うので、アプリの数だけ Tweak が存在していてもおかしくはありません。しかし、実際はそんなことはありません。何故なら多くのアプリが同じ様な検知手法を使っているからです。

Liberty Lite、Shadow、Breakthrough や Choicy といった名前を聞いたことがあるのではないでしょうか？これらは脱獄検知を回避するための Tweak です。最近では PokemonGO や Nintendo 製のアプリも回避できる KernBypass なども話題になっています。
あなたはこれらがどのように動作しているか考えたことはありますか？もし検知回避手法を自身で発見したい、或いは検知回避 Tweak を開発したいと思っているなら既存の Tweak がどのように動作するか知っておいて損はないでしょう。
私が以前書いた Qiita の記事があるので是非チェックしてみたください。

[脱獄検知回避アプリを解析する Liberty lite](https://qiita.com/sh1ma/items/4763e6a4272564cca662)

とはいえ、今すぐ回避手法を教えろ！という方もいるかと思います。
それでは早速解説していきましょう。

### 脱獄環境でのみ生成されるファイルの存在確認

恐らくこれが一番回避が簡単なものでしょう。

`/Applications/Cydia.app`や`/Library/MobileSubstrate/MobileSubstrate.dylib`、`/bin/bash`、`/private/var/lib/apt`等といったファイルの存在をチェックするものです。

回避手法は多く存在しますが、ここでは frida を使った回避を紹介します。
ファイルの存在チェックには[fileExists(atPath:isDirectory:)](https://developer.apple.com/documentation/foundation/filemanager/1410277-fileexists)を使っていて、`/Applications/Cydia.app`をチェックしていると想定します。

```
frida-trace -Uf com.application.jbdetection -m "*[* fileExists*]"
```

実行すると、カレントディレクトリ内の`__handlers__`フォルダが生成されたかと思います。その中の`FileManager`と`fileExists`が名前に含まれる js ファイルを開いてみましょう。

ファイルは大体この様になっていると思います。

`onEnter`は`args`を引数にとっています。ここでは関数の引数の値に対して任意の処理を行うことができます。

`onLeave`は`retval`を引数にとっています。ここでは関数の返り値に対して任意の処理を行うことができます。

```js
{
  onEnter: function (log, args, state) {
    // argsの0番目をnullに変更したい時は下記のように
    // args[0] = ptr(0)
  },
  onLeave: function (log, retval, state) {
		// retvalを変更したい時は下記のように
    // retval.replace(ptr(0))
  }
}
```

今回の検知対象は`/Applications/Cydia.app`なので、`args[0]`が`/Applications/Cydia.app`の時だけ、`retval`を`0`、つまり`false`にするコードを書いていきます。

```js
{
  onEnter: function (log, args, state) {
		// ObjCのargsを扱う時はObjC.Objectでキャストする
    path = ObjC.Object(args[0])
    console.log(path)
    if (path === "/Applications/Cydia.app") {
      state.flag = 1
    }
  },
  onLeave: function (log, retval, state) {
		if (state.flag === 1) {
      retval.replce(ptr(0))
    }
  }
}
```

すると上記のようなコードになります。

ね、簡単でしょう？

### 通常ではアクセスできないファイルへのアクセスの試行

TODO

###`cydia://`などの URL スキームが開けるかどうかのチェック

TODO

 ### その他システムコールを用いた検知

TODO