---
title: "Application Examples of 1808 Standard And Worldview System"
slug: "application-examples-of-1808-standard-and-worldview-system"
hidden: false
createdAt: "2019-03-17T03:38:37.684Z"
updatedAt: "2019-03-17T10:03:35.026Z"
---
This section explains how on-chain contract works on 1808 non-homogeneous digital assets and how non-homogeneous digital assets under worldview are transferred and linked. Please refer to Cocos-BCX Smart Contract User Guide for more information.
[block:api-header]
{
  "title": "Contract Works on 1808 Standard Assets"
}
[/block]
NH assets ownership transfer

Non-homogeneous assets transfer – caller

◼ Function prototype
void transfer_nht_from_caller(string to, string token_hash_or_id)

◼ Calling convention
Transfer non-homogeneous assets from contract caller to the account ‘to’

◼ Parameter specification 
to: Targeted account, token_hash_or_id: hash value or id number of specified non-homogeneous assets
Non-homogeneous assets transfer - owner 

◼ Function prototype
void transfer_nht_from_owner(string to, string token_hash_or_id)

◼ Calling convention
Transfer non-homogeneous assets from contract owner to the account ‘to’

◼ Parameter specification
to: Targeted account, token_hash_or_id: hash value or id number of specified non-homogeneous assets
Modify data of NH assets (Within specified data zone)

**Non-homogeneous assets transfer – owner**

◼ Function prototype
void nht_describe_change(string nht_hash_or_id, string key, string value)

◼ Calling convention
The modified description of non-homogeneous contract is corresponding zone to the contract. 

◼ Parameter specification
token_hash_or_id: Hash value or id number of specified non-homogeneous assets, key: Describe item index, value: Corresponding information to index
[block:api-header]
{
  "title": "Scenario and Examples"
}
[/block]
**Equipment Enhancement in Games (Contracts)** 

This example shows that paid items are authorized to cross game world, that is to say, players need to pay assets to get specified items into game world or contract system. 

Game extracts information from item zone and submits it to contract, and connections with original game develops a linkage to contract concerning game skills, such as eyes of hawk shown in the following code, and enables items across world with skill attributes.
[block:code]
{
  "codes": [
    {
      "code": "--Contract function: Initialized items that across worlds\n-- item_id: Item ID\nProject Cocos-BCX\n16\n-- original_skill: Information of skills in the original game\n-- add_skill: Added linkage skills in this game\n-- add_description:Added zone data description in this game\nfunction init_item_from_another_world( item_id, original_skill, add_skill, add_description)\n--Non-void judgment of information\nassert(original_skill!=nil,'null original skill info')\nassert(add_skill!=nil,'null add skill info')\nassert(add_description!=nil,'null description info')\nlocal add_skill_value='null'\n--Judging original skills and acquiring linkage skills in this game\nlocal switch={\n['eyes of hawk']=function() add_skill_value='{\"VIT_UP\":25}' end\n['heart of lion']=function() add_skill_value='{\"STR_UP\":50}' end\n['speed of pard']=function() add_skill_value='{\"AGI_UP\":40}' end\n['wisdom of dwarf']=function() add_skill_value='{\"INT_UP\":30}' end\n}\nlocal res=switch[original_skill]\nif(res)then\nres()\n--Update linkage skills into zone data \nnht_describe_change( item_id, add_skill, add_skill_value)\nnht_describe_change( item_id, 'another_world_message', add_description)\nelse\nassert(res,'unexpected original game skill type')",
      "language": "javascript"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "Implementation of Complex Business Models"
}
[/block]
Improved Cocos-BCX chain adds multiple atomic OP and data structure for possible new-type transactions. Based on BCX contract system, developers find it easy to achieve complex financial transactions, such as asset lease, mortgage and pledge. In this case, drawbacks in traditional blockchain system, including singular economic mode with deficient fluidity, will be overcome, and market activities further vitalized. The following shows how three transaction modes are achieved in BCX.

**Lease** 
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/3bc9834-36.png",
        "36.png",
        1297,
        221,
        "#f5f5f6"
      ],
      "caption": "Flow design of lease business"
    }
  ]
}
[/block]
Contract design: 
•  Defining lease process functions, such as lease, user right transfer, user right withdrawing, inventory check, inventory update. 
•  Defining an asset lease pool with price and other information.
Process:
•  Owner adds lease-required asset information, and draws up rental or computation rules through inventory updating function in the contract. 
•  Lease agreement takes into effect when lessee pays rental and other assets via lease function. 
•  Contract defines asset user right black and white list via user right function, and transfers user right to lessee and rental to the account of the owner. Contract gets inventory assets tagged as leased, and meanwhile defines a timing task - withdrawing function of user right upon expiration. 
•  When timing task is upon expiration, function of user right will be withdrawn and transferred to the owner through calling contract.

**Pledge**
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/1b348da-37.png",
        "37.png",
        1104,
        305,
        "#f6f6f7"
      ],
      "caption": "Flow design of pledge business"
    }
  ]
}
[/block]
Contract design:  
•  Defining pledge functions, such as pledge, user right transfer, user right withdrawing, pledge status check, pledge-able list. 
•  Defining a structured record of pledge with information of pledge-able assets and mortgaged assets.
Process: 
•  Pledgee provides information of pledge-able objects, marks pledge price or computation rules through establishing function of pledge-able list.
•  Pledger transfers asset right to pledgee through pledge function, and updates the pledge record list upon receiving deposit paid by pledgee. After that, pledger releases a timing task - transferring user right of objects according to redemption upon expiration.
•  If deposit payment and other conditions cannot meet the requirement upon expiration of timing task, contract function of withdrawing user right will be called, and asset right will be transferred to the account of the pledgee through function of changing user right. If redemption completed, contract function of user right of transfer will be called and ownership will return to pledger.

**Pawn**
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/c916ba1-38.png",
        "38.png",
        1148,
        358,
        "#f7f7f7"
      ],
      "caption": "Flow design of pawn business"
    }
  ]
}
[/block]
Contract design:
•  Defining pawn functions, such as pawn, user right transfer, user right withdrawing, pawn status check, pawn list and other process functions of pawn transactions. 
•  Defining a structured list of pawned goods with information of pawn-able assets and the pawned assets.
Deductive process:
•  Pawnee provides information of pawn-able objects through establishing function of pawn list, and identifies pawn price or computation rules. 
•  Pawner transfers asset user right to pawnee through defining pawn function, updates the record of pawn list upon receiving deposits paid by pawnee, and releases a timing task - designing modes of periodical or scheduled return of deposit, interests paid or both. 
•  If deposit payment and other conditions cannot meet the requirement upon expiration of timing task, contract function of withdrawing user right will be called, and asset right will be transferred to the account of the pawn through changing OP of user right. If all the requirements are met, user right will be transferred to pawner through changing OP of user right.