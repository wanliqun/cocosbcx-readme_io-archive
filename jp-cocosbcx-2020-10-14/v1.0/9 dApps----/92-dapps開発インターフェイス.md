---
title: "9.2 dApps開発インターフェイス"
slug: "92-dapps開発インターフェイス"
hidden: false
createdAt: "2019-10-03T05:30:25.067Z"
updatedAt: "2019-10-03T08:37:31.917Z"
---
[block:api-header]
{
  "title": "アカウント名を入手"
}
[/block]
window.BcxWeb.account_name
[block:api-header]
{
  "title": "振込手数料を入手"
}
[/block]
**インタフェース名**
transferAsset

**リクエストパラメーター** 
[block:parameters]
{
  "data": {
    "h-0": "Parameter",
    "h-1": "Type",
    "h-2": "Must or Not",
    "h-3": "Description",
    "0-0": "fromAccount",
    "0-1": "Sting",
    "0-2": "M",
    "0-3": "Sender",
    "1-0": "toAccount",
    "1-1": "Sting",
    "1-2": "M",
    "1-3": "Receiver",
    "2-0": "amount",
    "2-1": "Sting",
    "2-2": "M",
    "2-3": "Amount",
    "3-0": "assetId",
    "3-1": "Sting",
    "3-2": "M",
    "3-3": "Assets ID（Eg. XXX) or Token Symbol(Eg. COCOS)",
    "4-0": "memo",
    "4-1": "Sting",
    "4-2": "N",
    "4-3": "Memo",
    "5-0": "feeAssetId",
    "5-1": "Sting",
    "5-2": "M",
    "5-3": "Token asset symbol for fee payment",
    "6-0": "isPropose",
    "6-1": "boolean",
    "6-2": "M",
    "6-3": "Propose or not",
    "7-0": "onlyGetFee",
    "7-1": "boolean",
    "7-2": "M",
    "7-3": "true:Only get operation fee;\nfalse:Make a transfer"
  },
  "cols": 4,
  "rows": 8
}
[/block]
**レスポンスデータのフォーマット例** 
振込手数料ののみリターンする場合（onlyGetFee = true）：
[block:code]
{
  "codes": [
    {
      "code": "{\n    \"code\":1,\n    \"data\":{\n        \"fee_amount\":2.08984,\n        \"fee_symbol\":\"COCOS\"\n    }\n}",
      "language": "javascript"
    }
  ]
}
[/block]
振込操作データをリターンする場合（onlyGetFee = false）（モバイル端末はtrx_id fieldのみ提供します）
[block:code]
{
  "codes": [
    {
      "code": "{\n    \"code\":1,\n    \"data\":[\n        {\n            \"real_running_time\":179\n        }\n    ],\n    \"trx_data\":{\n        \"trx_id\":\"bfa20c68506dd830fe3217427835d5c186badc04839eab7ad2e923773fd8671d\",\n        \"block_num\":5226795\n    }\n}",
      "language": "javascript"
    }
  ]
}
[/block]
残高不足
[block:code]
{
  "codes": [
    {
      "code": "{\n    \"code\":0,\n    \"message\":\"Assert Exception: from != to: \",\n    \"error\":{\n        \"code\":56,\n        \"message\":\"Assert Exception: from != to: \",\n        \"messageDetail\":\"Assert Exception: from != to: \ndigest ec9e01d053bb55a3bd21c548f8ff4c27e7a077152ddd1b1ab65fa88b4d518fe4 transaction 660b90f837c620cbbf5c0100400d030000000000008801880140420f000000000000000000 {\"ref_block_num\":2918,\"ref_block_prefix\":3325556880,\"expiration\":\"2019-04-24T02:34:08\",\"operations\":[[0,{\"fee\":{\"amount\":\"200000\",\"asset_id\":\"1.3.0\"},\"from\":\"1.2.136\",\"to\":\"1.2.136\",\"amount\":{\"amount\":\"1000000\",\"asset_id\":\"1.3.0\"},\"extensions\":[]}]],\"extensions\":[],\"signatures\":[\"2002777d6199243d4dca821512fec827948ee840aca03cd14480e75b581c7456ad5e2a5a926320a9280d78631663659beffafb144629aa8ee3d8cb51d312eef81d\"]}\"\n    }\n}",
      "language": "javascript"
    }
  ]
}
[/block]
ログインしていない
[block:code]
{
  "codes": [
    {
      "code": "{\n    \"code\":-11,\n    \"message\":\"Please login first\"\n}\n\nmemoの暗号化が失敗：\nJavaScript\n{\n    \"code\":118,\n    \"message\":\"Encrypt memo failed\",\n    \"error\":{\n        \"message\":\"Encrypt memo failed\"\n    }\n}",
      "language": "javascript"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "コントラクト関数のコール"
}
[/block]
**インタフェース名**
callContractFunction
**
リクエストパラメーター** 
[block:parameters]
{
  "data": {
    "h-0": "Parameter",
    "h-1": "Type",
    "h-2": "Must or Not",
    "h-3": "Description",
    "0-0": "nameOrId",
    "0-1": "Sting",
    "0-2": "M",
    "0-3": "Contract name or ID",
    "1-0": "functionName",
    "1-1": "Sting",
    "1-2": "M",
    "2-2": "M",
    "3-2": "N",
    "4-2": "M",
    "1-3": "Target function name",
    "2-0": "valueList(array)",
    "2-1": "array",
    "2-3": "Parameter list",
    "3-0": "runtime",
    "3-1": "ong",
    "3-3": "runTime(in ms)",
    "4-0": "onlyGetFee",
    "4-1": "boolean",
    "4-3": "rue:Only get operation fee;\nfalse:Make a transfer"
  },
  "cols": 4,
  "rows": 5
}
[/block]
**リスポンスデータのフォーマット例** 
操作手数料のデータのみリターンする場合（onlyGetFee = true）：
[block:code]
{
  "codes": [
    {
      "code": "{\n    \"code\":1,\n    \"data\":{\n        \"fee_amount\":2.08984,\n        \"fee_symbol\":\"COCOS\"\n    }\n}",
      "language": "javascript"
    }
  ]
}
[/block]
操作データをリターンする場合（onlyGetFee = false）（モバイル端末はtrx_id fieldのみ提供します）
[block:code]
{
  "codes": [
    {
      "code": "{\n    \"code\":1,\n    \"data\":[\n        {\n            \"real_running_time\":179\n        }\n    ],\n    \"trx_data\":{\n        \"trx_id\":\"bfa20c68506dd830fe3217427835d5c186badc04839eab7ad2e923773fd8671d\",\n        \"block_num\":5226795\n    }\n}",
      "language": "javascript"
    }
  ]
}
[/block]
署名失敗
[block:code]
{
  "codes": [
    {
      "code": "{\n    \"code\":0,\n    \"message\":\"Transaction was not signed. Do you have a private key? [no_signers]\",\n    \"error\":{\n        \"message\":\"Transaction was not signed. Do you have a private key? [no_signers]\"\n    }\n}",
      "language": "javascript"
    }
  ]
}
[/block]
残高不足
[block:code]
{
  "codes": [
    {
      "code": "{\n    \"code\":0,\n    \"message\":\"Transaction was not signed. Do you have a private key? [no_signers]\",\n    \"error\":{\n        \"message\":\"Transaction was not signed. Do you have a private key? [no_signers]\"\n    }\n}",
      "language": "javascript"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "コントラクト情報を入手（モバイル端末に対応していない）"
}
[/block]
**インタフェース名**
queryContract

**リクエストパラメーター** 
[block:parameters]
{
  "data": {
    "h-0": "Parameter",
    "h-1": "Type",
    "h-2": "Must or Not",
    "h-3": "Description",
    "0-0": "nameOrId",
    "0-1": "Sting",
    "0-2": "M",
    "0-3": "Contract name or ID"
  },
  "cols": 4,
  "rows": 1
}
[/block]
**リスポンスデータのフォーマット例** 
[block:code]
{
  "codes": [
    {
      "code": "{\n    \"code\":1,\n    \"data\":{\n        \"check_contract_authority\":false,\n        \"abi_actions\":[\n            {\n                \"name\":\"add_num\",\n                \"arglist\":[\n                    \"num1\",\n                    \"num2\"\n                ]\n            },\n            {\n                \"name\":\"init\",\n                \"arglist\":[\n\n                ]\n            },\n            {\n                \"name\":\"log_pubdata\",\n                \"arglist\":[\n\n                ]\n            }\n        ],\n        \"contract_authority\":\"COCOS5skVs12sjHtEvsKEpMfwiSvjkrubPKYKhBjKtX4bFBki4xiDvJ\",\n        \"contract_data\":{\n            \"num\":20\n        },\n        \"contract_data_type\":[\n            {\n                \"key_type\":\"string\",\n                \"key\":\"num\",\n                \"value_type\":\"init\",\n                \"value\":20\n            }\n        ],\n        \"create_date\":\"2019/03/27 20:00:00\",\n        \"current_version\":\"4853897d105a2f3c020bc0ec47ba12e33a2c3ccf24e68f93b922bf8917f61355\",\n        \"id\":\"1.16.15\",\n        \"lua_code\":\"-- English \n-- The digit that Cocos currency precise to, available for currency information query by chain\n-- rate parameter error updates\n-- COCOS_ACCURACY = 100000 \nfunction init() \nassert(chainhelper:is_owner(),'no auth')\nread_list = {public_data={num=true}} \nchainhelper:read_chain() \npublic_data.num = 0 \nwrite_list = {public_data={num=true}} \nchainhelper:write_chain() \nend \n\nfunction add_num(num1,num2) \nread_list = {public_data={num=true}}\nchainhelper:read_chain()\n\npub_num = tonumber(public_data.num) \nchainhelper:log(string.format(\"num_add the pub_num value is:%d\",pub_num))\n\nnum1 = tonumber(num1) \nadd_num = num1 + num2 \n\nchainhelper:log(string.format(\"num_add the add_num value is:%d\",add_num))\n\n-- Enter the added value\npublic_data.num = add_num \nwrite_list = {public_data={num=true}} \nchainhelper:write_chain() \nend\n\n-- Output the run-able number\nfunction log_pubdata() \nread_list = {public_data={num=true}}\nchainhelper:read_chain() \n\npub_num = tonumber(public_data.num) \nchainhelper:log(string.format(\"log_pubdata the public_data value is:%d\",pub_num))\n\nwrite_list = {public_data={num=true}} \nchainhelper:write_chain() \nend\",\n        \"contract_name\":\"contract.syling\",\n        \"owner_account_name\":\"syling\"\n    }\n}",
      "language": "javascript"
    }
  ]
}
[/block]
コントラクトが存在していない
[block:code]
{
  "codes": [
    {
      "code": "{\n    \"code\":145,\n    \"message\":\"The contract (contract.sylin) does not exist\",\n    \"error\":{\n        \"code\":15,\n        \"message\":\"Assert Exception: contract_itr != con_index.end(): The contract (contract.sylin) does not exist\"\n    }\n}",
      "language": "javascript"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "アカウント内のコントラクト情報を入手（モバイル端末に対応していない）"
}
[/block]
**インタフェース名**
queryAccountContractData

**リクエストパラメーター**
[block:parameters]
{
  "data": {
    "h-0": "Parameter",
    "h-1": "Type",
    "h-2": "Must or Not",
    "h-3": "Description",
    "0-0": "account",
    "0-1": "Sting",
    "0-2": "M",
    "0-3": "Account name or ID",
    "1-0": "contractNameOrId",
    "1-1": "Sting",
    "1-2": "M",
    "1-3": "Contract name or ID"
  },
  "cols": 4,
  "rows": 2
}
[/block]
**レスポンスデータのフォーマット例** 
[block:code]
{
  "codes": [
    {
      "code": "{\n    \"code\":0,\n    \"message\":\"Transaction was not signed. Do you have a private key? [no_signers]\",\n    \"error\":{\n        \"message\":\"Transaction was not signed. Do you have a private key? [no_signers]\"\n    }\n}",
      "language": "javascript"
    }
  ]
}
[/block]
アカウントが存在していない
[block:code]
{
  "codes": [
    {
      "code": "{\n    \"code\":104,\n    \"message\":\"sylingjj Account not found\",\n    \"error\":{\n        \"message\":\"sylingjj Account not found\"\n    }\n}",
      "language": "javascript"
    }
  ]
}
[/block]
コントラクトが存在していない
[block:code]
{
  "codes": [
    {
      "code": "{\n    \"code\":145,\n    \"message\":\"The contract (contract.sylingkk) does not exist\",\n    \"error\":{\n        \"code\":39,\n        \"message\":\"Assert Exception: contract_itr != con_index.end(): The contract (contract.sylingkk) does not exist\"\n    }\n}",
      "language": "javascript"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "アカウント情報を入手"
}
[/block]
**インタフェース名**
queryAccountInfo

**リクエストパラメーター**
[block:parameters]
{
  "data": {
    "h-0": "Parameter",
    "h-1": "Type",
    "h-2": "Must or Not",
    "h-3": "Description",
    "0-0": "account",
    "0-1": "sting",
    "0-2": "M",
    "0-3": "Account name or ID"
  },
  "cols": 4,
  "rows": 1
}
[/block]
**レスポンスデータのフォーマット例** 
[block:code]
{
  "codes": [
    {
      "code": "{\n    \"code\":1,\n    \"data\":{\n        \"account\":{\n            \"id\":\"1.2.139\",\n            \"membership_expiration_date\":\"1970-01-01T00:00:00\",\n            \"registrar\":\"1.2.17\",\n            \"referrer\":\"1.2.17\",\n            \"lifetime_referrer\":\"1.2.17\",\n            \"network_fee_percentage\":2000,\n            \"lifetime_referrer_fee_percentage\":3000,\n            \"referrer_rewards_percentage\":5000,\n            \"name\":\"gnkhandsome2\",\n            \"owner\":{\n                \"weight_threshold\":1,\n                \"account_auths\":[\n\n                ],\n                \"key_auths\":[\n                    [\n                        \"COCOS5n9n3eT83AsYnU7smuTQw55iGMkaucetnzmtLoFWbF2cr7YXzd\",\n                        1\n                    ]\n                ],\n                \"address_auths\":[\n\n                ]\n            },\n            \"active\":{\n                \"weight_threshold\":1,\n                \"account_auths\":[\n\n                ],\n                \"key_auths\":[\n                    [\n                        \"COCOS61qJmvPif4seDKUjEkoL9qUP9cSvwBvgme5djcK8thuUS6o4Mg\",\n                        1\n                    ]\n                ],\n                \"address_auths\":[\n\n                ]\n            },\n            \"options\":{\n                \"memo_key\":\"COCOS61qJmvPif4seDKUjEkoL9qUP9cSvwBvgme5djcK8thuUS6o4Mg\",\n                \"voting_account\":\"1.2.5\",\n                \"num_witness\":0,\n                \"num_committee\":0,\n                \"votes\":[\n\n                ],\n                \"extensions\":[\n\n                ]\n            },\n            \"statistics\":\"2.6.139\",\n            \"contract_asset_locked\":{\n                \"locked_total\":[\n\n                ],\n                \"lock_details\":[\n\n                ]\n            },\n            \"whitelisting_accounts\":[\n\n            ],\n            \"blacklisting_accounts\":[\n\n            ],\n            \"whitelisted_accounts\":[\n\n            ],\n            \"blacklisted_accounts\":[\n\n            ],\n            \"owner_special_authority\":[\n                0,\n                {\n\n                }\n            ],\n            \"active_special_authority\":[\n                0,\n                {\n\n                }\n            ],\n            \"top_n_control_flags\":0\n        },\n        \"statistics\":{\n            \"id\":\"2.6.139\",\n            \"owner\":\"1.2.139\",\n            \"most_recent_op\":\"2.9.2850\",\n            \"total_ops\":37,\n            \"removed_ops\":0,\n            \"total_core_in_orders\":0,\n            \"lifetime_fees_paid\":2881770,\n            \"pending_fees\":0,\n            \"pending_vested_fees\":0\n        },\n        \"registrar_name\":\"official-account\",\n        \"referrer_name\":\"official-account\",\n        \"lifetime_referrer_name\":\"official-account\",\n        \"votes\":[\n\n        ],\n        \"balances\":[\n            {\n                \"id\":\"2.5.131\",\n                \"owner\":\"1.2.139\",\n                \"asset_type\":\"1.3.0\",\n                \"balance\":453190\n            },\n            {\n                \"id\":\"2.5.142\",\n                \"owner\":\"1.2.139\",\n                \"asset_type\":\"1.3.2\",\n                \"balance\":6296404\n            }\n        ],\n        \"vesting_balances\":[\n\n        ],\n        \"limit_orders\":[\n\n        ],\n        \"call_orders\":[\n\n        ],\n        \"settle_orders\":[\n\n        ],\n        \"proposals\":[\n\n        ],\n        \"assets\":[\n\n        ],\n        \"withdraws\":[\n\n        ]\n    }\n}",
      "language": "javascript"
    }
  ]
}
[/block]
アカウントが存在していない
[block:code]
{
  "codes": [
    {
      "code": "{\n    \"code\":104,\n    \"message\":\"1.2.666 Account not found\",\n    \"error\":{\n        \"message\":\"1.2.666 Account not found\"\n    }\n}",
      "language": "javascript"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "ログイン中のアカウント情報を入手"
}
[/block]
**インタフェース名**
getAccountInfo

**レスポンスデータのフォーマット例（モバイル端末では「lock」、「mode」fieldがない）**
[block:code]
{
  "codes": [
    {
      "code": "{\n    \"account_id\":\"1.2.136\",\n    \"locked\":false,\n    \"account_name\":\"gnkhandsome1\",\n    \"mode\":\"account\"\n}",
      "language": "javascript"
    }
  ]
}
[/block]
アカウントが存在していない
[block:code]
{
  "codes": [
    {
      "code": "{\n    \"account_id\":\"\",\n    \"locked\":true,\n    \"account_name\":\"\",\n    \"mode\":\"account\"\n}",
      "language": "javascript"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "NHアセットの詳細を入手"
}
[/block]
**インタフェース名**
queryNHAssets

**リクエストパラメーター**
[block:parameters]
{
  "data": {
    "h-0": "Parameter",
    "h-1": "Type",
    "h-2": "Must or Not",
    "h-3": "Description",
    "0-0": "NHAssetIds(array)",
    "0-1": "array",
    "0-2": "M",
    "0-3": "NH Assets hash or ID"
  },
  "cols": 4,
  "rows": 1
}
[/block]
レスポンスデータのフォーマット
[block:code]
{
  "codes": [
    {
      "code": "{\n    \"code\":1,\n    \"data\":[\n        {\n            \"id\":\"4.2.11\",\n            \"nh_hash\":\"866c7e61648c1cc7d6df2b3e0c532c4d8e470d152c0f88c6a2dda591f27f8f07\",\n            \"nh_asset_creator\":\"1.2.38\",\n            \"nh_asset_owner\":\"1.2.38\",\n            \"nh_asset_active\":\"1.2.38\",\n            \"authority_account\":\"1.2.38\",\n            \"asset_qualifier\":\"COCOS\",\n            \"world_view\":\"joy\",\n            \"base_describe\":{\n\n            },\n            \"parent\":[\n\n            ],\n            \"child\":[\n\n            ],\n            \"describe_with_contract\":{\n\n            },\n            \"create_time\":\"2019/03/06 16:03:05\",\n            \"limit_list\":[\n\n            ],\n            \"limit_type\":\"black_list\",\n            \"nh_asset_creator_name\":\"reedhong\",\n            \"nh_asset_owner_name\":\"reedhong\",\n            \"nh_asset_active_name\":\"reedhong\",\n            \"authority_account_name\":\"reedhong\"\n        }\n    ]\n}",
      "language": "javascript"
    }
  ]
}
[/block]
NHアセットが存在していない
[block:code]
{
  "codes": [
    {
      "code": "{\n    \"code\":147,\n    \"message\":\"4.2.4141 NHAsset do not exist\"\n}",
      "language": "javascript"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "アカウント内のNHアセットの注文履歴を入手"
}
[/block]
**インタフェース名**
queryAccountNHAssetsOrders

**リクエストパラメーター**
[block:parameters]
{
  "data": {
    "h-0": "Parameter",
    "h-1": "Type",
    "h-2": "Must or Not",
    "h-3": "Description",
    "0-0": "account",
    "0-1": "Sting",
    "0-2": "M",
    "0-3": "Account",
    "1-0": "Page",
    "1-1": "int",
    "1-2": "M",
    "1-3": "Page",
    "2-0": "pageSize",
    "2-1": "int",
    "2-2": "M",
    "2-3": "Amount"
  },
  "cols": 4,
  "rows": 3
}
[/block]
**レスポンスデータのフォーマット例** 
[block:code]
{
  "codes": [
    {
      "code": "{\n    \"code\":1,\n    \"data\":[\n        {\n            \"id\":\"4.3.16\",\n            \"seller\":\"1.2.136\",\n            \"otcaccount\":\"1.2.40\",\n            \"nh_asset_id\":\"4.2.187\",\n            \"asset_qualifier\":\"GNKHANDSOME\",\n            \"world_view\":\"GNKHAND\",\n            \"base_describe\":\"{\"name\":\"GNKHANDSOME\"}\",\n            \"nh_hash\":\"888e7617b8a55f9246d6788ae104133a7dbf31229653da31d72200b731fee6ce\",\n            \"price\":{\n                \"amount\":1000000,\n                \"asset_id\":\"1.3.0\"\n            },\n            \"memo\":\"\",\n            \"expiration\":\"2019/04/24 13:51:00\"\n        }\n    ],\n    \"total\":3\n}",
      "language": "javascript"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "NHアセットすべての注文履歴を入手"
}
[/block]
**インタフェース名**
queryNHAssetOrders

**リクエストパラメーター** 
[block:parameters]
{
  "data": {
    "h-0": "Parameter",
    "h-1": "Type",
    "h-2": "Must or Not",
    "h-3": "Description",
    "0-0": "assetIds",
    "0-1": "Sting",
    "0-2": "M",
    "0-3": "Assets ID or name",
    "1-0": "worldViews",
    "1-1": "Sting",
    "1-2": "N",
    "1-3": "Worldview ID or name",
    "2-0": "baseDescribe",
    "2-1": "Sting",
    "2-2": "N",
    "3-0": "page",
    "2-3": "baseDescribe",
    "3-1": "int",
    "3-2": "M",
    "3-3": "Page",
    "4-0": "pageSize",
    "4-1": "int",
    "4-2": "M",
    "4-3": "Amount"
  },
  "cols": 4,
  "rows": 5
}
[/block]
**レスポンスデータのフォーマット例** 
[block:code]
{
  "codes": [
    {
      "code": "{\n    \"code\":1,\n    \"data\":[\n        {\n            \"id\":\"4.3.16\",\n            \"seller\":\"1.2.136\",\n            \"otcaccount\":\"1.2.40\",\n            \"nh_asset_id\":\"4.2.187\",\n            \"asset_qualifier\":\"GNKHANDSOME\",\n            \"world_view\":\"GNKHAND\",\n            \"base_describe\":\"{\"name\":\"GNKHANDSOME\"}\",\n            \"nh_hash\":\"888e7617b8a55f9246d6788ae104133a7dbf31229653da31d72200b731fee6ce\",\n            \"price\":{\n                \"amount\":1000000,\n                \"asset_id\":\"1.3.0\"\n            },\n            \"memo\":\"\",\n            \"expiration\":\"2019/04/24 13:51:00\"\n        }\n    ],\n    \"total\":1\n}",
      "language": "javascript"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "アカウント内アイテム（NHアセット）情報を入手"
}
[/block]
**インタフェース名**
queryAccountNHAssets

**リクエストパラメーター**
[block:parameters]
{
  "data": {
    "h-0": "Parameter",
    "h-1": "Type",
    "h-2": "Must or Not",
    "h-3": "Description",
    "0-0": "account",
    "0-1": "Sting",
    "0-2": "M",
    "0-3": "Query account",
    "1-0": "worldViews(array)",
    "1-1": "array",
    "1-2": "N",
    "1-3": "The worldviews in query are separated by“,\".",
    "2-0": "page",
    "2-1": "int",
    "2-2": "M",
    "2-3": "Page",
    "3-0": "pageSize",
    "3-1": "int",
    "3-2": "M",
    "3-3": "Amount"
  },
  "cols": 4,
  "rows": 4
}
[/block]
**レスポンスデータのフォーマット例** 
[block:code]
{
  "codes": [
    {
      "code": "JavaScript\n{\n    \"code\":1,\n    \"data\":[\n        {\n            \"id\":\"4.2.189\",\n            \"nh_hash\":\"8e8e7617b8a55f9246d6788ae104133a7dbf31229653da31d72200b731fee6ce\",\n            \"nh_asset_creator\":\"1.2.139\",\n            \"nh_asset_owner\":\"1.2.136\",\n            \"nh_asset_active\":\"1.2.136\",\n            \"authority_account\":\"1.2.136\",\n            \"asset_qualifier\":\"COCOS\",\n            \"world_view\":\"GNKHAND\",\n            \"base_describe\":\"{\"name\":\"GNKHANDSOME\"}\",\n            \"parent\":[\n\n            ],\n            \"child\":[\n\n            ],\n            \"describe_with_contract\":[\n\n            ],\n            \"create_time\":\"2019-04-10T11:34:55\",\n            \"limit_list\":[\n\n            ],\n            \"limit_type\":\"black_list\"\n        }\n    ],\n    \"total\":1\n}",
      "language": "javascript"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "取引memoの復号"
}
[/block]
**インタフェース名**
decodeMemo

**リクエストパラメーター**
[block:parameters]
{
  "data": {
    "h-0": "Type",
    "h-1": "Must or Not",
    "h-2": "Description",
    "0-0": "Sting",
    "0-1": "M",
    "0-2": "Memo transfers in the following format data directly:"
  },
  "cols": 3,
  "rows": 1
}
[/block]

[block:code]
{
  "codes": [
    {
      "code": "{\n    \"from\":\"COCOS6G55VgR94GZmELS4UHEf2eVggmhPRnWLTWgGiEmzuBKdvEwoAB\",\n    \"to\":\"COCOS61qJmvPif4seDKUjEkoL9qUP9cSvwBvgme5djcK8thuUS6o4Mg\",\n    \"nonce\":\"12970368479715836292\",\n    \"message\":\"b9b37e032e205a78ce7238bfdeebc791\"\n}",
      "language": "javascript"
    }
  ]
}
[/block]
**コード例** 
[block:code]
{
  "codes": [
    {
      "code": "exports.decodeMemo = function(successCallBack,failCallBack){\n        var memo = {\n            from:\"COCOS6P1TAsfLCoPpyzjRtcgDTXL62oCxiZK3yYMer2hZGJ4ZvoRhx6\",\n            to:\"COCOS61qJmvPif4seDKUjEkoL9qUP9cSvwBvgme5djcK8thuUS6o4Mg\",\n            nonce:3354427411,\n            message:\"06659ec71b56cef9fcdb86d3fe30330f\"\n            }\n        BcxWeb.decodeMemo(memo).then(result => {\n            console.log('decodeMemo - successCallBack- result',JSON.stringify(result))\n            successCallBack(result);\n        }).catch(error => {\n            console.log('decodeMemo - failCallBack- result',JSON.stringify(error))\n            failCallBack(error);\n        });\n    }",
      "language": "javascript"
    }
  ]
}
[/block]
**レスポンスデータのフォーマット例（モバイル端末では「isMine」fieldがない）** 
[block:code]
{
  "codes": [
    {
      "code": "{\n    \"code\":1,\n    \"data\" :{\n      \"isMine\":0,\n        \"text\":\"ress\"\n    }\n}",
      "language": "javascript"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "NHアセットの取引（モバイル端末はtrx_id fieldのみ提供します）"
}
[/block]
**インタフェース名**
transferNHAsset

**リクエストパラメーター** 
[block:parameters]
{
  "data": {
    "h-0": "Parameter",
    "h-1": "Type",
    "h-2": "Must or Not",
    "h-3": "Description",
    "0-0": "toAccount",
    "0-1": "Sting",
    "0-2": "M",
    "0-3": "Transfer target account",
    "1-0": "NHAssetIds(array)",
    "1-1": "array",
    "1-2": "M",
    "1-3": "NH Assets ID"
  },
  "cols": 4,
  "rows": 2
}
[/block]
**レスポンスデータのフォーマット例** 
[block:code]
{
  "codes": [
    {
      "code": "{\n    \"code\":1,\n    \"data\":[\n        {\n            \"real_running_time\":125\n      }\n    ],\n    \"trx_data\":{\n        \"trx_id\":\"\"b50b2cf155e91df08e7e0e3756ae76b423679e71f5cf633fa05dedeeb96204fd\"\",\n        \"block_num\":5322683\n}\n}",
      "language": "javascript"
    }
  ]
}
[/block]
アカウントが存在していない
[block:code]
{
  "codes": [
    {
      "code": "{\n    \"code\":104,\n    \"message\":\"XXX Account not found\",\n    \"error\":{\n        \"message\":\"XXX Account not found\"\n    }\n}\n\nNHアセットが存在していない\nJavaScript\n{\n    \"code\":147,\n    \"message\":\"XXX NHAsset do not exist\"\n}",
      "language": "javascript"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "NHアセットの購入"
}
[/block]
**インタフェース名**
fillNHAssetOrder

**リクエストパラメーター**
[block:parameters]
{
  "data": {
    "h-0": "Parameter",
    "h-1": "Type",
    "h-2": "Must or Not",
    "h-3": "Description",
    "0-0": "orderId",
    "0-1": "Sting",
    "0-2": "M",
    "0-3": "Order ID",
    "1-0": "onlyGetFee",
    "1-1": "boolean",
    "1-2": "M",
    "1-3": "true:Only get the operating fee of this purchase of NH Assets；false:Purchase NH Assets\n\nTrue：\nFalse："
  },
  "cols": 4,
  "rows": 2
}
[/block]
**レスポンスデータのフォーマット例** 
NHアセットの購入操作の手数料データのみリターンする場合（onlyGetFee = true）：
[block:code]
{
  "codes": [
    {
      "code": "JavaScript\n{\n    \"code\":1,\n    \"data\":{\n        \"fee_amount\":0,\n        \"fee_symbol\":\"COCOS\"\n    }\n}",
      "language": "javascript"
    }
  ]
}
[/block]
NHアセットの購入操作データをリターンする場合（onlyGetFee = false）（モバイル端末はtrx_id fieldのみ提供します）：
[block:code]
{
  "codes": [
    {
      "code": "{\n    \"code\":1,\n    \"data\":[\n        {\n            \"result\": \"4.2.192\",\n            \"real_running_time\":204\n        }\n    ],\n    \"trx_data\":{\n    \"trx_id\":\"01e7036237896f9069905d4fc9c5d86a55bb2d0ef2fca43e6df5d5123766f223\",\n        \"block_num\":5409694\n    }\n}",
      "language": "javascript"
    }
  ]
}
[/block]
残高不足
[block:code]
{
  "codes": [
    {
      "code": "{\n    \"code\":0,\n    \"message\":\"Assert Exception: insufficient_balance: Insufficieble to pay 1000 COCOS from gnkhandsome2 to syling\" \",\n    \"error\":{\n        \"code\":31,\n        \"message\":\"Assert Exception: insufficient_balance: Insufficient Balance: 3.53190 COCOS, unable to transfer '1000 COCOS' from account 'gnkhandsome2' to 'syling' Unable\",\n        \"messageDetail\":\"Assert Exception: insufficient_balance: Insufficient Balance: 3.53190 COCOS, unable to transfer '1000 COCOS' from account 'gnkhandsome2' to 'syling\"]}\"\n    }\n}",
      "language": "javascript"
    }
  ]
}
[/block]
ログインしていない
[block:code]
{
  "codes": [
    {
      "code": "{\n    \"code\":-11,\n    \"message\":\"Please login first\"\n}",
      "language": "javascript"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "アカウント残高を入手"
}
[/block]
**インタフェース名**
queryAccountBalances

**リクエストパラメーター**
[block:parameters]
{
  "data": {
    "h-0": "Parameter",
    "h-1": "Type",
    "h-2": "Must or Not",
    "h-3": "Description",
    "0-0": "assetId",
    "0-1": "Sting",
    "0-2": "M",
    "0-3": "Assets identity or ID",
    "1-0": "account",
    "1-1": "Sting",
    "1-2": "M",
    "1-3": "Account name"
  },
  "cols": 4,
  "rows": 2
}
[/block]
**レスポンスデータのフォーマット例**
残高データをリターンする：
[block:code]
{
  "codes": [
    {
      "code": "{\n \"code\":1,\n    \"data\":{\n        \"COCOS\":\"8949.18901\"\n    }\n}\n\nインターネットへ接続できない\nJavaScript\n{\n    \"code\":102,\n    \"message\":\"It doesnt connect to the server.\",\n    \"data\":{\n        \"COCOS\":\"0\"\n    }\n}",
      "language": "javascript"
    }
  ]
}
[/block]
詳細は「[7.1 JS-SDK](https://dash.readme.io/project/jp-dev/v1.0/docs/71-js-sdk)」をご参照ください。