---
title: "7.5 Cocos-BCX HTTP API"
slug: "cocos-bcx-chain-api-doc"
hidden: false
createdAt: "2020-04-29T01:14:52.936Z"
updatedAt: "2020-04-30T01:59:53.705Z"
---
[block:api-header]
{
  "title": "API 基本信息"
}
[/block]
本篇列出接口的baseurl: https://test.cocosbcx.net
所有接口的响应都是 JSON 格式。
所有请求都是POST方式，数据在 request body 中发送。

[block:api-header]
{
  "title": "请求体基础结构"
}
[/block]

[block:code]
{
  "codes": [
    {
      "code": " {\n   \"method\": \"call\", \n   \"params\": [0, \"rpc_name\", [param]],\n   \"id\": 2 \n }",
      "language": "javascript"
    }
  ]
}
[/block]
参数说明
[block:parameters]
{
  "data": {
    "h-0": "名称",
    "h-1": "类型",
    "h-2": "是否必须",
    "h-3": "描述",
    "0-3": "固定值：call",
    "1-3": "自定义消息id，自己在应用中维护即可，用途：链上消息响应会将此id带回，方便应用开发者区分。",
    "2-3": "0：函数所属的api对应的id，http 请求默认为0； \nrpc_name：RPC函数名；\nparam：对应RPC函数的参数",
    "0-2": "Y",
    "1-2": "Y",
    "2-2": "Y",
    "1-1": "INT",
    "0-1": "STRING",
    "2-1": "ARRAY",
    "1-0": "id",
    "0-0": "method",
    "2-0": "params"
  },
  "cols": 3,
  "rows": 4
}
[/block]

[block:api-header]
{
  "title": "响应体基础结构"
}
[/block]

[block:code]
{
  "codes": [
    {
      "code": "{\n  \"id\": String, \n  \"jsonrpc\": String,\n  \"result\": T,\n  \"error\":{\"code\":int, \"message\":String, \"data\":Object}\n}",
      "language": "javascript"
    }
  ]
}
[/block]
参数说明

[block:parameters]
{
  "data": {
    "h-0": "名称",
    "h-1": "类型",
    "h-2": "",
    "0-0": "id",
    "0-1": "INT",
    "0-2": "请求时传入的id",
    "1-2": "rpc版本号",
    "1-1": "STRING",
    "1-0": "jsonrpc",
    "2-0": "result",
    "3-0": "error",
    "2-1": "T (泛型)",
    "3-1": "OBJECT",
    "2-2": "正确返回值",
    "3-2": "错误/异常返回值"
  },
  "cols": 3,
  "rows": 5
}
[/block]