---
title: "7.5.5 非同质资产相关API"
slug: "755-miscellaneous-api"
hidden: false
createdAt: "2020-04-29T08:46:59.584Z"
updatedAt: "2020-04-29T10:55:34.119Z"
---
[block:api-header]
{
  "title": "lookup_nh_asset / 通过id查询非同质资产信息"
}
[/block]

[block:code]
{
  "codes": [
    {
      "code": "curl --location --request POST 'https://test.cocosbcx.net' \\\n--header 'Content-Type: application/json' \\\n--data-raw '{\n    \"method\": \"call\",\n    \"params\": [\n        0,\n        \"lookup_nh_asset\",\n        [\n            [\n                \"4.2.1\"\n            ]\n        ]\n    ],\n    \"id\": 1326\n}'",
      "language": "javascript"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "list_account_nh_asset / 查询账户下所拥有的NH资产"
}
[/block]
[
            "1.2.73", //账户id
            [], // 世界观
            100, // pageSize
            1, // page
            4
 ]
[block:code]
{
  "codes": [
    {
      "code": "curl --location --request POST 'https://test.cocosbcx.net' \\\n--header 'Content-Type: application/json' \\\n--data-raw '{\n    \"method\": \"call\",\n    \"params\": [\n        0,\n        \"list_account_nh_asset\",\n        [\n            \"1.2.73\",\n            [],\n            100,\n            1,\n            4\n        ]\n    ],\n    \"id\": 1129\n}'",
      "language": "javascript"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "list_account_nh_asset_order / 查询账户下的NH资产售卖单"
}
[/block]
[
            "1.2.73", // 账户id;
            10, // pageSize
            1 // page
 ]
[block:code]
{
  "codes": [
    {
      "code": "curl --location --request POST 'https://test.cocosbcx.net' \\\n--header 'Content-Type: application/json' \\\n--data-raw '{\n    \"method\": \"call\",\n    \"params\": [\n        0,\n        \"list_account_nh_asset_order\",\n        [\n            \"1.2.73\",\n            10,\n            1\n        ]\n    ],\n    \"id\": 1332\n}'",
      "language": "javascript"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "list_nh_asset_order / 查询全网NH资产售卖单"
}
[/block]
[
            "COCOS", // 通行资产
            "", // 世界观
            "", // 基础数据
            10,// pagesize
            1, // page
            true
   ]

[block:code]
{
  "codes": [
    {
      "code": "\ncurl --location --request POST 'https://test.cocosbcx.net' \\\n--header 'Content-Type: application/json' \\\n--data-raw '{\n    \"method\": \"call\",\n    \"params\": [\n        0,\n        \"list_nh_asset_order\",\n        [\n            \"COCOS\",\n            \"\",\n            \"\",\n            10,\n            1,\n            true\n        ]\n    ],\n    \"id\": 2\n}'",
      "language": "javascript"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "lookup_world_view / 查询世界观详细信息"
}
[/block]

[block:code]
{
  "codes": [
    {
      "code": "curl --location --request POST 'https://test.cocosbcx.net' \\\n--header 'Content-Type: application/json' \\\n--data-raw '{\n    \"method\": \"call\",\n    \"params\": [\n        0,\n        \"lookup_world_view\",\n        [\n            [\n                \"worldview\"\n            ]\n        ]\n    ],\n    \"id\": 1425\n}'",
      "language": "javascript"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "get_nh_creator  / 查询开发者关联的世界观"
}
[/block]
查询账户需注册开发者
[block:code]
{
  "codes": [
    {
      "code": "curl --location --request POST 'https://test.cocosbcx.net' \\\n--header 'Content-Type: application/json' \\\n--data-raw '{\n    \"method\": \"call\",\n    \"params\": [\n        0,\n        \"get_nh_creator\",\n        [\n            \"1.2.17\"\n        ]\n    ],\n    \"id\": 1439\n}'",
      "language": "javascript"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "list_nh_asset_by_creator / 查询开发者所创建的NH资产"
}
[/block]
查询账户需注册开发者
 [
            "1.2.17",//帐户id
            "", // 世界观
            1, // pageSize
            1 // page
  ]
[block:code]
{
  "codes": [
    {
      "code": "curl --location --request POST 'https://test.cocosbcx.net' \\\n--header 'Content-Type: application/json' \\\n--data-raw '{\n    \"id\": 34,\n    \"method\": \"call\",\n    \"params\": [\n        0,\n        \"list_nh_asset_by_creator\",\n        [\n            \"1.2.17\",\n            \"\",\n            1,\n            1\n        ]\n    ]\n}'",
      "language": "javascript"
    }
  ]
}
[/block]