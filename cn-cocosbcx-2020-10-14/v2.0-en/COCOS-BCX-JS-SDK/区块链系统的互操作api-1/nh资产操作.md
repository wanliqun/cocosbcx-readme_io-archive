---
title: "NH资产操作"
slug: "nh资产操作"
hidden: false
createdAt: "2018-12-20T05:59:10.426Z"
updatedAt: "2019-05-31T11:31:35.079Z"
---
[block:api-header]
{
  "title": "1.注册开发者"
}
[/block]
方法：registerCreator
功能：将当前账户注册成为开发者
[block:api-header]
{
  "title": "2.创建世界观"
}
[/block]
方法：creatWorldView
功能：创建支持的NH资产世界观，向区块链系统注册当前账号（通常为游戏的账号）支持的NH资产世界观
参数：
worldView：世界观名称，区分大小写;
[block:api-header]
{
  "title": "3.创造NH资产"
}
[/block]
方法：creatNHAsset
功能：创建一个唯一的NH资产，具有唯一性。本接口仅限NH资产制造商（铁匠铺）使用。
参数：
assetId：当前NH资产交易时，适用的资产ID；
worldView：世界观；
baseDescribe：当前NH资产的具体内容描述，由制造者定义;
ownerAccount：指定NH资产拥有者(NH资产归属权账户，默认为NH资产创建者)
NHAssetsCount (Number)：创建NH资产的数量，默认值为1，只有type为0即创建同一种NH资产生效
type：创建NH资产方式的类型，默认值为0。值为0时默认创建同一种NH资产，1是创建不同NH资产。
NHAssets(Array)示例: 
[block:code]
{
  "codes": [
    {
      "code": "\n[{\n\t\"assetId\": \"1.3.0\",\n\t\"worldView\": \"TEST\",\n\t\"baseDescribe\": \"{name:\\\"预言家\\\"}\",\n\t\"ownerAccount\": \"test2\"\n}, {\n\t\"assetId\": \"1.3.0\",\n\t\"worldView\": \"TEST\",\n\t\"baseDescribe\": \"{name:\\\"女巫\\\"}\",\n\t\"ownerAccount\": \"test2\"\n}, {\n\t\"assetId\": \"1.3.0\",\n\t\"worldView\": \"TEST\",\n\t\"baseDescribe\": \"{name:\\\"猎人\\\"}\",\n\t\"ownerAccount\": \"test2\"\n}]",
      "language": "text"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "4.删除NH资产"
}
[/block]
方法：deleteNHAsset
功能：删除整条NH资产数据记录，通常在商品销毁时使用（仅能由用户自己授权处理自己想要销毁的数据）。
参数：
NHAssetIds (Array)：NH资产实例的唯一标识ID;示例：[4.2.195,4.2.194]
[block:api-header]
{
  "title": "5.转移NH资产"
}
[/block]
方法：transferNHAsset
功能：用户可以将自己的NH资产转移到另外一个用户
参数：
toAccount：转移NH资产的目标用户名
NHAssetIds（Array）：多个NH资产id组成的数组，示例：[4.2.332,4.2.333]。
[block:api-header]
{
  "title": "6.提议关联世界观"
}
[/block]
方法：proposeRelateWorldView
功能：提议关联到某一个世界观，需要该世界观的创建人审批
参数：
worldView：需要关联的世界观名
viewOwner：需要关联的世界观创建者
[block:api-header]
{
  "title": "7.批准关联世界观的提议"
}
[/block]
方法：approvalProposal
功能：批准其他用户关联自己的世界观的提议
参数：
proposalId：提议Id
[block:api-header]
{
  "title": "8.获取当前用户收到的提议"
}
[/block]
方法：getAccountProposals
功能：获取当前操作用户收到的提议