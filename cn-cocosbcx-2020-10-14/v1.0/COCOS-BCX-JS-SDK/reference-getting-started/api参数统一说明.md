---
title: "API参数统一说明"
slug: "api参数统一说明"
hidden: false
createdAt: "2018-12-19T08:34:01.096Z"
updatedAt: "2018-12-20T08:48:30.124Z"
---
[block:api-header]
{
  "title": "没有特殊说明均有一个可选参数callback"
}
[/block]
callback返回的result为Object对象,结构为{code:0,message:””}。
code=1时表示成功，无message状态描述。
code!=1时意味执行失败，message为失败状态描述。
[block:api-header]
{
  "title": "没有殊说明均只有一个参数，该参数为一个对象，对象包含所有相关参数，其中也包含callback"
}
[/block]
调用示例：
[block:code]
{
  "codes": [
    {
      "code": "bcl.getPrivateKey({\n     callback:res=>{}\n})",
      "language": "javascript"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "除订阅类接口，其他接口在不传callback参数时均返回promise对象；"
}
[/block]
调用实例
//转账
[block:code]
{
  "codes": [
    {
      "code": "bcx.transferAsset({\nto:test2,\namount:1\nassetId:\"1.3.0\",\nmemo:\"\"\n}).then(res=>{\nconsole.info('transferAsset res',res);\n})",
      "language": "javascript"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "接口的参数类型没有特殊说明均为字符串；"
}
[/block]

[block:api-header]
{
  "title": "接口的参数没有特殊说明均不能为空，callback为可选参数；"
}
[/block]

[block:api-header]
{
  "title": "查询类接口返回数据实例:{code:1,data:[]}"
}
[/block]

[block:api-header]
{
  "title": "非查询类接口返回数据会多一个数据字段trx_data,值为一个对象示例："
}
[/block]

[block:code]
{
  "codes": [
    {
      "code": "trx_data:{\nblock_num:112260,//区块高度\ntrx_id:\"c34021555e01e846ade1e119e2060a60eb514309\"//交易ID\n}",
      "language": "javascript"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "非查询类接口若涉及关联ID业务(如创建NH资产产生的ID)返回的数据中将包含data对象。"
}
[/block]
示例：
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