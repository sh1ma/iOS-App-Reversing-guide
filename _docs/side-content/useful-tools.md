---
title: 有用なツール(用途別)
---

役に立つツールを用途別にまとめました。

## 復号済み ipa をデバイスから抽出する

- [frida-ios-dump(frida が必要)](https://github.com/AloneMonkey/frida-ios-dump)
- [xia0LLDB `dumpdecrypted -X`(lldb プラグイン)](https://github.com/4ch12dy/xia0LLDB#dumpdecrypted-20190922)
- [CrackerXI+ - デバイス単体で抽出可能(リンクは cydia リポジトリ)](http://pokego2.com/)

## SSL Pinning を回避する

- [Frida-Scripts / ssl_bypass.js - Github(frida 必須)](https://github.com/machoreverser/Frida-Scripts/blob/master/ssl_bypass.js)

## 脱獄検知を回避する

- [BreakThrough(リンクは cydia リポジトリ)](http://ftp.sident.net/cydia-beta)
- [Liberty Lite(リンクは cydia リポジトリ)](https://ryleyangus.com/repo)
- [FlyJB(リンクは cydia リポジトリ)](https://repo.xsf1re.kr/)
- FLEX 3(関数フックができる Tweak。標準リポジトリでインストール可能)

## 脱獄済み iOS デバイス用ファイルマネージャ

- [Filza(リンクは cydia リポジトリ)](http://tigisoftware.com/cydia/)

## 通信解析

- [mitmproxy - TUI で動くプロキシツール。スクリプティングもできる。](https://mitmproxy.org/)
- [Burp Suite - GUI で動くプロキシツール。有料版じゃないと物足りないかも](https://portswigger.net/burp)

## 動的解析

- lldb
- debugserver
- [frida - 動的解析ツールキット。関数フックなどに使える](https://frida.re/)
- FLEXing ステータスバー長押し or 三本指タップで起動する FLEXLoader(標準リポジトリでインストール可能)

## 静的解析

- [Hopper DisAssembler(有料。10000 円くらい)](https://www.hopperapp.com/)
- [Ghidra(無料でプラットフォーム関係なしに動くが、重い。arm64 とは相性悪い(?))](https://ghidra-sre.org/)
- [IDA Pro(すっげー高い。が、その分の価値はある)](https://www.hex-rays.com/)
- [`dsdump`コマンド nm と class-dump 合体させたようなツール。Swift のクラスダンプもできる。](https://github.com/DerekSelander/dsdump)
- [`strings`コマンド(リンクは使い方の説明サイト)](https://kazmax.zpp.jp/cmd/s/strings.1.html)

## 便利系プラグイン

- [iOSreExtension - VSCode で色々できるようになる！これ一個で結構解決したりする](https://github.com/co2333/iosreextension)
- [xia0LLDB - ios に特化した lldb の拡張プラグイン。lldb 使うなら必須](https://github.com/4ch12dy/xia0LLDB)
- [issh - ios とリモートマシンとのやり取りが便利になるコマンド](https://github.com/4ch12dy/issh)
