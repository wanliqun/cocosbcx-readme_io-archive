---
title: "API"
slug: "web容器的互操作接口概述"
hidden: true
createdAt: "2018-12-14T14:11:22.635Z"
updatedAt: "2018-12-17T11:48:59.526Z"
---
[block:api-header]
{
  "title": "WEB容器的互操作接口概述"
}
[/block]

[block:api-header]
{
  "title": "类库引用说明"
}
[/block]
引入方式
[block:code]
{
  "codes": [
    {
      "code": "<script type=\"text/javascript\" src=\"bcx.min.js\"></script>",
      "language": "javascript"
    }
  ]
}
[/block]
实例化类库对象
[block:code]
{
  "codes": [
    {
      "code": "bcx对象为类与区块链交互入口，bcx对象实例化调用方式如下：\nVar config={\n\t\t api_node:{//api服务器节点\n\t\turl:”ws://XXXXXXXXX”,//节点websocket地址\n\t\tname:”XXXX”//节点名称,开发者自定义名称\n\t\t },\n         ws_node_list:[\n                {url:\"ws://xxxxxxx\",name:\"xxxxx\"}\n         ]//API服务器节点列表\nfaucet_url:\"http://***.***.***.***:****\", //注册入口\n\t      networks:[{\n            core_asset:\"***\",//核心资产符号\n  chain_id:\"***************************\"   \n         }], \nauto_reconnect:false,//当RPC断开时是否自动连接，默认为true\n        app_keys:[\"************************\"]//合约授权，不进行合约授权，则不用配置此选项\n\t }\nVar bcx=new BCX(config)\n",
      "language": "javascript"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "API参数统一说明"
}
[/block]
API不做特殊说明均有一个可选参数callback：
result为Object对象,结构为{code:0,message:””},
code=1的时候表示成功，无message状态描述,
code!=1时, 意味执行失败，message为失败状态描述，

API不做特殊说明均只有一个参数，该参数为一个对象，对象包含所有相关参数，其中也包含callback
调用示例：
[block:code]
{
  "codes": [
    {
      "code": "Var options={\ncallback:function(res){}\n}\n bcx.getPrivateKey(options)\n",
      "language": "javascript"
    }
  ]
}
[/block]
除订阅类API，其他API在不传callback参数情况下均返回promise对象
调用实例
[block:code]
{
  "codes": [
    {
      "code": "//转账\nbcx.transferAsset({\n     to:test2,\n     amount:1\n     assetId:\"1.3.0\",\nmemo:\"\",\n      onlyGetFee:false\n}).then(res=>{\n        console.info('transferAsset res',res);\n})\n",
      "language": "javascript"
    }
  ]
}
[/block]
API的参数类型不做特殊说明均为字符串     
API的参数不做特殊说明均不能为空，callback可选参数     
查询类API的callback返回数据实例:{status:1,data:[]}
非查询类API的callback返回数据会多一个数据字段trxData,值为一个对象
示例
[block:code]
{
  "codes": [
    {
      "code": "trxData:{\nblock_num:112260,//区块高度\ntrx_id:\"c34021555e01e846ade1e119e2060a60eb514309\"//交易ID\n}\n",
      "language": "javascript"
    }
  ]
}
[/block]
非查询类API如果涉及到关联ID业务(如创建道具产生道具ID)的callback返回数据中将包含data对象
示例
[block:code]
{
  "codes": [
    {
      "code": "data:{\nreal_running_time: 387//运行时间\nresult: \"4.2.288\"//关联业务id\n}\n",
      "language": "javascript"
    }
  ]
}
[/block]
demo上的API调用返回数据在控制台会有打印
[block:api-header]
{
  "title": "状态码"
}
[/block]

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/876b416-1111111.jpg",
        "1111111.jpg",
        2792,
        10200,
        "#f0f0f0"
      ],
      "caption": "状态码"
    }
  ]
}
[/block]