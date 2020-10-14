---
title: "Example 2: Using Contract To Manage Description of Non-Homogeneous Assets"
slug: "example-2-using-contract-to-manage-description-of-non-homogeneous-assets"
hidden: false
createdAt: "2019-03-15T06:29:40.463Z"
updatedAt: "2019-03-18T03:15:19.366Z"
---
[block:code]
{
  "codes": [
    {
      "code": "function my_nht_describe_change( nht_hash_or_id,change_values_json)\nlocal change_values=cjson.decode(change_values_json)--Note: cjson module is used here\nfor key,value in pairs(change_values) do--Note: iterate through lua table，distinguish ipairs与and pairs\nlog('key:'..key..',value:'..value)\nnht_describe_change( nht_hash_or_id,key,value,true)\nend\nend\n//nht_hash_or_id：Hash or ID of non-fungible tokens\n//change_values_json: Designated json content to be modified, used for mass modification ",
      "language": "lua"
    }
  ]
}
[/block]
**Revise contract authentication** 
[block:code]
{
  "codes": [
    {
      "code": "function my_change_contract_authority(publickey)\nassert(is_owner(),'You`re not the contract`s owner')\n    change_contract_authority(publickey)\nend",
      "language": "lua"
    }
  ]
}
[/block]
**Set contract authentication identifier to initiate or suspend request for contract signature. Only the corresponding trusted execution environment has contract authentication** 
[block:code]
{
  "codes": [
    {
      "code": "function set_permissions_flag(flag)\n    assert(is_owner(),'You`re not the contract`s owner')\n    set_permissions_flag(flag)\nend",
      "language": "lua"
    }
  ]
}
[/block]
**Encrypted data creator** 
[block:code]
{
  "codes": [
    {
      "code": "function my_make_memo(to,key,value) make_memo(to,key,value,true) end",
      "language": "lua"
    }
  ]
}
[/block]