---
title: "10.2 Non-homogeneous Assets"
slug: "102-non-homogeneous-assets"
hidden: false
createdAt: "2019-06-24T07:22:36.326Z"
updatedAt: "2019-06-24T07:22:41.104Z"
---
Non-homogeneous assets, also known as NH assets, are props in the game.


## Preconditions

1. Account private key needs to be imported to command line wallet;
2. There should be sufficient funds in the accounts, and the specific consumption amount is yet to be determined;
3. Unlock the wallet when executing the command;

## 1. 
1.Register as a developer

Open command line wallet cli_wallet, and execute the following command:

**Command Format:** 

[block:code]
{
  "codes": [
    {
      "code": "register_nh_asset_creator <creator> <broadcast>",
      "language": "shell"
    }
  ]
}
[/block]
**Example:** 

[block:code]
{
  "codes": [
    {
      "code": "register_nh_asset_creator official-account true",
      "language": "lua"
    }
  ]
}
[/block]
## 2. Create Worldview

**Command Format:** 

[block:code]
{
  "codes": [
    {
      "code": "create_world_view <creator> <world_view> <broadcast>",
      "language": "shell"
    }
  ]
}
[/block]
**Example:** 

[block:code]
{
  "codes": [
    {
      "code": "create_world_view official-account MOBA true",
      "language": "shell"
    }
  ]
}
[/block]

##3. Create and Issue Homogeneous Assets

**Command Format:** 

[block:code]
{
  "codes": [
    {
      "code": "create_nh_asset <ceator> <owner> <asset_qualifier> <world_view> <base_describe> <broadcast>",
      "language": "shell"
    }
  ]
}
[/block]
**Example:** 

[block:code]
{
  "codes": [
    {
      "code": "create_nh_asset official-account official-account 1.3.0 MOBA “this is a describe” true",
      "language": "shell"
    }
  ]
}
[/block]

**Tips**

Demo program of JS-SDK (provided by Cocos-BCX) can be used for issuing NH assets as well.