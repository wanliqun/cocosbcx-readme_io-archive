---
title: "7.1 Database API"
slug: "74-database-api"
hidden: false
createdAt: "2019-04-23T08:05:09.816Z"
updatedAt: "2020-04-29T02:04:34.305Z"
---
## 7.1.1对象

**get_objects** 

原型
[block:code]
{
  "codes": [
    {
      "code": "fc::variants graphene::app::database_api::get_objects(const vector<object_id_type> &ids)const",
      "language": "cplusplus"
    }
  ]
}
[/block]

说明
获取与提供的ID对应的对象。
如果任何提供的ID未映射到对象，则在其位置返回值null变量。
返回值
检索的对象按ID中提到的顺序检索
参数
ids：要检索的对象的ID

## 7.1.2 订阅

**set_subscribe_callback** 

原型
[block:code]
{
  "codes": [
    {
      "code": "void graphene::app::database_api::set_subscribe_callback(std::function<void(const variant&)> cb, bool notify_remove_create, )\n",
      "language": "cplusplus"
    }
  ]
}
[/block]
说明
注册一个回调句柄，然后可以用来订阅对象数据库的更改。
参数
cb：要注册的回调句柄
nofity_remove_create：是否订阅通用对象创建和删除事件。如果将其设置为true，则无论客户端是否订阅了对象，API服务器都会将所有新创建的对象和所有新删除的对象的ID通知给客户端。默认情况下，API服务器不允许订阅通用事件，可以在服务器启动时更改这些事件。

**set_pending_transaction_callback **

原型
[block:code]
{
  "codes": [
    {
      "code": "void graphene::app::database_api::set_pending_transaction_callback(std::function<void(constvariant &signed_transaction_object)> cb)",
      "language": "cplusplus"
    }
  ]
}
[/block]
说明
注册一个回调句柄，当事务被推送到数据库时会收到通知。
注意：事务可以推送到数据库，并在处理时，在包含在块之前和之后多次从数据库中弹出。每次推送完成后，都会通知客户端。
参数
cb：要注册的回调句柄

**set_block_applied_callback **

原型
[block:code]
{
  "codes": [
    {
      "code": "void graphene::app::database_api::set_block_applied_callback(std::function<void(const variant &block_id)> cb)",
      "language": "cplusplus"
    }
  ]
}
[/block]
说明
注册一个回调句柄，当块被推送到数据库时会收到通知。
参数
cb：要注册的回调句柄

**cancel_all_subscriptions **

原型
[block:code]
{
  "codes": [
    {
      "code": "void graphene::app::database_api::cancel_all_subscriptions()",
      "language": "cplusplus"
    }
  ]
}
[/block]
说明
停止接收任何通知。
这取消了所有订阅市场和对象的订阅。

## 7.1.3 块和事务
**get_block_header **

原型
[block:code]
{
  "codes": [
    {
      "code": "optional<block_header> graphene::app::database_api::get_block_header(uint32_t block_num)const",
      "language": "cplusplus"
    }
  ]
}
[/block]
说明
检索块头。
返回值
引用块的标头，如果未找到匹配块，则返回值null
参数
block_num：应返回值其标题的块的高度

**get_block **

原型
[block:code]
{
  "codes": [
    {
      "code": "optional<signed_block> graphene::app::database_api::get_block(uint32_t block_num)const",
      "language": "cplusplus"
    }
  ]
}
[/block]
说明
检索完整的已签名块。
返回值
引用的块，如果未找到匹配的块，则返回值null
参数
block_num：要返回值的块的高度

**get_transaction **

原型
[block:code]
{
  "codes": [
    {
      "code": "processed_transaction graphene::app::database_api::get_transaction(uint32_t block_num, uint32_t trx_in_block)const",
      "language": "cplusplus"
    }
  ]
}
[/block]
说明
用于获取单个事务。
参数
block_num：块的高度
trx_in_block：事务所在块

**get_recent_transaction_by_id** 

原型
[block:code]
{
  "codes": [
    {
      "code": "optional<signed_transaction> graphene::app::database_api::get_recent_transaction_by_id(const string &id)const",
      "language": "cplusplus"
    }
  ]
}
[/block]
说明
如果事务尚未到期，则此方法将返回值给定ID的事务，否则将返回值NULL（如果未知）。仅仅因为它未知并不意味着它没有包含在区块链中。
参数
transaction_id_type：交易id

## 7.1.4 全局

**get_chain_properties **

原型
[block:code]
{
  "codes": [
    {
      "code": "chain_property_object graphene::app::database_api::get_chain_properties()const",
      "language": "cplusplus"
    }
  ]
}
[/block]
说明
检索链所有的全局属性

**get_global_properties **

原型
[block:code]
{
  "codes": [
    {
      "code": "global_property_object graphene::app::database_api::get_global_properties()const",
      "language": "cplusplus"
    }
  ]
}
[/block]
说明
检索当前链的全局属性

**get_config** 

原型
[block:code]
{
  "codes": [
    {
      "code": "fc::variant_object graphene::app::database_api::get_config()const",
      "language": "cplusplus"
    }
  ]
}
[/block]
说明
检索编译时常量。

**get_chain_id** 

原型
[block:code]
{
  "codes": [
    {
      "code": "chain_id_type graphene::app::database_api::get_chain_id()const",
      "language": "cplusplus"
    }
  ]
}
[/block]
说明
获取链ID。

**get_dynamic_global_properties** 

原型
[block:code]
{
  "codes": [
    {
      "code": "chain_id_type graphene::app::database_api::get_dynamic_global_properties()const",
      "language": "cplusplus"
    }
  ]
}
[/block]
说明
检索当前的动态全局属性


## 7.1.5 KEY

**get_key_references **

原型
[block:code]
{
  "codes": [
    {
      "code": "vector<vector<account_id_type>> graphene::app::database_api::get_key_references(vector<public_key_type> key)const",
      "language": "cplusplus"
    }
  ]
}
[/block]
说明
获得数据库中key的references
参数
key：所指定的key

## 7.1.6 账号

**get_accounts **

原型
[block:code]
{
  "codes": [
    {
      "code": "vector<optional<account_object>> graphene::app::database_api::get_accounts(const vector<std::string> &account_ids)const",
      "language": "cplusplus"
    }
  ]
}
[/block]
说明
按ID获取帐户列表。
此函数的语义与get_objects相同
返回值
与提供的ID对应的帐户
参数
account_ids：要检索的帐户的ID

**get_full_accounts** 

原型
[block:code]
{
  "codes": [
    {
      "code": "std::map<string, full_account> graphene::app::database_api::get_full_accounts(constvector<string> &names_or_ids, bool subscribe)",
      "language": "cplusplus"
    }
  ]
}
[/block]
说明
获取与指定帐户相关的所有对象并订阅更新。
此函数获取给定帐户的所有相关对象，并订阅对给定帐户的更新。如果names_or_ids中的任何字符串无法绑定到帐户，则该输入将被忽略。将检索和订阅所有其他帐户。
返回值
从names_or_ids到相应帐户的字符串映射
参数
subscribe：订阅与否
names_or_ids：每个项目必须是要检索的帐户的名称或ID

**get_account_by_name **

原型
[block:code]
{
  "codes": [
    {
      "code": "optional<account_object> graphene::app::database_api::get_account_by_name(string name)const",
      "language": "cplusplus"
    }
  ]
}
[/block]
**get_account_references **

原型
[block:code]
{
  "codes": [
    {
      "code": "vector<account_id_type> graphene::app::database_api::get_account_references(const std::string account_id)const",
      "language": "cplusplus"
    }
  ]
}
[/block]
返回值
所有引用其所有者或活动权限中的密钥或帐户ID的帐户。

**lookup_account_names** 

原型
[block:code]
{
  "codes": [
    {
      "code": "vector<optional<account_object>> graphene::app::database_api::lookup_account_names(constvector<string> &account_names)const",
      "language": "cplusplus"
    }
  ]
}
[/block]
说明
按名称获取帐户列表。
此函数的语义与get_objects相同
返回值
持有提供名称的帐户
参数
account_names：要检索的帐户的名称

 **lookup_accounts** 

原型
[block:code]
{
  "codes": [
    {
      "code": "map<string, account_id_type> graphene::app::database_api::lookup_accounts(const string &lower_bound_name, uint32_t limit)const",
      "language": "cplusplus"
    }
  ]
}
[/block]
说明
获取已注册帐户的名称和ID。
返回值
帐户名称映射到相应的ID
参数
lower_bound_name：要返回值的名字的下限
limit：要返回值的最大结果数不得超过1000

**get_account_count **

原型
[block:code]
{
  "codes": [
    {
      "code": "uint64_t graphene::app::database_api::get_account_count()const",
      "language": "cplusplus"
    }
  ]
}
[/block]
说明
获取区块链注册的帐户总数。

## 7.1.7 余额

**get_account_balances** 

原型
[block:code]
{
  "codes": [
    {
      "code": "vector<asset> graphene::app::database_api::get_account_balances(const std::string &account_id, const flat_set<asset_id_type> &assets)const",
      "language": "clojure"
    }
  ]
}
[/block]
说明
获取各种资产的帐户余额。
返回值
帐户余额
参数
account_id：要获得余额的帐户的ID
assets：要获得余额的资产的ID; 如果为空，则获取所有资产帐户中的余额

**get_named_account_balances** 

原型
[block:code]
{
  "codes": [
    {
      "code": "vector<asset> graphene::app::database_api::get_named_account_balances(const std::string &name, const flat_set<asset_id_type> &assets)const",
      "language": "cplusplus"
    }
  ]
}
[/block]
说明
在语义上等同于get_account_balances，但是使用名称而不是ID。
参数
account_name：要获得余额的帐户名称
assets：要获得余额的资产的ID; 如果为空，则获取所有资产帐户中的余额

**get_balance_objects** 

原型
[block:code]
{
  "codes": [
    {
      "code": "vector<balance_object> graphene::app::database_api::get_balance_objects(constvector<address> &addrs)const",
      "language": "cplusplus"
    }
  ]
}
[/block]
返回值
一组地址的所有无人认领的余额对象
参数
addrs：要获得余额对象的一组地址

**get_vested_balances** 

原型
[block:code]
{
  "codes": [
    {
      "code": "vector<asset> graphene::app::database_api::get_vested_balances(const vector<balance_id_type> &objs)const",
      "language": "cplusplus"
    }
  ]
}
[/block]
说明
获取已经解冻的资产余额
参数
objs：资产名或ID

**get_vesting_balances **

原型
[block:code]
{
  "codes": [
    {
      "code": "vector<vesting_balance_object> graphene::app::database_api::get_vesting_balances(conststd::string account_id)const",
      "language": "cplusplus"
    }
  ]
}
[/block]
说明
获取正在冻结的资产余额
参数
account_id：账户id


## 7.1.8 资产

**get_assets** 

原型
[block:code]
{
  "codes": [
    {
      "code": "vector<optional<asset_object>> graphene::app::database_api::get_assets(constvector<std::string> &asset_symbols_or_ids)const",
      "language": "cplusplus"
    }
  ]
}
[/block]
说明
按ID获取资产列表。
此函数的语义与get_objects相同
返回值
与提供的ID对应的资产
参数
asset_symbols_or_ids：要检索的资产的符号名称或ID

**list_assets **

原型
[block:code]
{
  "codes": [
    {
      "code": "vector<asset_object> graphene::app::database_api::list_assets(const string &lower_bound_symbol, uint32_t limit)const",
      "language": "cplusplus"
    }
  ]
}
[/block]
原型按符号名称按字母顺序获取资产。
返回值
找到的资产
参数
lower_bound_symbol：要检索的符号名称的下限
limit：要获取的最大资产数（不得超过101）

**lookup_asset_symbols** 

原型
[block:code]
{
  "codes": [
    {
      "code": "vector<optional<asset_object>> graphene::app::database_api::lookup_asset_symbols(constvector<string> &symbols_or_ids)const",
      "language": "cplusplus"
    }
  ]
}
[/block]
说明
按符号获取资产列表。
此函数的语义与get_objects相同
返回值
与提供的符号或ID对应的资产
参数
asset_symbols：要检索的资产的符号或字符串ID


## 7.1.9 市场与喂价

**get_order_book** 

原型
[block:code]
{
  "codes": [
    {
      "code": "order_book graphene::app::database_api::get_order_book(const string &base, const string &quote, unsigned limit = 50)const",
      "language": "cplusplus"
    }
  ]
}
[/block]
说明
返回值市场基础的订单簿：quote。
返回值
市场订单
参数
base：第一个资产的字符串名称
quote：第二个资产的字符串名称
depth：订单簿。每个要求和出价的深度，最高限额为50.优先考虑每个要求最低的

**get_limit_orders **

原型
[block:code]
{
  "codes": [
    {
      "code": "vector<limit_order_object> graphene::app::database_api::get_limit_orders(std::string a, std::string b, uint32_t limit)const",
      "language": "cplusplus"
    }
  ]
}
[/block]
说明
获取特定市场的限价单。
返回值
限价单，从最低价到最高价
参数
a：出售资产的符号或ID
b：正在购买的资产的符号或ID
limit：要检索的最大订单数

**get_call_orders** 

原型
[block:code]
{
  "codes": [
    {
      "code": "vector<call_order_object> graphene::app::database_api::get_call_orders(const std::string &a, uint32_t limit)const",
      "language": "cplusplus"
    }
  ]
}
[/block]
获取给定资产中的呼叫订单。
返回值
通话订单，从最早的订单到最新订购
参数
a：被调用资产的符号或ID
limit：要检索的最大订单数

**get_settle_orders** 

原型
[block:code]
{
  "codes": [
    {
      "code": "vector<force_settlement_object> graphene::app::database_api::get_settle_orders(conststd::string &a, uint32_t limit)const",
      "language": "cplusplus"
    }
  ]
}
[/block]
说明
获取给定资产的强制结算订单。
返回值
结算订单，从最早的结算日期到最晚的订购
参数
a：已结算资产的符号或ID
limit：要检索的最大订单数

**get_margin_positions** 

原型
[block:code]
{
  "codes": [
    {
      "code": "vector<call_order_object> graphene::app::database_api::get_margin_positions(const std::string account_id_or_name)const",
      "language": "cplusplus"
    }
  ]
}
[/block]
返回值
给定帐户ID或名称的所有未结保证金。
参数
account_id_or_name：账户名或id

**subscribe_to_market** 

原型
[block:code]
{
  "codes": [
    {
      "code": "void graphene::app::database_api::subscribe_to_market(std::function<void(const variant&)> callback, const std::string &a, const std::string &b )",
      "language": "cplusplus"
    }
  ]
}
[/block]
说明
当两个资产之间的市场中的活动订单发生变化时请求通知。
回调将传递包含向量<pair <operation，operation_result >>的变体。该向量将按顺序包含改变市场的操作及其结果。
参数
callback：市场变化时调用的回调方法
a：第一个资产符号或ID
b：第二个资产符号或ID

**unsubscribe_from_market** 

原型
[block:code]
{
  "codes": [
    {
      "code": "void graphene::app::database_api::unsubscribe_from_market(const std::string &a, conststd::string &b)",
      "language": "cplusplus"
    }
  ]
}
[/block]
说明
取消订阅特定市场的更新。
参数
a：第一个资产符号ID
b：第二个资产符号ID

**get_ticker** 

原型
[block:code]
{
  "codes": [
    {
      "code": "market_ticker graphene::app::database_api::get_ticker(const string &base, const string &quote)const",
      "language": "text"
    }
  ]
}
[/block]
说明
返回市场资产代码
返回值
过去24小时的市场代码。
参数
a：第一个资产的字符串名称
b：第二个资产的字符串名称

**get_24_volume** 

原型
[block:code]
{
  "codes": [
    {
      "code": "market_volume graphene::app::database_api::get_24_volume(const string &base, const string &quote)const",
      "language": "cplusplus"
    }
  ]
}
[/block]
说明
返回市场资产24小时交易量
返回值
过去24小时的市场交易量
参数
a：第一个资产的字符串名称
b：第二个资产的字符串名称

**get_trade_history **

原型
[block:code]
{
  "codes": [
    {
      "code": "vector<market_trade> graphene::app::database_api::get_trade_history(const string &base, const string &quote, fc::time_point_sec start, fc::time_point_sec stop, unsigned limit = 100)const",
      "language": "cplusplus"
    }
  ]
}
[/block]
说明
返回最近的交易市场基础报价，按最近一次的时间排序。
注意
目前不支持跨时区。时间必须是UTC。范围是[stop, start)。如果同一秒内发生的交易超过100次，则此API仅返回前100条记录，可以使用另一个API get_trade_history_by_sequence查询其余的记录。
返回值
近期市场交易
参数
base：基础资产的符号或ID
quote：报价资产的符号或ID
start：作为UNIX时间戳的开始时间，要检索的最新交易
stop：停止时间作为UNIX时间戳，是最早检索的交易
limit：要检索的trasactions数量，上限为100。

7.1.10 见证人

**get_witnesses** 

原型
[block:code]
{
  "codes": [
    {
      "code": "vector<optional<witness_object>> graphene::app::database_api::get_witnesses(constvector<witness_id_type> &witness_ids)const",
      "language": "cplusplus"
    }
  ]
}
[/block]
说明
按ID获取见证人列表。
此函数的语义与get_objects相同。
返回值
见证人对应的ID。
参数
witness_ids：要检索的证人的ID

**get_witness_by_account **

原型
[block:code]
{
  "codes": [
    {
      "code": "fc::optional<witness_object> graphene::app::database_api::get_witness_by_account(conststd::string account_id_or_name)const",
      "language": "cplusplus"
    }
  ]
}
[/block]
说明
获取给定帐户存在的见证人。
返回值
对应见证人，如果帐户没有见证人，则为null
参数
account_id_or_name：应检索其见证的帐户的ID

**lookup_witness_accounts** 

原型
[block:code]
{
  "codes": [
    {
      "code": "map<string, witness_id_type> graphene::app::database_api::lookup_witness_accounts(conststring &lower_bound_name, uint32_t limit)const",
      "language": "cplusplus"
    }
  ]
}
[/block]
说明
获取已登记证人的姓名和身份证件。
返回值
见证人姓名映射到相应的ID
参数
lower_bound_name：要返回值的名字的下限
limit：要返回值的最大结果数不得超过1000

**get_witness_count** 

原型
[block:code]
{
  "codes": [
    {
      "code": "uint64_t graphene::app::database_api::get_witness_count()const",
      "language": "cplusplus"
    }
  ]
}
[/block]
说明
获取在区块链中注册的证人总数。

7.1.11 委员会成员

**get_committee_members** 

原型
[block:code]
{
  "codes": [
    {
      "code": "vector<optional<committee_member_object>> graphene::app::database_api::get_committee_members(const vector<committee_member_id_type> &committee_member_ids)const",
      "language": "cplusplus"
    }
  ]
}
[/block]
说明
按ID获取committee_members列表。
此函数的语义与get_objects相同
返回值
委员会成员对应于提供的ID
参数
committee_member_ids：要检索的committee_members的ID

**get_committee_member_by_account** 

原型
[block:code]
{
  "codes": [
    {
      "code": "fc::optional<committee_member_object> graphene::app::database_api::get_committee_member_by_account(const std::string account_id_or_name)const",
      "language": "cplusplus"
    }
  ]
}
[/block]
说明
获取由给定帐户拥有的委员会成员。
返回值
committee_member对象，如果帐户没有委员会成员，则为null
参数
account：应检索其committee_member的帐户的ID或名称

**lookup_committee_member_accounts** 

原型
[block:code]
{
  "codes": [
    {
      "code": "map<string, committee_member_id_type> \ngraphene::app::database_api::lookup_committee_member_accounts(const string &lower_bound_name, uint32_t limit)const",
      "language": "cplusplus"
    }
  ]
}
[/block]
说明
获取已注册的committee_members的名称和ID。
返回值
委员会成员的地图名称为相应的ID
参数
lower_bound_name：要返回值的名字的下限
limit：要返回值的最大结果数不得超过1000

7.1.12 Workers

**get_workers_by_account** 

原型
[block:code]
{
  "codes": [
    {
      "code": "vector<optional<worker_object>> graphene::app::database_api::get_workers_by_account(conststd::string account_id_or_name)const",
      "language": "cplusplus"
    }
  ]
}
[/block]
说明
获取给定帐户拥有的工作人员。
返回值
worker对象，如果帐户没有worker，则返回值null
参数
account_id_or_name：应检索其工作人员的帐户的ID或名称

7.1.13 投票

**lookup_vote_ids** 

原型
[block:code]
{
  "codes": [
    {
      "code": "vector<variant> graphene::app::database_api::lookup_vote_ids(const vector<vote_id_type> &votes)const",
      "language": "cplusplus"
    }
  ]
}
[/block]
说明
给定一组投票，返回值他们投票的对象。
这将是committee_member_object，witness_objects和worker_objects的混合体
结果将与投票的顺序相同。对于未找到的任何投票ID，将返回值Null。
参数
votes：某一组投票的名称或id

## 7.1.14 权限与验证

**get_transaction_hex **

原型
[block:code]
{
  "codes": [
    {
      "code": "std::string graphene::app::database_api::get_transaction_hex(const signed_transaction &trx)const",
      "language": "cplusplus"
    }
  ]
}
[/block]
说明
获取事务的序列化二进制形式的hexdump。
参数
trx：事务ID

**get_required_signatures** 

原型
[block:code]
{
  "codes": [
    {
      "code": "set<public_key_type> graphene::app::database_api::get_required_signatures(constsigned_transaction &trx, const flat_set<public_key_type> &available_keys)const",
      "language": "cplusplus"
    }
  ]
}
[/block]
说明
此API将采用部分签名的事务和一组公共密钥，所有者可以签名并返回值应将签名添加到事务的最小公钥子集。
参数
trx：事务ID
available_keys：公共秘钥

**get_potential_signatures** 

原型
[block:code]
{
  "codes": [
    {
      "code": "set<public_key_type> graphene::app::database_api::get_potential_signatures(constsigned_transaction &trx)const",
      "language": "cplusplus"
    }
  ]
}
[/block]
说明
此方法将返回值可能为给定事务签名的所有公钥的集合。钱包可以使用这个调用，在调用get_required_signatures以获得最小子集之前，将它们的公钥集过滤到相关子集。
参数
trx：事务ID

**get_potential_address_signatures **

原型
[block:code]
{
  "codes": [
    {
      "code": "set<address> graphene::app::database_api::get_potential_address_signatures(constsigned_transaction &trx)const",
      "language": "cplusplus"
    }
  ]
}
[/block]
说明
获取可能存在的签名地址
参数
trx：事务ID

**verify_authority** 

原型
[block:code]
{
  "codes": [
    {
      "code": "bool graphene::app::database_api::verify_authority(const signed_transaction &trx)const",
      "language": "cplusplus"
    }
  ]
}
[/block]
返回值
如果trx具有所有必需的签名，则返回值true，否则抛出异常
参数
trx：事务ID

**verify_account_authority** 

原型
[block:code]
{
  "codes": [
    {
      "code": "bool graphene::app::database_api::verify_account_authority(const string &account_name_or_id, const flat_set<public_key_type> &signers)const",
      "language": "cplusplus"
    }
  ]
}
[/block]
说明
验证公钥是否具有足够的权限来批准此帐户的操作。
返回值
如果传入的密钥具有足够的权限来批准此帐户的操作，则为true
参数
account_name_or_id：要检查的帐户
signers：公钥

**validate_transaction** 

原型
[block:code]
{
  "codes": [
    {
      "code": "processed_transaction graphene::app::database_api::validate_transaction(constsigned_transaction &trx)const",
      "language": "cplusplus"
    }
  ]
}
[/block]
说明
针对当前状态验证事务而不在网络上广播它。
参数
trx：事务ID


**7.1.15 交易提议**

**get_proposed_transactions** 

原型
[block:code]
{
  "codes": [
    {
      "code": "vector<proposal_object> graphene::app::database_api::get_proposed_transactions(conststd::string account_id_or_name)const",
      "language": "cplusplus"
    }
  ]
}
[/block]
返回值
与指定帐户ID相关的提议集。
参数
asset_id_or_symbol：资产ID或符号


## 7.1.17 获取用户合约数据

**get_account_contract_data**

原型
[block:code]
{
  "codes": [
    {
      "code": "fc::variant get_account_contract_data(account_id_type account_id, const contract_id_type contract_id) const;",
      "language": "cplusplus"
    }
  ]
}
[/block]
返回值
返回值查询到的数据
参数
account_id：查询账户的ID
contract_id：查询合约的ID

## 7.1.18 获取合约公共数据

**get_contract_public_data**

原型
[block:code]
{
  "codes": [
    {
      "code": "map<lua_key, lua_types> get_contract_public_data(string contract_id_or_name, map<lua_key, lua_types> filter) const;",
      "language": "cplusplus"
    }
  ]
}
[/block]
返回值
返回值查询到的数据
参数
contract_id_or_name：查询的合约的名称或ID
Filter：查询条件

## 7.1.19 根据交易的ID获取交易信息

**get_transaction_by_id**

原型
[block:code]
{
  "codes": [
    {
      "code": "optional<processed_transaction> get_transaction_by_id(const string &id) const;",
      "language": "cplusplus"
    }
  ]
}
[/block]
返回值
返回值获取到的交易信息
参数
Id：查询的交易ID

## 7.1.20 获取合约对象

**get_contract**

原型
[block:code]
{
  "codes": [
    {
      "code": "optional<contract_object> get_contract(string contract_id_or_name);",
      "language": "cplusplus"
    }
  ]
}
[/block]
返回值
返回值获取的合约对象
参数
contract_id_or_name：查询的合约的名称或ID

## 7.1.21 根据交易ID获取该交易在块中的信息

**get_transaction_in_block_info**

原型
[block:code]
{
  "codes": [
    {
      "code": "fc::optional<transaction_in_block_info> get_transaction_in_block_info(const string &id);",
      "language": "cplusplus"
    }
  ]
}
[/block]
返回值
该交易在块中的信息
参数
id：所查询的交易的hashID

## 7.1.22 查询世界观

**lookup_world_view**

原型
[block:code]
{
  "codes": [
    {
      "code": "vector<optional<world_view_object>> lookup_world_view(const vector<string> &world_view_name_or_ids) const;",
      "language": "cplusplus"
    }
  ]
}
[/block]
返回值
返回值查询到的世界观对象
参数
World_view_name_or_ids：查询的世界观名字或ID

## 7.1.23 查询非同质资产

**lookup_nh_asset**

原型
[block:code]
{
  "codes": [
    {
      "code": "vector<optional<nh_asset_object>> lookup_nh_asset(const vector<string> &nh_asset_hash_or_ids) const;",
      "language": "cplusplus"
    }
  ]
}
[/block]
返回值
返回值查询到的非同质资产对象
参数
nh_asset_hash_or_ids：查询的非同质资产的hashid 或 ID

## 7.1.24 列出非同质资产创造者所创建的非同质资产

**list_nh_asset_by_creator**

原型
[block:code]
{
  "codes": [
    {
      "code": "std::pair<vector<nh_asset_object>, uint32_t> list_nh_asset_by_creator(const account_id_type &nh_asset_creator,uint32_t pagesize,uint32_t page);",
      "language": "cplusplus"
    }
  ]
}
[/block]
返回值
返回值非同质资产列表及符合查询条件的总个数
参数
nh_asset_creator：所查询的创造者
pagesize：返回值结果中每页显示的个数
page：显示第多少页

## 7.1.25 查询账户下的非同质资产

**list_account_nh_asset**

原型
[block:code]
{
  "codes": [
    {
      "code": "std::pair<vector<nh_asset_object>, uint32_t> list_account_nh_asset(const account_id_type &nh_asset_owner,const vector<string> &world_view_name_or_ids,uint32_t pagesize,uint32_t page, nh_asset_list_type list_type = nh_asset_list_type::all_owner);",
      "language": "cplusplus"
    }
  ]
}
[/block]
返回值
非同质资产列表及符合查询条件的总个数
参数
nh_asset_owner：所查询的用户
world_view_name_or_ids：非同质资产所属世界观
pagesize：返回值结果中每页显示的个数
page：显示第多少页
list_type：查询类型(查询类型根据使用权和拥有权分为了5种，enum class nh_asset_list_type
{only_active = 0, // 只查询租借的资产
    only_owner = 1, // 只查询出租的资产
    all_active = 2, // 所有可使用的资产
    all_owner = 3, // 所拥有的所有资产
owner_and_active = 4 // 同时拥有所有权和使用权};)

## 7.1.26 获取非同质资产创造者的信息

**get_nh_creator**

原型
[block:code]
{
  "codes": [
    {
      "code": "fc::optional<nh_asset_creator_object> get_nh_creator(const account_id_type &nh_asset_creator);",
      "language": "cplusplus"
    }
  ]
}
[/block]
返回值
该创造者的信息
参数
nh_asset_creator：创造者的账户名或id

## 7.1.27 列出非同质资产出售单

**list_nh_asset_order**

原型
[block:code]
{
  "codes": [
    {
      "code": "std::pair<vector<nh_asset_order_object>, uint32_t> list_nh_asset_order(const string &world_view_name_or_id,const string &asset_symbols_or_id, const string &base_describe = \"\",uint32_t pagesize = 10,uint32_t page = 1, bool is_ascending_order = true);",
      "language": "cplusplus"
    }
  ]
}
[/block]
返回值
非同质资产出售单列表以及符合查询条件的总个数
参数
world_view_name_or_id：非同质资产所属的世界观
asset_symbols_or_id：非同质资产的同质资产资质
base_describe：非同质资产的基本描述
pagesize：返回值结果中每页显示的个数
page：显示第多少页
is_ascending_order：是否正序排列，true为正序，false为反序

## 7.1.28 列出该账户下所挂单的非同质资产出售单
 
**list_account_nh_asset_order**

原型
[block:code]
{
  "codes": [
    {
      "code": "std::pair<vector<nh_asset_order_object>, uint32_t> list_account_nh_asset_order(const account_id_type &nh_asset_order_owner,uint32_t pagesize,uint32_t page);",
      "language": "cplusplus"
    }
  ]
}
[/block]
返回值
非同质资产出售单列表以及符合查询条件的总个数
参数
nh_asset_order_owner：所查询的账户
pagesize：返回值结果中每页显示的个数
page：显示第多少页

## 7.1.29 查找文件

**lookup_file**

原型
[block:code]
{
  "codes": [
    {
      "code": "fc::optional<file_object> lookup_file(const string &file_name_or_ids) const;",
      "language": "cplusplus"
    }
  ]
}
[/block]
返回值
返回值查找到的文件的信息
参数
file_name_or_ids：要查找的文件的名字或ID

## 7.1.30 列出用户创建的文件

**list_account_created_file**

原型
[block:code]
{
  "codes": [
    {
      "code": "map<string, file_id_type> list_account_created_file(const account_id_type &file_creator) const;",
      "language": "cplusplus"
    }
  ]
}
[/block]
返回值
返回值该用户创建的文件的文件名及ID
参数
file_creator：查询的用户

## 7.1.31 列出用户创建的定时任务

**list_account_crontab**

原型
[block:code]
{
  "codes": [
    {
      "code": "vector<crontab_object> list_account_crontab(const account_id_type &crontab_creator, bool contain_normal = true, bool contain_suspended = true) const;",
      "language": "cplusplus"
    }
  ]
}
[/block]
返回值
返回值符合查询条件的任务
参数
crontab_creator：任务创建者
contain_normal：是否包含状态正常的任务
contain_suspended：是否包含被挂起的任务