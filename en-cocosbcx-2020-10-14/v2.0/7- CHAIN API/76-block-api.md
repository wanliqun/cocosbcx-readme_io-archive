---
title: "7.4 Block API"
slug: "76-block-api"
hidden: false
createdAt: "2019-10-11T03:40:12.122Z"
updatedAt: "2020-04-15T03:13:48.072Z"
---
## 1 block

**get_blocks**

**Prototype**
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
**Description**
Blocks to get signatures
**Return value**
From the number of the highest block to the number of the smallest block
**Parameter**
block_num_from: the smallest block number
block_num_to: the highest block number

## 2 Asset

**1. get_asset_holders** 

**Prototype**
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
**Description**
Owners of specific assets
**Return value**
Owners of specific assets
**Parameter**
asset: specific asset ID or token
start: starting index
limit: the upper limit shall not exceed 100

**2. get_all_asset_holders** 

**Prototype**
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
**Description**
Get all asset holders
**Return value**
List of all asset holders
**Parameter**
block_num_from: the smallest block number
block_num_to: the highest block number

## 3 order

**get_grouped_limit_orders** 

**Prototype**
[block:code]
{
  "codes": [
    {
      "code": "vector<limit_order_group> graphene::app::orders_api::get_grouped_limit_orders(std::string base_asset, std::string quote_asset, uint16_t group, optional<price> start, uint32_t limit)const",
      "language": "csharp"
    }
  ]
}
[/block]
**Description**
Get group limit orders in a given market
**Return value**
Group limit orders, from best quotation to worst quotation
**Parameter**
base_asset: ID or token of the asset sold
quote_asset: ID or token of the asset being purchased
group: the largest price difference in each order group must be one of the configuration values
start: optional price, indicating the first-order group to index
limit: maximum number of order groups to index (no more than 101)