---
title: "5.1 Hello World！"
slug: "hello_world"
hidden: false
createdAt: "2019-04-01T03:20:23.592Z"
updatedAt: "2019-06-05T13:34:59.482Z"
---
As the first lesson to get started with any programming language, let's start with a detailed introduction to Hello World.

1. Create a hello directory via command line or GUI tool
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

2. Create a hello.lua file and open it with your favorite editor
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

3. Add codes directly to hello.lua 
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

4. Use the created test account (see here for details) to deploy the contract via cli_wallet
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

5. View the results of the contract deployment through the Terminal browser
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/80069b0-_1.png",
        "图片 1.png",
        865,
        236,
        "#292e33"
      ]
    }
  ]
}
[/block]

6. Call the hello interface via cli_wallet
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

7. View transaction history via Terminal browser
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/faa55ee-_1.png",
        "图片 1.png",
        864,
        255,
        "#2b2f36"
      ]
    }
  ]
}
[/block]
8. If you want to print the specific time, modify the codes as follows
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

9. Name the updated contract via cli_wallet
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
10. View the transaction history of the updated contract through the Terminal browser
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/93de938-d736de6-4.png",
        "d736de6-4.png",
        1569,
        368,
        "#292d33"
      ]
    }
  ]
}
[/block]
11. Call the hello interface via cli_wallet
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

12. View transaction history via Terminal browser
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/d584ac0-_1.png",
        "图片 1.png",
        865,
        316,
        "#2d3138"
      ]
    }
  ]
}
[/block]
**Conclusion**

The development, deployment and update process of basic contract is demoed with the example of Hello World, which is very simple. Due to the nature of the Lua language, the code of the contract is uploaded on the blockchain, which involves no intermediate code. Although the privacy is slightly compromised, the transparency is increased.