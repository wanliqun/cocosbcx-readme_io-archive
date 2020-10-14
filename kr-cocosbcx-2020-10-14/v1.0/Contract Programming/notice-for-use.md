---
title: "Notice for Use"
slug: "notice-for-use"
hidden: false
createdAt: "2019-03-15T06:28:18.573Z"
updatedAt: "2019-03-18T03:15:19.365Z"
---
Cocos-BCX smart contract is written in Lua and revised upon the official Version 5.3 without altering the grammar. New on-chain manipulation function has been added and the function library adjusted for better adaptation to the chain environment.

--Contract data is classified as:  User data zone and public data zone.
--User data zone: To store the data generated from users’ call of contract and is defined by the contract writer.  
--Public data zone: To store regular data of the contract. Contract writer can impose restrictions on the callers with owner assert (is_owner())) Public data zone is recorded with public_data table. Writer shall put public data into public_data object.
--Special object: 
--public_data: used to record public data zone. The object properties are defined by the contract writer.
--private_data: User data zone points to the current contract caller.
--read_list: Contract data IO read operation registry. The read_list may be written to indicate the necessary context to be loaded. Default state: read_list={public_data={},private_data={}}，Default load all the data in partitions of public_data and private_data. 
--read_list={public_data={test=true}}, only read data of public_data.test, effective when the read_chain() function is executed. 
--write_list:Contract data IO write operation registry. The write_list may be written to indicate the context to be recorded by the chain. Default state: read_list={public_data={},private_data={}}, Record all the data in partitions of public_data and private_data zones by default. 
--write_list={public_data={test=true}}, only write data of public_data.test, effective when the write_chain() function is executed. Value in each write_list path (true/false): true—update if exits else create; false—delete if exists. 
--contract_base_info: Used to store the basic information of the contract. Object revised inside the contract shall not be recorded. Object properties: name (contract name), id（ contract ID）、owner (contract owner ID), caller (current caller ID), creation_date (contract writing time), contract_authority(contract request for authorized signature)

**Chain-related modules: * 

Static function: Calling method: directly using function name inside the contract.
--Function: Read data of designated users through the corresponding path.
--name_or_id: Account name or ID of users to be queried.
--private_data_register_list: Path to the user data zone related to this contract of the corresponding users.
--Return user data in a table format. Where there is not the data designated by the path, the corresponding table branch is empty.
--e.g.: nico_data=get_account_contract_data('nicotest',{nicodata0={nicodata1=true})
--To read the data in nicodata0.nicodata1 of the account “nicotest” in this contract, if nicotest is the contract caller, then nico_data shall be the same as private_data.nicodata0.nicodata1. 
table get_account_contract_data(string name_or_id,table private_data_register_list)
Dynamic function: calling method: chainhelper: function name (parameter…)
[block:code]
{
  "codes": [
    {
      "code": "--source:Source data to be computed\n\t--Return hash256 string\n\tstring hash256(string source)\n\t--source:Source data to be computed\n\t--Return hash512 string\n\tstring hash512(string source)\n\t--Create non-homogeneous items. Contract owners must have corresponding creating authentication \n\t--name_or_id:New Owner of props \n\t--symbol：COCOSQualifier of homogeneous assets, eg. COCOS\n\t--world_view: Worldview\n\t--base_describe: Basic description\n\t--enable_logger identifies whether related influence is recorded in the contract result\n\tvoid create_nh_asset(string owner_id_or_name, string symbol, string world_view, string base_describe, bool enable_logger)\n\t--Adjust contract owners' assets that are locked in this contract\n\t--symbol_or_id: Asset ID or symbol in need of adjustment\n\t--amount: Amount with precision may be negative (i.e. lowering the locked amount). The locked amount after adjustment shall be larger than 0 and smaller than the maximum amount of the assets of the contract owner\n\tvoid adjust_lock_asset(string symbol_or_id, int64_t amount)\n\t--Contact data IO read operation, corresponding to read_list registry\n\tvoid read_chain()\n\t--Contact data IO write operation, corresponding to write_list registry\n\tvoid write_chain()\n\t--account_name_or_id:Name or ID of account to be queried\n\t--asset_symbol_or_id:Name or ID of account to be queried\n\tint get_account_balance(string account_name_or_id,string asset_symbol_or_id)\n\t--Transfer assets from contract caller to account 'to', Ammount: token，token symbol: symbol\n\t--The amount of token shall be larger than 0 and smaller than the maximal lua number\n\t--enable_logger identifies whether related influence is recorded in the contract result\n\tvoid transfer_from_caller(string to, uint token, string symbol,bool enable_logger)\n\t--Transfer assets from contract caller to account 'to'，Amount：token，Token symbol：symbol\n\t--The amount of token  shall be larger than 0 and smaller than the maximal lua number\n\t--enable_logger identifies whether related influence is recorded in the contract result\n\tvoid transfer_from_owner(string to, uint token, string symbol,bool enable_logger)\n\t--Encrypted data constructor，to：designated decrypter，key：encrypted torrent provided by the ECC shared secret，value：the encrypted content \n\t--enable_logger identifies whether related influence is recorded in the contract result\n\tvoid make_memo (string to, string key, string value,bool enable_logger)\n\t--Transfer non-homogeneous assets from contract caller to account 'to'，token_hash_or_id：designated non-homogeneous token hash value or ID number\n\t--enable_logger identifies whether related influence is recorded in the contract result \n\tvoid transfer_nht_from_caller(string to, string token_hash_or_id,bool enable_logger)\n\t--Transfer non-homogeneous assets from contract owner to accountTransfer non-homogeneous assets from contract owner to account 'to'，token_hash_or_id：Designated non-homogeneous token hash value or ID number\n\t--enable_logger identifies whether related influence is recorded in the contract result \n\tvoid transfer_nht_from_owner(string to, string token_hash_or_id,bool enable_logger)\n\t--On-chain random function\n\tint  random()\n\t--Judge whether contract caller is the owner，used for contract assert\n\tbool is_owner()\n\t--Revise related contract description of non-fungible tokens. The revised part is the related zone of the contract \n\t--enable_logger identifies whether related influence is recorded in the contract result\n\tvoid nht_describe_change(string nht_hash_or_id, string key, string value,bool enable_logger) \n\t--Set contract authentication identifier to initiate or stop the request for contract signature. Only the corresponding trusted execution environment has contract authentication.\n\t--In the trusted execution environment, when the user calls the contract, the user signature and contact signature shall be completed at the same time\n\tvoid set_permissions_flag(bool flag)\n\t--Revise contract authentication\n\tvoid change_contract_authority(string publickey)\n\t--message:Information to be recorded, shall be recorded in the contract result\n\tvoid log(string message)",
      "language": "lua"
    }
  ]
}
[/block]
Basic module: configurable based on No.0 contract. Support from the sandbox for the basic module is controlled. In the later period, No.0 basic support contract shall be managed by the council.   

Basic module expansion: cjson module. The current contract ABI has accepted the external table parameters. Yet the cjson module is retained for incoming objects in strings and object serialization.
[block:code]
{
  "codes": [
    {
      "code": "\t--cjson module, Often used to interpret the incoming structured function parameters\n\t--Calling method cjson.function_name(*)\n\t\ttable  decode(string jsonstr)\n\t\tstring encode(table tal)",
      "language": "lua"
    }
  ]
}
[/block]
**Notes: **
1. Session recovery does not include the recovery of codes during run time (i.e., lambda expression is only effective in the current function context, including the dynamic property functions of table and metatable)  
2. Unified contract application layer tables. Suspend metatable (because (a) common lambda function in metastable is used and codes cannot be recovered during run time; (b) IO speed of metatable is slower than that of table)

**Support common Lua standard library function** 
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/1810ccb-35.png",
        "35.png",
        928,
        644,
        "#fafafa"
      ]
    }
  ]
}
[/block]
**Specification of contract data**

Contract data is classified as:  User data zone and public data zone
User data zone stores the data generated from users’ call of contract and is defined by the contract writer. Only global variables shall be recorded by the chain.
Public data zone: Stores regular data of the contract. Contract writer can impose restrictions on the callers with owner assert assert(is_owner()). Public data zone is recorded with public_data table. Writer shall put public data into public_data object.

**Special Object** 

public_data //Public data zone stores regular data of the contract. Contract writer can revise authentication with is_owner. The properties are defined by the contract writer. 
private_data //User data zone is used to record all the data generated from users’ call of contract.
contract_base_info //Used to store the basic information of contract.
contract_base_info objects are read only. Objects revised inside the contract shall not be recorded: 
name (Contract name)
id (Contract ID)
owner (Contract owner ID)
caller (Current caller ID)
creation_date (Contract writing time)
contract_authority (contract request for authorized signature)