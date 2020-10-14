---
title: "11.2 Non-homogeneous Assets"
slug: "102-non-homogeneous-assets"
hidden: false
createdAt: "2019-06-24T07:22:36.326Z"
updatedAt: "2020-03-20T10:00:26.507Z"
---
Non-homogeneous assets, also known as NH assets, are props in the game.


## Preconditions

1. Account private key needs to be imported to command line wallet;
2. There should be sufficient funds in the accounts, and the specific consumption amount is yet to be determined;
3. Unlock the wallet when executing the command;

## 1. Register as a developer

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
**Parameter explanation:**

creator: string Creator account name

broadcast: bool Whether to broadcast or not


**Example:** 
[block:code]
{
  "codes": [
    {
      "code": "register_nh_asset_creator official-account true",
      "language": "shell"
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
**Parameter explanation:**

creator: string Creator account name

world_view: string Created worldview

broadcast: bool Whether to broadcast or not


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
## 3.  Propose connecting worldview

**Command Format:** 
[block:code]
{
  "codes": [
    {
      "code": "propose_relate_world_view proposing_account,expiration_time, world_view_owner,world_view,broadcast",
      "language": "shell"
    }
  ]
}
[/block]
**Parameter explanation:**

proposing_account: string Associated account name

expiration_time: fc::time_point_sec type Propose expiration time

world_view_owner: string The current owner of the worldview

world_view: string Worldview name

broadcast: bool Whether to broadcast or not

**Example:** 
[block:code]
{
  "codes": [
    {
      "code": "propose_relate_world_view nicotest1 \"2019-09-02T06:22:48\" init1 bWorldView true",
      "language": "shell"
    }
  ]
}
[/block]
##4. Create and Issue Homogeneous Assets

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
**Parameter explanation:**

creator: string Creator account name

owner: string Created worldview

asset_qualifier: string Asset qualifier

world_view: string Worldview name

base_describe: string Description

broadcast: bool Whether to broadcast or not


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