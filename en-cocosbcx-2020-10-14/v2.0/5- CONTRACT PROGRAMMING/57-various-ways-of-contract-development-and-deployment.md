---
title: "5.7 Various Ways of Contract Development and Deployment"
slug: "57-various-ways-of-contract-development-and-deployment"
hidden: false
createdAt: "2019-09-30T04:25:37.498Z"
updatedAt: "2019-10-09T09:43:01.487Z"
---
## Cocos-BCX Contract Development Guide:
Contract Development Language: Lua
Cocos-BCX will directly deploy the source code to the chain without any middle code.
Writing intelligent contracts is a very important step in the process of developing blockchain products. The following are four ways to develop Cocos-BCX contracts:

## 1. Develop Contract in Terminal
The Contract management function of Terminal makes it easy for developers to create, update contracts, and execute contract interfaces directly.

**1.1. Introduction to Simple Tools
1.1.1 Log in to Cocos-BCX account on Terminal
1.1.2 Click Contract Management in the left directory bar to view all information about the contract already existing under this account, including basic contact information, code, interface information, data zone (public_data), etc. as follows:
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/7381eac-2.png",
        "2.png",
        1920,
        902,
        "#292c2e"
      ]
    }
  ]
}
[/block]
**1.2. Create a Contract
1.2.1 Click Add to create a new contract
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/3742282-3.png",
        "3.png",
        1873,
        883,
        "#313232"
      ]
    }
  ]
}
[/block]
1.2.2 Fill in the contract name in the pop-up window. The contract name should be 4-63 characters consisting of lowercase letters or numbers​ and starts with "contract.", for example, "contract.testnew"
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/dbf6be9-4.png",
        "4.png",
        529,
        259,
        "#50555d"
      ]
    }
  ]
}
[/block]
**1.3 Edit Contract Code and Update Existing Contracts** 
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
**1.4 Release Contract**
1.4.1 Click Release
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/3fe97bc-5.png",
        "5.png",
        1256,
        428,
        "#262829"
      ]
    }
  ]
}
[/block]
1.4.2 Click Random Generation. If the contract opens the permission validation, the app_keys configuration entry of JS-SDK must be filled in with the key. It is recommended to copy and save the key.
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/45d220c-6.png",
        "6.png",
        930,
        491,
        "#4a4d54"
      ]
    }
  ]
}
[/block]
1.4.3 Click OK. Contract​ creation requires a certain fee.
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/3071e5c-7.png",
        "7.png",
        802,
        439,
        "#373b42"
      ]
    }
  ]
}
[/block]
**1.5 Call the Contract**
1.5.1 After the contract is released, you can find the interface of the contract as directed by the arrow in the picture below. Click Interfaces to fill in the parameters to execute the interface.
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/698dcac-8.png",
        "8.png",
        1311,
        581,
        "#28282a"
      ]
    }
  ]
}
[/block]
1.5.2 It requires a certain fee to call the contract.
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/14e2be4-9.png",
        "9.png",
        1080,
        574,
        "#2d3035"
      ]
    }
  ]
}
[/block]
1.5.3 The result of the call will be displayed below the editing area.
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/9e8200c-10.png",
        "10.png",
        1156,
        694,
        "#212121"
      ]
    }
  ]
}
[/block]
**1.6 Update the Contract**
1.6.1 Use init_data () to initialize the data
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
1.6.2 Click Release Contract (the existing contract will be updated to the latest). After the release is done, the init_data() interface must be called to initialize the data.
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/6db5fef-11.png",
        "11.png",
        1154,
        567,
        "#292c31"
      ]
    }
  ]
}
[/block]
1.6.3 Click Data to initialize the data.
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/ac03ef7-12.png",
        "12.png",
        1311,
        450,
        "#27292b"
      ]
    }
  ]
}
[/block]
##2. Develop and Deploy Contract with cli_wallet
Please note that: you must log in to the account, import assets, and unlock the wallet first.

**2.1 Create a Contract**

* Command format
create_contract [contract owner] [contract name] [contract authority (publicKey in the key pair of public and private keys] [contract content] [broadcast (true/false)]

* Example
create_contract 1.2.17 contract.helloworld "COCOS1DE213......" "function hello() chainhelper:log('Hello World!') end" true
* Prototype
[block:code]
{
  "codes": [
    {
      "code": "create_contract owner name contract_authority data broadcast",
      "language": "shell"
    }
  ]
}
[/block]
* Results
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/de948b7-13.png",
        "13.png",
        805,
        665,
        "#080908"
      ]
    }
  ]
}
[/block]
**2.2 Update Contract**
* Command format
revise_contract [account name who updated the contract] [contract name or ID] [contract content] [broadcast (true/false)]

* Example
revise_contract 1.2.17 contract.helloworld "function hello() chainhelper:log('Hello World!') chainhelper:log(date('%Y-%m-%dT%H:%M:%S', chainhelper:time())) end" true
* Prototype
[block:code]
{
  "codes": [
    {
      "code": "revise_contract owner name contract_authority data broadcast\n",
      "language": "shell"
    }
  ]
}
[/block]
* Results
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/af7c8f7-14.png",
        "14.png",
        804,
        634,
        "#080808"
      ]
    }
  ]
}
[/block]
** Call Contract**
* Command format
call_contract_function [username or ID] [contract name or contract ID] [function name] [parameter list] [broadcast (true/false)]
* Example
call_contract_function 1.2.17 contract.helloworld [] true
* Prototype
[block:code]
{
  "codes": [
    {
      "code": "call_contract_function account_id_or_name contract_id_or_name function_name value_list broadcast",
      "language": "shell"
    }
  ]
}
[/block]
* Results
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/8d6a331-15.png",
        "15.png",
        804,
        579,
        "#060606"
      ]
    }
  ]
}
[/block]
## 3. Develop a Contract through js-sdk
Develop the contract according to the ​input box of the js-sdk demo, as shown below:
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/1920e5b-16.png",
        "16.png",
        1634,
        1204,
        "#fbfbfb"
      ]
    }
  ]
}
[/block]
The deployment of the contract requires these parameters. The public-private key pair can be simply generated by clicking a button for generating a public-private key pair on the contract deployment function. Then enter the appropriate contact name and code. Click Confirm to create a contract.

if there is an error, it may be caused by the following reasons:
1	You forgot to log in to the account before deploying the contract (login directly in the js-sdk demo).
2	The logged-in account is not registered as a developer.
3	COCOS in the account is insufficient to cover the fee.
4	There is an error in the code of contract deployment. You need to correct the error and redeploy the contract.

The specific error can be found in the js console output in the js-sdk demo with the developer tools under the chrome.

So far, we have successfully deployed the contract to the chain. 

##  4 View the Contract
We can enter the name of deployed contract in the Terminal to view the contract information, including the basic information of the contract, code, interfaces, data zones (public_data), call statistics.

**4.1 View contract basic information** 
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/51906e7-18.png",
        "18.png",
        1503,
        680,
        "#42464b"
      ]
    }
  ]
}
[/block]
**4.2 Contract Statistics**
 It is convenient to check operational data including the number of contract calls, the number of tokens transferred in and out.
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/0857fc5-19.png",
        "19.png",
        3142,
        1746,
        "#33363b"
      ]
    }
  ]
}
[/block]
4.2.1 The ranking of hot contracts is also provided in Terminal, enabling a clear view of the number of contract calls, as well as a quick view of the contract details and the execution results of the contract.
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/8eb8fcc-20.jpg",
        "20.jpg",
        3542,
        1892,
        "#303338"
      ]
    }
  ]
}
[/block]
4.2.2 Click the contract to view the contract code, data and statistics.
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/029b14a-21.jpg",
        "21.jpg",
        3464,
        2332,
        "#32353a"
      ]
    }
  ]
}
[/block]