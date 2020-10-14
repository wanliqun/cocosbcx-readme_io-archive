---
title: "9.1 Interfacing Traditional Games into Cocos-BCX Chain System"
slug: "91-link-method"
hidden: false
createdAt: "2019-06-24T07:25:15.965Z"
updatedAt: "2019-07-19T07:48:10.447Z"
---
1. Import the relevant js files in order 
a. import in cdn way
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
b. import local file
Download the above files and place them into the local folder, importing them one by one in the local import way.
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
2. Find SDK objects
a. Build a link and initialize the Sdk interface object that interacts with the chain
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
b. Detect whether the Sdk object injected by the mobile wallet ([AndroidWallet](https://github.com/Cocos-BCX/AndroidWallet), [iOSWallet](https://github.com/Cocos-BCX/IOSWallet) or [Goole plugin wallet](https://github.com/Cocos-BCX/CocosPay)) exists, and if it exists, overwrite the Sdk interface object created in 1. (Mobile wallet and Goole plugin wallet will mount a BcxWeb object on the window by injection.）

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
After starting the detection, it will try to link your desktop wallet. (If the user installs both the Goole plugin and the desktop wallet: windows, mac, the wallet that first gets the bcx object will interact with the DApp)

3. Call SDK Object Example
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
4. DApp Demo
[Demo](https://github.com/Cocos-BCX/cocos-dice-sample)