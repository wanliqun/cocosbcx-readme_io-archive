---
title: "Release of Homogeneous Assets"
slug: "release-of-homogeneous-assets"
hidden: false
createdAt: "2019-03-15T06:25:32.998Z"
updatedAt: "2019-03-16T16:10:12.344Z"
---
[block:api-header]
{
  "title": "1. Create Homogeneous Assets"
}
[/block]
Open command line wallet and execute the following command: 
Command format:
[block:code]
{
  "codes": [
    {
      "code": "create_asset <issuer> <symbol> <precision> <common> <bitasset_operations> <broadcast>",
      "language": "lua"
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
      "language": "lua"
    }
  ]
}
[/block]
**Parameter explanation:** 
max_supply:Maximum issue of assets

market_fee_percent: The ratio of service charge paid to the issuer in assets trading. Default value is 0. If it's set as 100, the ratio is 1%

max_market_fee:The maximum service charge paid to the issuer in assets trading

core_exchange_rate:Conversion rate of the assets and core assets

description：Assets description

Since issued assets are non-bit assets, <bitasset_operations> parameter is set to null. If it needs to issue bit assets, set the parameter as {} and use system default parameter.
[block:api-header]
{
  "title": "Release Homogeneous Assets"
}
[/block]
Command format: 
[block:code]
{
  "codes": [
    {
      "code": "issue_asset <to_account> <amount> <symbol> <memo> <broadcast>",
      "language": "lua"
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
      "language": "lua"
    }
  ]
}
[/block]