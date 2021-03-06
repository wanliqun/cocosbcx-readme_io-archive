---
title: "5.2 Lua仮想マシン"
slug: "52-lua仮想マシン"
hidden: false
createdAt: "2019-09-17T08:46:09.205Z"
updatedAt: "2019-09-17T08:46:21.132Z"
---
ビットコインをはじめとしたブロックチェーン1.0では、ブロックチェーンは単なる分散型台帳に過ぎないです。現在に至って、イーサリアムを代表としたブロックチェーン2.0では、ブロックチェーンの本質は台帳を遥かに超えて、スーパークラウドコンピューターになっています。根本的な原因はインフラチェーンシステムに、スマートコントラクトを実行できる仮想マシンを追加したのです。

仮想マシンのおかげで、チェーンシステムは信頼できる実行環境を持つようになりました。開発者はプログラムをチェーンシステムへデプロイし、トランザクションとしてコントラクトAPIをコールできます。

実装技術から言うと、仮想マシン、イーサリアムのEVMと従来のJava仮想マシン、Pythonの仮想マシンとは大きいな相違を持っていません。Javaを例にすると、開発者はJava言語でプログラムを作成してから、バイトコードにコンパイルし、そして仮想マシンで実行します。

Cocos-BCXは独自の仮想マシンをデザインしたとき、大抵の開発者はLuaに精通しているのを踏まえて、Lua仮想マシンを採用しました。ゲーム開発者にとっては、イーサリアムのSolidity言語やEOSが使用しているC++を勉強しなくても、Lua言語でコントラクトを作成できますので、ハードがかなり低くなりました。

また、仮想マシンを実装した際、Cocos-BCXは既存のLua仮想マシンに対して、機能の削除やインターフェイスの拡張を行いました。