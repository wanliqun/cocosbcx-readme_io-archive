---
title: "5.4 Contract Sample Code"
slug: "54-contract-sample-code"
hidden: false
createdAt: "2019-06-25T05:40:04.737Z"
updatedAt: "2019-10-18T03:00:39.373Z"
---
For a better understanding of the Cocos-BCX contract, we will show you the commonly used contract sample code.

##1. Get the blockchain time
[block:code]
{
  "codes": [
    {
      "code": "function timetest() \n    public_data.time=date('%Y-%m-%dT%H:%M:%S', chainhelper:time()) \n    write_list={public_data={time=true}} \n    chainhelper:write_chain() \nend\n\n",
      "language": "lua"
    }
  ]
}
[/block]
##2. Transfer
[block:code]
{
  "codes": [
    {
      "code": "function transfer(amount,symbol,islog) \n  chainhelper:transfer_from_owner(contract_base_info.caller,amount,symbol,islog)\nend\n",
      "language": "lua"
    }
  ]
}
[/block]
##3. Asset lock configuration
[block:code]
{
  "codes": [
    {
      "code": "function init()\n    assert(chainhelper:is_owner(),'chainhelper:is_owner()')\n    read_list={public_data={is_init=true}}\n    chainhelper:read_chain()\n    assert(public_data.is_init==nil,'public_data.is_init==nil')\n    public_data.locked=0\n    public_data.is_init=true\n    chainhelper:write_chain()\nend\n\nfunction pay_with_lock(amount,symbol)\n    assert(amount>0,'amount > 0')\n    read_list={public_data={}}\n    chainhelper:read_chain()\n    assert(public_data.locked+amount>public_data.locked,'public_data.locked+amount>public_data.locked')\n    public_data.locked=public_data.locked+amount;  --[[To adjust the lock record]] \n    assert(public_data.locked<=chainhelper:number_max(),'public_data.locked<=chainhelper:number_max()')\n    chainhelper:transfer_from_caller(contract_base_info.owner,amount,symbol,true)\n--[[Transfer tokens in]]\n    chainhelper:adjust_lock_asset(symbol,amount)  --[[Lock the tokens]]\n    write_list=read_list\n    chainhelper:write_chain()\nend    \n\nfunction adjustment_lock_and_transfer(to,amount,symbol)\n    assert(chainhelper:is_owner(),'chainhelper:is_owner()')\n    read_list={public_data={}}\n    chainhelper:read_chain()\n    assert(amount > 0 and public_data.locked – amount >= 0, 'amount>0 and public_data.locked-amount>=0')\n    public_data.locked=public_data.locked-amount  --[[To adjust the lock record]]\n    chainhelper:adjust_lock_asset(symbol,-amount)      --[[Unlock the tokens]]\n    if(to~=contract_base_info.owner)then\n        chainhelper:transfer_from_owner(to,amount,symbol,true)  --[[Transfer the tokens out]]\n    end\n    write_list=read_list\n    chainhelper:write_chain()\nend\n\n",
      "language": "lua"
    }
  ]
}
[/block]
##4. Generate/verify hash
[block:code]
{
  "codes": [
    {
      "code": "function set_hash(source) \n    public_data.hash256=chainhelper:hash256(source) \n    public_data.hash512=chainhelper:hash512(source) \n    chainhelper:write_chain() --Default：write_list={public_data={},private_data={}} ,Update the data. This contract has only two data of hash256 and hash512\nend \nfunction check_hash(source) \n    chainhelper:read_chain() --Default：read_list={public_data={},private_data={}} ,Load the data. This contract has only two data of hash256 and hash512\n    assert(public_data.hash256==chainhelper:hash256(source),'hash256 check error') \n    assert(public_data.hash512==chainhelper:hash512(source),'hash512 check error') \nend\n\n",
      "language": "lua"
    }
  ]
}
[/block]
##5. Change non-homogeneous asset description data
[block:code]
{
  "codes": [
    {
      "code": "--Change the non-homogeneous asset description with a json string\nfunction my_nht_describe_change( nht_hash_or_id,values_json) \n    local values=cjson.decode(values_json) \n    for key,value in pairs(values)  do  \n        chainhelper:log('key:'..key..',value:'..value)   \n        chainhelper:nht_describe_change( nht_hash_or_id,key,value,true)  \n    end  \nend\n\n--Change the non-homogeneous asset description with lua table\nfunction nht_change_with_table( nht_hash_or_id,values_table) \n    for key,value in pairs(values_table)  do  \n        chainhelper:log('key:'..key..',value:'..value)   \n        chainhelper:nht_describe_change( nht_hash_or_id,key,value,true)  \n    end  \nend\n\n",
      "language": "lua"
    }
  ]
}
[/block]
##6. Example of random functions
[block:code]
{
  "codes": [
    {
      "code": "--This random number example is a function of 10 random accumulations and outputting results.\nfunction sum_public_by_rand()\n    read_list={public_data={sum_rand_10=true}}\nchainhelper:read_chain()\n--Limit the interface caller permission by asserting the is_owner function\n    assert(chainhelper:is_owner(),'You`re not the contract`s owner')\n    local i=0\n    while(i<10)do\n        i=i+1\n        if(public_data.sum_rand_10==nil)then\n            public_data.sum_rand_10=0\n            public_data.sum_rand_10=public_data.sum_rand_10+chainhelper:random()%100\n--The value of % after random() is the range of values that need to be random. For example, the random result in this example is 0~99.\n        else\n            public_data.sum_rand_10=public_data.sum_rand_10+chainhelper:random()%100\n        end\n    end\n    write_list={public_data={sum_rand_10=true}}\n    chainhelper:write_chain()\n    chainhelper:log('date:'..date('%Y-%m-%dT%H:%M:%S', \tchainhelper:time())..',sum:'..public_data.sum_rand_10) end\nend\n\n",
      "language": "lua"
    }
  ]
}
[/block]
##7. Lottery game
[block:code]
{
  "codes": [
    {
      "code": "--Set the prize pool\nfunction set_ticket(ticket)                \n  assert(chainhelper:is_owner(),'You`re not the contract`s owner')            \n  read_list={public_data={ticket_pool_1=true,ticket_pool_2=true}}  \n  chainhelper:read_chain()  \n  if(public_data.ticket_pool_1==nil)then  \n    public_data.ticket_pool_1={}  \n    public_data.ticket_pool_2={}  \n    if (public_data.ticket_pool_1[ticket]==nil) then            \n        public_data.ticket_pool_2[#public_data.ticket_pool_2+1]=ticket  \n        public_data.ticket_pool_1[ticket]=#public_data.ticket_pool_2  \n    end     \n  else\n    if (public_data.ticket_pool_1[ticket]==nil) then  \n        public_data.ticket_pool_2[#public_data.ticket_pool_2+1]=ticket  \n        public_data.ticket_pool_1[ticket]=#public_data.ticket_pool_2  \n    end     \n  end\n  assert(#public_data.ticket_pool_2<=12)\n  write_list={public_data={ticket_pool_1={[ticket]=true},ticket_pool_2={[#public_data.ticket_pool_2]=true}}}  \n  chainhelper:write_chain()  \n  end\n\n--Draw a lottery\nfunction luck_draw(ticket,amount,asset)  \n  assert(amount>=1000000,'amount should not be less than 1000000')  \n  assert(asset=='COCOS','asset error')  \n  read_list={public_data={ticket_pool_1=true,ticket_pool_2=true}}  \n  chainhelper:read_chain()      \n  local total=chainhelper:get_account_balance(contract_base_info.owner,asset)      \n  assert((#public_data.ticket_pool_2)*amount<=total,'Current maximum compensation ratio:'..#public_data.ticket_pool_2..'The biggest bet at present:'..total/(#public_data.ticket_pool_2))  \n  chainhelper:transfer_from_caller(contract_base_info.owner,amount,asset,true)  \n  local index=chainhelper:random()%(#public_data.ticket_pool_2)+1      \n  local rate = chainhelper:random()%(#public_data.ticket_pool_2)+1\n  chainhelper:log('luck:'..public_data.ticket_pool_2[index]..',rate:'..rate)\n  if(public_data.ticket_pool_2[index]==ticket)then  \n    chainhelper:transfer_from_owner(contract_base_info.caller,rate*amount,asset,true)      \n  end\n end\n --Reset the  pool\nfunction reset_ticket() \n    write_list_list={public_data={ticket_pool_1=false,ticket_pool_2=false}}\n    chainhelper:write_chain()\nend \n\n",
      "language": "lua"
    }
  ]
}
[/block]