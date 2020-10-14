---
title: "Example 1: Setting Prizing Pool"
slug: "example-1-setting-prizing-pool"
hidden: false
createdAt: "2019-03-15T06:29:24.628Z"
updatedAt: "2019-03-17T02:40:00.747Z"
---
[block:code]
{
  "codes": [
    {
      "code": "\nassert(is_owner(),'You`re not the contract`s owner')\n    if(public_data.ticket_pool_1==nil)then\n        public_data.ticket_pool_1={}\n        public_data.ticket_pool_2={}\n        if (public_data.ticket_pool_1[ticket]==nil) then\n            public_data.ticket_pool_2[#public_data.ticket_pool_2+1]=ticket -Note: the subscript of array lua starts with 1\n            public_data.ticket_pool_1[ticket]=#public_data.ticket_pool_2\n        end\n    else\n        if (public_data.ticket_pool_1[ticket]==nil) then\n            public_data.ticket_pool_2[#public_data.ticket_pool_2+1]=ticket\n            public_data.ticket_pool_1[ticket]=#public_data.ticket_pool_2\n        end\n    end\nend",
      "language": "lua"
    }
  ]
}
[/block]
lucky draw，ticket：prize ticket，amount：token amount，asset： token type
[block:code]
{
  "codes": [
    {
      "code": "\n    assert(amount>=1000000,'amount should not be less than 1000000')\n    assert(asset=='COCOS','asset error')\nlocal total=get_account_balance(contract_base_info.owner,asset)\nassert((#public_data.ticket_pool_2)*amount<=total,'Current maximum compensation ratio:'..#public_data.ticket_pool_2..'The biggest bet at present:'..total/(#public_data.ticket_pool_2))\n    transfer_from_caller(contract_base_info.owner,amount,asset,true)\n    local index=random()%(#public_data.ticket_pool_2)+1  --Note: the subscript of array lua starts with 1\nlocal rate=0\n    if(public_data.ticket_pool_2[index]==ticket)then\n        while(true)do\nrate =random()%(#public_data.ticket_pool_2)\nif(rate*amount<=total) then\ntransfer_from_owner(contract_base_info.caller,rate*amount,asset,true)\nbreak\nend\nend\n    end\nlog('ticket:'..public_data.ticket_pool_2[index]..',rate:'..rate)\nend",
      "language": "lua"
    }
  ]
}
[/block]
Random accumulation function, used to verify on-chain random number (for testing)
[block:code]
{
  "codes": [
    {
      "code": "function sum_public_by_rand()\nassert(is_owner(),'You`re not the contract`s owner')\n    local i=0\n    while(i<10)do\n        i=i+1\n        if(public_data.sum_rand_10==nil)then\n            public_data.sum_rand_10=0\n          public_data.sum_rand_10=public_data.sum_rand_10+random()%100\n        else\n            public_data.sum_rand_10=public_data.sum_rand_10+random()%100\n        end\n    end\nend",
      "language": "lua"
    }
  ]
}
[/block]