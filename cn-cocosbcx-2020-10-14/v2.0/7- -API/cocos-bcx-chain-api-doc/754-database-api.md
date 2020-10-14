---
title: "7.5.4 交易相关API"
slug: "754-database-api"
hidden: false
createdAt: "2020-04-29T01:14:51.367Z"
updatedAt: "2020-04-29T10:54:49.121Z"
---
[block:api-header]
{
  "title": "get_transaction_by_id / 通过trx_id 查询交易信息"
}
[/block]

[block:code]
{
  "codes": [
    {
      "code": "curl --location --request POST 'https://test.cocosbcx.net' \\\n--header 'Content-Type: application/json' \\\n--data-raw '{\n    \"method\": \"call\",\n    \"params\": [\n        0,\n        \"get_transaction_by_id\",\n        [\n            \"01cb8270dc0855c8f05364820f4d7bc99d454f801aba5a9c11e4db75d06527d1\"\n        ]\n    ],\n    \"id\": 21\n}'",
      "language": "javascript"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "get_transaction_in_block_info / 通过trx_id查询交易所在区块"
}
[/block]

[block:code]
{
  "codes": [
    {
      "code": "curl --location --request POST 'https://test.cocosbcx.net' \\\n--header 'Content-Type: application/json' \\\n--data-raw '{\n    \"method\": \"call\",\n    \"params\": [\n        0,\n        \"get_transaction_in_block_info\",\n        [\n            \"01cb8270dc0855c8f05364820f4d7bc99d454f801aba5a9c11e4db75d06527d1\"\n        ]\n    ],\n    \"id\": 13\n}'",
      "language": "javascript"
    }
  ]
}
[/block]