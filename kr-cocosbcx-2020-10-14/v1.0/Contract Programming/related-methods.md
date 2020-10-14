---
title: "Related Methods"
slug: "related-methods"
hidden: false
createdAt: "2019-03-15T06:28:43.696Z"
updatedAt: "2019-03-18T03:15:19.365Z"
---
[block:api-header]
{
  "title": "Asset Transfer"
}
[/block]
**Transfer of homogeneous assets—caller** 

Function prototype  Transfer homogeneous assets from contract caller to account 'to'
void transfer_from_caller(string to, uint token, string symbol,bool enable_logger)
to: Target account
token: Amount
symbol: Asset symbol
Token amount shall be larger than 0 and smaller than the maximal lua number
enable_logger identifies whether related influence is recorded in the contract result 

**Transfer of non-homogeneous assets—caller**

Function prototype  
Transfer non-homogeneous assets from contract caller to account 'to'

void transfer_nht_from_caller(string to, string token_hash_or_id,bool enable_logger)
to: Target account
token_hash_or_id: Hash value or ID number of designated non-homogeneous assets

enable_logger identifyies whether related influence is recorded in the contract result 
[block:api-header]
{
  "title": "Generate Internal Source Random Number"
}
[/block]
**Function prototype** 

int random()
on-chain internal source random function. Scope of return value(0 – 2147483647)

**Use the function to design probability judgment**

Calling random function in the contract will generate an internal source random outcome via the chain network. The outcome is an int value without symbol. random()%N may be used to determine the scope of the outcome. The following is an example of determining the probability in a game contract: 
--Determine successful upgrade. The random probability is acquired via the internal source random function
local success_judge=random()%100
if(success_judge<=success_rate)then
--Write the object property value into zone data
nht_describe_change( equipment_id, upgrade_name, target_value)
end

The precision of the probability in the example is 1%. Hence. The N in the random ()%N takes the value of 100. success_rate is the input specific determined value. For instance, 10 represents the success rate of 10%.
[block:api-header]
{
  "title": "Determine Contract Owner"
}
[/block]
Function prototype 
bool is_owner()
Determine whether the contract caller is the contract owner, used for contract assert
[block:api-header]
{
  "title": "Update The Description of Non-Homogeneous Assets"
}
[/block]
Function prototype
Transfer non-homogeneous assets from contract owner to account 'to'
Revise related contract description of the non-homogeneous assets. The revised part is the related zone in the contract.

void nht_describe_change(string nht_hash_or_id, string key, string value,bool enable_logger)
nht_hash_or_id: Hash value or ID number of the designated non-homogeneous assets
key: Descriptor item index, value: indexing related description
The function shall update the changes according to the standards for non-homogeneous digital assets. enable_logger identifies whether related influence is recorded in the contract result.
[block:api-header]
{
  "title": "Set Contract Authentication Identifier"
}
[/block]
Function prototype
Set contract authentication identifier to initiate or suspend request for contract signature 

void set_permissions_flag(bool flag)

Only the corresponding trusted execution environment has contract authentication. In the trusted execution environment, when a user calls the contract, the user signature and contact signature will be completed at the same time.
[block:api-header]
{
  "title": "Revise Contract Authentication"
}
[/block]
Function prototype
Revise the contract authentication certificate into target publickey
void change_contract_authority(string publickey)
[block:api-header]
{
  "title": "Construct Encrypted Data"
}
[/block]
Function prototype 
Encrypted data constructor 
void make_memo (string to, string key, string value,bool enable_logger)
to: Designated decrypter
key:  Encryption torrent provided by the ECC shared secret
value: Encrypted text
enable_logger identifies whether related influence is recorded in the contract result
[block:api-header]
{
  "title": "Query Account Name And Asset Symbol"
}
[/block]
Function prototype
int get_account_balance(string account_name_or_id,string asset_symbol_or_id)
account_name_or_id: Name of account to be queried or
asset_symbol_or_id: Asset symbol or ID to be queried
[block:api-header]
{
  "title": "Record Information"
}
[/block]
Function prototype
void log(string message)
message: Information to be recorded, shall be recorded in the contract result 
[block:api-header]
{
  "title": "Interpret Incoming Function"
}
[/block]
Function prototype
table decode(string jsonstr)
string encode(table tal)
cjson module, often used to interpret the structured function parameters
Calling method cjson.function_name(*)