---
title: "7.6 Block API"
slug: "76-block-api"
hidden: true
createdAt: "2019-04-23T07:58:31.401Z"
updatedAt: "2019-05-31T11:31:35.021Z"
---
## 7.6.1 块

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

## 7.6.2资产

**1. get_asset_holders** 

**原型**
[block:code]
{
  "codes": [
    {
      "code": "vector<account_asset_balance> graphene::app::asset_api::get_asset_holders(std::string asset, uint32_t start, uint32_t limit)const",
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
asset：特定资产ID或符号
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
block_num_from: 最小的块号 
block_num_to: 最高的块号

## 7.6.3 订单

**get_grouped_limit_orders** 

**原型**
[block:code]
{
  "codes": [
    {
      "code": "vector<limit_order_group> graphene::app::orders_api::get_grouped_limit_orders(std::string base_asset, std::string quote_asset, uint16_t group, optional<price> start, uint32_t limit)const",
      "language": "cplusplus"
    }
  ]
}
[/block]
**说明**
在给定市场中获取分组限价订单
**返回值**
分组限价订单，从最佳报价到最差报价
**参数**
base_asset：出售资产的ID或符号
quote_asset：正在购买的资产的ID或符号
group：每个订单组中的最高价格差异必须是配置值之一
start：可选价格，表示要检索的第一个订单组
limit：要检索的最大订单组数量（不超过101）