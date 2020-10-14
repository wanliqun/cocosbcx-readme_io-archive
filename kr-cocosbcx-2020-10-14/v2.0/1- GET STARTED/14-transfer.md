---
title: "1.4 Transfer"
slug: "14-transfer"
hidden: false
createdAt: "2019-06-24T07:02:32.246Z"
updatedAt: "2019-06-24T07:02:37.854Z"
---
[block:api-header]
{
  "title": "Log in to the command line wallet"
}
[/block]
1. Get the command line wallet executable file: cli_wallet and copy it to the scheduled directory
2. Go to the directory where the command line wallet is located. Run the following command to log in to the command line wallet
◼ Command format
--chain-id [chain ID] -s [witness node RPC address] -r [the address that the command line wallet's RPC service listens on]
[block:code]
{
  "codes": [
    {
      "code": "./cli_wallet --chain-id 81003974d328ff17b64076928ab87b24d7dffbc87df3d4cde89d2fa1877e4f6a -s ws://127.0.0.1:8070 -r 127.0.0.1:8099",
      "language": "shell"
    }
  ]
}
[/block]

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/1f62d9d-a3beeeb-2.2.1.2.png",
        "a3beeeb-2.2.1.2.png",
        804,
        341,
        "#0d0c0c"
      ]
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "Set password for the wallet"
}
[/block]
1. You need to set a password for your wallet when login for the first time
◼ Command format unlock [set password]
[block:code]
{
  "codes": [
    {
      "code": "set_password xxxx",
      "language": "shell"
    }
  ]
}
[/block]

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/c750e34-95066aa-2.2.2.1.png",
        "95066aa-2.2.2.1.png",
        802,
        80,
        "#050605"
      ]
    }
  ]
}
[/block]
2. After setting the password, you need to unlock the wallet.
◼ Command format unlock [password]
[block:code]
{
  "codes": [
    {
      "code": "unlock xxxx",
      "language": "shell"
    }
  ]
}
[/block]

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/a44d8a8-cb33d4a-2.2.2.2.png",
        "cb33d4a-2.2.2.2.png",
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
  "title": "Import the account to the wallet"
}
[/block]
1. Log in to unlock the wallet and execute the following command to import the user.
◼ Command format
import_key [username] [user private key]
◼ Private key
To view your private key, please find in section 1.3 Create an Account
[block:code]
{
  "codes": [
    {
      "code": "import_key official-account 5KaVpJa9G4oqA5WHcSGitauFRuzdHcPVEAaESaA",
      "language": "shell"
    }
  ]
}
[/block]

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/8f323e2-7224f30-2.2.3.3.png",
        "7224f30-2.2.3.3.png",
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
  "title": "Import assets to the wallet"
}
[/block]
1. Log in to unlock the wallet to import the assets
◼ Command format
import_balance  [username] [private key corresponding to the asset address] [true/false]
◼ Context
A new chain whose founding assets have not been exported
[block:code]
{
  "codes": [
    {
      "code": "import_balance official-account [\"5KAUeN3Yv51FzpLGGf4S1ByKpMqVFNzXTJK7euqc3L\"] true",
      "language": "shell"
    }
  ]
}
[/block]

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/8b7fafd-0000776-2.2.4.png",
        "0000776-2.2.4.png",
        803,
        139,
        "#090a07"
      ]
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "Transfer"
}
[/block]
◼ Command format
import_balance [transfer] [from to] [amount] [token asset type] [remarks] [broadcast (true/false)]
◼ Conditions
Login to unlock the wallet. There shall have enough balance in the account
◼ Example
transfer official-account test-account 100 COCOS "info" true
[block:code]
{
  "codes": [
    {
      "code": "transfer from to amount asset_symblo \"memo_info\" true",
      "language": "shell"
    }
  ]
}
[/block]

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/620e77c-ca4ade8-2.2.5.png",
        "ca4ade8-2.2.5.png",
        937,
        721,
        "#050505"
      ]
    }
  ]
}
[/block]