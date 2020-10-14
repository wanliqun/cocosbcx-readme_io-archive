---
title: "5.3 Data Persistence"
slug: "53-data-persistence"
hidden: false
createdAt: "2019-06-25T05:27:27.260Z"
updatedAt: "2019-10-18T03:00:39.373Z"
---
The public_data, private_data, read_list, and write_list in the previous chapter use the same context for a contract data store. Public_data can be viewed on the blockchain explorer. Specific examples of use are as follows:
[block:code]
{
  "codes": [
    {
      "code": "function init()\n    assert(chainhelper:is_owner(),'no auth')\n    \n    -- read data    \n    read_list = {public_data={rate=true,max_bet=true}}\n    chainhelper:read_chain()\n    \n    public_data.rate  = 98\n    public_data.max_bet = 1000000 \n    \n    -- write data\n    write_list = {public_data={rate=true,max_bet=true}}\n    chainhelper:write_chain()\nend",
      "language": "lua"
    }
  ]
}
[/block]
The data field should be defined via read_list each time you use it and then read the data via chainhelper:read_chain(). After the data changes, you should define the write_list and then write the data back to the chain via chainhelper:write_chain().