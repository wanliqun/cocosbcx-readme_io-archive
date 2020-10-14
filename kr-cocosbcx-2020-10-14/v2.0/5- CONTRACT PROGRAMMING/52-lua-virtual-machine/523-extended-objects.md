---
title: "5.2.3 Extended Objects"
slug: "523-extended-objects"
hidden: false
createdAt: "2019-06-25T04:06:59.704Z"
updatedAt: "2019-06-26T09:16:54.655Z"
---
##public_data

The public data zone is used to record contract rules and other public data for contract compilers to define the modification permission via the is_owner() assertion and the attributes. See the next section for specific use.


##private_data

The user data zone is used to record the data generated during the user's call to the contract. See the next section for specific use.


##read_list

The read list of contract data IO. The contract can be notified of the context to be loaded by writing a read_list.


##write_list

The write list of contract data IO. The contract can be notified by writing a write_list to the context that needs to be recorded.


##contract_base_info

This is used to store the basic information of the contract. The object is read-only. If the object is modified within the contract, it will not be recorded. Contract_base_info contains the following fields:
[block:parameters]
{
  "data": {
    "h-0": "Field",
    "h-1": "Description",
    "0-0": "name",
    "0-1": "contract name",
    "1-0": "id",
    "2-0": "owner",
    "1-1": "contract id",
    "2-1": "contract owner id",
    "3-0": "caller",
    "3-1": "current caller id",
    "4-0": "creation_date",
    "4-1": "contract creation time",
    "5-0": "contract_authority",
    "5-1": "contract authority signature"
  },
  "cols": 2,
  "rows": 6
}
[/block]