---
title: "9.1.4 Contract Debugging"
slug: "814-contract-debugging"
hidden: false
createdAt: "2019-06-26T06:13:40.455Z"
updatedAt: "2020-03-02T09:29:35.385Z"
---
Generally, there are two ways for debugging:
1	Select single-step debugging in the debug mode. View context information and stack information to locate errors by watch, break and other methods. VisualStudio is the leader in this area. You can also use GDB command line. 
2	Use the log to debug directly, which is commonly used by Lua developers and kernel developers.

However, developers who used to work on the Ethereum contract development must familiar with the painstaking process of contract debugging, which is very inconvenient to find the error in the program execution. The log can only be achieved by defining EVENT disguise for there is no debug.

Cocos-BCX inherits the fine tradition of Lua in this respect, and extends the interface of chainhelper:log, which is easy to view through the log. For example, the hello_world interface on our contract.

[block:code]
{
  "codes": [
    {
      "code": "function hello_world()\n    chainhelper:log('hello world')\n    chainhelper:log(date('%Y-%m-%dT%H:%M:%S', chainhelper:time()))\nend",
      "language": "lua"
    }
  ]
}
[/block]
By executing the hello_world interface directly through the contract calling method above, a transaction will be generated: 

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/bcaba57-64efb4f-_1.png",
        "64efb4f-_1.png",
        865,
        384,
        "#33373c"
      ]
    }
  ]
}
[/block]
Click to check the result

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/4b59056-21afb83-_1.png",
        "21afb83-_1.png",
        864,
        298,
        "#2e3237"
      ]
    }
  ]
}
[/block]
We can modify the contract, print the log at a critical location, then update the contract, re-execute, and locate the problem through the log conveniently.