---
title: "5.1 Hello World！"
slug: "hello_world"
hidden: false
createdAt: "2019-04-01T03:20:23.592Z"
updatedAt: "2019-04-10T06:44:32.823Z"
---
作为任何语言入门的第一课，我们从一个详细的Hello World开始。

1. 创建一个hello 目录，通过命令行或者GUI工具

[block:code]
{
  "codes": [
    {
      "code": "cd CONTRACTS_DIR\nmkdir hello\ncd hello",
      "language": "shell"
    }
  ]
}
[/block]

2. 创建一个hello.lua文件，然后用你喜欢的编辑打开
[block:code]
{
  "codes": [
    {
      "code": "touch hello.lua",
      "language": "shell"
    }
  ]
}
[/block]

3. 直接往hello.lua里面添加代码
[block:code]
{
  "codes": [
    {
      "code": "function hello()\n    chainhelper:log('Hello World!')\nend",
      "language": "lua"
    }
  ]
}
[/block]

4. 利用创建好的测试账号（详细步骤见这里），通过cli_wallet部署合约

[block:code]
{
  "codes": [
    {
      "code": "create_contract chandlerette contract.helloraven \"COCOS8EgNn68Pydk3QatmPQc2mWJNYLP8w6ezszvfwEBygXxT5BKi4j\" \"function hello() chainhelper:log('Hello World!') end\" true",
      "language": "shell"
    }
  ]
}
[/block]

5. 通过terminal浏览器查看合约部署上去的结果
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/08e40ac-5.png",
        "5.png",
        1556,
        365,
        "#292e33"
      ]
    }
  ]
}
[/block]

6. 通过cli_wallet调用hello接口
[block:code]
{
  "codes": [
    {
      "code": "call_contract_function chandlerette contract.helloraven hello [] true",
      "language": "shell"
    }
  ]
}
[/block]

7. 通过terminal浏览器查看交易记录

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/bfa3fef-3.png",
        "3.png",
        982,
        289,
        "#2b2f36"
      ]
    }
  ]
}
[/block]
8. 如果想打印一下具体时间，修改代码如下
[block:code]
{
  "codes": [
    {
      "code": "function hello()\n    chainhelper:log('Hello World!')\n    chainhelper:log(date('%Y-%m-%dT%H:%M:%S', chainhelper:time()))\nend",
      "language": "lua"
    }
  ]
}
[/block]

9. 通过cli_wallet命名更新合约

[block:code]
{
  "codes": [
    {
      "code": "revise_contract chandlerette contract.helloraven \"function hello() chainhelper:log('Hello World!') chainhelper:log(date('%Y-%m-%dT%H:%M:%S', chainhelper:time())) end\" true",
      "language": "shell"
    }
  ]
}
[/block]
10. 通过terminal浏览器查看更新合约的交易记录

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/d736de6-4.png",
        "4.png",
        1569,
        368,
        "#282d33"
      ]
    }
  ]
}
[/block]
11. 通过cli_wallet重新调用hello接口
[block:code]
{
  "codes": [
    {
      "code": "call_contract_function chandlerette contract.helloraven hello [] true",
      "language": "shell"
    }
  ]
}
[/block]

12. 通过terminal浏览器查看交易记录

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/3755427-1.png",
        "1.png",
        958,
        351,
        "#2d3138"
      ]
    }
  ]
}
[/block]
**总结**

我们通过Hello World的示例演示基本合约的开发，部署，更新流程，整个流程非常简洁。由于Lua语言的特性，我们整个合约代码直接上链，不涉及中间代码。虽然隐私性稍差，当公开透明性更好。