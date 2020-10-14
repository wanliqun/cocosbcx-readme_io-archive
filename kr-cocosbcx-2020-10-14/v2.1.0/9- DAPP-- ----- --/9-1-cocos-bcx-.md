---
title: "9.1 전통적인 게임을 Cocos-BCX 체인 시스템에 인터페이스"
slug: "9-1-cocos-bcx-"
hidden: false
createdAt: "2019-08-26T04:48:34.419Z"
updatedAt: "2019-08-26T05:02:01.769Z"
---
1. 관련 js 파일을 순서대로 가져 오기
a. CDN방식으로 가져오기
[block:code]
{
  "codes": [
    {
      "code": "// Import JSSDK files, links and signature toolkit \n <script src=\"https://jdi.cocosbcx.net/static/js/bcx.min.js\"></script>\n <script src=\"https://jdi.cocosbcx.net/static/js/core.min.js\"></script>\n <script src=\"https://jdi.cocosbcx.net/static/js/plugin.min.js\"></script>",
      "language": "javascript"
    }
  ]
}
[/block]
b. 로컬 파일 가져 오기
위 파일을 다운로드하여 로컬 가져오기 방식으로 하나씩 가져와서 로컬 폴더에 배치하십시오.
[block:code]
{
  "codes": [
    {
      "code": "<script src=\"bcx.min.js\"></script>\n<script src=\"core.min.js\"></script>\n<script src=\"plugin.min.js\"></script>",
      "language": "javascript"
    }
  ]
}
[/block]
2. SDK객체 찾기
a. 링크를 구축하고 체인과 상호 작용하는 SDK 인터페이스 객체를 초기화하십시오.
[block:code]
{
  "codes": [
    {
      "code": "var _configParams = {\n      ws_node_list: [{\n        url: \"ws://39.106.126.54:8049\",\n        name: \"COCOS3.0节点2\"\n      }],\n      networks: [{\n        core_asset: \"COCOS\",\n        chain_id: '7d89b84f22af0b150780a2b121aa6c715b19261c8b7fe0fda3a564574ed7d3e9'\n      }],\n      // faucet_url:\"http://47.93.62.96:3000\",\n      faucetUrl: 'http://47.93.62.96:8041',\n      auto_reconnect: true,\n      worker: false,\n      real_sub: true,\n      check_cached_nodes_data: true,\n      // app_keys: [\"5HxzZncKDjx7NEaEv989Huh7yYY7RukcJLKBDQztXAmZYCHWPgd\"]\n    };\n    bcx = new BCX(_configParams);",
      "language": "javascript"
    }
  ]
}
[/block]
b. 모바일 지갑 ([AndroidWallet](https://github.com/Cocos-BCX/AndroidWallet), [iOSWallet](https://github.com/Cocos-BCX/IOSWallet), 혹은 [구글플러그인 지갑](https://github.com/Cocos-BCX/CocosPay) 에 의해 삽입된 SDK객체의 존재를 감지합니다. 또한 기존에 이미 존재하고 있는 객체가 있다면 SDK 인터페이스 객체를 덮어 씁니다. (모바일 지갑과 Goole 플러그인 지갑은 BcxWeb 객체를 주입)
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
디텍션이 시작되면 데스크탑 지갑을 연결하려고 시도합니다. (사용자가 Goole 플러그인과 데스크톱 월렛 (windows, mac)을 모두 설치하면 BCX객체를 처음받는 월렛은 DApp과 상호 작용합니다)

3. SDK 객체 호출 예제
[block:code]
{
  "codes": [
    {
      "code": "// Get Account Balance\nbcx.queryAccountBalances({\n  assetId: \"COCOS\",//Asset Tag\n  account: 'test1' // Username\n}).then(()=>{})\n\n// Way to call contract\nbcx.callContractFunction({\n  nameOrId: \"contract.dicegame\", // contract\n  functionName: \"bet\", // operation\n  valueList: [rollUnder, cocos], //rollUnder and coin\n  runtime: 10,\n  onlyGetFee: false\n}).then(()=>{})",
      "language": "javascript"
    }
  ]
}
[/block]
4. DApp 데모
[Demo](https://github.com/Cocos-BCX/cocos-dice-sample)