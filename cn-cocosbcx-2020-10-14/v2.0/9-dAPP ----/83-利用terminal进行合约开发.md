---
title: "9.3 利用Terminal进行合约开发"
slug: "83-利用terminal进行合约开发"
excerpt: "Terminal 上线了新的功能 开发工具 -> 合约管理\n合约管理功能非常方便开发者创建、更新合约，和直接执行合约接口。"
hidden: false
createdAt: "2019-07-17T07:10:37.786Z"
updatedAt: "2019-12-13T03:14:59.919Z"
---
# 一、合约开发

##  1. 简单工具介绍
a. 使用[Terminal](http://cocos-terminal.com/) 登录Cocos-BCX的账号
b. 在左侧目录栏中点击合约管理可以查看此账号下已经存在的合约的各种信息，包括合约的基本信息，代码，接口信息，数据区(public_data)等，如下图：

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/b410978-_20190717164306.png",
        "微信图片_20190717164306.png",
        1920,
        902,
        "#292c2e"
      ]
    }
  ]
}
[/block]
## 2. 创建合约
a. 点击添加合约即是创建新的合约
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/0c15012-_20190717151128.png",
        "微信图片_20190717151128.png",
        1873,
        883,
        "#313232"
      ]
    }
  ]
}
[/block]
b. 弹出界面填写合约名称，合约名长度为4-63位，由小写字母或数字构成且以"contract."开头，例如 "contract.testnew"
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/f23586a-_20190717151935.png",
        "微信图片_20190717151935.png",
        529,
        259,
        "#50555d"
      ]
    }
  ]
}
[/block]
## 3. 编辑合约代码，和更新已存在合约
[block:code]
{
  "codes": [
    {
      "code": "function hello()\n    chainhelper:log('Hello World! contract.testnew')\nend",
      "language": "lua"
    }
  ]
}
[/block]
## 4.发布合约
a. 点击“发布合约”按钮
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/8aaa342-_20190717152125.png",
        "微信图片_20190717152125.png",
        1256,
        428,
        "#262829"
      ]
    }
  ]
}
[/block]
b. 点击随机生成， 若合约开启权限验证，则JS-SDK的app_keys配置项必须填入该key，建议复制保存
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/876f7ee-_20190717153033.png",
        "微信图片_20190717153033.png",
        930,
        491,
        "#4a4d54"
      ]
    }
  ]
}
[/block]
c. 点击确定，合约创建需要一定的费用作为手续费
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/6e88814-_20190717153039.png",
        "微信图片_20190717153039.png",
        802,
        439,
        "#373b42"
      ]
    }
  ]
}
[/block]
## 5. 调用合约
a. 发布合约后，可以在下图箭头位置看到合约的接口，点击接口填写参数可以执行接口
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/44f6a9a-_20190717153324.png",
        "微信图片_20190717153324.png",
        1311,
        581,
        "#28282a"
      ]
    }
  ]
}
[/block]
b.调用合约的需要一定的手续费
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/035e501-_20190717154019.png",
        "微信图片_20190717154019.png",
        1080,
        574,
        "#2d3035"
      ]
    }
  ]
}
[/block]
c. 调用结果会在编辑区下方显示
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/92b355e-_20190717165318.png",
        "微信图片_20190717165318.png",
        1156,
        694,
        "#212121"
      ]
    }
  ]
}
[/block]
## 6. 更新合约
a. init_data()为初始化数据的方法
[block:code]
{
  "codes": [
    {
      "code": "function hello()\n    chainhelper:log('Hello World! contract.testnew')\nend\n\nfunction hello2(num,amount)\n\tchainhelper:log('=======loooooog starts=======');\n\tchainhelper:log('{\"num\": \"'..num..'\",\"amount\":\"'..amount..'\"}');\n\tchainhelper:log('=======log ends=======');\nend\n\nfunction init_data()\n    read_list = {public_data={initdata=true}}\n    chainhelper:read_chain()\n    public_data.initdata  = 98\n    write_list = {public_data={initdata=true}}\n    chainhelper:write_chain()\nend",
      "language": "lua"
    }
  ]
}
[/block]
b. 点击发布合约（已存在的合约就会被更新为最新），发布成功后必须调用init_data()接口，数据才可初始化
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/4196fca-_20190717164256.png",
        "微信图片_20190717164256.png",
        1154,
        567,
        "#292c31"
      ]
    }
  ]
}
[/block]
c. 点击“数据”可现实初始化数据
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/39a4872-_20190717165807.png",
        "微信图片_20190717165807.png",
        1311,
        450,
        "#27292b"
      ]
    }
  ]
}
[/block]
## 6. 查看合约
也可以在搜索框中填入合约名称进行搜索，查看合约信息，以及合约的统计信息

a. 查看合约基本信息
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/a4bb604-_20190717153043.png",
        "微信图片_20190717153043.png",
        1503,
        680,
        "#42464b"
      ]
    }
  ]
}
[/block]
b. 合约统计，可以很方便统计一些运营数据包括合约的调用次数，币的转入转出数量。
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/e254e87-22791563357270_.pic_hd.jpg",
        "22791563357270_.pic_hd.jpg",
        3142,
        1746,
        "#33363b"
      ]
    }
  ]
}
[/block]
# 二、合约统计
  a. 在Terminal 中还提供了热门合约的排名，可以清晰查看合约的调用次数，以及可以快速查看合约的详情，以及合约的执行结果。
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/75e51d2-48452FA2-A205-40A4-A33D-3123FEA3721D.png",
        "48452FA2-A205-40A4-A33D-3123FEA3721D.png",
        3542,
        1892,
        "#303338"
      ]
    }
  ]
}
[/block]
 b.点击合约进入可以查看合约代码、合约数据和合约统计。
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/1245a87-61824CD8-5D5A-45D9-B65F-308462A8CD2D.png",
        "61824CD8-5D5A-45D9-B65F-308462A8CD2D.png",
        3464,
        2332,
        "#32353a"
      ]
    }
  ]
}
[/block]