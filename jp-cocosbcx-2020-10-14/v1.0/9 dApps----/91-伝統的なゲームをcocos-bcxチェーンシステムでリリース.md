---
title: "9.1 伝統的なゲームをCocos-BCXチェーンシステムでリリース"
slug: "91-伝統的なゲームをcocos-bcxチェーンシステムでリリース"
hidden: false
createdAt: "2019-09-27T03:32:43.522Z"
updatedAt: "2019-09-27T05:15:47.686Z"
---
[block:api-header]
{
  "title": "1．順番を追って関連ファイルをインポートします"
}
[/block]
a．cdnを通してインポート
[block:code]
{
  "codes": [
    {
      "code": "// JSSDKファイル、リンク、署名付きツールキットをインポートします \n <script src=\"https://jdi.cocosbcx.net/static/js/bcx.min.js\"></script>\n <script src=\"https://jdi.cocosbcx.net/static/js/core.min.js\"></script>\n <script src=\"https://jdi.cocosbcx.net/static/js/plugin.min.js\"></script>",
      "language": "javascript"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "2．SDKオブジェクトを確認します"
}
[/block]
a．リンクを作り、チェーンとインタラクションするSDKオブジェクトを初期化します。
[block:code]
{
  "codes": [
    {
      "code": "var _configParams = {\n      ws_node_list: [{\n        url: \"ws://39.106.126.54:8049\",\n        name: \"COCOS3.0ノード2\"\n      }],\n      networks: [{\n        core_asset: \"COCOS\",\n        chain_id: '7d89b84f22af0b150780a2b121aa6c715b19261c8b7fe0fda3a564574ed7d3e9'\n      }],\n      // faucet_url:\"http://47.93.62.96:3000\",\n      faucetUrl: 'http://47.93.62.96:8041',\n      auto_reconnect: true,\n      worker: false,\n      real_sub: true,\n      check_cached_nodes_data: true,\n      // app_keys: [\"5HxzZncKDjx7NEaEv989Huh7yYY7RukcJLKBDQztXAmZYCHWPgd\"]\n    };\n    bcx = new BCX(_configParams);",
      "language": "text"
    }
  ]
}
[/block]
b．モバイルウォレット（AndroidWallet、iOSWalletまたはGooglePlug-in Wallet）にインジェクションされたSDKオブジェクトの存在をテストします。存在した場合、1で作成したSDKオブジェクトを上書きします。（備考：モバイルウォレットとGoogleプラグインウォレットの場合だと、インポートを通して、BcxWebオブジェクトをWindowでマウントします。）
[block:code]
{
  "codes": [
    {
      "code": "if (window.BcxWeb) {\n         // The injected object exists, covering the Sdk interface object.\n          bcx = window.BcxWeb\n          })\n          return\n        }\n  // The injection object window.BcxWeb does not exist, the timer is started to perform timing detection.\n  let timer = null\n        clearInterval(timer)\n        timer = setInterval(() => {\n          if (window.BcxWeb) {\n              // Cover the Sdk interface object and return\n               bcx = window.BcxWeb       \n                return\n              } \n            })\n            clearInterval(timer)\n          }\n        }, 1000)\n\n Cocosjs.plugins(new CocosBCX())\n        await Cocosjs.cocos.connect('My-App').then(connected => {\n          if (!connected) {\n            return\n          }\n          //Connecting successfully and clearing timer\n          clearInterval(timer)\n          const cocos = Cocosjs.cocos\n          //Overwrite the write SDK interface object,\n          bcx = cocos.cocosBcx(bcx)\n        })",
      "language": "javascript"
    }
  ]
}
[/block]
検波を機能して、デスクトップウォレットへアクセスしてみてください。（Googleプラグインウォレットとデスクトップウォレット（windows/mac）両方インストールしている場合、最初にbcxオブジェクトを入手したウォレットがdappとインタラクションすることになります）。
[block:api-header]
{
  "title": "3．SDKオブジェクトのコール例"
}
[/block]

[block:code]
{
  "codes": [
    {
      "code": "// アカウント内残高を確認します\nbcx.queryAccountBalances({\n  assetId: \"COCOS\",//トークンシンボル\n  account: 'test1' // アカウント名\n}).then(()=>{})\n\n// コントラクトのコール方\nbcx.callContractFunction({\n  nameOrId: \"contract.dicegame\", // contract\n  functionName: \"bet\", // operation\n  valueList: [rollUnder, cocos], //rollUnder and coin\n  runtime: 10,\n  onlyGetFee: false\n}).then(()=>{})",
      "language": "javascript"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "4．dApp例"
}
[/block]
[Demo](https://github.com/Cocos-BCX/cocos-dice-sample)