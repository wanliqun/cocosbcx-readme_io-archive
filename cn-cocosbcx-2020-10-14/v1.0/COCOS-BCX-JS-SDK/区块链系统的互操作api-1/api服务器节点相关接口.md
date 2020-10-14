---
title: "API服务器节点相关接口"
slug: "api服务器节点相关接口"
hidden: false
createdAt: "2018-12-20T06:59:49.875Z"
updatedAt: "2018-12-20T09:10:37.859Z"
---
[block:api-header]
{
  "title": "1.查看API服务器节点列表"
}
[/block]
方法：lookupWSNodeList
功能：查看API服务器节点列表信息
参数：
callback：回调函数
[block:api-header]
{
  "title": "2.连接API服务器节点"
}
[/block]
方法：switchAPINode
功能：切换节点
参数：
url：API服务器节点地址，此地址必须是API服务器节点列表中的websoket地址
callback：回调函数
[block:api-header]
{
  "title": "3.添加新的API服务器节点"
}
[/block]
方法：addAPINode
功能：添加新节点
参数：
name：新节点名称
url：API服务器节点websoket地址
callback：回调函数
[block:api-header]
{
  "title": "4.删除API服务器节点"
}
[/block]
方法：deleteAPINode
功能：删除节点
参数：
url：API服务器节点websoket地址
callback：回调函数
[block:api-header]
{
  "title": "5.监听与API服务器节点的连接状态变化"
}
[/block]
方法：subscribeToRpcConnectionStatus
功能：监听rpc连接状态变化
参数：
callback：回调会返回状态，包括下述结果: 
closed：rpc连接关闭
error：rpc连接错误
realopen：rpc连接成功