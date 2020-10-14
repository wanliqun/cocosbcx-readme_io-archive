---
title: "Smart Contract Tutorials And Examples"
slug: "smart-contract-tutorials-and-examples"
hidden: false
createdAt: "2019-03-15T06:24:52.578Z"
updatedAt: "2019-03-16T15:49:06.063Z"
---
[block:api-header]
{
  "title": "Hello World"
}
[/block]

[block:code]
{
  "codes": [
    {
      "code": "function logtest()\n\tchainhelper:log('hello world')\n\tchainhelper:log(date('%Y-%m-%dT%H:%M:%S', chainhelper:time()))\nend",
      "language": "lua",
      "name": null
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "Acquire Block Header Time"
}
[/block]

[block:code]
{
  "codes": [
    {
      "code": "function timetest() \n\tpublic_data.time=date('%Y-%m-%dT%H:%M:%S', chainhelper:time()) \n\twrite_list={public_data={time=true}} \n\tchainhelper:write_chain() \nend",
      "language": "lua"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "Transfer"
}
[/block]

[block:code]
{
  "codes": [
    {
      "code": "function transfer(amount,symbol,islog) \n\tchainhelper:transfer_from_caller(contract_base_info.owner,amount,symbol,islog) --Transfer homogeneous assets from contract owners to accounts\n\tchainhelper:transfer_from_owner(contract_base_info.caller,amount,symbol,islog) --Transfer homogeneous assets from contract callers to accounts\nend",
      "language": "lua"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "Assets Lock-Up Configuration"
}
[/block]

[block:code]
{
  "codes": [
    {
      "code": "function init()\n\tassert(chainhelper:is_owner(),'chainhelper:is_owner()')\n\tread_list={public_data={is_init=true}}\n\tchainhelper:read_chain()\n\tassert(public_data.is_init==nil,'public_data.is_init==nil')\n\tpublic_data.locked=0\n\tpublic_data.is_init=true\n\tchainhelper:write_chain()\nend\n\nfunction pay_with_lock(amount,symbol)\n\tassert(amount>0,'amount > 0')\n\tread_list={public_data={}}\n\tchainhelper:read_chain()\n\tassert(public_data.locked+amount>public_data.locked,'public_data.locked+amount>public_data.locked')\n\tpublic_data.locked=public_data.locked+amount;  --[[Adjust lock-up record]] \n\tassert(public_data.locked<=chainhelper:number_max(),'public_data.locked<=chainhelper:number_max()')\n\tchainhelper:transfer_from_caller(contract_base_info.owner,amount,symbol,true)\n--[[Deposit token]]\n\tchainhelper:adjust_lock_asset(symbol,amount)  --[[Lock up token]]\n\twrite_list=read_list\n\tchainhelper:write_chain()\nend\t\n\nfunction adjustment_lock_and_transfer(to,amount,symbol)\n\tassert(chainhelper:is_owner(),'chainhelper:is_owner()')\n\tread_list={public_data={}}\n\tchainhelper:read_chain()\n\tassert(amount > 0 and public_data.locked – amount >= 0, 'amount>0 and public_data.locked-amount>=0')\n\tpublic_data.locked=public_data.locked-amount  --[[Adjust lock-up record]]\n\tchainhelper:adjust_lock_asset(symbol,-amount)\t  --[[Unlock token]]\n\tif(to~=contract_base_info.owner)then\n\t\tchainhelper:transfer_from_owner(to,amount,symbol,true)  --[[Withdraw token]]\n\tend\n\twrite_list=read_list\n\tchainhelper:write_chain()\nend",
      "language": "lua"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "Generate/ Verify Hash"
}
[/block]

[block:code]
{
  "codes": [
    {
      "code": "function set_hash(source) \n\tpublic_data.hash256=chainhelper:hash256(source) \n\tpublic_data.hash512=chainhelper:hash512(source) \n\tchainhelper:write_chain() --Default：write_list={public_data={},private_data={}} ,Update all the data, this contract contains only 2 pieces of data: hash256 and hash512\nend \nfunction check_hash(source) \n\tchainhelper:read_chain() --Default：read_list={public_data={},private_data={}} ,Load in all the data，this contract contains only 2 pieces of data: hash256 and hash512\n\tassert(public_data.hash256==chainhelper:hash256(source),'hash256 check error') \n\tassert(public_data.hash512==chainhelper:hash512(source),'hash512 check error') \nend",
      "language": "lua"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "Describe Modified Non-Homogeneous Assets"
}
[/block]

[block:code]
{
  "codes": [
    {
      "code": "--Modify non-homogeneous assets description through json string\nfunction my_nht_describe_change( nht_hash_or_id,values_json) \n\tlocal values=cjson.decode(values_json) \n\tfor key,value in pairs(values)  do  \n\t\tchainhelper:log('key:'..key..',value:'..value)   \n\t\tchainhelper:nht_describe_change( nht_hash_or_id,key,value,true)  \n\tend  \nend\n\n--Modify non-homogeneous assets description through lua table\nfunction nht_change_with_table( nht_hash_or_id,values_table) \n\tfor key,value in pairs(values_table)  do  \n\t\tchainhelper:log('key:'..key..',value:'..value)   \n\t\tchainhelper:nht_describe_change( nht_hash_or_id,key,value,true)  \n\tend  \nend",
      "language": "lua"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "Random Function Examples"
}
[/block]

[block:code]
{
  "codes": [
    {
      "code": "--A function example is with ten times of random accumulations as well as output\nfunction sum_public_by_rand()\n    read_list={public_data={sum_rand_10=true}}\nchainhelper:read_chain()\n--Refuse callers’ interface permission through assert and is_owner\n\tassert(chainhelper:is_owner(),'You`re not the contract`s owner')\n    local i=0\n    while(i<10)do\n        i=i+1\n        if(public_data.sum_rand_10==nil)then\n            public_data.sum_rand_10=0\n            public_data.sum_rand_10=public_data.sum_rand_10+chainhelper:random()%100\n--The value of % after random() indicates randomness range, for instance, randomness ranges from 0 to 99 in this example. \n        else\n            public_data.sum_rand_10=public_data.sum_rand_10+chainhelper:random()%100\n        end\n    end\n    write_list={public_data={sum_rand_10=true}}\n    chainhelper:write_chain()\n\tchainhelper:log('date:'..date('%Y-%m-%dT%H:%M:%S', chainhelper:time())..',sum:'..public_data.sum_rand_10) end\nend",
      "language": "lua"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "Lucky Draw Game Examples"
}
[/block]

[block:code]
{
  "codes": [
    {
      "code": "--Set prize pool\nfunction set_ticket(ticket)  \t  \t\t\n  assert(chainhelper:is_owner(),'You`re not the contract`s owner')    \t\t\n  read_list={public_data={ticket_pool_1=true,ticket_pool_2=true}}  \n  chainhelper:read_chain()  \n  if(public_data.ticket_pool_1==nil)then  \n\tpublic_data.ticket_pool_1={}  \n\tpublic_data.ticket_pool_2={}  \n\tif (public_data.ticket_pool_1[ticket]==nil) then    \t\t\n\t\tpublic_data.ticket_pool_2[#public_data.ticket_pool_2+1]=ticket  \n\t\tpublic_data.ticket_pool_1[ticket]=#public_data.ticket_pool_2  \n\tend     \n  else\n\tif (public_data.ticket_pool_1[ticket]==nil) then  \n\t\tpublic_data.ticket_pool_2[#public_data.ticket_pool_2+1]=ticket  \n\t\tpublic_data.ticket_pool_1[ticket]=#public_data.ticket_pool_2  \n\tend     \n  end\n  assert(#public_data.ticket_pool_2<=12)\n  write_list={public_data={ticket_pool_1={[ticket]=true},ticket_pool_2={[#public_data.ticket_pool_2]=true}}}  \n  chainhelper:write_chain()  \n  end\n\n--Raffle\nfunction luck_draw(ticket,amount,asset)  \n  assert(amount>=1000000,'amount should not be less than 1000000')  \n  assert(asset=='COCOS','asset error')  \n  read_list={public_data={ticket_pool_1=true,ticket_pool_2=true}}  \n  chainhelper:read_chain()  \t\n  local total=chainhelper:get_account_balance(contract_base_info.owner,asset)  \t\n  assert((#public_data.ticket_pool_2)*amount<=total,'Current maximum compensation ratio:'..#public_data.ticket_pool_2..'The biggest bet at present:'..total/(#public_data.ticket_pool_2))  \n  chainhelper:transfer_from_caller(contract_base_info.owner,amount,asset,true)  \n  local index=chainhelper:random()%(#public_data.ticket_pool_2)+1  \t\n  local rate = chainhelper:random()%(#public_data.ticket_pool_2)+1\n  chainhelper:log('luck:'..public_data.ticket_pool_2[index]..',rate:'..rate)\n  if(public_data.ticket_pool_2[index]==ticket)then  \n\tchainhelper:transfer_from_owner(contract_base_info.caller,rate*amount,asset,true)  \t\n  end\n end\n --Reset prize pool\nfunction reset_ticket() \n\twrite_list_list={public_data={ticket_pool_1=false,ticket_pool_2=false}}\n\tchainhelper:write_chain()\nend",
      "language": "lua"
    }
  ]
}
[/block]