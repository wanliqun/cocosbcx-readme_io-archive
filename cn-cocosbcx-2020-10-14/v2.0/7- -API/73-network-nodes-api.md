---
title: "7.3 Network Nodes API"
slug: "73-network-nodes-api"
hidden: false
createdAt: "2019-04-23T08:04:46.662Z"
updatedAt: "2020-05-07T06:23:59.536Z"
---
## 7.3.1.获取网络信息 
**get_info** 
原型
[block:code]
{
  "codes": [
    {
      "code": "fc::variant_object graphene::app::network_node_api::get_info()const\n",
      "language": "cplusplus"
    }
  ]
}
[/block]
说明
返回一般网络信息
**get_connected_peers**
原型

[block:code]
{
  "codes": [
    {
      "code": "std::vector<net::peer_status> graphene::app::network_node_api::get_connected_peers()const",
      "language": "cplusplus"
    }
  ]
}
[/block]
说明
获取当前节点的所有连接的状态。
**get_potential_peers**
原型

[block:code]
{
  "codes": [
    {
      "code": "std::vector<net::potential_peer_record> graphene::app::network_node_api::get_potential_peers()const",
      "language": "cplusplus"
    }
  ]
}
[/block]
说明
返回可能存在的节点列表。
**get_advanced_node_parameters**
原型

[block:code]
{
  "codes": [
    {
      "code": "fc::variant_object graphene::app::network_node_api::get_advanced_node_parameters()const",
      "language": "cplusplus"
    }
  ]
}
[/block]
说明
获取节点的高级参数，比如最大连接数。
## 7.3.2更改网络设置
**add_node**
原型
[block:code]
{
  "codes": [
    {
      "code": "void graphene::app::network_node_api::add_node(const fc::ip::endpoint &ep)",
      "language": "cplusplus"
    }
  ]
}
[/block]
说明
添加新节点。
参数
ep: 要连接的节点IP或端口。
**set_advanced_node_parameters**
原型
[block:code]
{
  "codes": [
    {
      "code": "void graphene::app::network_node_api::set_advanced_node_parameters(const fc::variant_object &params)",
      "language": "cplusplus"
    }
  ]
}
[/block]
说明
设置高级节点参数，比如最大连接数。
参数
params: 一个JSON对象，包含要设置的参数的名称/值