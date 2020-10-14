---
title: "2.2 cli_wallet"
slug: "22-cli_wallet"
hidden: false
createdAt: "2019-03-25T09:39:19.177Z"
updatedAt: "2019-06-06T05:44:38.392Z"
---
A wallet command line tool that supports interactions with the blockchain. The operation instructions are as follows:
[block:api-header]
{
  "title": "2.2.1 Login"
}
[/block]
1. Get the command line wallet executable file: cli_wallet and copy it to the scheduled directory
2. Go to the directory where the command line wallet is located. Run the following command to log in to the command line wallet
**Command format**
--chain-id [chain ID] -s [witness node RPC address] -r [the address that the command line wallet's RPC service listens on]
[block:code]
{
  "codes": [
    {
      "code": "./cli_wallet --chain-id 81003974d328ff17b64076928ab87b24d7dffbc87df3d4cde89d2fa1877e4f6a -s ws://127.0.0.1:8070 -r 127.0.0.1:8099",
      "language": "shell",
      "name": "Shell"
    }
  ]
}
[/block]
**Result: **
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/cda4ef2-2.2.1.2.png",
        "2.2.1.2.png",
        804,
        341,
        "#0d0c0c"
      ],
      "caption": ""
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "2.2.2 Set password for the wallet"
}
[/block]
1. You need to set a password for your wallet when login for the first time
**Command format**
unlock [set password]
[block:code]
{
  "codes": [
    {
      "code": "set_password xxxx",
      "language": "shell",
      "name": "Shell"
    }
  ]
}
[/block]
**Result: **
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/4cdbbbb-2.2.2.1.png",
        "2.2.2.1.png",
        802,
        80,
        "#050605"
      ],
      "caption": ""
    }
  ]
}
[/block]
2. After setting the password, you need to unlock the wallet.
**Command format **
unlock [set password]
[block:code]
{
  "codes": [
    {
      "code": "unlock xxxx",
      "language": "shell",
      "name": "Shell"
    }
  ]
}
[/block]
**Result: **
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/cb078c6-2.2.2.2.png",
        "2.2.2.2.png",
        804,
        82,
        "#040504"
      ]
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "2.2.3 Import the account to the wallet"
}
[/block]
1. Log in to unlock the wallet and execute the following command to import the user.
**Command format **
import_key [username] [user private key]
[block:code]
{
  "codes": [
    {
      "code": "import_key official-account 5KaVpJa9G4oqA5WHcSGitauFRuzdHcPVEAaESaA",
      "language": "shell",
      "name": "Shell"
    }
  ]
}
[/block]
**Result: **
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/9039bac-2.2.3.3.png",
        "2.2.3.3.png",
        803,
        159,
        "#0c0d06"
      ]
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "2.2.4 Import assets to the wallet"
}
[/block]
1. Log in to unlock the wallet to import the assets
**Command format **
import_balance [username] [private key corresponding to the asset address] [broadcast (true/false)]
**Context**
A new chain whose founding assets have not been exported
[block:code]
{
  "codes": [
    {
      "code": "import_balance official-account [\"5KAUeN3Yv51FzpLGGf4S1ByKpMqVFNzXTJK7euqc3L\"] true",
      "language": "shell",
      "name": "Shell"
    }
  ]
}
[/block]
**Result:**
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/096c7a8-2.2.4.png",
        "2.2.4.png",
        803,
        139,
        "#090a07"
      ],
      "sizing": "smart",
      "border": false
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "2.2.5 Transfer"
}
[/block]
**Command format**
import_balance [transfer] [from to] [amount] [token asset type] [remarks] [broadcast (true/false)]
**Conditions**
Login to unlock your wallet. There shall have enough balance in the account
**Example**
transfer official-account test-account 100 COCOS "info" true
[block:code]
{
  "codes": [
    {
      "code": "transfer from to amount asset_symblo \"memo_info\" true",
      "language": "shell",
      "name": "Shell"
    }
  ]
}
[/block]
**Result:**
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/16e8e31-2.2.5.png",
        "2.2.5.png",
        937,
        721,
        "#050505"
      ],
      "sizing": "smart"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "2.2.6 Register"
}
[/block]
**Command format **
register_account [username] [owner public key] [active public key] [registrar account name] [referrer account name] [cost percentage] [broadcast (true/false)]
**Conditions**
Login to unlock the wallet. The registrar should be a member who have enough balance in the account
**Example**
register_account test-account XXX6esv8d6u2eqzKyiQvCYJa6XK74c7BrmzUqL4Z7zfhtvB4db XXX6esv8d6u2eqzKyiQvCYJa6XK74c7BrmzUqL4Z7zfhtvB4db official-account official-account 0 true
[block:code]
{
  "codes": [
    {
      "code": "register_account name owner_key active_key registrar_account referrer_account referrer_percent true",
      "language": "shell",
      "name": "Shell"
    }
  ]
}
[/block]
**Result:**
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/45d2364-2.2.6.png",
        "2.2.6.png",
        798,
        1218,
        "#060606"
      ]
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "2.2.7 Upgrade the account for membership"
}
[/block]
**Conditions**
There is enough balance in the account
**Command format **
upgrade_account [username] [broadcast (true/false)]
**Example**
upgrade_account test-account true
**Note**
cli_wallet supports upgrading to a lifetime membership only, but not the annual membership.
[block:code]
{
  "codes": [
    {
      "code": "upgrade_account test-account true",
      "language": "shell",
      "name": "Shell"
    }
  ]
}
[/block]
**Result:**
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/38a7171-2.2.7.png",
        "2.2.7.png",
        802,
        525,
        "#050606"
      ]
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "2.2.8 Get information such as chain ID, current active witnesses and committee members"
}
[/block]
**Command format **
info
[block:code]
{
  "codes": [
    {
      "code": "info",
      "language": "shell",
      "name": "Shell"
    }
  ]
}
[/block]
**Result:**
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/3701e25-2.2.8.png",
        "2.2.8.png",
        801,
        743,
        "#040404"
      ]
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "2.2.9 Return information such as client version, compile time, boost version, openssl version, etc."
}
[/block]
**Command format **
about
[block:code]
{
  "codes": [
    {
      "code": "about",
      "language": "shell",
      "name": "Shell"
    }
  ]
}
[/block]
**Result:**
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/c22898e-2.2.9.png",
        "2.2.9.png",
        802,
        249,
        "#070707"
      ]
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "2.2.10 Get the information of a specified block"
}
[/block]
**Command format**
get_block [block height]
**Example**
get_block 10
[block:code]
{
  "codes": [
    {
      "code": "get_block block_num",
      "language": "shell",
      "name": "Shell"
    }
  ]
}
[/block]
**Result:**
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/d43e894-2.2.10.png",
        "2.2.10.png",
        803,
        249,
        "#0a0a0a"
      ]
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "2.2.11 Get the total number of accounts registered on-chain"
}
[/block]
**Command format **
get_account_count
[block:code]
{
  "codes": [
    {
      "code": "get_account_count",
      "language": "shell",
      "name": "Shell"
    }
  ]
}
[/block]
**Result:**
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/c7337d0-2.2.11.png",
        "2.2.11.png",
        800,
        59,
        "#040504"
      ]
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "2.2.12 List the accounts imported to the wallet"
}
[/block]
**Command format **
list_my_accounts
[block:code]
{
  "codes": [
    {
      "code": "list_my_accounts",
      "language": "shell",
      "name": "Shell"
    }
  ]
}
[/block]
**Result:**
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/c12c6f3-2.2.12.png",
        "2.2.12.png",
        801,
        1132,
        "#050505"
      ]
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "2.2.13 List the account balances"
}
[/block]
**Command format **
list_account_balances [account name]
**Example**
list_account_balances official-account
[block:code]
{
  "codes": [
    {
      "code": "list_account_balances official-account ",
      "language": "shell",
      "name": "Shell"
    }
  ]
}
[/block]
**Result:**
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/e5b10d7-2.2.13.png",
        "2.2.13.png",
        800,
        77,
        "#070707"
      ]
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "2.2.14 List the tokens on the chain"
}
[/block]
**Command format **
list_assets [lowerbound] [limit]
**Example**
list_assets “” 1
**Note**
The return results are sorted by the token symbols. The “lowerbound” parameter is the minimum limit, and the “limit” is the maximum number of returns, which is to return a maximum of “limit” tokens whose symbol is not less than the “lowerbound”.
[block:code]
{
  "codes": [
    {
      "code": "list_assets lowerbound limit",
      "language": "shell",
      "name": "Shell"
    }
  ]
}
[/block]
**Result:**
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/1cd17d4-2.2.14.png",
        "2.2.14.png",
        799,
        663,
        "#040404"
      ]
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "2.2.15 Get the account history"
}
[/block]
**Command format**
get_account_history [account name] [limit]
**Example**
get_account_history official-account 2
[block:code]
{
  "codes": [
    {
      "code": "get_account_history account limit",
      "language": "shell",
      "name": "Shell"
    }
  ]
}
[/block]
**Result:**
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/aebe3bf-2.2.15.png",
        "2.2.15.png",
        803,
        124,
        "#0b0c0b"
      ]
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "2.2.16 Get the static properties such as fees"
}
[/block]
**Command format**
get_global_properties
[block:code]
{
  "codes": [
    {
      "code": "get_global_properties",
      "language": "shell",
      "name": "Shell"
    }
  ]
}
[/block]
**Result:**
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/5c4a6db-2.2.16.1.png",
        "2.2.16.1.png",
        796,
        944,
        "#020202"
      ],
      "caption": "Part of the long results"
    }
  ]
}
[/block]

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/0f69190-2.2.16.2.png",
        "2.2.16.2.png",
        793,
        1228,
        "#050606"
      ]
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "2.2.17 Get the dynamic properties such as head block ID, time and next maintenance time"
}
[/block]
**Command format **
get_dynamic_global_properties
[block:code]
{
  "codes": [
    {
      "code": "get_dynamic_global_properties",
      "language": "shell",
      "name": "Shell"
    }
  ]
}
[/block]
**Result:**
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/1f1b7f3-2.2.17.png",
        "2.2.17.png",
        796,
        381,
        "#080808"
      ]
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "2.2.18 Get account information"
}
[/block]
**Command format **
get_account  [account name or ID]
**Example**
get_account official-account
[block:code]
{
  "codes": [
    {
      "code": "get_account_id account_name_or_id",
      "language": "shell",
      "name": "Shell"
    }
  ]
}
[/block]
**Result:**
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/579f8bb-2.2.18.png",
        "2.2.18.png",
        797,
        1142,
        "#050505"
      ]
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "2.2.19 Get the token asset information"
}
[/block]
**Command format **
get_asset  [asset name or ID]
**Example**
get_asset COCOS
[block:code]
{
  "codes": [
    {
      "code": "get_asset asset_name_or_id",
      "language": "shell",
      "name": "Shell"
    }
  ]
}
[/block]
**Result:**
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/0f8a2a0-2.2.19.png",
        "2.2.19.png",
        793,
        644,
        "#040404"
      ]
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "2.2.20 Get the account ID"
}
[/block]
**Command format **
get_account_id [account name]
**Example**
get_account_id official-account
[block:code]
{
  "codes": [
    {
      "code": "get_account_id account_name",
      "language": "shell",
      "name": "Shell"
    }
  ]
}
[/block]
**Result:**
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/87ccf1d-2.2.20.png",
        "2.2.20.png",
        795,
        63,
        "#050505"
      ]
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "2.2.21 Get information about token assets"
}
[/block]
**Command format **
get_asset [account name]
**Example**
get_asset COCOS
[block:code]
{
  "codes": [
    {
      "code": "get_asset asset_name",
      "language": "shell",
      "name": "Shell"
    }
  ]
}
[/block]
**Result:**
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/d9adb1e-2.2.21.png",
        "2.2.21.png",
        794,
        649,
        "#040404"
      ]
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "2.2.22 Get object"
}
[/block]
**Command format **
get_object [object ID]
**Example**
get_object 1.2.6
[block:code]
{
  "codes": [
    {
      "code": "get_object object_id",
      "language": "shell",
      "name": "Shell"
    }
  ]
}
[/block]
**Result:**
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/c4c2912-2.2.22.png",
        "2.2.22.png",
        795,
        1248,
        "#040505"
      ]
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "2.2.23 Get the private key"
}
[/block]
**Command format **
get_private_key [public key]
**Example**
get_private_key XXX6esv8d6u2eqzKyiQvCYJa6XK74c7BrmzUqL4Z3
**Note**
The private key must be saved in the wallet.
[block:code]
{
  "codes": [
    {
      "code": "get_private_key public_key",
      "language": "shell",
      "name": "Shell"
    }
  ]
}
[/block]
**Result:**
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/3c07c29-2.2.23.png",
        "2.2.23.png",
        804,
        98,
        "#0e0f0e"
      ]
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "2.2.24 Lock the wallet"
}
[/block]
**Command format **
lock
[block:code]
{
  "codes": [
    {
      "code": "lock",
      "language": "shell",
      "name": "Shell"
    }
  ]
}
[/block]
**Result:**
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/e762508-2.2.24.png",
        "2.2.24.png",
        799,
        64,
        "#020202"
      ]
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "2.2.25 Return a set of secure brain key, public key, and private key"
}
[/block]
**Command format **
suggest_brain_key
[block:code]
{
  "codes": [
    {
      "code": "suggest_brain_key",
      "language": "shell",
      "name": "Shell"
    }
  ]
}
[/block]
**Result:**
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/c5c3cfe-2.2.25.png",
        "2.2.25.png",
        802,
        163,
        "#0c0d0d"
      ]
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "2.2.26 Register to be a committee member"
}
[/block]
**Command format **
create_committee_member [account name] [url address] [broadcast (true/false)]
**Example**
create_committee_member official-account "http://my-web" true
**Note**
The user become a candidate committee member after registration. He will be the official member only by winning the vote.
[block:code]
{
  "codes": [
    {
      "code": "create_committee_member account \"url\" true",
      "language": "shell",
      "name": "Shell"
    }
  ]
}
[/block]
**Result:**
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/9a05f1c-2.2.26.png",
        "2.2.26.png",
        797,
        495,
        "#060706"
      ]
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "2.2.27 Register to be a witness"
}
[/block]
**Command format **
create_witness [account name] [url address] [broadcast (true/false)]
**Example**
create_witness official-account "http://my-web" true
**Note**
The user become a candidate witness after application. He will be the official witness only by winning the vote.
[block:code]
{
  "codes": [
    {
      "code": "create_witness account \"url\" true",
      "language": "shell",
      "name": "Shell"
    }
  ]
}
[/block]
**Result:**
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/505a3c8-2.2.27.png",
        "2.2.27.png",
        802,
        539,
        "#060706"
      ]
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "2.2.28 List the witnesses"
}
[/block]
**Command format **
list_witnesses [lowerbound] [limit]
**Example**
list_witnesses "" 100
**Note**
Returned results are sorted by the witness account name. The “lowerbound” parameter is the minimum limit, and the “limit” is the maximum number of returns.
[block:code]
{
  "codes": [
    {
      "code": "list_witnesses lowerbound limit",
      "language": "shell",
      "name": "Shell"
    }
  ]
}
[/block]
**Result:**
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/8c49eb3-2.2.28.png",
        "2.2.28.png",
        795,
        200,
        "#020303"
      ]
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "2.2.29 List the committee members"
}
[/block]
**Command format **
list_committee_members [lowerbound] [limit]
**Example**
list_committee_members "" 100
**Note**
Returned results are sorted by the committee member account name. The “lowerbound” parameter is the minimum limit, and the “limit” is the maximum number of returns.
[block:code]
{
  "codes": [
    {
      "code": "list_committee_members lowerbound limit",
      "language": "shell",
      "name": "Shell"
    }
  ]
}
[/block]
**Result:**
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/5d8b01e-2.2.29.png",
        "2.2.29.png",
        802,
        203,
        "#030303"
      ]
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "2.2.30 Get the witness information"
}
[/block]
**Command format **
get_witness [witness name or ID]
**Example**
get_witness Witness-0
[block:code]
{
  "codes": [
    {
      "code": "get_witness witness_name_or_id",
      "language": "shell",
      "name": "Shell"
    }
  ]
}
[/block]
**Result:**
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/c162d5b-2.2.30.png",
        "2.2.30.png",
        802,
        522,
        "#060606"
      ]
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "2.2.31 Get the committee member"
}
[/block]
*Command format **
get_committee_member [committee member name or ID]
**Example**
get_committee_member Witness-0
[block:code]
{
  "codes": [
    {
      "code": "get_committee_member committee_member_name_or_id",
      "language": "shell",
      "name": "Shell"
    }
  ]
}
[/block]
**Result:**
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/8cb9fd9-2.2.31.png",
        "2.2.31.png",
        801,
        180,
        "#060606"
      ]
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "2.2.32 Create a contract"
}
[/block]
**Command format **
create_contract [contract owner] [contract name] [contract authority (publicKey in a pair of public and private keys)] [data] [broadcast (true/false)]
**Example**
create_contract 1.2.17 contract.helloworld "COCOS1DE213......" "function hello() chainhelper:log('Hello World!') end" true
[block:code]
{
  "codes": [
    {
      "code": "create_contract owner name contract_authority data broadcast",
      "language": "shell",
      "name": "Shell"
    }
  ]
}
[/block]
**Result:**
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/2ee3d29-2.2.32.png",
        "2.2.32.png",
        805,
        665,
        "#080908"
      ]
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "2.2.33 Update the contract"
}
[/block]
**Command format **
revise_contract [contract updater username] [contract name or ID] [data] [broadcast (broadcast (true/false))]
**Example**
revise_contract 1.2.17 contract.helloworld "function hello() chainhelper:log('Hello World!') chainhelper:log(date('%Y-%m-%dT%H:%M:%S', chainhelper:time())) end" true
[block:code]
{
  "codes": [
    {
      "code": "revise_contract owner name contract_authority data broadcast",
      "language": "shell",
      "name": "Shell"
    }
  ]
}
[/block]
**Result:**
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/45637c9-2.2.33.png",
        "2.2.33.png",
        804,
        634,
        "#080808"
      ]
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "2.2.34 Call the contract"
}
[/block]
**Command format **
call_contract_function [username or ID] [contract name or contract ID] [function name] [value list] [broadcast (true/false)]
**Example**
call_contract_function 1.2.17 contract.helloworld [] true
[block:code]
{
  "codes": [
    {
      "code": "call_contract_function account_id_or_name contract_id_or_name function_name value_list broadcast",
      "language": "shell",
      "name": "Shell"
    }
  ]
}
[/block]
**Result:**
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/36057ef-2.2.34.png",
        "2.2.34.png",
        804,
        579,
        "#060606"
      ]
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "2.2.35 List the account bounty amount"
}
[/block]
**Command format **
get_vesting_balances [username]
**Example**
get_vesting_balances official-account
[block:code]
{
  "codes": [
    {
      "code": "get_vesting_balances account_name",
      "language": "shell",
      "name": "Shell"
    }
  ]
}
[/block]
**Result:**
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/66fefac-2.2.35.png",
        "2.2.35.png",
        797,
        484,
        "#050505"
      ]
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "2.2.36 Get the bounty (for witnesses only)"
}
[/block]
**Command format **
withdraw_vesting [witness name] [amount] [asset symbol] [broadcast (true/false)]
**Example**
withdraw_vesting cocos-witness-0 10 XXX true 

withdraw_vesting(string witness_name, string amount, string asset_symbol, bool broadcast)
[block:code]
{
  "codes": [
    {
      "code": "withdraw_vesting witness_name amount asset_symbol true",
      "language": "shell",
      "name": "Shell"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "2.2.37 Vote for witnesses"
}
[/block]
**Command format **
vote_for_witness [username] [witness username] [agree or not] [broadcast (true/false)]
**Example**
vote_for_witness official-account cocos-witness-0 true true
**Prerequisite steps**
1. Go to the directory where the command line wallet is located, and run the command ./cli_wallet-sws://127.0.0.1:8070-r127.0.0.1:8099 to log in to the wallet.
2. Execute the command unlock xxxx to unlock the wallet
3. Execute the import_key official-account 5KaVpJa9G4oqA5WHcSGitauFRuzdHcPVEAaESaA7jG8s to import user 
4. Execute the command import_balance official-account ["5KAUeN3Yv51FzpLGGf4S1ByKpMqVFNzXTyKpeuqc3"] true to import assets for users
5. Execute the command vote_for_witness official-account cocos-witness-0 true true, the official-account will vote for the witness account cocos-witness-0
6. Follow step 4 to vote for other witnesses
[block:code]
{
  "codes": [
    {
      "code": "vote_for_witness official-account cocos-witness-0 true true",
      "language": "shell",
      "name": "Shell"
    }
  ]
}
[/block]
**Result:**
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/3eb8d64-2.2.37.png",
        "2.2.37.png",
        801,
        718,
        "#050605"
      ]
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "2.2.38 Vote for committee members"
}
[/block]
**Command format **
vote_for_committee_member [username] [witness username] [agree or not] [broadcast (true/false)]
**Example**
vote_for_committee_member official-account cocos-witness-0 true true
**Prerequisite steps**
1. Go to the directory where the command line wallet is located, and run the command ./cli_wallet-sws://127.0.0.1:8070-r127.0.0.1:8099 to log in to the command line wallet
2. Execute the command unlock xxxx to unlock the wallet
3. Execute the import_key official-account 5KaVpJa9G4oqA5WHcSGitauFRuzdHcPVEAaESaA7jG8s to import user
4. Execute the command import_balance official-account "5KAUeN3Yv51FzpLGGf4S1ByKpMqVFNzXTJK7euq"] true to import assets for users
5. Execute the command vote_for_committee_member official-account Witness-0 true true, the official-account will vote for the witness account cocos-witness-0
6. Follow step 4 to vote for other witnesses
[block:code]
{
  "codes": [
    {
      "code": "vote_for_committee_member official-account cocos-witness-0 true true",
      "language": "shell",
      "name": "Shell"
    }
  ]
}
[/block]
**Result:**
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/55f232b-2.2.38.png",
        "2.2.38.png",
        802,
        723,
        "#050606"
      ]
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "2.2.39 Committee members propose to change the fee"
}
[/block]
**Command format **
1. propose_fee_change [username] [deadline] [content] [broadcast (true/false)]
2. approve_proposal [username] [proposal ID] [proposer username] [broadcast (true/false)]
**Example**
1. propose_fee_change Witness-0 "2018-07-24T06:55:40" {"transfer" : {"fee": 244000, "price_per_kbyte": 100000}} true
2. approve_proposal Witness-0 1.10.0 {"active_approvals_to_add" : ["Witness-0"]} true
**Prerequisite steps**
1. Go to the directory where the command line wallet is located, and run the command ./cli_wallet-sws://127.0.0.1:8070-r127.0.0.1:8099 to log in to the command line wallet
2. Execute the command unlock xxxx to unlock the wallet
3. Execute the import_key Witness-0 5KaVpJa9G4oqA5WHcSGitauFRuzdHcPVEAaE  to import user
4. Execute the command propose_fee_change Witness-0 "2018-07-24T06:55:40" {"transfer" : {"fee": 244000, "price_per_kbyte": 100000}} true to propose to change the transfer fee
5. Execute the command transfer official-account committee-account 100 XXX "" true to transfer to the user committee-account (the user is the proposed executor)
6. Execute the command approve_proposal Witness-0 1.10.0 {"active_approvals_to_add" : ["Witness-0"]} true to approve the proposal (The executor of the proposal is the committee-account, and each committee member holds a certain active authority weight of the account according to the number of votes obtained by the committee member. Therefore, the proposal can be executed when the weight of the committee members who approve the proposal exceeds the threshold of the committee-account.)
7. When the proposal is about to be expired, the system will automatically determine whether the proposal can be executed. If so, the proposal will be executed, and then the fee will be updated after the next maintenance. 
[block:code]
{
  "codes": [
    {
      "code": "propose_fee_change Witness-0 \"2018-07-24T06:55:40\" {\"transfer\" : {\"fee\": 244000, \"price_per_kbyte\": 100000}} true",
      "language": "shell",
      "name": "Shell"
    }
  ]
}
[/block]

[block:code]
{
  "codes": [
    {
      "code": "approve_proposal Witness-0 1.10.0 {\"active_approvals_to_add\" : [\"Witness-0\"]} true",
      "language": "shell"
    }
  ]
}
[/block]
Result:
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/f14ea5b-2.2.39.1.png",
        "2.2.39.1.png",
        799,
        918,
        "#040404"
      ],
      "caption": "Part of the long results"
    }
  ]
}
[/block]

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/3a00cea-2.2.39.2.png",
        "2.2.39.2.png",
        800,
        956,
        "#070707"
      ]
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "2.2.40 Committee members propose to change the global parameter of the chain"
}
[/block]
◼ Command format
propose_parameter_change [username] [deadline] [content] [broadcast (true/false)]
◼ Example
propose_parameter_change Witness-0 "2018-07-24T06:55:40" {"committee_proposal_review_period": 300} true
◼ Prerequisite steps
1. Go to the directory where the command line wallet is located, and run the command ./cli_wallet-sws://127.0.0.1:8070-r127.0.0.1:8099 to log in to the command line wallet
2. Execute the command unlock xxxx to unlock the wallet
3. Execute the command import_key Witness-0 5KaVpJa9G4oqA5WHcSGitauFRuzdHcPVEAaE to import committee member user
4. Execute the command prepare_parameter_change Witness-0 "2018-07-24T06:55:40" {"committee_proposal_review_period": 300} true to propose to change the committee proposed review period of the global parameter of the chain
5. Execute the command transfer official-account committee-account 100 XXX "" true to transfer to the committee-account (the user is the proposed executor)
6. Execute the command approve_proposal Witness-0 1.10.0 {"active_approvals_to_add" : ["Witness-0"]} true to approve the proposal (The executor of the proposal is committee-account, and each committee member holds a certain active authority weight of the account according to the number of votes obtained by the committee member. Therefore, the proposal can be executed when the weight of the committee members who approve the proposal exceeds the threshold of the committee-account.)
7. When the proposal is about to be expired, the system will automatically determine whether the proposal can be executed. If so, the proposal will be executed, and then the fee will be updated after the next maintenance.
◼ Configurable parameter
"block_interval"	
"maintenance_interval"	
"maintenance_skip_slots"
"committee_proposal_review_period"	
"maximum_transaction_size"	
"maximum_block_size"	
"maximum_time_until_expiration"	
"maximum_proposal_lifetime"	
"maximum_asset_whitelist_authorities"	
"maximum_asset_feed_publishers"
"maximum_witness_count"
"maximum_committee_count"
"maximum_authority_membership"
"reserve_percent_of_fee"
"network_percent_of_fee"
"lifetime_referrer_percent_of_fee"	
"cashback_vesting_period_seconds"	
"cashback_vesting_threshold"	
"count_non_member_votes"	
"allow_non_member_whitelists"	
"witness_pay_per_block"	
"worker_budget_per_day"	
"max_predicate_opcode"	
"fee_liquidation_threshold"	
"accounts_per_fee_scale"	
"account_fee_scale_bitshifts"	
"max_authority_depth"	One account can authorize another account. This parameter can be configured to be effective up to several layers downwards.
[block:code]
{
  "codes": [
    {
      "code": "propose_parameter_change Witness-0 \"2018-07-24T06:55:40\" {\"committee_proposal_review_period\": 300} true",
      "language": "shell",
      "name": "Shell"
    }
  ]
}
[/block]
Result:
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/8446cfe-2.2.40.2.png",
        "2.2.40.2.png",
        800,
        984,
        "#070808"
      ]
    }
  ]
}
[/block]