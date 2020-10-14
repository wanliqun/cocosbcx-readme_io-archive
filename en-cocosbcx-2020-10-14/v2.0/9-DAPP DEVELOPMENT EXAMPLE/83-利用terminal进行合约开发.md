---
title: "9.3 Contract Development with Cocos Terminal"
slug: "83-利用terminal进行合约开发"
excerpt: "Cocos Terminal adds Contract Manage function in Toolkits for​ developers to create, update contracts, and execute contract interfaces directly."
hidden: false
createdAt: "2019-07-18T06:53:02.891Z"
updatedAt: "2020-03-02T09:30:00.482Z"
---
# Contract Development

##  1. Introduction
a. Log in to [Terminal]( http://cocos-terminal.com/#/)
b. Click Contract Manage in the left directory bar to view various information about the contracts existed under this account, including the basic information of the contract, code, interface, data zone (public_data), etc., as shown below:

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/af24778-1.png",
        "1.png",
        1920,
        902,
        "#2b2d2f"
      ]
    }
  ]
}
[/block]
## 2. Create a contract
a. Click Add to create a new contract.
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/3119512-2.png",
        "2.png",
        1920,
        902,
        "#2c2d2f"
      ]
    }
  ]
}
[/block]
b. Fill in the contract name in the pop-up window. The contract name should be 4-63 characters consisting of lowercase letters or numbers​ and starts with "contract.", for example, "contract.testnew"
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/b9411b5-3.png",
        "3.png",
        538,
        259,
        "#50555c"
      ]
    }
  ]
}
[/block]
## 3. Edit contract code, and update existing contracts
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
## 4. Release contract
a. Click Release
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/4cbc546-4.png",
        "4.png",
        1237,
        569,
        "#242425"
      ]
    }
  ]
}
[/block]
b. Click Random Generation. If the contract opens the permission validation, the app_keys configuration entry of JS-SDK must be filled in with the key. It is recommended to copy and save the key.
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/3d0246d-5.png",
        "5.png",
        940,
        507,
        "#494b51"
      ]
    }
  ]
}
[/block]
c. Click OK. Contract​ creation requires a certain fee.
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/def7ca8-6.png",
        "6.png",
        804,
        418,
        "#383d44"
      ]
    }
  ]
}
[/block]
## 5. Call the contract
a. After the contract is released, you can find the interface of the contract as directed by the arrow in the picture below. Click Interfaces to fill in the parameters to execute the interface.
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/8bbb501-7.png",
        "7.png",
        1397,
        544,
        "#262626"
      ]
    }
  ]
}
[/block]
b. It requires a certain fee to call the contract.
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/035240b-8.png",
        "8.png",
        1103,
        637,
        "#2b2e33"
      ]
    }
  ]
}
[/block]
c. The result of the call will be displayed below the editing area
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/6723626-9.png",
        "9.png",
        1165,
        711,
        "#212121"
      ]
    }
  ]
}
[/block]
## 6. Update contract
a. Use init_data () to initialize the data
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
b. Click Release Contract (the existing contract will be updated to the latest). After the release is done, the init_data() interface must be called to initialize the data.
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/fc60e00-10.png",
        "10.png",
        1119,
        567,
        "#2a2e32"
      ]
    }
  ]
}
[/block]
c. Click Data to initialize the data.
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/7a1db29-11.png",
        "11.png",
        1435,
        621,
        "#252627"
      ]
    }
  ]
}
[/block]
## 7. View contract
You can also fill in the contract name in the search box to view the contract info and statistics.

a. View contract basic information
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/c99f5cc-12.png",
        "12.png",
        1662,
        705,
        "#404349"
      ]
    }
  ]
}
[/block]
b. Contract statistics. It is convenient to check operational data including the number of contract calls, the number of tokens transferred in and out.
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/07f5d63-13.png",
        "13.png",
        1659,
        818,
        "#34383e"
      ]
    }
  ]
}
[/block]
#Contract Statistics
   a. The ranking of hot contracts is also provided in Terminal, enabling a clear view of the number of contract calls, as well as a quick view of the contract details and the execution results of the contract.
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/b549696-14.png",
        "14.png",
        1920,
        902,
        "#34393f"
      ]
    }
  ]
}
[/block]
b. Click the contract to view the contract code, data and statistics.
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/5bf72db-15.png",
        "15.png",
        1907,
        850,
        "#31353b"
      ]
    }
  ]
}
[/block]