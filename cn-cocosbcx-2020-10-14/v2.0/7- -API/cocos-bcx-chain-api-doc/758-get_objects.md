---
title: "7.5.8 get_objects"
slug: "758-get_objects"
hidden: false
createdAt: "2020-04-29T10:40:05.879Z"
updatedAt: "2020-04-29T10:56:50.980Z"
---
[block:api-header]
{
  "title": "get_objects / 通过id获取id对应的数据信息。"
}
[/block]
（账户id对应的账户信息，资产id对应的资产信息，合约id对应的合约信息……）
[block:code]
{
  "codes": [
    {
      "code": "curl --location --request POST 'https://test.cocosbcx.net/' \\\n--header 'Content-Type: application/json' \\\n--data-raw '{\n  \"id\" : 4,\n  \"method\" : \"call\",\n  \"params\" : [\n    0,\n    \"get_objects\",\n    [\n      [\n        \"2.1.0\"\n      ]\n    ]\n  ]\n}\n'",
      "language": "javascript"
    }
  ]
}
[/block]