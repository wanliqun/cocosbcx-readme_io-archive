---
title: "7.1 Wallet API"
slug: "71-wallet-api"
hidden: true
createdAt: "2019-04-23T08:38:35.489Z"
updatedAt: "2019-05-31T11:31:35.023Z"
---
##7.1.1一般命令

**help**
原型
[block:code]
{
  "codes": [
    {
      "code": "string graphene::wallet::wallet_api::help()const",
      "language": "cplusplus"
    }
  ]
}
[/block]
说明
返回值wallet_api支持的所有命令的列表。
列出每个命令及其参数和返回值类型。
有关单个命令的更详细帮助，使用gethelp()
**返回值**
对应的字符串

**gethelp**
原型
[block:code]
{
  "codes": [
    {
      "code": "string graphene::wallet::wallet_api::gethelp(const string &method)const",
      "language": "cplusplus"
    }
  ]
}
[/block]
说明
返回值单个API命令的详细帮助。
返回值
对应的字符串
参数
method：需要帮助的API命令的名称

**info**
原型
[block:code]
{
  "codes": [
    {
      "code": "variant graphene::wallet::wallet_api::info()",
      "language": "cplusplus"
    }
  ]
}
[/block]
说明
打印连接信息

**about**
原型
[block:code]
{
  "codes": [
    {
      "code": "variant_object graphene::wallet::wallet_api::about()const",
      "language": "cplusplus"
    }
  ]
}
[/block]
说明
返回值客户端版本，graphene的git版本，boost版本，openssl等信息。
返回值
编译时间信息以及客户端和依赖项版本

**network_add_nodes**
原型
[block:code]
{
  "codes": [
    {
      "code": "void graphene::wallet::wallet_api::network_add_nodes(const vector<string> &nodes)",
      "language": "cplusplus"
    }
  ]
}
[/block]
说明
添加节点
参数
&nodes：节点ip

**network_get_connected_peers**
原型
[block:code]
{
  "codes": [
    {
      "code": "vector<variant> graphene::wallet::wallet_api::network_get_connected_peers()",
      "language": "cplusplus"
    }
  ]
}
[/block]
说明
打印链接节点

##7.1.2 钱包信息
** is_new**
原型
[block:code]
{
  "codes": [
    {
      "code": "bool graphene::wallet::wallet_api::is_new()const",
      "language": "cplusplus"
    }
  ]
}
[/block]
说明
检查钱包是否刚刚创建并且尚未设置密码。
set_password将钱包转换为锁定状态。
返回值
如果钱包是新的，则为ture。

**is_locked**
原型
[block:code]
{
  "codes": [
    {
      "code": "bool graphene::wallet::wallet_api::is_locked()const",
      "language": "cplusplus"
    }
  ]
}
[/block]
说明
检查钱包是否已锁定（无法使用其私钥）。
可以通过调用lock()或更改此状态unlock()。
返回值
如果钱包被锁定，则为true。

**lock**
原型
[block:code]
{
  "codes": [
    {
      "code": "void graphene::wallet::wallet_api::lock()",
      "language": "cplusplus"
    }
  ]
}
[/block]
说明
立即锁定钱包。
 
**unlock**
原型
[block:code]
{
  "codes": [
    {
      "code": "void graphene::wallet::wallet_api::unlock(string password)",
      "language": "cplusplus"
    }
  ]
}
[/block]
说明
解锁钱包
钱包保持解锁状态，直到lock被终止或程序退出。
参数
password：以前设置的密码 set_password()

**set_password**
原型
[block:code]
{
  "codes": [
    {
      "code": "void graphene::wallet::wallet_api::set_password(string password)",
      "language": "cplusplus"
    }
  ]
}
[/block]
说明
在钱包上设置新密码。
钱包必须是“新”或“未锁定”才能执行此命令。

**dump_private_keys**
原型
[block:code]
{
  "codes": [
    {
      "code": "map<public_key_type, string> graphene::wallet::wallet_api::dump_private_keys()",
      "language": "cplusplus"
    }
  ]
}
[/block]
说明
转储钱包拥有的所有私钥。
键以WIF格式打印。您可以使用将这些密钥导入另一个钱包import_key()
返回值
包含私钥的映射

**import_key**
原型
[block:code]
{
  "codes": [
    {
      "code": "bool graphene::wallet::wallet_api::import_key(string account_name_or_id, string wif_key)",
      "language": "cplusplus"
    }
  ]
}
[/block]
说明
导入现有帐户的私钥。
私钥必须与指定帐户的密钥匹配。
返回值
如果密钥已导入，则为true
参数
account_name_or_id：拥有密钥的帐户
wif_key：WIF格式的私钥

**import_accounts**
原型
[block:code]
{
  "codes": [
    {
      "code": "map<string, bool> graphene::wallet::wallet_api::import_accounts(string filename, string password)",
      "language": "cplusplus"
    }
  ]
}
[/block]
说明
添加账户文件
参数
filename：存放账户文件的文件名
password：设置的密码

**import_account_keys**
原型
[block:code]
{
  "codes": [
    {
      "code": "bool graphene::wallet::wallet_api::import_account_keys(string filename, string password, string src_account_name, string dest_account_name)",
      "language": "cplusplus"
    }
  ]
}
[/block]
说明
在账户文件中导入账户
参数
filename：账户文件名
password：设置的密码
src_account_name:文件中已有的账户
dest_account_name:校验账户

**import_balance**
原型
[block:code]
{
  "codes": [
    {
      "code": "vector<signed_transaction> graphene::wallet::wallet_api::import_balance(string account_name_or_id, const vector<string> &wif_keys, bool broadcast)",
      "language": "cplusplus"
    }
  ]
}
[/block]
说明
此调用将构建将声明由wif_keys控制的所有余额并将其存入给定帐户的事务。
参数
account_name_or_id：存入的账户名
wif_keys：转出账户的key
broadcast：是否广播

**suggest_brain_key**
原型
[block:code]
{
  "codes": [
    {
      "code": "brain_key_info graphene::wallet::wallet_api::suggest_brain_key()const",
      "language": "cplusplus"
    }
  ]
}
[/block]
说明
建议使用安全的助记词来创建您的帐户。
create_account_with_brain_key()要求你指定一个“助记词”，一个长密码，提供足够的变量来生成密钥。这个函数将提供一个适当的随机字符串，相对比较容易容易写下来。
返回值
一个建议的助记词。

**get_transaction_id**
原型
[block:code]
{
  "codes": [
    {
      "code": "transaction_id_type graphene::wallet::wallet_api::get_transaction_id(const signed_transaction &trx)const",
      "language": "cplusplus"
    }
  ]
}
[/block]
说明
此方法用于将JSON事务转换为其transactin ID。
参数
signed_transaction：需要转换的JSON事务

**get_private_key**
原型
[block:code]
{
  "codes": [
    {
      "code": "string graphene::wallet::wallet_api::get_private_key(public_key_type pubkey)const",
      "language": "cplusplus"
    }
  ]
}
[/block]
说明
获取与公钥对应的WIF私钥。私钥必须已经登录在钱包中。
参数
public_key_type：查询账户的公钥

load_wallet_file
原型
[block:code]
{
  "codes": [
    {
      "code": "bool graphene::wallet::wallet_api::load_wallet_file(string wallet_filename = \"\")",
      "language": "cplusplus"
    }
  ]
}
[/block]
说明
加载指定的Graphene钱包。
在装入新钱包之前，确认当前钱包已关闭。
返回值
如果加载了指定的钱包，则为true
参数
wallet_filename：要加载的钱包JSON文件的文件名。
如果wallet_filename为空，则重新加载现有的钱包文件

**normalize_brain_key**
原型
[block:code]
{
  "codes": [
    {
      "code": "string graphene::wallet::wallet_api::normalize_brain_key(string s)const",
      "language": "cplusplus"
    }
  ]
}
[/block]
说明
转换助记词以减少从内存重新输入密钥时出错的可能性。
这需要用户提供的助记词并将其规范化为用于生成私钥的形式。注意，这个大写所有ASCII字符并将多个空格折叠成一个。
返回值
标准助记词。
参数
s: 用户提供的助记词

**save_wallet_file**
原型
[block:code]
{
  "codes": [
    {
      "code": "void graphene::wallet::wallet_api::save_wallet_file(string wallet_filename = \"\")",
      "language": "cplusplus"
    }
  ]
}
[/block]
说明
将当前钱包保存到指定的文件名。
注意
这个操作不会更改文件名，因此请将此功能视为“将副本另存为...”而不是“另存为...”。 
参数
wallet_filename：要创建或覆盖的新钱包JSON文件的文件名。如果wallet_filename为空，则保存为当前文件名。

[block:code]
{
  "codes": [
    {
      "code": "",
      "language": "text"
    }
  ]
}
[/block]
## 7.1.3 账户操作
**list_my_accounts**
原型
[block:code]
{
  "codes": [
    {
      "code": "vector<account_object> graphene::wallet::wallet_api::list_my_accounts()",
      "language": "cplusplus"
    }
  ]
}
[/block]
说明
列出此钱包控制的所有帐户。返回值拥有其私钥的所有帐户的完整帐户对象的列表。
返回值
帐户对象列表

**list_accounts**
原型
[block:code]
{
  "codes": [
    {
      "code": "map<string, account_id_type> graphene::wallet::wallet_api::list_accounts(const string &lowerbound, uint32_t limit)",
      "language": "cplusplus"
    }
  ]
}
[/block]
说明
列出区块链中注册的所有帐户。返回值所有帐户名及其帐户ID的列表，按帐户名称排序。
使用lowerbound和limit参数可以在列表中翻页。要检索所有帐户，首先设置lowerbound为空字符串""，然后每次迭代，将最后一个帐户名称作为lowerbound下一次list_accounts()调用返回值。
返回值
将帐户名称映射到帐户ID的帐户列表
参数
lowerbound：要返回值的第一个帐户的名称。如果指定的帐户不存在，则列表将从之后的帐户开始lowerbound
limit：要返回值的最大帐户数（最大值：1000）

**list_account_balances**
原型
[block:code]
{
  "codes": [
    {
      "code": "vector<asset> graphene::wallet::wallet_api::list_account_balances(const string &id)",
      "language": "cplusplus"
    }
  ]
}
[/block]
说明
列出帐户的余额。每个帐户可以有多个余额，每个帐户拥有一种资产。返回值的列表将仅包含帐户具有非零余额的资产
返回值
给定帐户余额的列表
参数
id：想要查询余额的帐户的名称或ID

**register_account**
原型
[block:code]
{
  "codes": [
    {
      "code": "signed_transaction graphene::wallet::wallet_api::register_account(string name, public_key_type owner, public_key_type active, string registrar_account, string referrer_account, uint32_t referrer_percent, bool broadcast = false)",
      "language": "cplusplus"
    }
  ]
}
[/block]
说明
在区块上注册第三方的账户。
此功能用于注册您不拥有私钥的帐户。作为注册商时，最终用户将生成自己的私钥并向您发送公钥。注册商将使用此功能代表最终用户注册帐户。
返回值
签署的交易注册帐户
参数
name：帐户名称，区块链必须是唯一的。更短的名字注册更昂贵; 规则仍然在变化，但一般来说，超过8个字符的名称至少有一个数字将是便宜的。
owner：新帐户的所有者密钥
active：新帐户的活动密钥
registrar_account：将支付注册用户费用的帐户
referrer_account：作为推荐人的帐户，可能会收到部分用户的交易费用。如果没有引荐来源，这可以与registrar_account相同。
referrer_percent：未分配给推荐人的区块链未申领的新用户交易费用的百分比（0 - 100）; 其余的将发送给注册商。在构造事务时将乘以GRAPHENE_1_PERCENT。
broadcast：true表示在网络上广播事务

**upgrade_account**
原型
[block:code]
{
  "codes": [
    {
      "code": "signed_transaction graphene::wallet::wallet_api::upgrade_account(string name, bool broadcast)",
      "language": "text"
    }
  ]
}
[/block]
说明
升级用户使用户成为终身账户
返回值
已经升级的账户
参数
name: 要升级的帐户的名称或id
broadcast: 在链上广播为true

**create_account_with_brain_key** 
[block:code]
{
  "codes": [
    {
      "code": "signed_transaction graphene::wallet::wallet_api::create_account_with_brain_key(string brain_key, string account_name, string registrar_account, string referrer_account, bool broadcast = false)",
      "language": "cplusplus"
    }
  ]
}
[/block]
创建一个新帐户并将其注册到区块链上。
返回值
签署的交易注册帐户
参数
brain_key：用于生成帐户私钥的助记词
account_name：帐户名称，在链中必须是唯一的。
registrar_account：支付注册用户费用的帐户
referrer_account：作为推荐人的帐户，可能会收到部分用户的交易费用。如果没有引荐来源，这可以与registrar_account相同。
broadcast：true表示在网络上广播事务

**transfer**
[block:code]
{
  "codes": [
    {
      "code": "signed_transaction graphene::wallet::wallet_api::transfer(string from, string to, string amount, string asset_symbol, string memo, bool broadcast = false)",
      "language": "cplusplus"
    }
  ]
}
[/block]
转账，把资产从一个账户转移到另一个账户。
返回值
交易信息
参数
from：发送资金的帐户的名称或ID
to：接收资金的帐户的名称或ID
amount：发送金额
asset_symbol：要发送的资产的符号或ID
memo：附加到交易的备忘录。备忘录将在交易中加密，并为接收者可读。除了最大事务大小所施加的限制之外没有长度限制，但事务随着事务大小而增加
broadcast：true表示在网络上广播事务
maximum transaction size, but transaction increase with transaction size
broadcast: true to broadcast the transaction on the network

**whitelist_account**
原型
[block:code]
{
  "codes": [
    {
      "code": "signed_transaction graphene::wallet::wallet_api::whitelist_account(string authorizing_account, string account_to_list, account_whitelist_operation::account_listing new_listing_status, bool broadcast = false)",
      "language": "cplusplus"
    }
  ]
}
[/block]
说明
白名单和黑名单帐户，主要用于在白名单资产中进行交易。
帐户可以以白名单或将其列入黑名单的形式自由指定有关其他帐户的意见。此信息仅用于链验证，以确定帐户是否有权以强制执行白名单的资产类型进行交易，但第三方也可以将此信息用于其他用途，只要它不使用白名单资产。
强制执行白名单的资产指定用于维护其白名单的帐户列表，以及用于维护其黑名单的帐户列表。为了使给定帐户A在白名单资产S中持有和交易，A必须被S的白名单权限中的至少一个列入白名单，并且不被S的blacklist_authorities列入黑名单。如果A收到S的余额，并且稍后从允许其保留S的白名单中删除，或者添加到任何黑名单S指定为权威，则A的余额将被冻结，直到A的授权恢复。
返回值
已签名的事务更改白名单状态
参数
authorizing_account：正在执行白名单的帐户
account_to_list：该帐户已列入白名单
new_listing_status：新的白名单状态
broadcast：true表示在网络上广播事务

**get_vesting_balances**
原型
[block:code]
{
  "codes": [
    {
      "code": "vector<vesting_balance_object_with_info> graphene::wallet::wallet_api::get_vesting_balances(string account_name)",
      "language": "cplusplus"
    }
  ]
}
[/block]
说明
获取有关归属平衡对象的信息。
参数
account_name：帐户名称，帐户ID或归属余额对象ID。

**withdraw_vesting**
原型
[block:code]
{
  "codes": [
    {
      "code": "signed_transaction graphene::wallet::wallet_api::withdraw_vesting(string witness_name, string amount, string asset_symbol, bool broadcast = false)",
      "language": "cplusplus"
    }
  ]
}
[/block]
说明
撤回归属余额。
参数
witness_name：见证人的帐户名称，也接受帐户ID或归属余额ID类型。
amount：退出金额。
asset_symbol：要撤回的资产的符号。
broadcast：如果您希望广播交易，则为true

**get_account**
原型
[block:code]
{
  "codes": [
    {
      "code": "account_object graphene::wallet::wallet_api::get_account(string account_name_or_id)const",
      "language": "cplusplus"
    }
  ]
}
[/block]
说明
返回值有关给定帐户的信息。
返回值
存储在区块链中的公共账户数据
参数
account_name_or_id：提供有关信息的帐户的名称或ID

**get_account_id**
原型
[block:code]
{
  "codes": [
    {
      "code": "account_id_type graphene::wallet::wallet_api::get_account_id(string account_name_or_id)const",
      "language": "cplusplus"
    }
  ]
}
[/block]
说明
查找指定帐户的ID。
返回值
指定帐户的ID
参数
account_name_or_id：要查找的帐户的名称

**get_account_history**
原型
[block:code]
{
  "codes": [
    {
      "code": "vector<operation_detail> graphene::wallet::wallet_api::get_account_history(string name, int limit)const",
      "language": "cplusplus"
    }
  ]
}
[/block]
说明
返回值指定帐户的最新操作。
这将返回值操作历史记录对象的列表，这些对象描述帐户上的活动。
返回值
一个列表 operation_history_objects
参数
name：帐户的名称或ID
limit：要返回值的条目数（从最近开始）

**approve_proposal**
原型
[block:code]
{
  "codes": [
    {
      "code": "signed_transaction graphene::wallet::wallet_api::approve_proposal(const string &fee_paying_account, const string &proposal_id, const approval_delta &delta, bool broadcast)",
      "language": "cplusplus"
    }
  ]
}
[/block]
说明
批准或拒绝提案。
返回值
签名版本的交易
参数
fee_paying_account：支付运费费用的帐户。
proposal_id：修改提案。
delta：成员包含创建或删除的批准。在JSON中，您可以保留未定义的空成员。
broadcast：如果希望广播交易，则为true

## 7.1.4 交易信息
**sell_asset**	
原型
[block:code]
{
  "codes": [
    {
      "code": "signed_transaction graphene::wallet::wallet_api::sell_asset(string seller_account, string amount_to_sell, string symbol_to_sell, string min_to_receive, string symbol_to_receive, uint32_t timeout_sec = 0, bool fill_or_kill = false, bool broadcast = false)",
      "language": "cplusplus"
    }
  ]
}
[/block]
说明
下达限价单以试图将一种资产出售给另一种资产。
只要价格至少是min_to_receive/amount_to_sell，区块链将尝试以尽可能多的以symbol_to_receive的价格出售symbol_to_sell。
除交易费外，市场费用将按出售资产和接收资产的发行人的指定，按交换金额的百分比计算。
如果销售资产或接收资产是白名单限制，则只有在卖方位于受限资产类型的白名单中时才会创建订单。
市场订单按它们包含在区块链中的顺序进行匹配。
返回值
签署的交易出售资金
参数
seller_account：提供资产出售的账户，该账户将收到销售收益。
amount_to_sell：出售的资产出售金额（以名义单位计）
symbol_to_sell：要出售的资产的名称或ID
min_to_receive：您愿意收到的最低金额，以换取出售整个amount_to_sell
symbol_to_receive：您希望收到的资产的名称或ID
timeout_sec：如果订单没有立即填写，这是订单在取消之前保留在订单簿上的时间长度，并且未用完的资金将返回值到卖方的帐户
fill_or_kill：如果为true，则只有在立即填写的情况下，订单才会包含在区块链中; 如果为假，则会在账簿上留下未结订单，以填补任何无法立即填写的金额。
broadcast：true表示在网络上广播事务

**borrow_asset**
原型
[block:code]
{
  "codes": [
    {
      "code": "signed_transaction graphene::wallet::wallet_api::borrow_asset(string borrower_name, string amount_to_borrow, string asset_symbol, string amount_of_collateral, bool broadcast = false)",
      "language": "cplusplus"
    }
  ]
}
[/block]
说明
借入资产或更新贷款的债务/抵押比率。
返回值
签署的交易借入资产
参数
borrower_name：与事务关联的帐户的名称或ID。
amount_to_borrow：借入资产的金额。使这个价值为负值以偿还债务。
asset_symbol：借入资产的符号或ID。
amount_of_collateral：要添加到抵押品头寸的支持资产金额。将此否定权归还一些抵押品。支持资产在bitasset_options借用资产中定义。
broadcast：true表示在网络上广播事务

**cancel_order**
原型
[block:code]
{
  "codes": [
    {
      "code": "signed_transaction graphene::wallet::wallet_api::cancel_order(object_id_type order_id, bool broadcast = false)",
      "language": "cplusplus"
    }
  ]
}
[/block]
说明
取消现有订单
返回值
签署的交易取消订单
参数
order_id：要取消的订单的ID
broadcast：true表示在网络上广播事务

**settle_asset**
原型
[block:code]
{
  "codes": [
    {
      "code": "signed_transaction graphene::wallet::wallet_api::settle_asset(string account_to_settle, string amount_to_settle, string symbol, bool broadcast = false)",
      "language": "cplusplus"
    }
  ]
}
[/block]
说明
安排市场发行的资产进行自动结算。
市场发行的债券持有人可以要求强制结算其资产的一部分。这意味着指定的金额将被链锁定并在结算期内持有，之后链将选择保证金的持有人并使用保证金的抵押品购买已结算的资产。此次出售的价格将基于市场发行资产的结算价格。确切的结算价格将是结算时的进料价格，偏移量有利于保证金位置，其中偏移量是global_property_object中设置的区块链参数。
返回值
已签署的交易结算指定资产
参数
account_to_settle：拥有资产的帐户的名称或ID
amount_to_settle：要计划结算的指定资产的金额
symbol：要结算的资产的名称或ID
broadcast：true表示在网络上广播事务

**get_market_history**
原型
[block:code]
{
  "codes": [
    {
      "code": "vector<bucket_object> graphene::wallet::wallet_api::get_market_history(string symbol, string symbol2, uint32_t bucket, fc::time_point_sec start, fc::time_point_sec end)const",
      "language": "cplusplus"
    }
  ]
}
[/block]
说明
获取交易历史
参数
symbol：资产名称或ID
bucket：交易类型

**get_limit_orders**
原型
[block:code]
{
  "codes": [
    {
      "code": "vector<limit_order_object> graphene::wallet::wallet_api::get_limit_orders(string a, string b, uint32_t limit)const",
      "language": "cplusplus"
    }
  ]
}
[/block]
说明
获取限价订单
参数
a,b:资产id
limit：获取的数量

**get_call_orders**
原型
[block:code]
{
  "codes": [
    {
      "code": "vector<call_order_object> graphene::wallet::wallet_api::get_call_orders(string a, uint32_t limit)const",
      "language": "cplusplus"
    }
  ]
}
[/block]
说明
查看订单
参数
a：资产id
limit：获取的数量

**get_settle_orders**
原型
[block:code]
{
  "codes": [
    {
      "code": "vector<force_settlement_object> graphene::wallet::wallet_api::get_settle_orders(string a, uint32_t limit)const",
      "language": "cplusplus"
    }
  ]
}
[/block]
说明
获取已成交的订单
a：资产id
limit：获取的数量


7.1.5 资产调用
**list_assets**
原型
[block:code]
{
  "codes": [
    {
      "code": "vector<asset_object> graphene::wallet::wallet_api::list_assets(const string &lowerbound, uint32_t limit)const",
      "language": "cplusplus"
    }
  ]
}
[/block]
说明
列出区块链上注册的所有资产。
要列出所有资产，""请将下限的空字符串传递到列表开头，然后根据需要进行迭代。
返回值
资产对象列表，按符号排序
参数
lowerbound：要包含在列表中的第一个资产的符号。
limit：要返回值的最大资产数（最大值：100）

**create_asset**
原型
[block:code]
{
  "codes": [
    {
      "code": "signed_transaction graphene::wallet::wallet_api::create_asset(string issuer, string symbol, uint8_t precision, asset_options common, fc::optional<bitasset_options> bitasset_opts, bool broadcast = false)",
      "language": "cplusplus"
    }
  ]
}
[/block]
说明
创建新的用户发行或市场发行的资产。
可以使用更改许多选项 update_asset()
这个函数现在用起来很麻烦，因为必须为选项对象提供原始的JSON数据结构，包括价格和资产ID。
返回值
已签名的交易创建新资产
参数
issuer：将支付费用并成为新资产发行人的帐户的名称或ID。这可以在以后更新
symbol：新资产的股票代码
precision：小数点右边的精度位数必须小于或等于12
common：所有新资产所需的资产选项。请注意，core_exchange_rate在技术上需要存储此新资产的资产ID。由于在创建此操作时不知道此ID，因此创建此价格就像新资产具有实例ID 1一样，并且链将使用新资产的ID覆盖它。
bitasset_opts：BitAssets特有的选项。除非market_issued在common.flags中设置标志，否则这可能为null
broadcast：true表示在网络上广播事务

**update_asset**
原型
[block:code]
{
  "codes": [
    {
      "code": "signed_transaction graphene::wallet::wallet_api::update_asset(string symbol, optional<string> new_issuer, asset_options new_options, bool broadcast = false)",
      "language": "cplusplus"
    }
  ]
}
[/block]
说明
更新资产的核心选项。网络中的所有资产都使用多种选项。这些选项在asset_object :: asset_options结构中枚举。此命令用于更新现有资产的这些选项。
注意
此操作不能用于更新BitAsset特定的选项。update_bitasset()相反。
返回值
已签名的事务更新资产
参数
symbol：要更新的资产的名称或ID
new_issuer：如果更改资产的发行人，新发行人的名称或ID。如果您希望保留资产的发行人，则为null
new_options：新的asset_options对象，它将完全取代现有选项。
broadcast：true表示在网络上广播事务

**update_bitasset**
原型
[block:code]
{
  "codes": [
    {
      "code": "signed_transaction graphene::wallet::wallet_api::update_bitasset(string symbol, bitasset_options new_options, bool broadcast = false)",
      "language": "cplusplus"
    }
  ]
}
[/block]
说明
更新特定于BitAsset的选项。
返回值
已签名的事务更新bitasset
参数
symbol：要更新的资产的名称或ID，必须是市场发行的资产
new_options：新的bitasset_options对象，它将完全取代现有选项。
broadcast：true表示在网络上广播事务

**update_asset_feed_producers**
原型
[block:code]
{
  "codes": [
    {
      "code": "signed_transaction graphene::wallet::wallet_api::update_asset_feed_producers(string symbol, flat_set<string> new_feed_producers, bool broadcast = false)",
      "language": "cplusplus"
    }
  ]
}
[/block]
说明
更新BitAsset的Feed生成帐户集。
BitAssets通过获取来自一组饲料生产者的推荐的中值来选择价格饲料。此命令用于指定哪些帐户可以为给定的BitAsset生成订阅源。
返回值
已签名的事务更新了bitasset的feed生成器
参数
symbol：要更新的资产的名称或ID
new_feed_producers：已授权为资产生成订阅源的帐户名称或ID列表。此列表将完全替换现有列表
broadcast：true表示在网络上广播事务

**publish_asset_feed	**
原型
[block:code]
{
  "codes": [
    {
      "code": "signed_transaction graphene::wallet::wallet_api::publish_asset_feed(string publishing_account, string symbol, price_feed feed, bool broadcast = false)",
      "language": "cplusplus"
    }
  ]
}
[/block]
说明
发布指定资产的资产喂价
资产喂价提供商使用此命令发布市场发行资产的资产喂价。价格反馈用于调整特定市场发行资产的市场。对于资产喂价中的每个值，计算该资产的所有committee_member 喂价的中位数，并使用该值的中位数配置资产的市场。
此命令中的喂价对象包含三个价格：通话价格限制，短价格限制和结算价格。认购限价的结构为（抵押资产）/（债务资产），而短期限价的结构为（待售资产）/（抵押资产）。请注意，资产ID与彼此相反，因此，如果我们发布美元的喂价，则呼叫限制价格将为CORE / USD，短期限价将为USD / CORE。结算价格可以向任一方向翻转，只要它是市场发行资产与其抵押品之间的比率即可。
返回值
已签名的事务更新给定资产的资产喂价
参数
publishing_account：发布资产喂价的帐户
symbol：我们要发布其喂价的资产的名称或ID
feed：price_feed对象包含构成喂价的三个价格
broadcast：true表示在网络上广播事务

**issue_asset**
原型
[block:code]
{
  "codes": [
    {
      "code": "signed_transaction graphene::wallet::wallet_api::issue_asset(string to_account, string amount, string symbol, string memo, bool broadcast = false)",
      "language": "cplusplus"
    }
  ]
}
[/block]
说明
发行资产的新股份。
返回值
已签署的交易发行新股
参数
to_account：接收新股份的帐户的名称或ID
amount：以名义单位发行的金额
symbol：要发行的资产的股票代码
memo：包含在交易中的备忘录，可由收件人阅读
broadcast：true表示在网络上广播事务

**get_asset**
原型
[block:code]
{
  "codes": [
    {
      "code": "asset_object graphene::wallet::wallet_api::get_asset(string asset_name_or_id)const",
      "language": "cplusplus"
    }
  ]
}
[/block]
说明
返回有关给定资产的信息。
返回值
有关存储在区块链中的资产的信息
参数
asset_name_or_id：相关资产的符号或ID

**get_bitasset_data**
原型
[block:code]
{
  "codes": [
    {
      "code": "asset_bitasset_data_object graphene::wallet::wallet_api::get_bitasset_data(string asset_name_or_id)const",
      "language": "cplusplus"
    }
  ]
}
[/block]
说明
返回值给定资产的BitAsset特定数据。市场发行的资产的行为由他们的“BitAsset数据”及其基本资产数据决定get_asset()。
返回值
此资产的BitAsset特定数据
参数
asset_name_or_id：有问题的BitAsset的符号或ID

**fund_asset_fee_pool**
原型
[block:code]
{
  "codes": [
    {
      "code": "signed_transaction graphene::wallet::wallet_api::fund_asset_fee_pool(string from, string symbol, string amount, bool broadcast = false)",
      "language": "cplusplus"
    }
  ]
}
[/block]
说明
支付给定资产的费用池。
用户发行的资产可以选择拥有核心资产池，该资产池自动用于支付使用该资产的任何交易的交易费用（使用资产的核心汇率）。
此命令允许任何人将核心资产存入此费用池。
返回值
已签署的交易为费用池提供资金
参数
from：发送核心资产的帐户的名称或ID
symbol：您希望为其提供资金池的资产的名称或ID
amount：要存入的核心资产的金额
broadcast：true表示在网络上广播事务

**reserve_asset**
原型
[block:code]
{
  "codes": [
    {
      "code": "signed_transaction graphene::wallet::wallet_api::reserve_asset(string from, string amount, string symbol, bool broadcast = false)",
      "language": "cplusplus"
    }
  ]
}
[/block]
说明
销毁给定的用户发布的资产。
此命令会销毁用户发布的资产以减少流通量。
注意
无法销毁市场发行的资产。
返回值
签署的交易销毁资产
参数
from：包含您要刻录的资产的帐户
amount：销毁量，以标称单位表示
symbol：要刻录的资产的名称或ID
broadcast：true表示在网络上广播事务

**global_settle_asset**
原型
[block:code]
{
  "codes": [
    {
      "code": "signed_transaction graphene::wallet::wallet_api::global_settle_asset(string symbol, price settle_price, bool broadcast = false)",
      "language": "cplusplus"
    }
  ]
}
[/block]
说明
强制全球解决特定资产（黑天鹅或预测市场）。
要使用此操作，asset_to_settle必须设置global_settle标志
当执行此操作时，所有余额将在sett_price转换为支持资产，并以结算价格调用所有未结保证金头寸。如果此资产用作其他位集的支持，则这些位集将以其当前喂价价格强制结算。
注意
此操作仅由资产发行者使用，settle_asset()可由拥有该资产的任何用户使用
返回值
已签署的交易结算指定资产
参数
symbol：要强制结算的资产的名称或ID
settle_price：定价的价格
broadcast：true表示在网络上广播事务

## 7.1.6 管理
create_committee_member
原型
[block:code]
{
  "codes": [
    {
      "code": "signed_transaction graphene::wallet::wallet_api::create_committee_member(string owner_account, string url, bool broadcast = false)\n说明",
      "language": "cplusplus"
    }
  ]
}
[/block]
创建由给定帐户拥有的committee_member对象。
一个帐户最多只能有一个committee_member对象。
返回值
签署的交易登记委员会成员
参数
owner_account：创建委员会成员的帐户的名称或ID
url：包含在区块链中的committee_member记录中的URL。客户可以在显示委员会成员列表时显示此信息。可能是空白的。
broadcast：true表示在网络上广播事务

**get_witness**
原型
[block:code]
{
  "codes": [
    {
      "code": "witness_object graphene::wallet::wallet_api::get_witness(string owner_account)",
      "language": "cplusplus"
    }
  ]
}
[/block]
说明
返回值有关给定见证人的信息。
返回值
存储在区块链中的证人信息
参数
owner_account：见证帐户所有者的名称或ID，或见证人的ID

**get_committee_member**
原型
[block:code]
{
  "codes": [
    {
      "code": "committee_member_object graphene::wallet::wallet_api::get_committee_member(string owner_account)",
      "language": "cplusplus"
    }
  ]
}
[/block]
说明
返回值有关给定委员会成员的信息。
返回值
有关委员会成员的信息
参数
owner_account：委员会成员帐户所有者的名称或ID，或委员会成员的ID

list_witnesses
原型
[block:code]
{
  "codes": [
    {
      "code": "map<string, witness_id_type> graphene::wallet::wallet_api::list_witnesses(const string &lowerbound, uint32_t limit)",
      "language": "cplusplus"
    }
  ]
}
[/block]
说明
列出区块链中登记的所有证人。这将返回值一个列表，其中包含拥有证人的所有帐户名称，以及按名称排序的关联证人ID。这列出了证人目前是否投票。
使用lowerbound和limit参数可以在列表中翻页。要检索所有见证，首先设置lowerbound为空字符串""，然后每次迭代，传递最后一个作为lowerbound下一次list_witnesss()调用返回值的见证名称。
返回值
将证人姓名映射到证人ID的证人列表
参数
lowerbound：返回值的第一个证人的名字。如果指定的见证不存在，则列表将从后面的见证开始lowerbound
limit：要返回值的最大证人数（最多：1000）

**list_committee_members**
原型
[block:code]
{
  "codes": [
    {
      "code": "map<string, committee_member_id_type> graphene::wallet::wallet_api::list_committee_members(const string &lowerbound, uint32_t limit)",
      "language": "cplusplus"
    }
  ]
}
[/block]
说明
列出在区块链中注册的所有委员会成员。这将返回值一个列表，其中包含拥有委员会成员的所有帐户名称，以及按名称排序的相关委员会成员ID。这列出了委员会成员是否目前正在投票。
使用lowerbound和limit参数可以在列表中翻页。要检索所有的committee_members，首先设置lowerbound为空字符串""，然后每次迭代，将最后一个委员会成员名称作为lowerbound下一次list_committee_members()调用返回值。
返回值
委员会成员名单将委员会成员名称映射到委员会成员ID
参数
lowerbound：要返回值的第一个委员会成员的名字。如果指定的committee_member不存在，则列表将从之后的委员会成员开始lowerbound
limit：要返回值的最大委员会成员数（最多：1000）

**create_witness**
原型
[block:code]
{
  "codes": [
    {
      "code": "signed_transaction graphene::wallet::wallet_api::create_witness(string owner_account, string url, bool broadcast = false)",
      "language": "cplusplus"
    }
  ]
}
[/block]
说明
创建给定帐户拥有的见证对象。
一个帐户最多只能有一个见证对象。
返回值
签署的交易登记证人
参数
owner_account：创建见证人的帐户的名称或ID
url：要包含在区块链中的见证记录中的URL。客户可以在显示证人列表时显示此信息。可能是空白的。
broadcast：true表示在网络上广播事务

**update_witness**
原型
[block:code]
{
  "codes": [
    {
      "code": "signed_transaction graphene::wallet::wallet_api::update_witness(string witness_name, string url, string block_signing_key, bool broadcast = false)",
      "language": "cplusplus"
    }
  ]
}
[/block]
说明
更新给定帐户拥有的见证对象。
参数
witness_name：见证人所有者帐户的名称。还接受所有者帐户的ID或见证人的ID。
url：与create_witness相同。空字符串使它保持不变。
block_signing_key：新块签名公钥。空字符串使它保持不变。
broadcast：如果您希望广播交易，则为true。

**create_worker**
原型
[block:code]
{
  "codes": [
    {
      "code": "signed_transaction graphene::wallet::wallet_api::create_worker(string owner_account, time_point_sec work_begin_date, time_point_sec work_end_date, share_type daily_pay, string name, string url, variant worker_settings, bool broadcast = false)",
      "language": "cplusplus"
    }
  ]
}
[/block]
说明
创建一个工作对象。
参数
owner_account：拥有该工人并将获得支付的帐户
work_begin_date：工作开始时
work_end_date：当工作结束时
daily_pay：每日支付金额（非每个缺货间隔）
name：任何文字
url：任何文字
worker_settings：{“type”：“burn”|“退款”|“归属”，“pay_vesting_period_days”：x}
broadcast：如果您希望广播交易，则为true。

**update_worker_votes**
原型
[block:code]
{
  "codes": [
    {
      "code": "signed_transaction graphene::wallet::wallet_api::update_worker_votes(string account, worker_vote_delta delta, bool broadcast = false)",
      "language": "cplusplus"
    }
  ]
}
[/block]
说明
更新工人的投票
参数
account：将支付费用并更新投票的帐户。
delta：{“vote_for”：[...]，“vote_against”：[...]，“vote_abstain”：[...]}
broadcast：如果您希望广播交易，则为true。

**vote_for_committee_member**
原型
[block:code]
{
  "codes": [
    {
      "code": "signed_transaction graphene::wallet::wallet_api::vote_for_committee_member(string voting_account, string committee_member, bool approve, bool broadcast = false)",
      "language": "cplusplus"
    }
  ]
}
[/block]
说明
为特定委员会成员投票。
帐户可以发布他们批准的所有committee_memberes的列表。此命令允许您从此列表中添加或删除committee_memberes。每个账户的投票根据投票统计时该账户拥有的核心资产的份额加权。
注意
你不能投票反对委员会成员，你只能投票给委员会成员或不投票给委员会成员。
返回值
签署的交易改变了对给定委员会成员的投票
参数
voting_account：使用其股票进行投票的帐户的名称或ID
committee_member：committee_member'所有者帐户的名称或ID
approve：如果您希望投票赞成该委员会成员，则为true，如果您不赞成该委员会成员，则为false
broadcast：如果您希望广播交易，则为true

**vote_for_witness**
原型
[block:code]
{
  "codes": [
    {
      "code": "signed_transaction graphene::wallet::wallet_api::vote_for_witness(string voting_account, string witness, bool approve, bool broadcast = false)",
      "language": "cplusplus"
    }
  ]
}
[/block]
说明
为特定见证人投票。
帐户可以发布他们批准的所有见证人的列表。此命令允许您从此列表中添加或删除见证人。每个账户的投票根据投票统计时该账户拥有的核心资产的份额加权。
注意
你不能投票反对见证人，你只能投票给证人或不投票给见证人。
返回值
签署的交易改变了对给定见证人的投票
参数
voting_account：使用其股票进行投票的帐户的名称或ID
witness：见证人所有者帐户的名称或ID
approve：如果您希望投票支持该见证人，则为true，如果您拒绝投票支持该见证人，则为false
broadcast：如果您希望广播交易，则为true

**set_voting_proxy**
原型
[block:code]
{
  "codes": [
    {
      "code": "signed_transaction graphene::wallet::wallet_api::set_voting_proxy(string account_to_modify, optional<string> voting_account, bool broadcast = false)",
      "language": "cplusplus"
    }
  ]
}
[/block]
说明
设置帐户的投票代理。
如果用户不希望积极参与投票，他们可以选择允许其他帐户投票。
设置投票代理不会从区块链中删除您之前的投票，它们会保留在那里但会被忽略。如果您之后取消了您的投票代理，您之前的投票将再次生效。
此设置可以随时更改。
返回值
已签名的交易更改您的投票代理设置
参数
account_to_modify：要更新的帐户的名称或ID
voting_account：授权投票account_to_modify的股票的帐户的名称或ID，或null以投票您自己的股票
broadcast：如果您希望广播交易，则为true

**set_desired_witness_and_committee_member_count**
原型
[block:code]
{
  "codes": [
    {
      "code": "signed_transaction graphene::wallet::wallet_api::set_desired_witness_and_committee_member_count(string account_to_modify, uint16_t desired_number_of_witnesses, uint16_t desired_number_of_committee_members, bool broadcast = false)",
      "language": "cplusplus"
    }
  ]
}
[/block]
说明
设置对系统中证人和委员会成员数量的投票。
每个帐户都可以就活跃的委员会成员/活跃见证人名单中有多少委员会成员和有多少证人发表意见。它们彼此独立。你必须投票批准至少与你声称应该有的委员会成员或证人一样多（你不能说应该有20个委员会成员但只能投票10个）。
区块链参数中的每个组都有最大值（当前默认为1001）。
此设置可以随时更改。如果您的帐户具有投票代理集，则您的首选项将被忽略。
返回值
已签名的交易更改您的投票代理设置
参数
account_to_modify：要更新的帐户的名称或ID
desired_number_of_witnesses：所需数量的活跃证人
desired_number_of_committee_members：所需的活跃委员会成员人数
broadcast：如果您希望广播交易，则为true

**propose_parameter_change**
原型
[block:code]
{
  "codes": [
    {
      "code": "signed_transaction graphene::wallet::wallet_api::propose_parameter_change(const string &proposing_account, fc::time_point_sec expiration_time, const variant_object &changed_values, bool broadcast = false)",
      "language": "cplusplus"
    }
  ]
}
[/block]
说明
创建事务以建议参数更改。
如果需要原子变化，可以指定多个参数。
返回值
签名版本的交易
参数
proposing_account：支付费用以提出tx的帐户
expiration_time：时间戳指定提案何时生效或到期。
changed_values：要改变的价值观; 所有其他链参数都使用默认值填充
broadcast：如果您希望广播交易，则为true

**propose_fee_change**
原型
[block:code]
{
  "codes": [
    {
      "code": "signed_transaction graphene::wallet::wallet_api::propose_fee_change(const string &proposing_account, fc::time_point_sec expiration_time, const variant_object &changed_values, bool broadcast = false)",
      "language": "cplusplus"
    }
  ]
}
[/block]
说明
建议更改费用。
返回值
签名版本的交易
参数
proposing_account：支付费用以提出tx的帐户
expiration_time：时间戳指定提案何时生效或到期。
changed_values：运营类型地图到新费用。可以通过名称或ID指定操作。“比例”键改变了比例。所有其他操作将保持当前值。
broadcast：如果您希望广播交易，则为true


## 7.1.7 隐私模式
**set_key_label**
原型
[block:code]
{
  "codes": [
    {
      "code": "bool graphene::wallet::wallet_api::set_key_label(public_key_type key, string label)",
      "language": "cplusplus"
    }
  ]
}
[/block]
说明
此方法可用于设置公钥的标签
注意
没有两个公钥可以具有相同的标签。
返回值
如果标签已设置，则为true，否则为false
参数
key:公钥
label:标签

**get_key_label**
原型
string graphene::wallet::wallet_api::get_key_label(public_key_type key)const
说明
获取公钥的标签
参数
key：公钥
7.3. get_public_key
public_key_type graphene::wallet::wallet_api::get_public_key(string label)const
返回值
与给定标签关联的公钥
7.4. get_blind_accounts
原型
map<string, public_key_type> graphene::wallet::wallet_api::get_blind_accounts()const
返回值
所有的私密账户
7.5. get_my_blind_accounts
原型
map<string, public_key_type> graphene::wallet::wallet_api::get_my_blind_accounts()const
返回值
所有这个钱包存在私钥的私密账户
7.6. get_blind_balances
原型
vector<asset> graphene::wallet::wallet_api::get_blind_balances(string key_or_label)
说明
可以通过给定帐户密钥或标签声明的所有私密账户的总余额
7.7. create_blind_account
原型
public_key_type graphene::wallet::wallet_api::create_blind_account(string label, string brain_key)
说明
为给定的注记词生成一个新的私密账户，并为其分配给定的标签。
参数
label：标签
brain_key：注记词
7.8. transfer_to_blind
原型
blind_confirmationgraphene::wallet::wallet_api::transfer_to_blind(string from_account_id_or_name, string asset_symbol, vector<pair<string, string>> to_amounts, bool broadcast = false)
说明
使用不公开转移将公共余额转移到一个或多个私密账户。
参数
asset_symbol：资产符号
to_amounts：从公钥或标签映射到金额
from_account_id_or_name：使用私密转账将公共余额转移到一个或多个私密账户
7.9. transfer_from_blind
原型
blind_confirmationgraphene::wallet::wallet_api::transfer_from_blind(string from_blind_account_key_or_label, string to_account_id_or_name, string amount, string asset_symbol, bool broadcast = false)
说明
将资金从一组私密账户余额转入公共账户余额。
参数
asset_symbol：资产符号
to_amounts：从公钥或标签映射到金额
from_account_id_or_name：使用私密转账将公共余额转移到一个或多个私密账户
7.10. blind_transfer
原型
blind_confirmationgraphene::wallet::wallet_api::blind_transfer(string from_key_or_label, string to_key_or_label, string amount, string symbol, bool broadcast = false)
说明
用于从一组私密账户余额转移到另一组
参数
asset_symbol：资产符号
to_amounts：从公钥或标签映射到金额
from_account_id_or_name：使用私密转账将公共余额转移到一个或多个私密账户
7.11. blind_history
原型
vector<blind_receipt> graphene::wallet::wallet_api::blind_history(string key_or_account)
返回值
所有收据组成的特定私人账户
参数
key_or_account：私钥或账户名
7.12. receive_blind_transfer
原型
blind_receipt graphene::wallet::wallet_api::receive_blind_transfer(string confirmation_receipt, string opt_from, string opt_memo)
说明
给定确认收据后，此方法将解析它以获得私人账户余额并确认它存在于区块链中。如果它存在，那么它将报告收到的金额和发送者。
参数
opt_from：如果不为空并且发件人是未知的公钥，则将为未知的公钥提供标签 opt_from
confirmation_receipt：base58编码的隐形确认
opt_memo：此传输的自定义标签将保存在本地钱包文件中

________________________________________
8.	区块链检查
8.1. get_block
原型
optional<signed_block_with_info> graphene::wallet::wallet_api::get_block(uint32_t num)
说明

8.2. get_account_count
原型
uint64_t graphene::wallet::wallet_api::get_account_count()const
说明
返回值区块链上注册的帐户数
返回值
注册帐号的数量
8.3. get_global_properties
原型
global_property_object graphene::wallet::wallet_api::get_global_properties()const
说明
返回值链缓慢变化的设置。此对象包含已修复的区块链的所有属性，或者每个维护间隔（每天）仅更改一次的所有属性，例如当前的证人列表，委员会成员，阻止间隔等。
返回值
全局属性
8.4. get_dynamic_global_properties
原型
dynamic_global_property_object graphene::wallet::wallet_api::get_dynamic_global_properties()const
说明
返回块链快速变化的设置。返回值的对象包含更改每个块间隔的信息，例如头部块编号，下一个见证人等。
返回值
动态全局属性
8.5. get_object
原型
variant graphene::wallet::wallet_api::get_object(object_id_type id)const
说明
返回与给定id对应的区块链对象。
此通用函数可用于从分配了ID的区块链中检索任何对象。某些类型的对象具有专门的便利功能来返回值其对象，例如，资产具有get_asset()帐户get_account()，但此功能适用于任何对象。
返回值
请求的对象
参数
id：要返回值的对象的id
________________________________________
9.	事务发生器
9.1. begin_builder_transaction
原型
transaction_handle_typegraphene::wallet::wallet_api::begin_builder_transaction()
说明
创建一个新的事务发生器
9.2. add_operation_to_builder_transaction
原型
void graphene::wallet::wallet_api::add_operation_to_builder_transaction(transaction_handle_typetransaction_handle, const operation &op)
说明
向事务发生器中添加一个操作
参数
transaction_handle_typetransaction_handle：事务发生器的编号
operation：执行的op
9.3. replace_operation_in_builder_transaction
原型
void graphene::wallet::wallet_api::replace_operation_in_builder_transaction(transaction_handle_typehandle, unsigned operation_index, const operation &new_op)
说明
transaction_handle_typetransaction_handle：事务发生器的编号
operation_index：原先的op
operation：新的的op
9.4. set_fees_on_builder_transaction
原型
asset graphene::wallet::wallet_api::set_fees_on_builder_transaction(transaction_handle_typehandle, string fee_asset = GRAPHENE_SYMBOL)
说明
设定原子交易费用
参数
transaction_handle_typetransaction_handle：事务发生器的编号
fee_asset：设定的费用
9.5. preview_builder_transaction
原型
transaction graphene::wallet::wallet_api::preview_builder_transaction(transaction_handle_typehandle)
说明
查看事务发生器执行的操作
参数
transaction_handle_typetransaction_handle：事务发生器的编号
9.6. sign_builder_transaction
原型
signed_transaction graphene::wallet::wallet_api::sign_builder_transaction(transaction_handle_typetransaction_handle, bool broadcast = true)
说明
给事务发生器签名（执行事务发生器）
参数
transaction_handle_typetransaction_handle：事务发生器的编号
9.7. propose_builder_transaction
原型
signed_transaction graphene::wallet::wallet_api::propose_builder_transaction(transaction_handle_typehandle, time_point_sec expiration = time_point::now() + fc::minutes(1), uint32_t review_period_seconds = 0, bool broadcast = true)
说明
提议事务发生器

9.8. propose_builder_transaction2
原型
signed_transaction graphene::wallet::wallet_api::propose_builder_transaction2(transaction_handle_typehandle, string account_name_or_id, time_point_sec expiration = time_point::now() + fc::minutes(1), uint32_t review_period_seconds = 0, bool broadcast = true)
说明
另一个提议事务发生器
9.9. remove_builder_transaction
原型
void graphene::wallet::wallet_api::remove_builder_transaction(transaction_handle_typehandle)
说明
删除事务发生器
参数
transaction_handle_typetransaction_handle：事务发生器的编号

9.10. serialize_transaction
string graphene::wallet::wallet_api::serialize_transaction(signed_transaction tx)const
说明
将JSON格式的signed_transaction转换为其二进制表示形式。
返回值
交易的二进制形式。它不会被十六进制编码，这将返回值一个原始字符串，其中可能嵌入了空字符
参数
tx：要序列化的事务
9.11. sign_transaction
原型
signed_transaction graphene::wallet::wallet_api::sign_transaction(signed_transaction tx, bool broadcast = false)
说明
签署交易。
给定仅缺少签名的完全形成的事务，这使得事务具有必要的密钥并且可选地广播事务
返回值
签名版本的交易
参数
tx：未签名的交易
broadcast：如果您希望广播交易，则为true
9.12. get_prototype_operation
原型
operation graphene::wallet::wallet_api::get_prototype_operation(string operation_type)
说明
返回表示给定区块链操作的未初始化对象。
将返回给定类型的默认初始化对象; 当我们还没有用于创建区块链支持的所有操作的自定义命令时，它可以在钱包的早期开发期间使用。
可以使用事务构建器创建区块链支持的任何操作add_operation_to_builder_transaction()，但是要从CLI执行此操作，您需要知道操作的JSON形式是什么样的。这将为您提供一个可以填写的模板。
返回值
给定类型的默认构造操作
参数
operation_type：要返回值的操作类型，必须是其中定义的操作之一graphene/chain/operations.hpp（例如，“global_parameters_update_operation”）