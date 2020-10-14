---
title: "7.5.2 资产相关API"
slug: "752-history-api"
hidden: false
createdAt: "2020-04-29T01:14:50.567Z"
updatedAt: "2020-04-29T10:54:00.665Z"
---
[block:api-header]
{
  "title": "lookup_asset_symbols / 查询资产信息/通过资产Symbol"
}
[/block]

[block:code]
{
  "codes": [
    {
      "code": "curl --location --request POST 'https://test.cocosbcx.net' \\\n--header 'Content-Type: application/json' \\\n--data-raw '{\n  \"id\" : 0,\n  \"method\" : \"call\",\n  \"params\" : [\n    0,\n    \"lookup_asset_symbols\",\n    [\n      [\n        \"COCOS\"\n      ]\n    ]\n  ]\n}'",
      "language": "javascript"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "get_assets / 查询资产信息/通过资产Id"
}
[/block]

[block:code]
{
  "codes": [
    {
      "code": "curl --location --request POST 'https://test.cocosbcx.net' \\\n--header 'Content-Type: application/json' \\\n--data-raw '{\n    \"id\": 22,\n    \"method\": \"call\",\n    \"params\": [\n        0,\n        \"get_assets\",\n        [\n            [\n                \"1.3.0\"\n            ]\n        ]\n    ]\n}'",
      "language": "javascript"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "list_assets / 查询链上发行的所有资产"
}
[/block]
A:  symbol A-Z
100:  查100条
[block:code]
{
  "codes": [
    {
      "code": "curl --location --request POST 'https://test.cocosbcx.net/' \\\n--header 'Content-Type: application/json' \\\n--data-raw '{\n    \"id\": 37,\n    \"method\": \"call\",\n    \"params\": [\n        0,\n        \"list_assets\",\n        [\n            \"A\",\n            100\n        ]\n    ]\n}'",
      "language": "javascript"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "estimation_gas / 获取抵押预估GAS"
}
[/block]
amount：抵押数量 = 实际数量 * 资产精度 ;
asset_id：资产id;
[block:code]
{
  "codes": [
    {
      "code": "{\n    \"id\": 16,\n    \"method\": \"call\",\n    \"params\": [\n        0,\n        \"estimation_gas\",\n        [\n            {\n                \"amount\": 100000,\n                \"asset_id\": \"1.3.0\"\n            }\n        ]\n    ]\n}",
      "language": "javascript"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "get_vesting_balances / 查询可领取的解冻资产"
}
[/block]
包含冻结gas / gas抵押赎回 / 投票抵押赎回 / 节点出块奖励
[block:code]
{
  "codes": [
    {
      "code": "curl --location --request POST 'https://test.cocosbcx.net/' \\\n--header 'Content-Type: application/json' \\\n--data-raw '{\n    \"id\": 29,\n    \"method\": \"call\",\n    \"params\": [\n        0,\n        \"get_vesting_balances\",\n        [\n            \"1.2.17\"\n        ]\n    ]\n}'",
      "language": "javascript"
    }
  ]
}
[/block]