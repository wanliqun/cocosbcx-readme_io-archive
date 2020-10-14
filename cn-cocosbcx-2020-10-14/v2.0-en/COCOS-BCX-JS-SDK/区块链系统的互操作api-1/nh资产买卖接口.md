---
title: "NH资产买卖接口"
slug: "nh资产买卖接口"
hidden: false
createdAt: "2018-12-20T06:19:42.126Z"
updatedAt: "2019-05-31T11:31:35.080Z"
---
[block:api-header]
{
  "title": "1.创建NH资产出售单"
}
[/block]
方法：creatNHAssetOrder
功能：卖出NH资产（在交易前可调用queryAccountGameItems函数，列举用户NH资产，以便用户选着卖出）
参数：
otcAccount：OTC交易平台账户，用于收取挂单费用；（OTC平台填写）
orderFee：挂单费用，用户向OTC平台账户支付的挂单费用；（OTC平台填写）
NHAssetId：NH资产实例的唯一标识ID; （用户填写）
price：商品挂单价格；（用户填写）
priceAssetId：商品挂单价格所使用的代币种类；（用户填写）
expiration：单位为秒，挂单时间，如60*60=3600(秒)，为1小时
memo：挂单备注信息；
callback：设置执行挂单卖出后的回调函数
[block:api-header]
{
  "title": "2.购买订单NH资产"
}
[/block]
方法：fillNHAssetOrder
功能：买入NH资产，支付购买游戏装备的代币费用，同时修改用户拥有的商品数据。该操作是一个多步合成的原子操作，在支付费用的同时完成用户账户NH资产数据的更新，如果支付动作或账户商品数据更新动作中某一个动作不被主链区块认可，则整个交易将被回滚，避免异常交易。
参数：
orderId：订单ID
callback：回调函数
[block:api-header]
{
  "title": "3.取消NH资产出售单"
}
[/block]
方法：cancelNHAssetOrder
功能：取消NH资产挂卖订单
参数：
orderId：订单ID
callback：回调函数