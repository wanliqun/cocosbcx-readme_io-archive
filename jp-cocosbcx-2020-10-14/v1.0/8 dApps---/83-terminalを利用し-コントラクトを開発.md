---
title: "8.3 Terminalでコントラクトを開発"
slug: "83-terminalを利用し-コントラクトを開発"
excerpt: "Cocos Terminalは「ツールキット」に「コントラクト管理」機能を追加しました。\nこの機能を使って、コントラクトの作成、アップデート、実行がより簡単になります。"
hidden: false
createdAt: "2019-09-27T02:18:23.508Z"
updatedAt: "2019-11-29T07:57:44.870Z"
---
[block:api-header]
{
  "title": "コントラクト作成"
}
[/block]
**1．ツールについて**

a．[Terminal]( http://cocos-terminal.com/#/)からCocos-BCXアカウントにログインしてください。
b．ディレクトリの「コントラクト管理」からアカウント内すべてのコントラクト情報（コントラクトの基本情報、コード、インタフェース、public_dataなど）が確認できます。
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/2307442-image026.png",
        "image026.png",
        850,
        399,
        "#2b2d2f"
      ]
    }
  ]
}
[/block]
**2．コントラクト作成** 
a．「コントラクト追加」をクリックし、コントラクトを作成してください。
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/a16ee28-image028.png",
        "image028.png",
        850,
        399,
        "#2b2d2f"
      ]
    }
  ]
}
[/block]
b．枠内にコントラクト名を入力してください。命名ルール：必ず「contract.」で始まり、小文字アルファベットと数字の組合せ、長さは4～63桁。例：contract.testnew
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/07900ae-image031.png",
        "image031.png",
        538,
        259,
        "#50555c"
      ]
    }
  ]
}
[/block]
**3．コントラクトコードを書き、既存コントラクトをアップデート** 
[block:code]
{
  "codes": [
    {
      "code": "function hello()\n    chainhelper:log('Hello World! contract.testnew')\nend",
      "language": "lua"
    }
  ]
}
[/block]
**4．コントラクトリリース**
a．「リリース」をクリックしてください。
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/a8b370f-image034.png",
        "image034.png",
        851,
        391,
        "#242425"
      ]
    }
  ]
}
[/block]
b．「ランダム生成」をクリックしてください。コントラクトの権限認証が存在する場合、JS-SDKのapp_keysの設定欄にkeyを入力する必要があります。コピーして保存してください。
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/685ec9e-image036.png",
        "image036.png",
        851,
        458,
        "#484b51"
      ]
    }
  ]
}
[/block]
c．「確認」をクリックしてください。また、コントラクトを作成するには一定の手数料がかかります。
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/59b4071-image040.jpg",
        "image040.jpg",
        850,
        442,
        "#393d44"
      ]
    }
  ]
}
[/block]
**5．コントラクトのコール** 
a．コントラクトをリリースしたら、下図矢印で示したところでコントロールのインタフェースが確認できます。パラメーターを入力し、インタフェースをコールしてください。
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/0cbeeb9-image042.png",
        "image042.png",
        850,
        331,
        "#262626"
      ]
    }
  ]
}
[/block]
b．コントロールをコールするには一定の手数料がかかります。
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/974f8b5-image044.png",
        "image044.png",
        850,
        492,
        "#2b2e33"
      ]
    }
  ]
}
[/block]
c．コール結果は編集エリアの下に表示されます。
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/948b4fa-image047.png",
        "image047.png",
        1165,
        711,
        "#212121"
      ]
    }
  ]
}
[/block]
**6．コントラクトのアップデート**
a．init_data()でデータを初期化します。
[block:code]
{
  "codes": [
    {
      "code": "function hello()\n    chainhelper:log('Hello World! contract.testnew')\nend\n\nfunction hello2(num,amount)\n\tchainhelper:log('=======loooooog starts=======');\n\tchainhelper:log('{\"num\": \"'..num..'\",\"amount\":\"'..amount..'\"}');\n\tchainhelper:log('=======log ends=======');\nend\n\nfunction init_data()\n    read_list = {public_data={initdata=true}}\n    chainhelper:read_chain()\n    public_data.initdata  = 98\n    write_list = {public_data={initdata=true}}\n    chainhelper:write_chain()\nend",
      "language": "lua"
    }
  ]
}
[/block]
b．リリースをクリックしたら、既存のコントラクトデータが上書きされ、新しいコントラクトに変わります。リリース後、init_data()をコールしてから初めてデータの初期化が完了になります。
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/2818057-image050.png",
        "image050.png",
        1119,
        567,
        "#2a2e32"
      ]
    }
  ]
}
[/block]
c．「データ」をクリックし、初期化されたデータが確認できます。
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/98576fa-image052.png",
        "image052.png",
        1435,
        621,
        "#252627"
      ]
    }
  ]
}
[/block]
**6．コントラクト照会** 
検索欄からコントラクト名を入力し、検索をクリックしてください。

a．コントラクトの基本情報の照会
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/b961eab-image056.png",
        "image056.png",
        1662,
        705,
        "#404349"
      ]
    }
  ]
}
[/block]
b．統計データ。コール回数、トークンの取引量などが確認できます。
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/6418203-image059.png",
        "image059.png",
        850,
        419,
        "#34383e"
      ]
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "コントラクト統計"
}
[/block]
a．Cocos Terminalはよくコールされるコントラクトのランキングを提供します。コール回数、基本情報や実行結果が照会できます。
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/358941a-image064.png",
        "image064.png",
        850,
        399,
        "#34393f"
      ]
    }
  ]
}
[/block]
b．「コントラクト」をクリックし、コード、データや統計データが照会できます。
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/5740fba-image066.png",
        "image066.png",
        851,
        379,
        "#31353b"
      ]
    }
  ]
}
[/block]