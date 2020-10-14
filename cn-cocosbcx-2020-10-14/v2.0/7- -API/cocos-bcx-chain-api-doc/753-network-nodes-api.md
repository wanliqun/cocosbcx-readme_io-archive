---
title: "7.5.3 合约相关API"
slug: "753-network-nodes-api"
hidden: false
createdAt: "2020-04-29T01:14:49.250Z"
updatedAt: "2020-04-29T10:54:30.420Z"
---
[block:api-header]
{
  "title": "get_contract / 通过合约id/合约名称查询合约信息"
}
[/block]
合约名称查询

[block:code]
{
  "codes": [
    {
      "code": "curl --location --request POST 'https://test.cocosbcx.net' \\\n--header 'Content-Type: application/json' \\\n--data-raw '{\n    \"id\": 47,\n    \"method\": \"call\",\n    \"params\": [\n        0,\n        \"get_contract\",\n        [\n            \"contract.contractname\"\n        ]\n    ]\n}'",
      "language": "javascript"
    }
  ]
}
[/block]

合约id查询
[block:code]
{
  "codes": [
    {
      "code": "curl --location --request POST 'https://test.cocosbcx.net' \\\n--header 'Content-Type: application/json' \\\n--data-raw '{\n    \"id\": 47,\n    \"method\": \"call\",\n    \"params\": [\n        0,\n        \"get_contract\",\n        [\n            \"1.16.10\"\n        ]\n    ]\n}'",
      "language": "javascript"
    }
  ]
}
[/block]