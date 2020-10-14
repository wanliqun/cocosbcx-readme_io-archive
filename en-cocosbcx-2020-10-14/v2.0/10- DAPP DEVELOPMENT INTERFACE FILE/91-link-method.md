---
title: "10.1 Interfacing Traditional Games into Cocos-BCX Chain System"
slug: "91-link-method"
hidden: false
createdAt: "2019-06-24T07:25:15.965Z"
updatedAt: "2020-03-03T08:48:18.444Z"
---
## 1. Import the relevant js files in order 

**import in cdn way**
[block:code]
{
  "codes": [
    {
      "code": "// Import JSSDK files, links and signature toolkit \n <script src=\"https://jdi.cocosbcx.net/static/js/bcx.min.js\"></script>\n <script src=\"https://jdi.cocosbcx.net/static/js/core.min.js\"></script>",
      "language": "javascript"
    }
  ]
}
[/block]
##2. Find SDK objects
**a. Build a link and initialize the Sdk interface object that interacts with the chain
**b. Detect whether the Sdk object injected by the mobile wallet ([AndroidWallet](https://github.com/Cocos-BCX/AndroidWallet), [iOSWallet](https://github.com/Cocos-BCX/IOSWallet) or [Goole plugin wallet](https://github.com/Cocos-BCX/CocosPay)) exists, and if it exists, overwrite the Sdk interface object created in 1. (Mobile wallet and Goole plugin wallet will mount a BcxWeb object on the window by injection.）



[block:code]
{
  "codes": [
    {
      "code": "try {\n    if (window.BcxWeb) {\n        bcx = window.BcxWeb\n        bcx.getAccountInfo().then(res => {\n            console.log(\"getAccountInfo---res\", res);\n        })\n        return\n    }\n    let timer = null\n    clearInterval(timer)\n    timer = setInterval(() => {\n        if (window.BcxWeb) {\n            bcx = window.BcxWeb\n            bcx.getAccountInfo().then(res => {\n                if (res.locked) {\n                    Message({\n                        duration: 1200,\n                        message: 'Account Locked',\n                        type: 'error',\n                    })\n                    return\n                }\n            })\n            clearInterval(timer)\n        }\n    }, 1000)\n} catch (e) {\n    console.log(\"error----\",e);\n}",
      "language": "javascript"
    }
  ]
}
[/block]
After starting the detection, it will try to link your desktop wallet. (If the user installs both the Goole plugin  the wallet that first gets the bcx object will interact with the DApp)

##3. Call SDK Object Example
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
##4. DApp Demo
##[Demo](https://github.com/Cocos-BCX/cocos-dice-sample)