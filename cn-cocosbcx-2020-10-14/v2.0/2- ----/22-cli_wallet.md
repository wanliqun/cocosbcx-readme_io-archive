---
title: "2.2 cli_wallet使用入门"
slug: "22-cli_wallet"
hidden: false
createdAt: "2019-03-25T09:39:19.177Z"
updatedAt: "2020-05-18T06:17:50.443Z"
---
钱包命令行工具，提供跟链之间的交互操作。操作说明如下：
[block:api-header]
{
  "title": "2.2.1 登录命令行钱包"
}
[/block]
1. 获取命令行钱包可执行文件: cli_wallet，并拷贝到预定目录

    cli_wallet的[git仓库地址](https://github.com/Cocos-BCX/cocos-bcx-node-bin.git)，该仓库包含多个版本的cli_wallet。以v1.0.8版本为例，[cli_wallet的路径](https://github.com/Cocos-BCX/cocos-bcx-node-bin/tree/master/cli/mainnet/v1.0.8/linux)

2. 进入命令行钱包所在目录，执行如下命令登录命令行钱包
**命令格式**
--chain-id [链 ID] -s [节点 RPC 地址] -r [命令行钱包的 RPC 服务所监听的地址]
[block:code]
{
  "codes": [
    {
      "code": "./cli_wallet  --chain-id 90a45949c27a3de6f71d2cfb68e4a04a2fce9052f8192d405c581ba9b36d991b -s ws://127.0.0.1:8020  -r  127.0.0.1:8099",
      "language": "shell",
      "name": "Shell"
    }
  ]
}
[/block]
结果：

[block:code]
{
  "codes": [
    {
      "code": "Logging RPC to file: logs/rpc/rpc.log\n2125047ms th_a       main.cpp:131                  main                 ] key_to_wif( committee_private_key ): 5KCBDTcyDqzsqeh******c3saYSzbDZ5W \n2125062ms th_a       main.cpp:135                  main                 ] nico_pub_key: COCOS7yE9skpB******tXTz88HtbpQsZf \n2125063ms th_a       main.cpp:136                  main                 ] key_to_wif( nico_private_key ): 5KAUeN3Yv51******XTJK7euqc3NnaaLz1GJm \nStarting a new wallet with chain ID 90a45949c27a3de6f71d2cfb68e4a04a2fce9052f8192d405c581ba9b36d991b (from CLI)\n2125073ms th_a       main.cpp:183                  main                 ] wdata.ws_server: ws://127.0.0.1:8020 \n2125108ms th_a       main.cpp:188                  main                 ] wdata.ws_user:  wdata.ws_password:  \n\nPlease use the set_password method to initialize a new wallet before continuing\n2139294ms th_a       main.cpp:227                  main                 ] Listening for incoming RPC requests on 127.0.0.1:8099\nnew >>> ",
      "language": "text"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "2.2.2 命令行钱包设置锁与解锁"
}
[/block]
1. 第一次登录命令行钱包，需要设置钱包密码
**命令格式**
set_password [设置的密码]
**函数原型**
void graphene::wallet::wallet_api::set_password(string password)
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
**结果：**
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
2. 设置钱包密码后，需要解锁钱包
**命令格式 **
unlock [设置的密码]
**函数原型**
void graphene::wallet::wallet_api::unlock(string password)
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
**结果：**
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
  "title": "2.2.3 命令行钱包导入账户"
}
[/block]
1. 登陆并解锁钱包，执行如下命令导入用户
**命令格式 **
import_key [用户名] [用户私钥]
**函数原型**
bool graphene::wallet::wallet_api::import_key(string account_name_or_id, string wif_key)
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
**结果：**
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
  "title": "2.2.4 命令行钱包导入资产"
}
[/block]
1. 登录并解锁钱包，导入资产
**命令格式 **
import_balance [用户名] [资产地址对应的私钥] [是否广播（true/false）]
**函数原型**
vector<signed_transaction> graphene::wallet::wallet_api::import_balance(string account_name_or_id, const vector<string> &wif_keys, bool broadcast)
**背景**
新链，创世资产尚未导出
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
**结果：**
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
  "title": "2.2.5 转账"
}
[/block]
**命令格式 **
transfer [转账人] [接收人] [转账数量] [代币资产类型] [备注] [是否广播（true/false）]
**函数原型**
signed_transaction graphene::wallet::wallet_api::transfer(string from, string to, string amount, string asset_symbol, pair<string,bool> memo, bool broadcast = false)
**条件**
登录并解锁钱包，账户内有足够余额
**示例**
transfer official-account test-account 100 COCOS ["info",false] true
[block:code]
{
  "codes": [
    {
      "code": "transfer from to amount asset_symblo [\"memo_info\",false] true",
      "language": "shell",
      "name": "Shell"
    }
  ]
}
[/block]
**结果：**
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
  "title": "2.2.6 注册账户"
}
[/block]
**命令格式 **
register_account [用户名] [owner公钥] [active公钥] [记录人账户名] [是否广播（true/false）]
**函数原型**
signed_transaction graphene::wallet::wallet_api::register_account(string name, public_key_type owner, public_key_type active, string registrar_account, bool broadcast = false)
**条件**
登录并解锁钱包，注册人终身会员，账户内有足够余额
**示例**
register_account test-account XXX6esv8d6u2eqzKyiQvCYJa6XK74c7BrmzUqL4Z7zfhtvB4db XXX6esv8d6u2eqzKyiQvCYJa6XK74c7BrmzUqL4Z7zfhtvB4db official-account true
[block:code]
{
  "codes": [
    {
      "code": "register_account name owner_key active_key registrar_account true",
      "language": "shell",
      "name": "Shell"
    }
  ]
}
[/block]
**结果：**
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
  "title": "2.2.7 账户升级会员"
}
[/block]
**条件**
账户内有足够余额
**命令格式 **
upgrade_account [用户名] [是否广播（true/false）]
**函数原型**
signed_transaction graphene::wallet::wallet_api::upgrade_account(string name, bool broadcast)
**示例**
upgrade_account test-account true
**注意**
命令行钱包只支持升级为永久会员，不支持升级为年费会员
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
**结果：**
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
  "title": "2.2.8 获取链 ID、当前活跃见证人及委员会成员等信息"
}
[/block]
**命令格式 **
info
**函数原型**
variant graphene::wallet::wallet_api::info()
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
**结果：**
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
  "title": "2.2.9 返回客户端版本、编译时间、boost 版本、openssl 版 本等信息"
}
[/block]
**命令格式 **
about
**函数原型**
variant_object graphene::wallet::wallet_api::about()const
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
**结果：**
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
  "title": "2.2.10 获取指定块信息"
}
[/block]
**命令格式 **
get_block [区块高度]
**函数原型**
optional<signed_block_with_info> graphene::wallet::wallet_api::get_block(uint32_t num)
**示例**
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
**结果：**
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
  "title": "2.2.11 获取链上注册账户总数"
}
[/block]
**命令格式 **
get_account_count
**函数原型**
uint64_t graphene::wallet::wallet_api::get_account_count() const
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
**结果：**
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
  "title": "2.2.12 列出钱包中导入的账户"
}
[/block]
**命令格式 **
list_my_accounts
**函数原型**
vector<account_object> graphene::wallet::wallet_api::list_my_accounts()
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
**结果：**
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
  "title": "2.2.13 列出账户余额"
}
[/block]
**命令格式 **
list_account_balances [账户名]
**函数原型**
vector<asset> graphene::wallet::wallet_api::list_account_balances(const string &id)
**示例**
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
**结果：**
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
  "title": "2.2.14 列出链上的代币"
}
[/block]
**命令格式 **
list_assets [最小限制] [最大返回个数]
**函数原型**
vector<asset_object> graphene::wallet::wallet_api::list_assets(const string &lowerbound, uint32_t limit) const
**示例**
list_assets “” 1
**说明**
返回结果以代币符号进行排序，lowerbound 参数为最小限制，limit 为最大返回个数，即返回最大 limit 个代币符号不小于 lowerbound 的代币
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
**结果：**
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
  "title": "2.2.15 返回账户历史操作"
}
[/block]
**命令格式 **
get_account_history [账户名] [最大返回个数]
**函数原型**
vector<operation_detail> graphene::wallet::wallet_api::get_account_history(string name, int limit) const
**示例**
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
**结果：**
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
  "title": "2.2.16 返回链操作费用等不易变化的属性"
}
[/block]
**命令格式 **
get_global_properties
**函数原型**
global_property_object graphene::wallet::wallet_api::get_global_properties() const
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
**结果：**
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
      "caption": "结果过长，只取部分"
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
  "title": "2.2.17 返回链头块 ID、时间、下一维护周期时间等易变化的属性"
}
[/block]
**命令格式 **
get_dynamic_global_properties
**函数原型**
dynamic_global_property_object graphene::wallet::wallet_api::get_dynamic_global_properties() const
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
**结果：**
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
  "title": "2.2.18 获取账户信息"
}
[/block]
**命令格式 **
get_account  [账户名或ID]
**函数原型**
account_object graphene::wallet::wallet_api::get_account(string account_name_or_id) const
**示例**
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
**结果：**
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
  "title": "2.2.19 返回代币资产信息"
}
[/block]
**命令格式 **
get_asset  [资产名称或ID]
**函数原型**
asset_object graphene::wallet::wallet_api::get_asset(string asset_name_or_id)const
**示例**
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
**结果：**
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
  "title": "2.2.20 获取账户的账户 ID"
}
[/block]
**命令格式 **
get_account_id [账户名]
**函数原型**
account_id_type graphene::wallet::wallet_api::get_account_id(string account_name_or_id) const
**示例**
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
**结果：**
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
  "title": "2.2.21 返回操作历史列表"
}
[/block]
**命令格式 **
get_relative_account_history(string name, uint32_t stop,  int limit, uint32_t start)
 [账户名] [最新操作的序列数] [要返回值的条目数] [开始回溯的起始序列数]
**函数原型**
vector<operation_detail> graphene::wallet::wallet_api::get_relative_account_history(string name, uint32_t stop,  int limit, uint32_t start) const
**示例**
get_relative_account_history nicotest 100 10 50
[block:code]
{
  "codes": [
    {
      "code": "get_relative_account_history nicotest 100 10 50",
      "language": "shell",
      "name": "Shell"
    }
  ]
}
[/block]
**结果：**
[block:api-header]
{
  "title": "2.2.22 获取对象"
}
[/block]
**命令格式 **
get_object [对象ID]
**函数原型**
variant graphene::wallet::wallet_api::get_object(object_id_type id) const
**示例**
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
**结果：**
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
  "title": "2.2.23 获取私钥"
}
[/block]
**命令格式 **
get_private_key [公钥]
**函数原型**
string graphene::wallet::wallet_api::get_private_key(public_key_type pubkey) const
**示例**
get_private_key XXX6esv8d6u2eqzKyiQvCYJa6XK74c7BrmzUqL4Z3
**说明**
该私钥必须已经保存于钱包中才可获取
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
**结果：**
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
  "title": "2.2.24 锁定钱包"
}
[/block]
**命令格式 **
lock
**函数原型**
void graphene::wallet::wallet_api::lock()
说明
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
**结果：**
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
  "title": "2.2.25 返回一组安全的脑密钥、公钥、私钥"
}
[/block]
**命令格式 **
suggest_brain_key
**函数原型**
brain_key_info graphene::wallet::wallet_api::suggest_brain_key() const
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
**结果：**
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
  "title": "2.2.26 注册委员会成员"
}
[/block]
**命令格式 **
create_committee_member [账户名] [url地址] [是否广播（true/false）]
**函数原型**
signed_transaction graphene::wallet::wallet_api::create_committee_member(string owner_account, string url, bool broadcast = false)
**示例**
create_committee_member official-account "http://my-web" true
**说明**
注册后只是成为了候选委员会成员，需获得一定的投票后才会成为正式的委员会成员
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
**结果：**
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
  "title": "2.2.27 注册见证人"
}
[/block]
**命令格式 **
create_witness [账户名] [url地址] [是否广播（true/false）]
**函数原型**
signed_transaction graphene::wallet::wallet_api::create_witness(string owner_account, string url, bool broadcast = false)
**示例**
create_witness official-account "http://my-web" true
**说明**
注册后只是成为了候选见证人，需获得一定的投票后才会成为正式的见证人
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
**结果：**
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
  "title": "2.2.28 列出见证人"
}
[/block]
**命令格式 **
list_witnesses [lowerbound] [limit]
**函数原型**
map<string, witness_id_type> graphene::wallet::wallet_api::list_witnesses(const string &lowerbound, uint32_t limit)
**示例**
list_witnesses "" 100
**说明**
以见证人账户名进行排序返回见证人，lowerbound 为最小限制，limit 为最大返回个数
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
**结果：**
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
  "title": "2.2.29 列出委员会成员"
}
[/block]
**命令格式 **
list_committee_members [lowerbound] [limit]
**函数原型**
map<string, committee_member_id_type> graphene::wallet::wallet_api::list_committee_members(const string &lowerbound, uint32_t limit)
**示例**
list_committee_members "" 100
**说明**
以委员会成员账户名进行排序返回委员会成员，lowerbound 为最小限制，limit 为最大返回个数
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
**结果：**
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
  "title": "2.2.30 返回见证人信息"
}
[/block]
**命令格式 **
get_witness [见证人名称或ID]
**函数原型**
witness_object graphene::wallet::wallet_api::get_witness(string owner_account)
**示例**
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
**结果：**
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
  "title": "2.2.31 返回委员会成员信息"
}
[/block]
**命令格式 **
get_committee_member [委员会成员名称或ID]
**函数原型**
committee_member_object graphene::wallet::wallet_api::get_committee_member(string owner_account)
**示例**
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
**结果：**
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
  "title": "2.2.32 创建合约"
}
[/block]
**命令格式 **
create_contract [合约拥有者] [合约名称] [合约权限(一对公私钥中的公钥publicKey)] [合约内容] [是否广播（true/false）]
**函数原型**
pair<tx_hash_type, signed_transaction> graphene::wallet::wallet_api::create_contract(string owner, string name, public_key_type contract_authority, string data, bool broadcast = false) 
**示例**
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
**结果：**
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
  "title": "2.2.33 更新合约"
}
[/block]
**命令格式 **
revise_contract [合约更新人用户名] [合约名称或ID] [合约内容] [是否广播（true/false）]
**函数原型**
pair<tx_hash_type, signed_transaction> graphene::wallet::wallet_api::revise_contract(string reviser, string contract_id_or_name, string data, bool broadcast = false)
**示例**
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
**结果：**
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
  "title": "2.2.34 调用合约"
}
[/block]
**命令格式 **
call_contract_function [用户名或ID] [合约名称或合约ID] [函数名] [参数列表] [是否广播（true/false）]
**函数原型**
pair<tx_hash_type, signed_transaction> graphene::wallet::wallet_api::call_contract_function(string account_id_or_name, string contract_id_or_name, string function_name, vector<lua_types> value_list, bool broadcast = false);
**示例**
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
**结果：**
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
  "title": "2.2.35 列出账户奖励金额信息"
}
[/block]
**命令格式 **
get_vesting_balances [用户名]
**函数原型**
vector<vesting_balance_object_with_info> graphene::wallet::wallet_api::get_vesting_balances(string account_name)
**示例**
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
**结果：**
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
  "title": "2.2.36 领取奖励金额(仅限见证人成员)"
}
[/block]
**命令格式 **
withdraw_vesting [用户名] [数量] [资产符号] [是否广播（true/false）]
**函数原型**
signed_transaction graphene::wallet::wallet_api::withdraw_vesting(string witness_name, string amount, string asset_symbol, bool broadcast = false)
**示例**
withdraw_vesting cocos-witness-0 10 XXX true 
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
  "title": "2.2.37 给见证人投票"
}
[/block]
**命令格式 **
vote_for_witness [用户名] [见证人用户名] [投票数量（带5位精度）] [是否广播（true/false）]
**函数原型**
signed_transaction graphene::wallet::wallet_api::vote_for_witness(string voting_account, string witness, uint64_t approve, bool broadcast = false)
**示例**
vote_for_witness official-account cocos-witness-0 10000000 true
**前提步骤**
1. 进入命令行钱包所在目录，执行命令./cli_wallet-sws://127.0.0.1:8070-r127.0.0.1:8099登录命令行钱包
2. 执行命令 unlock xxxx 解锁钱包
3. 执行命令import_key official-account 5KaVpJa9G4oqA5WHcSGitauFRuzdHcPVEAaESaA7jG8s 导入用户 
4. 执行命令 import_balance official-
 account ["5KAUeN3Yv51FzpLGGf4S1ByKpMqVFNzXTJK7euqc3"] true 为用户导入资产
5. 执行命令 vote_for_witness official-account cocos-witness-0 10000000 true ，official-account 账户将 会为见证人账户 cocos-witness-0 投票
6. 按照步骤4为其他见证人投票 
[block:code]
{
  "codes": [
    {
      "code": "vote_for_witness official-account cocos-witness-0 10000000 true",
      "language": "shell",
      "name": "Shell"
    }
  ]
}
[/block]
**结果：**
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
  "title": "2.2.38 给委员会成员投票"
}
[/block]
**命令格式 **
vote_for_committee_member [用户名] [见证人用户名] [投票数量（带5位精度）] [是否广播（true/false）]
**函数原型**
signed_transaction graphene::wallet::wallet_api::vote_for_committee_member(string voting_account, string committee_member, uint64_t approve, bool broadcast = false)
**示例**
vote_for_committee_member official-account cocos-witness-0 10000000 true
**前提步骤**
1. 进入命令行钱包所在目录，执行命令./cli_wallet-sws://127.0.0.1:8070-r127.0.0.1:8099登录命令行钱包
2. 执行命令 unlock xxxx 解锁钱包
3. 执行命令import_keyofficial-account 5KaVpJa9G4oqA5WHcSGitauFRuzdHcPVEAaESaA7jG8s 导入用户
4. 执行命令 import_balance official-account ["5KAUeN3Yv51FzpLGGf4S1ByKpMqVFNzXTJK7euq"] true 为用户导入资产
5. 执行命令 vote_for_committee_member official-account Witness-0 10000000 true ，official- account 账户将会为见证人账户 Witness-0 投票
6. 按照步骤4为其他见委员会成员投票
[block:code]
{
  "codes": [
    {
      "code": "vote_for_committee_member official-account cocos-witness-0 10000000 true",
      "language": "shell",
      "name": "Shell"
    }
  ]
}
[/block]
**结果：**
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
  "title": "2.2.39 委员会成员提议修改操作费率"
}
[/block]
**命令格式**
1. propose_fee_change [用户名] [过期时间] [修改内容] [基础提议（可选）] [是否广播（true/false）]
2. approve_proposal [用户名] [提议ID] [提议人用户名] [是否广播（true/false）]
**函数原型**
signed_transaction graphene::wallet::wallet_api::propose_fee_change(const string &proposing_account, fc::time_point_sec expiration_time, const variant_object &changed_values,fc::optional<proposal_id_type> proposal_base, bool broadcast = false)
pair<tx_hash_type, signed_transaction> graphene::wallet::wallet_api::approve_proposal(const string &fee_paying_account,
const string &proposal_id,const approval_delta &delta,bool broadcast /* = false */
);
**示例**
[block:code]
{
  "codes": [
    {
      "code": "propose_fee_change Witness-0 \"2018-07-24T06:55:40\" {\"transfer\" : {\"fee\": 244000, \"price_per_kbyte\": 100000}} null true",
      "language": "shell"
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
**前提步骤**
1. 进入命令行钱包所在目录，执行命令./cli_wallet-sws://127.0.0.1:8070-r127.0.0.1:8099登录命令行钱包
2. 执行命令 unlock xxxx 解锁钱包
3. 执行命令 import_key Witness-0 5KaVpJa9G4oqA5WHcSGitauFRuzdHcPVEAaE 导入委员会成员用户
4. 执行命令 propose_fee_change Witness-0 "2018-07-24T06:55:40" {"transfer" : {"fee": 244000, "price_per_kbyte": 100000}} true 提议修改转账操作费率
5. 执行命令 transfer official-account committee-account 100 XXX ["",false] true 向用户 committee- account 转账(该用户是提议的执行者)
6. 执行命令 approve_proposal Witness-0 1.10.0 {"active_approvals_to_add" : ["Witness-0"]} true 批准提议(提议的执行者是账户 committee-account，每个委员会成员根据自己的得票数占有该账户一定的活跃权限权重，因此，当批准该提议的委员会成员加起来的权重超过 committee-account 的阈值时，该提议才可以被执行)
7. 当提议到达过期时间时，系统会自动判断提议是否可以执行，如果是，则会执行提议， 然后再下一个维护时间结束后更新操作费率。 

结果：
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
      "caption": "结果过长，只取部分"
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
  "title": "2.2.40 委员会成员提议修改链全局配置"
}
[/block]
**命令格式**
propose_parameter_change [用户名] [过期时间] [修改内容] [基础提议（可选）] [是否广播（true/false）]
**函数原型**
signed_transaction graphene::wallet::wallet_api::propose_parameter_change(const string &proposing_account, fc::time_point_sec expiration_time, const variant_object &changed_values,fc::optional<proposal_id_type> proposal_base,bool broadcast = false
**示例**
propose_parameter_change Witness-0 "2018-07-24T06:55:40" {"committee_proposal_review_period": 300} null true
**前提步骤**
1. 进入命令行钱包所在目录，执行命令./cli_wallet-sws://127.0.0.1:8070-r127.0.0.1:8099登录命令行钱包
2. 执行命令 unlock xxxx 解锁钱包
3. 执行命令 import_key Witness-0 5KaVpJa9G4oqA5WHcSGitauFRuzdHcPVEAaE 导入委员会成员用户
4. 执行命令propose_parameter_change Witness-0 "2018-07-24T06:55:40" {"committee_proposal_review_period": 300} null true 提议修改链全局配置中的委员会提议复审期时常
5. 执行命令 transfer official-account committee-account 100 XXX ["",false] true 向用户 committee- account 转账(该用户是提议的执行者)
6. 执行命令 approve_proposal Witness-0 1.10.1 {"active_approvals_to_add" : ["Witness-0"]} true 批准提议(提议的执行者是账户 committee-account，每个委员会成员根据自己的得票 数占有该账户一定的活跃权限权重，因此，当批准该提议的委员会成员加起来的权重超过 committee-account 的阈值时，该提议才可以被执行)
7. 当提议到达过期时间时，系统会自动判断提议是否可以执行，如果是，则会执行提议， 然后再下一个维护时间结束后更新操作费率
**可配置参数**
"block_interval"	块间隔
"maintenance_interval"	维护间隔
"maintenance_skip_slots"	维护跳过周期
"committee_proposal_review_period"	理事会提案审查期
"maximum_transaction_size"	最大事务大小
"maximum_block_size"	最大的块大小
"maximum_time_until_expiration"	最长到期时间
"maximum_proposal_lifetime"	理事会提案最大失效期
"maximum_asset_whitelist_authorities"	最多资产白名单
"maximum_asset_feed_publishers"	资产喂价的最大人数
"maximum_witness_count"	最大BP节点数
"maximum_committee_count"	最大理事会成员数
"maximum_authority_membership"	最大权威会员数
"reserve_percent_of_fee"	保留费用
"network_percent_of_fee"	网络费用
"lifetime_referrer_percent_of_fee"	终身费用参考百分比
"cashback_vesting_period_seconds"	现金返还期（秒）
"cashback_vesting_threshold"	奖励金保留阈值
"count_non_member_votes"	非会员投票
"allow_non_member_whitelists"	允许非成员白名单
"witness_pay_per_block"	每个区块证人工资
"worker_budget_per_day"	矿工每日预计
"max_predicate_opcode"	（每个块）最大操作数
"fee_liquidation_threshold"	费用清算阈值
"accounts_per_fee_scale"	收费标准
"account_fee_scale_bitshifts"	账户费用转移比例
"max_authority_depth"	最大鉴权深度，一个账号可以赋予另一个账号权限，配置这个权限最大可以往下生效几层
[block:code]
{
  "codes": [
    {
      "code": "propose_parameter_change Witness-0 \"2018-07-24T06:55:40\" {\"committee_proposal_review_period\": 300} null true",
      "language": "shell",
      "name": "Shell"
    }
  ]
}
[/block]
结果：
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

[block:api-header]
{
  "title": "2.2.41 创建用户资产"
}
[/block]
**命令格式**
create_asset [新资产发行人的帐户的名称] [新资产的代码] [小数点右边的精度位数] [新资产所需的资产选项] [智能资产特有的选项] [是否广播（true/false）]
**函数原型**
signed_transaction graphene::wallet::wallet_api::create_asset(string issuer, string symbol, uint8_t precision, asset_options common, fc::optional<bitasset_options> bitasset_opts, bool broadcast = false)
**示例**
create_asset nicotest NODE 8  {"max_supply":"2100000000000000","market_fee_percent":0,"max_market_fee":0,"flags":0,"core_exchange_rate":{"base":{"amount":1,"asset_id":"1.3.4"},"quote":{"amount":1,"asset_id":"1.3.0"}},"description":"","extensions":[]} null true

[block:code]
{
  "codes": [
    {
      "code": "create_asset nicotest NODE 8  {\"max_supply\":\"2100000000000000\",\"market_fee_percent\":0,\"max_market_fee\":0,\"flags\":0,\"core_exchange_rate\":{\"base\":{\"amount\":1,\"asset_id\":\"1.3.4\"},\"quote\":{\"amount\":1,\"asset_id\":\"1.3.0\"}},\"description\":\"\",\"extensions\":[]} null true",
      "language": "shell",
      "name": "shell"
    }
  ]
}
[/block]
结果：
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/80e6c6f-5.png",
        "5.png",
        713,
        645,
        "#f5f0ef"
      ]
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "2.2.42 创建智能资产"
}
[/block]
**命令格式**
create_asset [新资产发行人的帐户的名称] [新资产的代码] [小数点右边的精度位数] [新资产所需的资产选项] [智能资产特有的选项] [是否广播（true/false）]
**函数原型**
signed_transaction graphene::wallet::wallet_api::create_asset(string issuer, string symbol, uint8_t precision, asset_options common, fc::optional<bitasset_options> bitasset_opts, bool broadcast = false)
**示例**
create_asset nicotest USDT 5 {"issuer_permissions": 511,"flags": 128,"core_exchange_rate":{"base":{"amount":1,"asset_id":"1.3.3"},"quote":{"amount":1,"asset_id":"1.3.0"}}} {"new_feed_producers":[],"feed_lifetime_sec":120} true
[block:code]
{
  "codes": [
    {
      "code": "",
      "language": "shell",
      "name": "shell"
    }
  ]
}
[/block]
结果：

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/06ac36c-4.png",
        "4.png",
        705,
        734,
        "#f5f1ef"
      ]
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "2.2.43 发行资产"
}
[/block]
**命令格式**
issue_asset [接收新股份的帐户的名称] [数量] [资产符号] [新资产所需的资产选项] [备忘录] [是否广播（true/false）]
**函数原型**
signed_transaction graphene::wallet::wallet_api::issue_asset(string to_account, string amount, string symbol, pair<string,bool> memo, bool broadcast = false)
**示例**
issue_asset cocos-test01 100000 USDB  ["issue 10w ETH to cocos-test12 account",false] true

[block:code]
{
  "codes": [
    {
      "code": "issue_asset cocos-test01 100000 USDB  [\"issue 10w ETH to cocos-test12 account\",false] true",
      "language": "shell",
      "name": "Shell"
    }
  ]
}
[/block]
结果：
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/5a18466-8.png",
        "8.png",
        713,
        700,
        "#f5f2f0"
      ]
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "2.2.44 更新用户资产"
}
[/block]
**命令格式**
update_asset [要更新的资产的名称或ID] [新发行人的名称或ID，不修改则为null] [新的资产选项] [是否广播（true/false）]
**函数原型**
signed_transaction graphene::wallet::wallet_api::update_asset(string symbol, optional<string> new_issuer, asset_options new_options, bool broadcast = false)
**示例**
update_asset 1.3.4 test1 {"core_exchange_rate":{"base":{"amount":1,"asset_id":"1.3.4"},"quote":{"amount":1,"asset_id":"1.3.0"}}} true


[block:code]
{
  "codes": [
    {
      "code": "update_asset 1.3.4 test1 {\"core_exchange_rate\":{\"base\":{\"amount\":1,\"asset_id\":\"1.3.4\"},\"quote\":{\"amount\":1,\"asset_id\":\"1.3.0\"}}} true",
      "language": "shell",
      "name": "Shell"
    }
  ]
}
[/block]
结果：
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/6b411ba-7.png",
        "7.png",
        713,
        802,
        "#f5f2f1"
      ]
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "2.2.45 更新智能资产"
}
[/block]
**命令格式**
update_bitasset [要更新的资产的名称或ID] [新的喂价者列表] [是否广播（true/false）]
**函数原型**
signed_transaction graphene::wallet::wallet_api::update_bitasset(string symbol, bitasset_options new_options, bool broadcast = false)
**示例**
update_bitasset  1.3.7  {"new_feed_producers":[],"feed_lifetime_sec":180} true
[block:code]
{
  "codes": [
    {
      "code": "update_bitasset  1.3.7  {\"new_feed_producers\":[],\"feed_lifetime_sec\":180} true",
      "language": "shell",
      "name": "Shell"
    }
  ]
}
[/block]
结果：
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/d84c694-9.png",
        "9.png",
        713,
        823,
        "#f5f2f1"
      ]
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "2.2.46 发布智能资产喂价者"
}
[/block]
**命令格式**
publish_asset_feed [发布资产喂价的帐户] [资产名称] [喂价对象] [是否广播（true/false)]
**函数原型**
signed_transaction graphene::wallet::wallet_api::publish_asset_feed(string publishing_account, string symbol, price_feed feed, bool broadcast = false)
**示例**
publish_asset_feed feeder STEEM {"settlement_price":{"base":{"amount":5,"asset_id":"1.3.10"},"quote":{"amount":10,"asset_id":"1.3.0"}},"core_exchange_rate":{"base":{"amount":100,"asset_id":"1.3.10"},"quote":{"amount":2,"asset_id":"1.3.0"}}} true
[block:code]
{
  "codes": [
    {
      "code": "publish_asset_feed feeder STEEM {\"settlement_price\":{\"base\":{\"amount\":5,\"asset_id\":\"1.3.10\"},\"quote\":{\"amount\":10,\"asset_id\":\"1.3.0\"}},\"core_exchange_rate\":{\"base\":{\"amount\":100,\"asset_id\":\"1.3.10\"},\"quote\":{\"amount\":2,\"asset_id\":\"1.3.0\"}}} true",
      "language": "shell",
      "name": "Shell"
    }
  ]
}
[/block]
结果：
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/cdfb3e3-10.png",
        "10.png",
        713,
        825,
        "#f5f2f1"
      ]
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "2.2.47 更新智能资产喂价者"
}
[/block]
**命令格式**
update_asset_feed_producers [要更新的资产的名称或ID] [新的资产选项] [是否广播（true/false)]
**函数原型**
signed_transaction graphene::wallet::wallet_api::update_asset_feed_producers(string symbol, flat_set<string> new_feed_producers, bool broadcast = false)
**示例**
update_asset_feed_producers 1.3.8 ["feeder"] true

[block:code]
{
  "codes": [
    {
      "code": "update_asset_feed_producers 1.3.8 [\"feeder\"] true",
      "language": "text",
      "name": null
    }
  ]
}
[/block]

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/6a5c69c-11.png",
        "11.png",
        713,
        691,
        "#f5f3f2"
      ]
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "2.2.48 获取用户资产数据"
}
[/block]
**命令格式**
get_asset [相关资产的符号或ID] 
**函数原型**
asset_object graphene::wallet::wallet_api::get_asset(string asset_name_or_id)const
**示例**
get_asset BAT

[block:code]
{
  "codes": [
    {
      "code": "get_asset BAT",
      "language": "shell",
      "name": "Shell"
    }
  ]
}
[/block]
结果：

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/e36b8f1-12.png",
        "12.png",
        713,
        782,
        "#f6f4f3"
      ]
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "2.2.49 获取智能资产数据"
}
[/block]
**命令格式**
get_bitasset_data  [相关资产的符号或ID] 
**函数原型**
asset_bitasset_data_object graphene::wallet::wallet_api::get_bitasset_data(string asset_name_or_id)const
**示例**
get_bitasset_data  BAT
[block:code]
{
  "codes": [
    {
      "code": "get_bitasset_data  BAT",
      "language": "shell",
      "name": null
    }
  ]
}
[/block]
结果：
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/b9a511e-13.png",
        "13.png",
        713,
        706,
        "#f6f4f3"
      ]
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "2.2.50 销毁资产"
}
[/block]
** 命令格式**
reserve_asset  [销毁资产的账户] [销毁量] [要销毁的资产的名称或ID] [要销毁的资产的名称或ID] [是否广播（true/false)]
**函数原型**
signed_transaction graphene::wallet::wallet_api::reserve_asset(string from, string amount, string symbol, bool broadcast = false)
** 示例**
reserve_asset nicotest 100 COCOS  true

[block:code]
{
  "codes": [
    {
      "code": "reserve_asset nicotest 100 COCOS  true",
      "language": "shell"
    }
  ]
}
[/block]
结果：
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/b9ece76-14.png",
        "14.png",
        713,
        721,
        "#f6f3f2"
      ]
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "2.2.51 智能资产全局清算"
}
[/block]
** 命令格式**
global_settle_asset  [要强制结算的资产的名称或ID] [清算的价格] [是否广播（true/false)]
**函数原型**
signed_transaction graphene::wallet::wallet_api::global_settle_asset(string symbol, price settle_price, bool broadcast = false)
**示例**
global_settle_asset nicotest 100 COCOS  true
[block:code]
{
  "codes": [
    {
      "code": "global_settle_asset nicotest 100 COCOS  true",
      "language": "shell"
    }
  ]
}
[/block]
结果：
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/be1b935-15.png",
        "15.png",
        713,
        723,
        "#f5f3f2"
      ]
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "2.2.52 理事会撤回"
}
[/block]
表明否定工作意愿
** 命令格式**
update_committee_member 账户名 url 工作意愿 是否广播
**函数原型**
pair<tx_hash_type, signed_transaction> update_committee_member(string committee_name,string url, bool work_status,bool broadcast = false);
**示例**
update_committee_member test www.cocosbcx.io false true
[block:code]
{
  "codes": [
    {
      "code": "update_committee_member test www.cocosbcx.io false true",
      "language": "shell"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "2.2.53 见证人撤回"
}
[/block]
表明否定工作意愿
** 命令格式**
update_witness 账户名 url  块签名公钥  工作意愿 是否广播
**函数原型**
signed_transaction update_witness(string witness_name,string url,string block_signing_key, bool work_status,bool broadcast)
**示例**
update_witness test www.cocosbcx.io xxxxxxxxxxxxxxxxxxxxxxxx false true
[block:code]
{
  "codes": [
    {
      "code": "update_witness test www.cocosbcx.io xxxxxxxxxx false true",
      "language": "shell"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "2.2.54 见证人更新出块公钥或URL"
}
[/block]
** 命令格式**
update_witness 账户名 url  块签名公钥  工作意愿 是否广播
**函数原型**
signed_transaction update_witness(string witness_name,string url,string block_signing_key, bool work_status,bool broadcast)
**示例**
update_witness test www.cocosbcx.io xxxxxxxxxxxxxxxxxxxxxxxx true true

[block:code]
{
  "codes": [
    {
      "code": "update_witness test www.cocosbcx.io xxxxxxxxxxxxxxxxxxxxxxxx true true",
      "language": "shell"
    }
  ]
}
[/block]