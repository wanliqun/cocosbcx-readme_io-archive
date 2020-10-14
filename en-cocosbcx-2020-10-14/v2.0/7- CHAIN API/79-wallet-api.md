---
title: "7.2  Wallet API"
slug: "79-wallet-api"
hidden: false
createdAt: "2019-10-11T07:26:53.709Z"
updatedAt: "2020-04-16T09:32:39.815Z"
---
##7.4.1 General commands

**help**
Prototype
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
Description
Return a list of all the commands supported by wallet_api.
List each command, parameters and return value types.
For more detailed help on individual commands, use gethelp()
**return value**
Corresponding strings

**gethelp**
Prototype
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
Description
Return the detailed help for a single API command.
Return value
Corresponding strings.
Parameters
method: The name of the API command that needs help

**info**
Prototype
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
Description
Print connection information

**about**
Prototype
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
Description
Return value client version, git version of graphene, boost version, openssl and other information.
Return value
Compiling time information, client and dependency versions.

**network_add_nodes**
Prototype
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
Description
Add node.
Parameters
&nodes：IP node.

**network_get_connected_peers**
Prototype
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
Description
Print link node.

##7.4.2 Wallet information
** is_new**
Prototype
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
Description
Check if the wallet has just been created and the password has not been set.
Set_password converts the wallet to a locked state.
Return value
If the wallet is new,it will be true.

**is_locked**
Prototype
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
Description
Check if the wallet is locked (you cannot use its private key).
This can be changed by calling lock() or by changing this state by calling unlock().
Return value
If the wallet is locked,it will be true.

**lock**
Prototype
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
Description
Lock the wallet now.
 
**unlock**
Prototype
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
Description
Unlock the wallet.
The wallet remains unlocked until the lock is terminated or the program exits.
Parameters
password:Previously password set_password().

**set_password**
Prototype
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
Description
Set a new password on wallet.
The wallet must be "new" or "unlocked" to execute this command.

**dump_private_keys**
Prototype
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
Description
Dump all private keys owned by wallet.
Print in WIF format. You can use these keys to import another wallet import_key().
Return value
Containing map the private key.

**import_key**
Prototype
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
Description
Import the private key of an existing account.
The private key must match the key of the specified account.
Return value
If the key has been imported,it will be true.
Parameters
account_name_or_id:Account with key.
wif_key:Private key in WIF format.

**import_accounts**
Prototype
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
Description
Add account files.
Parameters
filename:File name of the deposit account file.
password:Set password.

**import_account_keys**
Prototype
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
Description
Import account in account files.
Parameters
filename:Account file name.
password:Set password.
src_account_name:Existing account in the file.
dest_account_name:Check account.

**import_balance**
Prototype
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
Description
This call will build a transaction that will declare all the balances controlled by wif_keys and store them in the given account.
Parameters
account_name_or_id:The name of deposited account.
wif_keys:Transfer the key of the account.
broadcast:Whether to be broadcasted or not.

**suggest_brain_key**
Prototype
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
Description
It is recommended to use a secure brain key to create an account.
Create_account_with_brain_key() requires you to specify a "brain key", a long password that provides enough variables to generate the key. This function will provide an appropriate random string that is relatively easy to write down.
Return value
A suggested brain key.

**get_transaction_id**
Prototype
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
Description
This method is used to convert a JSON transaction to its transactin ID.
Parameters
signed_transaction:JSON transaction that needs to be converted.

**get_private_key**
Prototype
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
Description
Get the WIF private key corresponding to the public key. The private key should be logged in to the wallet.
Parameters
public_key_type:Query the public key of the account.

**load_wallet_file**
Prototype
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
Description
Load the specified Graphene wallet.
Confirm that the current wallet is closed before loading a new wallet.
Return value
If the specified wallet is loaded, it will be true.
Parameters
wallet_filename:The filename of the wallet JSON file that will be loaded.
 If wallet_filename is NULL,reload the existing wallet file.

**normalize_brain_key**
Prototype
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
Description
Convert brain keys to reduce the possibility of errors when re-entering the key from memory.
This requires a brain key that is provided by the user and normalized to the form used to generate the private key. Note that this capitalizes all ASCII characters and folds multiple spaces into one.
Return value
Standard brain keys.
Parameters
s: Brain keys that users provided.

**save_wallet_file**
Prototype
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
Description
Save the current wallet to the specified file name
Note
This does not change the file name, so treat this feature as "Save copy as..." instead of "Save as...".
Parameters
wallet_filename:The filename of the new wallet JSON file to be created or overwritten. If wallet_filename is NULL, it will be saved as the current file name.


**add_extern_sign_key**
prototype
void add_extern_sign_key (string wif)
description
Import the WIF format private key into the wallet. This private key can be used to sign the transaction.
parameter
wif: The private key to be imported.


**sign_memo**
prototype
memo_data sign_memo (string from, string to, string memo)
description
Encrypt a note of type string.
parameter
from: from account of the transfer
to: to account for transfer
memo: note string



## 7.4.3 Account operation

**list_my_accounts**
Prototype
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
Description
List all accounts controlled by this wallet. Return a list of full account objects for all accounts that have their private key.
Return value
The list of account object.

**list_accounts**
Prototype
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
Description
List all accounts registered in the blockchain. Return value a list of all account names and their account IDs,which are sorted by account names.
Use the lowerbound and limit parameters through page turning. To retrieve all accounts, first set lowerbound to null character string "", then the last account name as the lowerbound next time the list_accounts() call returns the value in each iteration.
Return value
Map the account name to the account ID of the account list.
Parameters
lowerbound:The name of the first account to return the value. If the specified account does not exist, the list will start lowerbound from the next account.
limit:Return to the maximum number of accounts (maximum: 1000).

**list_account_balances**
Prototype
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
Description
List the account balance. Each account can have multiple balances with an asset. The list of return value will contain assets with an account with a non-zero balance only.
Return value
a list of given account balances.
Parameters
id:The name or ID of the account which you want to check the balance.

**register_account**
Prototype
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
Description
Register a third-party account on the block.
This function is used to register an account for which you do not have a private key. As a registrar, the end user will generate his own private key and send you the public key. Registers will use this feature to sign up for an account on behalf of the end user.
Return value
Signed transaction registration account.
Parameters
name:The account's name in blockchain must be unique. Shorter name registrations are more expensive and rules are still changing, but in general, at least one number with more than 8 characters will be cheaper.
owner:The owner's key for new account.
active:The activity key for new account.
registrar_account:Account that will pay for user fees who registered.
referrer_account:As a referral account, you may receive transaction fees for some users. This can be the same as registrar_account if there is no referral source.
referrer_percent:The percentage of new user transaction fees that are not claimed to the recommender's blockchain (0 - 100); the rest will be sent to the registrar. Multiply GRAPHENE_1_PERCENT when constructing a transaction.
broadcast:If you want to broadcast a transaction,it will be true.

**upgrade_account**
Prototype
[block:code]
{
  "codes": [
    {
      "code": "signed_transaction graphene::wallet::wallet_api::upgrade_account(string name, bool broadcast)",
      "language": "cplusplus"
    }
  ]
}
[/block]
Description
Upgrade users to make their accounts that can be used for whole life long.
Return value
Upgraded account.
Parameters
name:The name or ID of the account to be upgraded.
broadcast:If you want to broadcast a transaction,it will be true.

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
Create a new account and register it on the blockchain.
Return value
Signed transaction registration account
Parameters
brain_key:Mnemonic used to generate the account private key
account_name:The account name must be unique within the chain.
registrar_account:Account that pays for registered user fees
referrer_account:As a referral account, you may receive transaction fees for some users. This can be the same as registrar_account if there is no referral source.
broadcast:If you want to broadcast a transaction,it will be true.

**transfer**
[block:code]
{
  "codes": [
    {
      "code": "signed_transaction graphene::wallet::wallet_api::transfer(string from, string to, string amount, string asset_symbol, pair<string,bool> memo, bool broadcast = false)",
      "language": "cplusplus"
    }
  ]
}
[/block]
Transfer, transfer assets from one account to another.
Return value
Signed registration account for transaction
Parameter
from:The name or ID of the account that sent the funds.
to:The name or ID of the account receiving the funds.
amount:Send amount.
asset_symbo:The symbol or ID of the asset to send.
memo:A memo attached to the transaction. The memo will be encrypted in the transaction and readable by the recipient. There is no length limit other than the limit imposed by the maximum transaction size, but the transaction increases with the size of the transaction
broadcast:If you want to broadcast a transaction,it will be true.
maximum transaction size, but transaction increase with transaction size broadcast: If you want to broadcast a transaction,it will be true.

**transfer**
prototype
signed_transaction transfer2(string from, string to, string amount, string asset_symbol, pair<string, bool> memo)
description
transfer, transfer assets from one account to another.
transfer parameter bool broadcast=encapsulation of true

**get_vesting_balances**
Prototype
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
Description
Get information about the home balance object.
Parameters
account_name:Account name, account ID or home balance object ID.

**withdraw_vesting**
Prototype
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
Description
Withdrawal of the return balance.
Parameters
witness_name:The witness's account name also accepts the account ID or the home balance ID type.
amount:Exit amount.
asset_symbol:The symbol of the asset to be withdrawn.
broadcast:If you want to broadcast a transaction,it will be true.

**get_account**
Prototype
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
Description
Return value information about a given account.
Return value
Public account data stored in the blockchain
Parameters
account_name_or_id: The name or ID of the account that provides the information

**get_account_id**
Prototype
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
Description
Find the ID of the specified account.
Return value
Specify the ID of the account
Parameters
account_name_or_id:The name of the account you are looking for

**get_account_history**
Prototype
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
Description
The return value specifies the latest action for the account.
This will return a list of value action history objects that describe the activity on the account.
Return value
a list of operation_history_objects
Parameters
name:Account name or ID
limit:The number of entries to return a value from (starting recently)

**approve_proposal**
Prototype
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
Description
Approve or reject the proposal.
Return value
Signed version of the transaction
Parameters
fee_paying_account:
proposal_id:Modify the proposal.
delta:Members contain approvals for creation or deletion. In JSON, you can keep undefined empty members.
broadcast:If you want to broadcast a transaction,it will be true.

## 7.4.4 Trading Information
**sell_asset**	
Prototype
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
Description
Release a limit order to attempt to sell one asset to another.
As long as the price is at least min_to_receive/amount_to_sell, the blockchain will try to sell symbol_to_sell as much as possible at symbol_to_receive.
In addition to the transaction fee, the market fee will be calculated as a percentage of the exchange amount as specified by the issuer of the asset being sold and the recipient of the asset.
If the sales or receiving asset is a whitelist limit, the order will only be created if the seller is in the whitelist of restricted asset types.
Market orders are matched in the order they are included in the blockchain.
Return value
Signed transaction sale funds
Parameters
seller_account:Provide an account for the sale of assets, which will receive sales proceeds.
amount_to_sell:Sale amount of assets sold (in nominal units)
symbol_to_sell:The name or ID of the asset to sell
min_to_receive:The minimum amount you are willing to receive in exchange for the sale of the entire amount_to_sell
symbol_to_receive:The name or ID of the asset you wish to receive
timeout_sec:If the order is not filled out immediately, this is the length of time the order remains on the order book before it is cancelled, and the unused funds will return the value to the seller's account.
fill_or_kill:If true, the order will only be included in the blockchain if it is filled in immediately; if it is false, an open order will be left on the ledger to fill any amount that cannot be filled out immediately.
broadcast:If you want to broadcast a transaction,it will be true.

**borrow_asset**
Prototype
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
Description
The debt/mortgage ratio of borrowing assets or renewing loans.
Return value
Signed transaction borrowed assets
Parameters
borrower_name：The name or ID of the account associated with the transaction.
amount_to_borrow：The amount of the borrowed asset. Make this value negative to pay off the debt.
asset_symbol:The symbol or ID of the borrowed asset.
amount_of_collateral:The amount of support assets to add to the collateral position. Return this negation to some collateral. Support assets are defined in borrow assets in bitasset_options.
broadcast:If you want to broadcast a transaction,it will be true.
**cancel_order**
Prototype
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
Description
Cancel existing order
Return value
Signed transaction cancel order
Parameters
order_id:The ID of the order to cancel
broadcast:If you want to broadcast a transaction,it will be true.

**settle_asset**
Prototype
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
Description
Arrange the assets issued by the market for automatic settlement.
Bondholders issued by the market may request mandatory settlement of a portion of their assets. This means that the specified amount will be locked by the chain and held during the settlement period, after which the chain will choose the holder of the margin and use the collateral of the margin to purchase the settled assets. The price of this sale will be based on the settlement price of the assets issued by the market. The exact settlement price will be the feed price at the time of settlement, and the offset will be beneficial to the margin position, where the offset is the blockchain parameter set in global_property_object.
Return value
Signed transaction settlement specified assets
Parameters
account_to_settle:The name or ID of the account that owns the asset
amount_to_settle:The amount of the specified asset to be scheduled for settlement
symbol:The name or ID of the asset to be settled
broadcast:If you want to broadcast a transaction,it will be true.

**get_market_history**
Prototype
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
Description
Get transaction history
Parameters
symbol:Asset name or ID
bucket:Transaction Type

**get_limit_orders**
Prototype
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
Description
Get a limit order
Parameters
a,b:asset ID
limit:Number of acquisitions

**get_call_orders**
Prototype
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
Description
check order
Parameters
a:asset ID
limit:Number of acquisitions
**get_settle_orders**
Prototype
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
Description
Get the order that has been filled
a:asset ID
limit:Number of acquisitions


## 7.4.5 Asset call
**list_assets**
Prototype
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
Description
List all assets registered on the blockchain.
To list all assets, "" pass the empty string of the lower bound to the beginning of the list and then iterate as needed.
Return value
List of asset objects, sorted by symbol
Parameters
lowerbound:The symbol of the first asset to include in the list.
limit:The maximum number of assets to return a value (maximum: 100)

**create_asset**
Prototype
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
Description
Create new user-issued or market-issued assets.
There are many options that can be changed with update_asset()
This function is now cumbersome to use because the original JSON data structure must be provided for the option object, including the price and asset ID.
Return value
Signed transactions create new assets
Parameters
issuer:The fee will be paid and become the name or ID of the account of the new asset issuer. This can be updated later
symbol:New asset ticker symbol
precision:The number of precision digits to the right of the decimal point must be less than or equal to 12
common:The asset options required for all new assets. Note that core_exchange_rate is technically required to store the asset ID of this new asset. Since this ID is not known when this operation is created, creating this price is like the new asset has instance ID 1, and the chain will overwrite it with the ID of the new asset.
bitasset_opts:BitAssets unique options. This may be null unless market_issued sets the flag in common.flags
broadcast:If you want to broadcast a transaction,it will be true.

**update_asset**
Prototype
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
Description
Update the core options of the asset. All assets in the network use multiple options. These options are enumerated in the asset_object::asses_options structure. This command is used to update these options for existing assets.
Note
This action cannot be used to update BitAsset specific options. Update_bitasset() is the opposite.
Return value
Signed transaction update asset
Parameters
symbol:The name or ID of the asset to be updated
new_issuer:If you change the issuer of an asset, the name or ID of the new issuer. Null if you wish to keep the issuer of the asset
new_options:The new asset_options object, which will completely replace the existing options.
broadcast:If you want to broadcast a transaction,it will be true.

**update_bitasset**
Prototype
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
Description
Update the options specific to BitAsset.
Return value
Signed transaction update bitasset
Parameters
symbol: The name or ID of the asset to be updated must be a market-issued asset
new_options: The new bitasset_options object, which will completely replace the existing options.
broadcast:If you want to broadcast a transaction,it will be true.

**update_asset_feed_producers**
Prototype
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
Description
Update the set of feed generation accounts for BitAsset.
BitAssets selects the price feed by obtaining a median of recommendations from a group of feed producers. This command is used to specify which accounts can generate feeds for a given BitAsset.
Return value
The signed transaction updates the bitasset feed generator
Parameters
symbol:The name or ID of the asset to be updated
new_feed_producers:A list of account names or IDs that have been authorized to generate feeds for the asset. This list will completely replace the existing list
Broadcast: If you want to broadcast a transaction,it will be true.
**publish_asset_feed	**
Prototype
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
Description
Publish the asset price of the specified asset
The asset feed provider uses this command to issue asset feed prices for market-issued assets. Price feedback is used to adjust the market for assets issued in a particular market. For each value in the asset feed, calculate the median of all commit_member feeds for that asset and use the median of the value to configure the market for the asset.
The price object in this command contains three prices: call price limit, short price limit, and settlement price. The structure of the subscription limit price is (collateralized assets) / (debt assets), and the structure of short term prices is (for assets for sale) / (collateralized assets). Note that asset IDs are the opposite of each other, so if we issue a dollar feed, the call limit price will be CORE / USD and the short term price will be USD / CORE. The settlement price can be reversed in either direction as long as it is the ratio between the market-issued asset and its collateral.
Return value
A signed transaction updates the asset feed for a given asset
Parameters
publishing_account:Issue an asset-paying account
symbol:The name or ID of the asset we want to post.
feed:The price_feed object contains the three prices that make up the feed price.
broadcast:If you want to broadcast a transaction,it will be true.

**issue_asset**
Prototype
[block:code]
{
  "codes": [
    {
      "code": "signed_transaction graphene::wallet::wallet_api::issue_asset(string to_account, string amount, string symbol, pair<string,bool> memo, bool broadcast = false)",
      "language": "cplusplus"
    }
  ]
}
[/block]
Description
Issue new shares in assets.
Return value
Signed shares issued new shares
Parameters
to_account:The name or ID of the account that receives the new shares
amount:Amount issued in nominal units
symbol:The stock symbol of the asset to be issued
memo:A memo contained in the transaction, which can be read by the recipient
broadcast:If you want to broadcast a transaction,it will be true.
**get_asset**
Prototype
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
Description
Returns information about a given asset.
Return value
Information about assets stored in the blockchain
Parameters
asset_name_or_id:The symbol or ID of the related asset

**get_bitasset_data**
Prototype
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
Description
Returns the BitAsset specific data for a given asset. The behavior of assets issued by the market is determined by their "BitAsset data" and its underlying asset data get_asset().
Return value
BitAsset specific data for this asset
Parameters
asset_name_or_id:Symbol or ID of the problematic BitAsset


**reserve_asset**
Prototype
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
Description
Destroy assets issued by a given user.
This command destroys user-published assets to reduce liquidity.
Note
Unable to destroy assets issued by the market.
Return value
Signed transaction destroying assets
Parameters
from：Account with the assets you want to burn
amount:The amount of destruction, expressed in nominal units
symbol:The name or ID of the asset to burn
broadcast:If you want to broadcast a transaction,it will be true.

**global_settle_asset**
Prototype
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
Description
Force global resolution of specific assets (black swan or forecast market).
To use this operation, asset_to_settle must set the global_settle flag
When this is done, all balances will be converted to support assets at sett_price and all open margin positions will be called at the settlement price. If this asset is used as support for other bit sets, these bit sets will be forced to settle at their current feed price.
Note
This operation is used by the asset issuer only and settle_asset() can be used by any users who own the asset.
Return value
Signed transaction settlement specified assets
Parameters
symbol:The name or ID of the asset to be billed
settle_price:The price settled.
broadcast:If you want to broadcast a transaction,it will be true.

## 7.4.6 Management

**create_committee_member**
Prototype
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
Create a commit_member object owned by the given account.
An account can only have one commit_member object at most.
Return value
Committee members signed the transaction registration.
Parameters
owner_account: The name or ID of the account that created the committee member.
url:The URL to be included in the witness record in blockchain. Customers can see this information when they display a list of witnesses( it may show a blank).
broadcast:If you want to broadcast a transaction,it will be true.

**get_witness**
Prototype
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
Description
Return value of information about a given witness.
Return value
Witness information stored in blockchain.
Parameters
owner_account:All the name or ID of the witness account owner, or the ID of the witness.

**get_committee_member**
Prototype
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
Description
Return value of information about a given committee member.
Return value
Information about committee members.
Parameters
owner_account:The name or ID of the committee member account owner, or the ID of the committee member.

**list_witnesses**
Prototype
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
Description
List all witnesses registered in blockchain. Return a list of value for all account names that have witnesses, as well as associated witness IDs sorted by name. This lists whether the witness is voting at present.
Use the lowerbound and limit parameters to page through the list. To retrieve all witnesses, first set lowerbound to a NULL string "". Each iteration, passing the last witness name as return value of the next list_witnesss() ,call in lowerbound.
Return value
Map the witness name to the witness ID.
Parameters
lowerbound:Return the name of the first witness. If the specified witness does not exist, the list will start lowerbound from the witness that follows.
limit:Return value of the maximum number of committee members (maximum: 1000).

**list_committee_members**
Prototype
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
Description
List all committee members registered in blockchain. Return a list of value for all account names that have committee members and the associated committee member IDs sorted by name. This lists whether the members of the committee are voting at present.
Use the lowerbound and limit parameters to page through the list. To retrieve all the commit_members, first set the lowerbound to the empty string "", then each iteration, and return the value of the last committee member name as the nextbound list_committee_members() call.
Return value
The committee member list maps the committee member name to the committee member ID.
Parameters
lowerbound: Return value of the first committee member's name. If the specified commit_member does not exist, the list will start lowerbound from the subsequent committee members.
limit:Return value of the maximum number of committee members (maximum: 1000).

**create_witness**
Prototype
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
Description
Create a witness to a given account.
One account can only have one witness.
Return value
Signed transaction registration witness.
Parameters
owner_account:The name or ID of the account that created the witness.
url:The URL to be included in the witness record in blockchain. Customers can see this information when they display a list of witnesses( it may show a blank).
broadcast:If you want to broadcast a transaction,it will be true.

**update_witness**
Prototype
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
Description
Update the witnesses owned by a given account.
Parameters
witness_name:The name of the witness's account. Also accept the ID of the owner account or the ID of the witness.
url:Same as create_witness. A NULL string remains.
block_signing_key:New block signature public key. A NULL string remains.
broadcast:If you want to broadcast a transaction,it will be true.

**vote_for_committee_member**
Prototype
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
Description
Vote for specific committee members.
The account can post a list of all the committed_memberes they approved. This command allows you to add or remove commit_memberes from this list. The vote for each account is weighted by the share of the core assets owned by the account when voting.
Note
You can only choose to vote for committee members or not vote for committee members. You can not vote against committee members.
Return value
The signed transaction changed the vote for a given committee members.
Parameters
voting_account:The name or ID of the account that used its stock to vote.
committee_member:committee_member'The name or ID of the owner account.
approve:If you vote for the committee member,it will be true. Otherwise it will be false.
broadcast: If you want to broadcast a transaction,it will be true.

**vote_for_witness**
Prototype
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
Description
Vote for a specific witness.
The account can post a list of all witnesses they approve. This command allows you to add or remove witnesses from this list. The vote for each account is weighted by the share of the core assets owned by the account when voting.
Note
You can only choose to vote for witnesses or not vote for witnesses. You can not vote against witnesses.
Return value
The signed transaction changed the vote for a given witness
Parameters
voting_account:The name or ID of the account that used its stock to vote.
witness：Witness owner account name or ID.
approve:If you wish to vote for this witness, it will be true. Otherwise it will be false.
broadcast: If you want to broadcast a transaction,it will be true.

**propose_parameter_change**
Prototype
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
Description
Create a transaction to suggest parameter changes.
If you need atomic changes, you can specify multiple parameters.
Return value
Sign the transaction version.
Parameters
proposing_account:Pay fees to make a tx account.
expiration_time:The timestamp specifies when the proposal will take effect or expire.
changed_values:Change values and other chain parameters are populated by default.
proposal_base: the base proposal to be modified,generally null.
broadcast:If you want to broadcast a transaction,it will be true.

**propose_fee_change**
Prototype
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
Description
It is recommended to change fees.
Return value
Sign the transaction version.
Parameters
proposing_account:Pay fees to make a tx account.
expiration_time:The timestamp specifies when the proposal will take effect or expire.
changed_values:Operation type map to new fees. The operation can be specified by name or ID. The "Proportional" key changes the scale. All other operations will maintain the current value.
proposal_base:Basic proposal to be modified,usually null.
broadcast:If you want to broadcast a transaction, it will be true.

## 7.4.7 Privacy mode

**set_key_label**
Prototype
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
Description
This method can be used to set the label of the public key.
Note
Any of two public keys can not have the same label.
Return value
If the tag is set, it will be true. Otherwise it will be false.
Parameters
key:Public key
label:Label

**get_key_label**
Prototype
[block:code]
{
  "codes": [
    {
      "code": "string graphene::wallet::wallet_api::get_key_label(public_key_type key)const",
      "language": "cplusplus"
    }
  ]
}
[/block]
Description
Get the label of the public key.
Parameters
key:Public key

**get_public_key**
Prototype
[block:code]
{
  "codes": [
    {
      "code": "public_key_type graphene::wallet::wallet_api::get_public_key(string label)const",
      "language": "cplusplus"
    }
  ]
}
[/block]
Return value
The public key associated with the given tag.


________________________________________
## 7.4.8 Blockchain check

**get_block**
Prototype
[block:code]
{
  "codes": [
    {
      "code": "optional<signed_block_with_info> graphene::wallet::wallet_api::get_block(uint32_t num)",
      "language": "cplusplus"
    }
  ]
}
[/block]
**get_account_count**
Prototype
[block:code]
{
  "codes": [
    {
      "code": "uint64_t graphene::wallet::wallet_api::get_account_count()const",
      "language": "cplusplus"
    }
  ]
}
[/block]
Description
Return value of the number of accounts registered in blockchain.
Return value
The number of registered accounts.

**get_global_properties**
Prototype
[block:code]
{
  "codes": [
    {
      "code": "global_property_object graphene::wallet::wallet_api::get_global_properties()const",
      "language": "cplusplus"
    }
  ]
}
[/block]
Description
Return setting for slowly changed blockchain. This object contains all the properties of the fixed blockchain, or all properties that change only once per maintenance interval (every day), such as the current witness list, committee members, blocking interval, and so on.
Return value
Global properties

**get_dynamic_global_properties**
Prototype
[block:code]
{
  "codes": [
    {
      "code": "dynamic_global_property_object graphene::wallet::wallet_api::get_dynamic_global_properties()const",
      "language": "cplusplus"
    }
  ]
}
[/block]
Description
Return setting for rapidly changed blockchain. Return value of the object containing information that fixes the interval of each block, such as the number of header block, the next witness, and so on.
Return value
Dynamic global property

**get_object**
Prototype
[block:code]
{
  "codes": [
    {
      "code": "variant graphene::wallet::wallet_api::get_object(object_id_type id)const",
      "language": "cplusplus"
    }
  ]
}
[/block]
Description
Return the blockchain object corresponding to the given ID.
This generic function can be used to retrieve any object from the blockchain to whose ID is assigned. Some types of objects have specialized convenient functions to return value to their objects. For example, an asset has a get_asset() account get_account(), but this function works for any object.
Return value
Requested objects.
Parameters
id:The ID of the object to return
________________________________________
## 7.4.9 Builder transaction

**begin_builder_transaction**
Prototype
[block:code]
{
  "codes": [
    {
      "code": "transaction_handle_typegraphene::wallet::wallet_api::begin_builder_transaction()",
      "language": "cplusplus"
    }
  ]
}
[/block]
Description
Create a new  builder transaction.

**add_operation_to_builder_transaction**
Prototype
[block:code]
{
  "codes": [
    {
      "code": "void graphene::wallet::wallet_api::add_operation_to_builder_transaction(transaction_handle_typetransaction_handle, const operation &op)",
      "language": "cplusplus"
    }
  ]
}
[/block]
Description
Add an action to builder transaction.
Parameters
transaction_handle_typetransaction_handle: The number of builder transaction
operation:Executed op

**replace_operation_in_builder_transaction**
Prototype
[block:code]
{
  "codes": [
    {
      "code": "void graphene::wallet::wallet_api::replace_operation_in_builder_transaction(transaction_handle_typehandle, unsigned operation_index, const operation &new_op)",
      "language": "cplusplus"
    }
  ]
}
[/block]
Parameters
transaction_handle_typetransaction_handle:The number of builder transaction
operation_index:Original op
operation:New op

**preview_builder_transaction**
Prototype
[block:code]
{
  "codes": [
    {
      "code": "transaction graphene::wallet::wallet_api::preview_builder_transaction(transaction_handle_typehandle)",
      "language": "cplusplus"
    }
  ]
}
[/block]
Description
Check the operations performed by builder transaction.
Parameters
transaction_handle_typetransaction_handle:The number of builder transaction.

**sign_builder_transaction**
Prototype
[block:code]
{
  "codes": [
    {
      "code": "signed_transaction graphene::wallet::wallet_api::sign_builder_transaction(transaction_handle_typetransaction_handle, bool broadcast = true)",
      "language": "cplusplus"
    }
  ]
}
[/block]
Description
Sign the builder transaction (execute the transaction generator).
Parameters
transaction_handle_typetransaction_handle:The number of builder transaction.

**propose_builder_transaction**
Prototype
[block:code]
{
  "codes": [
    {
      "code": "signed_transaction graphene::wallet::wallet_api::propose_builder_transaction(transaction_handle_typehandle, time_point_sec expiration = time_point::now() + fc::minutes(1), uint32_t review_period_seconds = 0, bool broadcast = true)",
      "language": "cplusplus"
    }
  ]
}
[/block]
**remove_builder_transaction**
Prototype
[block:code]
{
  "codes": [
    {
      "code": "void graphene::wallet::wallet_api::remove_builder_transaction(transaction_handle_typehandle)",
      "language": "cplusplus"
    }
  ]
}
[/block]
Description
Delete builder transaction.
Parameters
transaction_handle_typetransaction_handle:The number of builder transaction.

**serialize_transaction** 
Prototype
[block:code]
{
  "codes": [
    {
      "code": "string graphene::wallet::wallet_api::serialize_transaction(signed_transaction tx)const",
      "language": "cplusplus"
    }
  ]
}
[/block]
Description
Convert the signed_transaction in JSON format to its binary representation.
Return value
The transaction uses binary form. It won't be encoded in hexadecimal and return value of a raw string, which may have null characters embedded.
Parameters
tx: The transaction to be serialized.

**sign_transaction**
Prototype
[block:code]
{
  "codes": [
    {
      "code": "signed_transaction graphene::wallet::wallet_api::sign_transaction(signed_transaction tx, bool broadcast = false)",
      "language": "cplusplus"
    }
  ]
}
[/block]
Description
Sign the transaction.
Given a fully formed transaction with missing signatures. This gives the transaction a necessary key and broadcasts the transaction optionally.
Return value
Sign the version of the ​transaction.
Parameters
tx: Unsigned transaction.
broadcast: If you want to broadcast a transaction, it will be true.

**get_prototype_operation_by_name**
Prototype
[block:code]
{
  "codes": [
    {
      "code": "operation graphene::wallet::wallet_api::get_prototype_operation_by_name(string operation_type)",
      "language": "cplusplus"
    }
  ]
}
[/block]
Description
Return an uninitialized object representing a given blockchain operation.
The default initialization object of the given type will be returned. It can be used in the early stage of wallet development when we have no custom commands for creating all the operations supported by blockchain.
Use Transaction Builder, add_operation_to_builder_transaction(), to create any operations supported by blockchain. If you want to do this operation from CLI, you need to know what JSON form looks like. This will give you a template to fill out.
Return value
Default construction operation for a given type
Parameters
operation_type: Return an operation type. It must be one of the defined operations. For example, graphene/chain/operations.hpp（“global_parameters_update_operation”）
get_prototype_operation_by_name The following parameters can refer to [this](https://github.com/Cocos-BCX/Document/blob/master/chain_development/operations%E8%AF%B4%E6%98%8E.md)