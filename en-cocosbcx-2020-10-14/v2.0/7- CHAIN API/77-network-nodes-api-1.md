---
title: "7.1 Database API"
slug: "77-network-nodes-api-1"
hidden: false
createdAt: "2019-10-11T05:54:28.402Z"
updatedAt: "2020-04-15T03:13:29.325Z"
---
## 7.3.1 Object

**get_objects** 

Prototype
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
Description
Get the object corresponding to the ID provided
If any of the supplied IDs are not mapped to an object, return value null variable in its place.
Return value
The retrieved objects are in sequential search mentioned in ID
Parameters
ids:The IDs of the objects to retrieve

## 7.3.2 Subscribe Callback

**set_subscribe_callback** 


Prototype
[block:code]
{
  "codes": [
    {
      "code": "void graphene::app::database_api::set_subscribe_callback(std::function<void(const variant&)> cb, bool notify_remove_create, )",
      "language": "cplusplus"
    }
  ]
}
[/block]
Description
Register a callback handle that can be used to subscribe to changes of object database.
Parameters
cb:the callback handle to be registered
nofity_remove_create:Whether to subscribe to common object creation and deletion event. If set to true, the API server will notify IDs to clients of of all the newly created and deleted objects, regardless of whether clients subscribe to object. By default, the API server does not allow subscriptions to generic events, which can be changed at server startup.

**set_pending_transaction_callback **

Prototype
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
Description
Register a callback handle that will be notified when the transaction is pushed to the database.
Note: Transactions can be pushed to the database and popped from the database for multiple times before and after inclusion in the block. The client will be notified each time when the push is completed.
Parameters
cb:Callback handle to be registered

**set_block_applied_callback **

Prototype
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
Description
Register a callback handle that will be notified when the block is pushed to the database.
Parameters
cb:Callback handle to be registered

**cancel_all_subscriptions **

Prototype
[block:code]
{
  "codes": [
    {
      "code": "void （）graphene::app::database_api::cancel_all_subscriptions",
      "language": "cplusplus"
    }
  ]
}
[/block]
Description
Stop receiving any notifications.
This will cancel the subscription for all subscription markets and objects.

## 7.3.3 Block and transaction
**get_block_header **

Prototype
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
Description
Retrieve block header.
Return value
The the header of quotable  block will return NULL if matching block is not found
Parameters
block_num:return the height of the block

**get_block **

Prototype
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
Description
Retrieve the full signed block.
Return value
The quotable block will return NULL, if matching block is not found.
Parameters
block_num:The height of the block to return

**get_transaction **

Prototype
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
Description
Used to get a single transaction.
Parameters
block_num:Block height
trx_in_block:Firm in block

**get_recent_transaction_by_id** 

Prototype
[block:code]
{
  "codes": [
    {
      "code": "optional<signed_transaction> graphene::app::database_api::get_recent_transaction_by_id(const transaction_id_type &id)const",
      "language": "cplusplus"
    }
  ]
}
[/block]
Description
If the transaction has not expired, this method will return a transaction with the given ID. If it is unknown,it will return NULL,which means it also can be  included in the blockchain at the same time.
Parameters
transaction_id_type:Transaction id

## 7.3.4 Global property

**get_chain_properties **

Prototype
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
Description
Retrieve all global properties of the chain

**get_global_properties **

Prototype
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
Description
Retrieve the global properties of the current chain

**get_config** 

Prototype
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
Description
Retrieve constants at compile-time .

**get_chain_id** 

Prototype
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
Description
Get the chain ID.

**get_dynamic_global_properties** 

Prototype
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
Description
Retrieve current dynamic global properties


## 7.3.5 KEY

**get_key_references **

Prototype
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
Description
Get the keys reference in the database
Parameters
key:The specified key

## 7.3.6 Accounts

**get_accounts **

Prototype
[block:code]
{
  "codes": [
    {
      "code": "vector<optional<account_object>> graphene::app::database_api::get_accounts(constvector<std::string> &account_names_or_ids)const",
      "language": "cplusplus"
    }
  ]
}
[/block]
Description
Get a list of accounts according to ID.
The semantics of this function are the same as get_objects.
Return value
Account corresponding to the ID provided.
Parameters
account_names_or_ids:The IDs or names of the account to be retrieved

**get_full_accounts** 

Prototype
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
Description
Get all the objects associated with the specified account and subscribe to update.
This function gets all related objects for a given account and subscribes to update for a given account. If the strings in names_or_ids cannot be bound to the account, the input will be ignored. All the other accounts will be retrieved and subscribed.
Return value
Strings mapping from names_or_ids to the corresponding account.
Parameters
callback:Used for function of calling update.
names_or_ids:Each item must be the account's names or IDs that will be retrieved.

**get_account_by_name **
Prototype
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

Prototype
[block:code]
{
  "codes": [
    {
      "code": "vector<account_id_type> graphene::app::database_api::get_account_references(const std::string account_id_or_name)const",
      "language": "cplusplus"
    }
  ]
}
[/block]
Return value
All accounts that reference the key or account ID in their owner or activity permissions.

**lookup_account_names** 

Prototype
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
Description
Get a list of accounts by names.
The semantics of this function are the same as get_objects
Return value
Hold an account with a name
Parameters
account_names:The names of the account to be retrieved

 **lookup_accounts** 

Prototype
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
Description
Get the names and IDs of the registered account.
Return value
The account name is mapped to the corresponding ID
Parameters
lower_bound_name: Lower limit of return value name 
limit:The maximum number of results to return a value which can not exceed 1000

**get_account_count **

Prototype
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
Description
Get the total number of accounts registered in the blockchain.

## 7.3.7 Account balances

**get_account_balances** 

Prototype
[block:code]
{
  "codes": [
    {
      "code": "vector<asset> graphene::app::database_api::get_account_balances(const std::string &account_name_or_id, const flat_set<asset_id_type> &assets)const",
      "language": "clojure"
    }
  ]
}
[/block]
Description
Get account balances for various assets.
Return value
Account balances.
Parameters
account_name_or_id:ID or name of the account that will get the balance.
assets:ID of the account that will get the balance; if it is NULL, it will get the balance in all asset accounts.

**get_named_account_balances** 

Prototype
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
Description
It is semantically equivalent to get_account_balances. It is a username instead of an ID.
Parameters
account_name_or_id:ID or name of the account that will get the balance.
assets:ID of the account that will get the balance; if it is NULL, it will get the balance in all asset accounts.

**get_balance_objects** 

Prototype
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
Return value
All unclaimed balance objects for a group of addresses
Parameters
assets:ID of the account that will get the balance; if it is NULL, it will get the balance in all asset accounts.

**get_vested_balances** 

Prototype
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
Description
Get the unfrozen asset balance.
Parameters
objs:Asset name or ID.

**get_vesting_balances **

Prototype
[block:code]
{
  "codes": [
    {
      "code": "vector<vesting_balance_object> graphene::app::database_api::get_vesting_balances(conststd::string account_id_or_name)const",
      "language": "cplusplus"
    }
  ]
}
[/block]
Description
Get the balance of the assets that has been frozen.
Parameters
account_id_or_name:Account name or ID.


## 7.3.8 Assets

**get_assets** 

Prototype
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
Description
Get a list of assets according to ID.
The semantics of this function are the same as get_objects.
Return value
The asset corresponding to the ID provided.
Parameters
asset_symbols_or_ids:The symbolic names or IDs of the asset that will be retrieved.

**list_assets **

Prototype
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
Prototypes get assets in alphabetical order by symbolic name.
Return value
Found assets
Parameters
lower_bound_symbol:Lower limit of return value name 
limit:The maximum number of assets to acquire (no more than 101)

**lookup_asset_symbols** 

Prototype
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
Description
Get a list of assets according to symbol.
The semantics of this function are the same as get_objects.
Return value
The asset corresponding to the symbol or ID provided.
Parameters
asset_symbols:Symbols or string IDs of the asset that will be retrieved.


## 7.3.9 Market and price feed

**get_order_book** 

Prototype
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
Description
Return value to market basis book:quote.
Return value
Market orders.
Parameters
base:The string name of the first asset.
quote:The string name of the second asset.
depth:Order book. The depth of each request and bid,whose maximum limit is 50. Prioritize each request with the lowest.

**get_limit_orders **

Prototype
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
Description
Get a limited price order for a specific market.
Return value
Limited price orders from the lowest price to the highest price.
Parameters
a:The symbol or ID of the asset being sold.
b:The symbol or ID of the asset being purchased.
limit:The maximum number of orders that will be retrieved.

**get_call_orders** 

Prototype
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
Get a call order in a given asset.
Return value
Phone orders from the earliest order to the latest order.
Parameters
a:The symbol or ID of the asset called .
limit:The maximum number of orders that will be retrieved.

**get_settle_orders** 

Prototype
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
Description
Get a mandatory settlement order for a given asset.
Return value
Settlement orders, from the earliest settlement to the latest order.
Parameters
a:The symbol or ID of the settled asset
limit:The maximum number of orders that will be retrieved.

**get_margin_positions** 

Prototype
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
Return value
All open margins for a given account ID or name.
Parameters
account_id_or_name:Account name or ID.

**subscribe_to_market** 

Prototype
[block:code]
{
  "codes": [
    {
      "code": "void graphene::app::database_api::subscribe_to_market(std::function<void(const variant&)> callback, const std::string &a, const std::string &b, )",
      "language": "cplusplus"
    }
  ]
}
[/block]
Description
A notification is requested when an active order in the market between two assets changes.
The callback will pass a variant containing vector <pair parameters. 
Parameters
callback:Callback method called when the market changes.
a:First asset symbol or ID.
b:Second asset symbol or ID.

**unsubscribe_from_market** 

Prototype
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
Description
Unsubscribe to updates of specific markets.
Parameters
a:First asset symbol or ID.
b:Second asset symbol or ID.

**get_ticker** 

Prototype
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
Description
Return to market asset code.
Return value
Market code for the past 24 hours.
Parameters
a:The string name of the first asset.
b:The string name of the second asset.

**get_24_volume** 

Prototype
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
Description
Return to market assets 24-hour trading volume
Return value
Market volume in the past 24 hours
Parameters
a:The string name of the first asset.
b:The string name of the second asset.

**get_trade_history **

Prototype
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
Description
Returns to the recent trading market basis quotes, sorted from the latest.
Note
Cross-time zones are not supported currently . The time must be UTC. The range is [stop, start). If there are more than 100 transactions in one second, this API only returns the first 100 records, and another API get_trade_history_by_sequence can be used to query the rest of the records.
Return value
Recent market transactions.
Parameters
base:The symbol or ID of the underlying asset.
quote:The symbol or ID of the quote asset.
start:As the start time of the UNIX timestamp, the latest transaction will be retrieved.
stop:Stop time as the UNIX timestamp, is the earliest retrieved transaction.
limit：The maximum number of trasactions to retrieve whose upper limit is 100.

7.3.10 Witnesses

**get_witnesses** 

Prototype
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
Description
Get a list of witnesses according to ID.
The semantics of this function are the same as get_objects.
Return value
The ID corresponding to the witnesses.
Parameters
witness_ids:The IDs of the witness to be retrieved

**get_witness_by_account **

Prototype
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
Description
Get the witnesses that exist for a given account.
Return value
Corresponding to the witness, if the account has no witnesses, it will be NULL.
Parameters
account_id_or_name:The ID of the account whose witness can be retrieved

**lookup_witness_accounts** 

Prototype
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
Description
Get the name and ID of the registered witnesses.
Return value
Witness name should be mapped to the corresponding ID.
Parameters
lower_bound_name:Lower limit of return value name.
limit:The maximum number of results to return a value which can not exceed 1000.

**get_witness_count** 

Prototype
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
Description
Get the total number of witnesses registered in the blockchain.

7.3.11 Committee members

**get_committee_members** 

Prototype
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
Description
Get a list of committed_members according to IDs.
The semantics of this function are the same as get_objects.
Return value
Committee members correspond to the IDs provided.
Parameters
committee_member_ids:ID of the commit_members to retrieve.

**get_committee_member_by_account** 

Prototype
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
Description
Get the committee members owned by a given account.
Return value
Committee_member object will be NULL, if the account does not have a committee member.
Parameters
account:The ID or name of the account whose commit_member should be retrieved

**lookup_committee_member_accounts** 

Prototype
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
Description
Get the name and ID of the registered commit_members.
Return value
The map name of the committee member is the corresponding ID.
Parameters
lower_bound_name:Lower limit of return value name.
limit:The maximum number of results to return a value which can not exceed 1000.

7.3.12 Workers

**get_workers_by_account** 

Prototype
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
Description
Get the staff owned by a given account.
Return value
Worker object, if the account has no worker, the return value is null
Parameters
account_id_or_name:The ID or name of the account of its staff member should be retrieved

7.3.13 vote

**lookup_vote_ids** 

Prototype
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
Description
Give a set of votes, return value of the object they voted for.
This will be a mixture of commit_member_object, witness_objects and worker_objects.
The result will be the same as the vote order. If voting ID is not found, it will return Null.
Parameters
votes:The name or ID of a group of votes.

## 7.3.14 Permission and verification

**get_transaction_hex **

Prototype
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
Description
Get the hexdump of the serialized binary form of the transaction.
Parameters
trx:Transaction ID

**get_required_signatures** 

Prototype
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
Description
This API will take a partially signed transaction and a set of public keys, where the owner can sign and return. It should add the signature to the transaction's smallest public key subset.
Parameters
trx:Transaction ID.
available_keys:Public keys.

**get_potential_signatures** 

Prototype
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
Description
This method will return a collection of all public keys whose value might be signed for a given transaction. The wallet can use this call to filter their public key set to the relevant subset before calling get_required_signatures to get the smallest subset.
Parameters
trx:Transaction ID

**get_potential_address_signatures **

Prototype
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
Description
Get a possible signature address.
Parameters
trx:Transaction ID

**verify_authority** 

Prototype
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
Return value
Return true if trx has all required signatures, otherwise throw an exception.
Parameters
trx:Transaction ID

**verify_account_authority** 

Prototype
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
Description
Verify that the public key has sufficient permissions to approve the operation of this account.
Return value
If the passed key has sufficient permissions to approve the operation of this account, it will be true. 
Parameters
account_name_or_id:Account to check.
signers:Public keys.

**validate_transaction** 

Prototype
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
Description
Verify the transaction against the current state without broadcasting it on the network.
Parameters
trx:Transaction ID.

**get_required_fees** 

Prototype
[block:code]
{
  "codes": [
    {
      "code": "vector<fc::variant> graphene::app::database_api::get_required_fees(const vector<operation> &ops, const std::string &asset_id_or_symbol)const",
      "language": "cplusplus"
    }
  ]
}
[/block]
Description
Calculate the required cost in the specified asset type for each operation,.
Parameters
ops:Specific operation.
asset_id_or_symbol:Asset ID or symbol.

**7.3.15 Proposed transactions**

**get_proposed_transactions** 

Prototype
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
Return value
The set of offers associated with the specified account IDs.
Parameters
asset_id_or_symbo:Asset ID or symbol

**7.3.16 Blinded balances**

**get_blinded_balances** 

Prototype
[block:code]
{
  "codes": [
    {
      "code": "vector<blinded_balance_object> graphene::app::database_api::get_blinded_balances(constflat_set<commitment_type> &commitments)const",
      "language": "cplusplus"
    }
  ]
}
[/block]
Description
Get blinded transfer balance.
Return value
An blinded transfer record for an ID.
Parameters
commitments:Specific commitment.

## 7.3.17 Get account contract data

**get_account_contract_data**

Prototype
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
Return value
Return value to queried data
Parameters
account_id:Query the account ID.
contract_id:Query contract ID.

## 7.3.18 Get contract public data

**get_contract_public_data**

Prototype
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
Return value
Return value to queried data.
Parameters
contract_id_or_name:The name or ID of the contract being queried.
Filter:Query conditions.

## 7.3.19 Get transaction information based on the ID of the transaction

**get_transaction_by_id**

Prototype
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
Return value
Return value to obtained transaction information.
Parameters
Id:Query transaction ID.

## 7.3.20 Get contract object

**get_contract**

Prototype
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
Return value
Return value to contract object abtained.
Parameters
contract_id_or_name:The name or ID of the contract being queried.

## 7.3.21 Get the information of the transaction in the block according to the transaction ID

**get_transaction_in_block_info**

Prototype
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
Return value
The information in the block in this transaction
Parameters
id:The hashID being queried.

## 7.3.22 Lookup world view

**lookup_world_view**

Prototype
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
Return value
Return value to world view object queried.
Parameters
World_view_name_or_ids:World view name or IDs in the query.

## 7.3.23 .Lookup non-homogeneous asset

**lookup_nh_asset**

Prototype
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
Return value
Return value to the non-homogeneous asset object queried.
Parameters
nh_asset_hash_or_ids:The hashid or ID of the non-homogeneous asset being queried.

## 7.3.24 List non-homogenous assets created by creators of non-homogeneous assets

**list_nh_asset_by_creator**

Prototype
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
Return value
Return value to non-homogeneous asset list and the total number of items that match the query criteria.
Parameters
nh_asset_creator:The creator of the query.
pagesize: Return value to the number of each page in the result.
page:Display page numbers.

## 7.3.25 Look up non-homogeneous assets under the account

**list_account_nh_asset**

Prototype
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
Return value
Return value to non-homogeneous asset list and the total number of items that match the query criteria.
Parameters
nh_asset_owner:Queryed users.
world_view_name_or_ids:World view of non-homogeneous assets.
pagesize:Return value to the number of each page in the result.
page:Display page numbers.
list_type:Query type (query type is divided into 5 types according to the right to use and ownership,enum class nh_asset_list_type
{only_active = 0, // Query only rented assets
    only_owner = 1, // Query only for leased assets
    all_active = 2, // All available assets
    all_owner = 3, // All assets owned
owner_and_active = 4 // Ownership and the right to use at the same time};)

## 7.3.26 Get information about creators of non-homogeneous assets

**get_nh_creator**

Prototype
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
Return value
The creator's message.
Parameters
nh_asset_creator:Creator's account name or ID.

## 7.3.27 List non-homogeneous asset sales orders

**list_nh_asset_order**

Prototype
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
Return value
List of non-homogeneous asset sales orders and total number of eligible items
Parameters
world_view_name_or_id:World view of non-homogeneous assets.
asset_symbols_or_id:Homogenous asset qualification for non-homogeneous assets.
base_describe:Basic description of non-homogeneous assets.
pagesize:Return value to the number of each page in the result.
page:Display page numbers.
is_ascending_order:Whether the order is positive or not. True is positive, and false is reverse.

## 7.3.28 List the non-homogeneous asset sales orders for the pending orders under this account
 
**list_account_nh_asset_order**

Prototype
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
Return value
List of non-homogeneous asset sales orders and total number of eligible items
Parameters
nh_asset_order_owner:The account queried
pagesize:Return value to the number of each page in the result.
page:Display page numbers.

## 7.3.29 Lookup file

**lookup_file**

Prototype
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
Return value
Return value to the information that the file is found.
Parameters
file_name_or_ids:The name or ID of the file to be found.

## 7.3.30 List account created file

**list_account_created_file**

Prototype
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
Return value
Return value  to the file name and ID created by the user.
Parameters
file_creator:Query users.

## 7.3.31 List account crontab

**list_account_crontab**

Prototype
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
Return value
Return value for tasks that match the query criteria.
Parameters
crontab_creator:Task creator.
contain_normal:Whether to include a task with normal status.
contain_suspended:Whether it contains a suspended task.