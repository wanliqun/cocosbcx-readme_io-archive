---
title: "Dicing"
slug: "dicing"
hidden: false
createdAt: "2019-03-15T06:30:14.297Z"
updatedAt: "2019-03-17T02:53:55.555Z"
---
[block:api-header]
{
  "title": "Step1: Develop Contract"
}
[/block]
The contract has two interfaces, one for placing a bet and the other for drawing a lottery
[block:code]
{
  "codes": [
    {
      "code": "1) Placing a bet\na. When a user places a bet, the interface is called for inputting the information about the user’s bet and the round of the bet. \nb. After the contract interprets the information about the bet, the related amount is transferred from the user’s account to the contract account.\n\n2. Drawing a lottery \na. When a lottery is drawn, the dealer inputs the round of the lottery and the information of bets from all the players. \nb. The random function is called to generate three random numbers with three dices and the outcomes are computed. \nc. Based on the bets from the players, a lottery is drawn for each player and their income is calculated. The amount is transferred from the dealer’s account to the players’.",
      "language": "text"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "Step2：Client Connection To BCX SDK"
}
[/block]
Log in: call passwordLogin interface for login

Placing a bet and drawing a lottery 
a. call callContractFunction interface and then the functions for placing a bet and drawing a lottery respectively  
b. the outcomes shall be acquired by analyzing the message returned by the interface
[block:api-header]
{
  "title": "Example of Testing"
}
[/block]
test.js contains the following information

Initialize bcx example
 Call passwordLogin interface for login 
Call callContractFunction interface to call contract interface
[block:code]
{
  "codes": [
    {
      "code": "/**\n * Copyright (c) 2018 Xiamen Yaji Software Co.Ltd. All rights reserved.\n * Created by lizhiyi on 2018/10/25.\n */\n\n\nvar constants = require('./../shared/constants');\nvar _ = require('lodash');\nvar bclLibs = require('./../libs/bcx.min');\n\nvar CONTRACT_NAME = 'contract.tychem';\n\nmodule.exports = function (app) {\n    return new ModuleService(app);\n};\n\nvar ModuleService = function (app) {\n    this.app = app;\n    this.isLoginBcl = false;\n};\n\nvar moduleService = ModuleService.prototype;\n\nmoduleService.init = function () {\n    var _configParams={\n        api_node:{\n            url:\"ws://39.106.139.132:8010\",\n            name:\"xxxxxxxx\"\n        },\n        networks:[\n        {\n            core_asset:\"COCOS\",\n            chain_id:\"52e65ef663454f910ba3fe5f0b97a359f6a15aa50a329ae8de4d2b38eb0ee7a1\"\n        }],\n        faucet_url:\"http://39.106.139.132:4000\",\n        auto_reconnect:true,\n        worker:false\n        //app_keys:[\"5HxzZncKDjx7NEaEv989Huh7yYY7RukcJLKBDQztXAmZYCHWPgd\"]\n    };\n\n    var _this = this;\n    this.bcl = new BCX(_configParams);\n    this.bcl.init(function (res) {\n        console.log('init finish:', res);\n        _this.login();\n    });\n};\n\nmoduleService.login = function () {\n    var _this = this;\n    this.bcl.passwordLogin({account: 'xxxxx', password:'xxxxxxxx',  callback: function (result) {\n        _this.account = null;\n        if (result.code === 1) {\n            _this.isLoginBcl = true;\n            _this.account = result.data.account_name;\n            _this.userId = result.data.account_id;\n        }\n        console.log('login result', result);\n    }});\n};\n\nmoduleService.dice = function (roomId, roundId, objBetInfo, callback) {\n    this.bcl.callContractFunction({\n        nameOrId: CONTRACT_NAME,\n        functionName: 'dice',//[\"1\",1000001,'COCOS']\n        valueList:[roomId + '@' + roundId, JSON.stringify(objBetInfo)],////\n        callback:function(res){\n            console.info(\"dice res\",res);\n\n            if (res.code === 1) {\n                //Interpret results and directly return the corresponding numbers\n                var arrAffect = res.data[0].contract_affecteds;\n                console.log(arrAffect);\n                for (var idx = 0; idx < arrAffect.length; idx++) {\n                    if (arrAffect[idx].type === \"contract_affecteds_log\") {\n                        var text = arrAffect[idx].raw_data.message;\n                        var key = \"##result##:\";\n                        var idxFind = text.indexOf(key);\n                        if (idxFind !== -1) {\n                            var jsonStr = text.slice(idxFind + key.length);\n                            var result = JSON.parse(jsonStr);\n\n                            result.trx_id = res.trx_data.trx_id;\n\n                            if (callback) {\n                                callback(null, result);\n                                return;\n                            }\n                            break;\n                        }\n                    }\n                }\n\n                if (callback) {\n                    callback('result formate was error!', res);\n                }\n            } else if (callback) {\n                callback(res.message, res);\n            }\n        }\n    });\n};\n\n/**\n * Query the information about the bets from players according to transaction ID\n * @param {String} TXID transaction ID\n * @param {Function} callback\n */\nmoduleService.queryBetInfo = function (TXID, callback) {\n    this.bcl.queryTransaction({\n        transactionId: TXID,\n        callback:function (res) {\n            if (res.code !== 1) {\n                callback(res.message, res);\n                return;\n            }\n\n            if (!res.data || !res.data.parse_ops || !res.data.parse_ops[0]) {\n                callback('result formate was error!', res);\n            }\n\n            var parse =  res.data.parse_ops[0];\n            var arrAffect = parse.result.contract_affecteds;\n\n            for (var idx = 0; idx < arrAffect.length; idx++) {\n                if (arrAffect[idx].type === \"contract_affecteds_log\") {\n                    var text = arrAffect[idx].parse_operations_text;\n                    var key = \"##result##:\";\n                    var idxFind = text.indexOf(key);\n\n                    if (idxFind !== -1) {\n                        var jsonStr = text.slice(idxFind + key.length);\n                        var result = JSON.parse(jsonStr);\n\n                        if (callback) {\n                            callback(null, result);\n                            return;\n                        }\n                        break;\n                    }\n                }\n            }\n\n            if (callback) {\n                callback('result formate was error!', res);\n            }\n        },\n    });\n};",
      "language": "javascript"
    }
  ]
}
[/block]