---
title: 有用なツール(用途別)
---

役に立つツールを用途別にまとめました。

## 復号済みipaをデバイスから抽出する
- [frida-ios-dump(fridaが必要)](https://github.com/AloneMonkey/frida-ios-dump)
- [xia0LLDB `dumpdecrypted -X`(lldbプラグイン)](https://github.com/4ch12dy/xia0LLDB#dumpdecrypted-20190922)
- [CrackerXI+ - デバイス単体で抽出可能(リンクはcydiaリポジトリ)](http://pokego2.com/)

## SSL Pinningを回避する
- [Frida-Scripts / ssl_bypass.js - Github(frida必須)](https://github.com/machoreverser/Frida-Scripts/blob/master/ssl_bypass.js)

## 脱獄検知を回避する
- [BreakThrough(リンクはcydiaリポジトリ)](http://ftp.sident.net/cydia-beta)
- [Liberty Lite(リンクはcydiaリポジトリ)](https://ryleyangus.com/repo)
- [FlyJB(リンクはcydiaリポジトリ)](https://repo.xsf1re.kr/)
- FLEX 3(関数フックができるTweak。標準リポジトリでインストール可能)

## 脱獄済みiOSデバイス用ファイルマネージャ
- [Filza(リンクはcydiaリポジトリ)](http://tigisoftware.com/cydia/)

## 動的解析
- lldb
- debugserver
- [frida - 動的解析ツールキット。関数フックなどに使える](https://frida.re/)
- FLEXing ステータスバー長押し or 三本指タップで起動するFLEXLoader(標準リポジトリでインストール可能)


## 静的解析
- [Hopper DisAssembler(有料。10000円くらい)](https://www.hopperapp.com/)
- [Ghidra(無料でプラットフォーム関係なしに動くが、重い。arm64とは相性悪い(?))](https://ghidra-sre.org/)
- [IDA Pro(すっげー高い。が、その分の価値はある)](https://www.hex-rays.com/)
- [`dsdump`コマンド nmとclass-dump合体させたようなツール。Swiftのクラスダンプもできる。](https://github.com/DerekSelander/dsdump)
- [`strings`コマンド(リンクは使い方の説明サイト)](https://kazmax.zpp.jp/cmd/s/strings.1.html)


## 便利系プラグイン
- [iOSreExtension - VSCodeで色々できるようになる！これ一個で結構解決したりする](https://github.com/co2333/iosreextension)
- [xia0LLDB - iosに特化したlldbの拡張プラグイン。lldb使うなら必須](https://github.com/4ch12dy/xia0LLDB)
- [issh - iosとリモートマシンとのやり取りが便利になるコマンド](https://github.com/4ch12dy/issh)