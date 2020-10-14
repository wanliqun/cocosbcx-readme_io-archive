---
title: "7.4 Block API"
slug: "76-block-api"
hidden: false
createdAt: "2019-04-23T07:58:31.401Z"
updatedAt: "2020-05-07T06:22:37.447Z"
---
本部分为链API，通过http wensocket链接主链，直接调用。
内部以JSON2.0格式发送，数据格式说明如下
 
###1. 发送数据结构
**示例**
[block:code]
{
  "codes": [
    {
      "code": "{\"method\": \"call\", \"params\": [api_id, \"函数名\", [参数]], \"id\": 2}",
      "language": "json"
    }
  ]
}
[/block]
**参数说明：**
method : call
params: api_id:函数所属的api对应的id; 函数名：RPC函数名；参数：对应RPC函数的参数
id ：此id为自定义消息id，自己在应用中维护即可，用途：链上消息响应会将此id带回，方便应用开发者区分。

###2. 返回数据结构
**示例**
[block:code]
{
  "codes": [
    {
      "code": "{\"id\":2,\"jsonrpc\":\"2.0\",\"result\":\"\"}",
      "language": "json"
    }
  ]
}
[/block]
**参数说明：**
id : 此id和发送消息时的id对应；
jsonrpc : api对应的RPC版本；
result ：返回数据体，可以是任意数据结构。


## 7.4.1 块

**get_blocks**

**原型**
[block:code]
{
  "codes": [
    {
      "code": "vector<optional<signed_block>> graphene::app::block_api::get_blocks(uint32_t block_num_from, uint32_t block_num_to)const",
      "language": "cplusplus"
    }
  ]
}
[/block]
**说明**
获取签名的块
**返回值**
从最高块的号到最小块的号
**参数**
block_num_from: 最小的块号 
block_num_to: 最高的块号

## 7.4.2资产

**1. get_asset_holders** 

**原型**
[block:code]
{
  "codes": [
    {
      "code": "vector<account_asset_balance> graphene::app::asset_api::get_asset_holders(asset_id_type asset_id, uint32_t start, uint32_t limit)const",
      "language": "cplusplus"
    }
  ]
}
[/block]
**说明**
获取特定资产的所有者
**返回值**
值定资产的所有者
**参数**
asset_id：特定资产ID
start：起始索引
limit：最高限额不得超过100

**2. get_all_asset_holders** 

**原型**
[block:code]
{
  "codes": [
    {
      "code": "vector<asset_holders> graphene::app::asset_api::get_all_asset_holders()const",
      "language": "cplusplus"
    }
  ]
}
[/block]
**说明**
获得所有资产持有人
**返回值**
所有资产持有人清单
**参数**