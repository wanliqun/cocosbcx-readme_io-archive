---
title: "Props Release Tutorial"
slug: "props-release-tutorial"
hidden: false
createdAt: "2019-03-15T06:25:03.947Z"
updatedAt: "2019-03-18T03:15:19.363Z"
---
[block:code]
{
  "codes": [
    {
      "code": "/*\nPre-determined conditions\n1.Command line wallet requires account private key import\n2.Enough assets in the account. Those who registered as non-homogeneous assets creators need one core token, and so do worldview creators. One or two tokens are required to create non-homogeneous assets, 500,000 tokens for homogeneous assets with a three-letter name, 300,000 tokens for a four-letter name, 5,000 tokens for a four-more -letter name and 500 tokens for issuing homogeneous assets to accounts.\n3.Unlock wallet before executing command\n*/",
      "language": "text"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "1. Registered As Creator of Non-Homogeneous Assets"
}
[/block]
Open command line wallet and execute the following command:  
Command format: 
[block:code]
{
  "codes": [
    {
      "code": "register_nh_asset_creator <creator> <broadcast>",
      "language": "lua"
    }
  ]
}
[/block]
Example: 
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

[block:api-header]
{
  "title": "2. Create Worldview"
}
[/block]
Command format: 
[block:code]
{
  "codes": [
    {
      "code": "create_world_view <creator> <world_view> <broadcast>",
      "language": "lua"
    }
  ]
}
[/block]
Example:
[block:code]
{
  "codes": [
    {
      "code": "create_world_view official-account MOBA true",
      "language": "text"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "3. Create And Release Non-Homogeneous Assets"
}
[/block]
Command format: 
[block:code]
{
  "codes": [
    {
      "code": "create_nh_asset <ceator> <owner> <asset_qualifier> <world_view> <base_describe> <broadcast>",
      "language": "lua"
    }
  ]
}
[/block]
Example: 
[block:code]
{
  "codes": [
    {
      "code": "create_nh_asset official-account official-account 1.3.0 MOBA “this is a describe” true",
      "language": "lua"
    }
  ]
}
[/block]