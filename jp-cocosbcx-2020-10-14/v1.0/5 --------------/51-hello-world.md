---
title: "5.1 Hello World！"
slug: "51-hello-world"
hidden: false
createdAt: "2019-09-17T08:36:34.432Z"
updatedAt: "2019-09-17T08:45:11.650Z"
---
プログラミング言語の最初のレッスンとして、Hello Worldの紹介から始めましょう。

1．コマンドラインまたはGUIを利用し、helloディレクトリを作成します。
[block:code]
{
  "codes": [
    {
      "code": "cd CONTRACTS_DIR\nmkdir hello\ncd hello",
      "language": "shell"
    }
  ]
}
[/block]
2．hello.luaファイルを作成し、エディタで開きます。
[block:code]
{
  "codes": [
    {
      "code": "touch hello.lua",
      "language": "shell"
    }
  ]
}
[/block]
3．hello.luaへコードを書きます。
[block:code]
{
  "codes": [
    {
      "code": "function hello()\n    chainhelper:log('Hello World!')\nend\n",
      "language": "lua"
    }
  ]
}
[/block]
4．テスト用アカウントへログインし、cli.walletでコントラクトをデプロイします。
[block:code]
{
  "codes": [
    {
      "code": "create_contract chandlerette contract.helloraven \"COCOS8EgNn68Pydk3QatmPQc2mWJNYLP8w6ezszvfwEBygXxT5BKi4j\" \"function hello() chainhelper:log('Hello World!') end\" true",
      "language": "shell"
    }
  ]
}
[/block]
5．Terminal内のブラウザでコントラクトを確認します。
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/3f1a504-image001.png",
        "image001.png",
        865,
        236,
        "#292e33"
      ]
    }
  ]
}
[/block]
6．cli.walletでhelloインターフェイスをコールします。
call_contract_function chandlerette contract.helloraven hello [] true

7．Terminal内のブラウザで取引履歴を照会します。
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/03167e5-image003.png",
        "image003.png",
        864,
        255,
        "#2b2f36"
      ]
    }
  ]
}
[/block]
8．日時をプリントする場合、コードを以下のように修正します。
[block:code]
{
  "codes": [
    {
      "code": "function hello()\n    chainhelper:log('Hello World!')\n    chainhelper:log(date('%Y-%m-%dT%H:%M:%S', chainhelper:time()))\nend",
      "language": "lua"
    }
  ]
}
[/block]
9．cli.walletでコントラクトをリネームし、アップデートします。
[block:code]
{
  "codes": [
    {
      "code": "revise_contract chandlerette contract.helloraven \"function hello() chainhelper:log('Hello World!') chainhelper:log(date('%Y-%m-%dT%H:%M:%S', chainhelper:time())) end\" true",
      "language": "shell"
    }
  ]
}
[/block]
10．Terminal内のブラウザでアップデート後の取引履歴を照会します。
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/bf9f354-image005.png",
        "image005.png",
        1298,
        304,
        "#292d33"
      ]
    }
  ]
}
[/block]
11．cli.walletでhelloインターフェイスを再びコールします。
[block:code]
{
  "codes": [
    {
      "code": "call_contract_function chandlerette contract.helloraven hello [] true",
      "language": "shell"
    }
  ]
}
[/block]
12．Terminal内のブラウザで取引履歴を照会します。
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/c785f47-image007.png",
        "image007.png",
        865,
        316,
        "#2d3138"
      ]
    }
  ]
}
[/block]
まとめ
Hello Worldを例にしてコントラクトを作成、デプロイとアップデートのプロセスを簡単に説明しました。Lua言語の特徴によって、コントラクトコードを中間コードへの変換なしに、直接オンチェーンで実行します。プライバシー面では弱まっていますが、公開透明性が保証できます。