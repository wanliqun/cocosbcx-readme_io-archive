---
title: "7.3 Network Nodes API"
slug: "77-network-nodes-api"
hidden: false
createdAt: "2019-10-11T03:57:23.932Z"
updatedAt: "2020-04-15T03:14:38.413Z"
---
## 7.2.1 access to network information
**get_info** 
prototype
[block:code]
{
  "codes": [
    {
      "code": "fc::variant_object graphene::app::network_node_api::get_info()const\n",
      "language": "text"
    }
  ]
}
[/block]
description
return general network information
**get_connected_peers**
prototype

[block:code]
{
  "codes": [
    {
      "code": "std::vector<net::peer_status> graphene::app::network_node_api::get_connected_peers()const",
      "language": "text"
    }
  ]
}
[/block]
description
Get the status of connection for all the current nodes.
**get_potential_peers**
prototype

[block:code]
{
  "codes": [
    {
      "code": "std::vector<net::potential_peer_record> graphene::app::network_node_api::get_potential_peers()const",
      "language": "text"
    }
  ]
}
[/block]
description
Return a list of potential nodes.
**get_advanced_node_parameters**
prototype

[block:code]
{
  "codes": [
    {
      "code": "fc::variant_objectgraphene::app::network_node_api::get_advanced_node_parameters()const",
      "language": "text"
    }
  ]
}
[/block]
description
Get the advanced parameters of the node, such as the maximum number of connections.

## 7.2.2 change the network setting 
**add_node**
prototype
[block:code]
{
  "codes": [
    {
      "code": "void graphene::app::network_node_api::add_node(const fc::ip::endpoint &ep)",
      "language": "text"
    }
  ]
}
[/block]
description
Add new nodes.
parameter
ep: the node IP or port to be connected.
**set_advanced_node_parameters**
prototype
[block:code]
{
  "codes": [
    {
      "code": "void graphene::app::network_node_api::set_advanced_node_parameters(const fc::variant_object &params)",
      "language": "text"
    }
  ]
}
[/block]
description
Set advanced node parameters, such as the maximum number of connections.
parameter
params: a JSON object containing the name/value of the parameter to be set