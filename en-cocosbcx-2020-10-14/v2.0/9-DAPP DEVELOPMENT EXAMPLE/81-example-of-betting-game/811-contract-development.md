---
title: "9.1.1 Contract Development"
slug: "811-contract-development"
hidden: false
createdAt: "2019-06-26T06:06:29.441Z"
updatedAt: "2020-03-02T09:29:02.812Z"
---
There are a large number of random numbers in the game. In the previous chain systems, such as Ethereum or EOS, it was hard to find a trusted random number. In order to ensure security and reliability, a double random number seed including the server and the client are required. For details, please find in the project: [fairdicegame](https://github.com/Dappub/fairdicegame) 

The built-in random number solution of Cocos-BCX can solve this problem. Our contract is easy to write, which requires only the implementation of a betting interface. The system will settle each bet immediately, as specified below:

[block:code]
{
  "codes": [
    {
      "code": "-- very import \nCOCOS_ACCURACY = 100000\n\nfunction init()\n    assert(chainhelper:is_owner(),'no auth')\n    read_list = {public_data={rate=true,max_bet=true}}\n    chainhelper:read_chain()\n    public_data.rate  = 98\n    public_data.max_bet = 1000000 \n    write_list = {public_data={rate=true,max_bet=true}}\n    chainhelper:write_chain()\nend\n\n\nfunction bet(num, amount)\n    read_list = {public_data={rate=true,max_bet=true}}\n    chainhelper:read_chain()\n\n    num = tonumber(num)\n    amount = tonumber(amount) * COCOS_ACCURACY\n\n    assert( 1 < num and num < 97, \"num must in [2,96] \" )\n    assert( 0 < amount and amount < public_data.max_bet * COCOS_ACCURACY, \"amount must in [1, max]\")\n\n    chainhelper:transfer_from_caller(contract_base_info.owner, amount, 'COCOS', true)\n\n    result_num = chainhelper:random() % 100\n\n    if result_num < num then\n        win_chance = num - 1\n        reward_ratio = public_data.rate*1.0/win_chance\n        reward = amount*reward_ratio\n        chainhelper:transfer_from_owner(contract_base_info.caller, reward, 'COCOS', true)\n    end\nend\n\nfunction hello_world()\n    chainhelper:log('hello world')\n    chainhelper:log(date('%Y-%m-%dT%H:%M:%S', chainhelper:time()))\nend",
      "language": "lua"
    }
  ]
}
[/block]