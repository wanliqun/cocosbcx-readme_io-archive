---
title: "5.6 Sample of Contract Call"
slug: "56-samples-of-contract-mutual-call"
hidden: false
createdAt: "2019-09-30T03:13:59.756Z"
updatedAt: "2019-10-09T08:31:29.805Z"
---
## Call another contract in one contract, and in this sample, contract 2 calls the method in contract 1

**Sample contract 1**

**Contract name**
contract.test002
[block:code]
{
  "codes": [
    {
      "code": "function logtest()\n\tchainhelper:log('hello world')\n\tchainhelper:log(date('%Y-%m-%dT%H:%M:%S', chainhelper:time()))\nend\n\nfunction handsome_parem(num,amount)\n\tchainhelper:log('=======log starts=======');\n\tchainhelper:log('{\"num\": \"'..num..'\",\"amount\":\"'..amount..'\"}');\n\tchainhelper:log('=======log ends=======');\nend",
      "language": "lua"
    }
  ]
}
[/block]
**Sample contract 2**

**Contract name**
contract.test003
[block:code]
{
  "codes": [
    {
      "code": "function raven_call_handsome_parem(num1,num2)\n    -- contract name: contract.test002\n    local temp=import_contract('contract.test002')\n    temp.chainhelper=chainhelper\n    chainhelper:log('{\"name\": \"raven\",\"num1\": \"'..num1..'\",\"num2\":\"'..num2..'\"}');\n    chainhelper:log('xxxxx call test002 handsome_parem begin xxxxx');\n    temp.handsome_parem(num1,num2);\n    chainhelper:log('xxxxx call test002 handsome_parem end xxxxx');\nend\n\nfunction raven_call_logtest()\n    -- contract name: contract.test002\n    local temp=import_contract('contract.test002')\n    temp.chainhelper=chainhelper\n    chainhelper:log('xxxxx call test002 logtest begin xxxxx');\n    --because method logtest() in contract 1 calls method date(), so need temp.date = date, if other is needed, same way\n    temp.date = date;\n    temp.logtest();\n    chainhelper:log('xxxxx call test002 logtest end xxxxx');\nend",
      "language": "lua"
    }
  ]
}
[/block]
**Call result**
The following is a screenshot of the results of calling the raven_call_handsome_parent method in the sample contract 2
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/a19c1db-cb9499b-_20190709155214.png",
        "cb9499b-_20190709155214.png",
        969,
        619,
        "#2e3339"
      ]
    }
  ]
}
[/block]