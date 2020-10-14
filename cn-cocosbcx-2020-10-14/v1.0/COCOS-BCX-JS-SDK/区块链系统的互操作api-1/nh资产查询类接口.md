---
title: "NH资产查询类接口"
slug: "nh资产查询类接口"
hidden: false
createdAt: "2018-12-20T06:34:24.431Z"
updatedAt: "2018-12-20T09:08:47.166Z"
---
[block:api-header]
{
  "title": "1.查询全网用户NH资产售卖订单"
}
[/block]
方法：queryNHAssetOrders
功能：查询全网用户NH资产的售卖订单	
参数：
assetIds (array）：资产符号或id筛选条件
worldViews (array)：版本名称或版本id筛选条件
pageSize：页容量
page：页数
[block:api-header]
{
  "title": "2.查询指定用户的NH资产售卖订单"
}
[/block]
方法：queryAccountNHAssetOrders
功能：查询指定用户的NH资产售卖订单
参数：
account：查询账户名或账户Id
pageSize：页容量
page：页数
callback：回调函数
[block:api-header]
{
  "title": "3.查询账户下所拥有的道具NH资产"
}
[/block]
方法：queryAccountNHAssets
功能：读取当前用户账户下所有可在对应游戏中使用的NH资产
参数：
account：账户名或账户id
worldViews (array)：世界观名集合
page：页数
pageSize：页容量，每页的数据条数
callback：返回值。示例：
{status:1,data:[],total:0}
[block:api-header]
{
  "title": "4.查询开发者所关联的世界观"
}
[/block]
方法：queryNHCreator
功能：查询开发者所关联的世界观	
参数：
account：账户名或账户ID
callback：回调函数
[block:api-header]
{
  "title": "5.查询开发者创建的NH资产"
}
[/block]
方法：queryNHCreator
功能：查询开发者所创建的世界观	
参数：
account：账户名或账户ID
callback：回调函数
[block:api-header]
{
  "title": "6.查询NH资产详细信息"
}
[/block]
方法：queryNHAssets
功能：查询NH资产详细信息	
参数：
NHAssetIds：NH资产id或hash
callback：回调函数
[block:api-header]
{
  "title": "7.查询世界观详细信息"
}
[/block]
方法：lookupWorldViews
功能：查询世界观详细信息	
参数：
worldViews (array)：世界观名称或id
callback：回调函数