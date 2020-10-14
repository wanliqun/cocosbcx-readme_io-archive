---
title: "11.1  Homogeneous Assets"
slug: "101-homogeneous-assets"
hidden: false
createdAt: "2019-06-24T07:15:32.999Z"
updatedAt: "2020-03-02T09:34:04.401Z"
---
##1.Create Homogeneous Assets

Open command line wallet, and execute the command:

**Command Format:** 
[block:code]
{
  "codes": [
    {
      "code": "create_asset <issuer> <symbol> <precision> <common> <bitasset_operations> <broadcast>",
      "language": "shell"
    }
  ]
}
[/block]
Example:

[block:code]
{
  "codes": [
    {
      "code": "create_asset official-account MYCOIN 5 {\"max_supply\" : 100000000,\"market_fee_percent\" : 0,\"max_market_fee\" : 0,\"core_exchange_rate\" : {\"base\": {\"amount\": 10,\"asset_id\": \"1.3.0\"},\"quote\": {\"amount\": 10,\"asset_id\": \"1.3.1\"}},\"description\" : \"asset description\"} null true",
      "language": "shell"
    }
  ]
}
[/block]
**Parameters Explanation:**
 
max_supply: maximum circulation of assets

market_fee_percent: the ratio of the fee paid to the publishers when trading the assets. The default value is 0 and turns to 1% if set to 100

max_market_fee: the maximum fee paid to the publishers when trading the assets
core_exchange_rate: the exchange rate between the assets and core assets 

description: description of the assets

The parameters of <bitasset_operations> are set to null since the issued assets are non-bit assets. And it can be set to {} and default value when issuing the bit assets


##2. Issue homogeneous assets

**Command Format:** 
[block:code]
{
  "codes": [
    {
      "code": "issue_asset <to_account> <amount> <symbol> <memo> <broadcast>",
      "language": "shell"
    }
  ]
}
[/block]
 Example:
[block:code]
{
  "codes": [
    {
      "code": "issue_asset eg-account 100 MYCOIN “issue asset to you” true",
      "language": "shell"
    }
  ]
}
[/block]
**Tips**

Demo program of JS-SDK (provided by Cocos-BCX) can be used for issuing homogeneous assets as well.