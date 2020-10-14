---
title: "8.4 Python-SDK"
slug: "74-python-sdk"
hidden: false
createdAt: "2019-06-26T05:46:50.542Z"
updatedAt: "2020-03-02T09:27:49.804Z"
---
## Get Started
We propose to build on Ubuntu 16.04 LTS (64 bit) with a default of python3.5 
**Manual installation:** 

[block:code]
{
  "codes": [
    {
      "code": "cd python-grapheneEnhance\npython3 setup.py install --user",
      "language": "python"
    }
  ]
}
[/block]
**Modify the blockchain parameters:** 

[block:code]
{
  "codes": [
    {
      "code": "vi python-grapheneEnhance/grapheneEnhancebase/chains.py # Edit blockchain related parameters\n\n```python\nknown_chains = {\n\"xxxxxx\": {\n    \"chain_id\": \"xxxxxx\",\n    \"core_symbol\": \"xxxxxx\",\n    \"prefix\": \"xxxxxx\"} # Code edited in chains.py\n```\n\npython3 setup.py install --user # Reload the python library",
      "language": "python"
    }
  ]
}
[/block]
**Build the python script:** 

[block:code]
{
  "codes": [
    {
      "code": "from grapheneEnhance.graphene import Graphene\nfrom grapheneEnhance.instance import set_shared_graphene_instance\nfrom grapheneEnhance.storage import configStorage as config\nfrom pprint import pprint\n\nnodeAddress = \"ws://127.0.0.1:8000\" # The RPC node to be connected\ngph = Graphene(node=nodeAddress, blocking=True) # Instantiated object\nset_shared_graphene_instance(gph) # Set gph as a shared global instance\n\nif gph.wallet.created() is False: # Create a local wallet database, if not, create a new wallet database\n    gph.newWallet(\"xxxxxx\")\ngph.wallet.unlock(\"xxxxxx\") # Unlock the wallet, if you need to interact with the wallet in subsequent operations, you need to unlock the wallet.\n\nconfig[\"default_prefix\"] = gph.rpc.chain_params[\"prefix\"] # Add default information to the wallet database\ngph.wallet.addPrivateKey(privateKey) # Add a private key to the wallet\nconfig[\"default_account\"] = yourname # Add default information to the wallet database",
      "language": "text"
    }
  ]
}
[/block]
## API User Guide
**Account**
Method: create_account

Function: Create an account and import the private key into the wallet

Parameters: 
account_name: Account name registration rules, /^[a-z][a-z0-9.-]{4,63}$/, begin with lowercase letters + digits or lowercase letters or dots or dashes -, with a length of 4 to 63 characters
password: account password
Note: Only a lifetime account can create an account
Example:

[block:code]
{
  "codes": [
    {
      "code": "pprint(gph.create_account(\"test3\", \"password\"))",
      "language": "python"
    }
  ]
}
[/block]
Method: upgrade_account

Function: You can create a sub-account by upgrading your account to a lifetime account, which requires a certain fee.

Parameters: 
account: Account to be upgraded
Example:

[block:code]
{
  "codes": [
    {
      "code": "pprint(gph.upgrade_account(\"test1\"))",
      "language": "python"
    }
  ]
}
[/block]
**Asset**
Method: transfer

Function: Send tokens to the recipient

Parameters: 
to: Recipient account name
amount(int): Amount of tokens sent
asset: Asset ID or token
memo: Transfer memo
account: Sender account name
Example:

[block:code]
{
  "codes": [
    {
      "code": "pprint(gph.transfer(\"test2\",100, \"1.3.0\", \" \", \"test1\"))",
      "language": "python"
    }
  ]
}
[/block]
Method: asset_create

Function: Create token

Parameters: 
symbol: native token, regular ^[.A-Z]+$
precision(int): precise to decimal digit
amount(int): The amount of base assets (i.e. the created token, default 1)
asset: Base asset ID
_amount(int): quote asset (i.e. core asset, default 1)
_asset: quote asset
common_options(dict): Token option
bitasset_opts(dict): Bit token option (not required), if the default parameters is used to create bit tokens, just pass {}
is_prediction_market(bool): Whether it is a prediction market (non-bit tokens do not need to pay attention to this parameter)
account: Token creator
commen_options parameters example:

[block:code]
{
  "codes": [
    {
      "code": "common_options = {\n    \"max_supply\": 10000000000000, # Maximum supply\n    \"market_fee_percent\": 0, # Market transaction fee percent, default\n    \"max_market_fee\": 0, # Maximum market transaction fee, default\n    \"issuer_permissions\": 79, # Permissions can be updated by issuer, default\n    \"flags\": 0, # Current permissions\n    \"core_exchange_rate\": {\"base\": {}, \"quote\": {}}, # Exchange rate with core assets, determined by the above base assets and quote assets\n    \"whitelist_authorities\": [], # Whitelist accounts\n    \"blacklist_authorities\": [], # Blacklist accounts\n    \"whitelist_markets\": [], # Whitelist assets\n    \"blacklist_markets\": [], # Blacklist assets\n    \"description\": '{\"main\":\"\",\"short_name\":\"\",\"market\":\"\"}', #Content description\n    \"extension\": {}",
      "language": "python"
    }
  ]
}
[/block]
Example:

[block:code]
{
  "codes": [
    {
      "code": "pprint(gph.asset_create(\"TESTS\", 5, 1, \"1.3.0\", 1, \"1.3.1\", common_options=common_options, bitasset_opts={}, account=\"test1\"))",
      "language": "python"
    }
  ]
}
[/block]
Method: asset_issue

Function: Issue token

Parameters: 
amount(int)：Issuance amount
asset：token to be issued
issue_to_account：Issue object
memo：Additional message (not required)
account：Token creator
Example:

[block:code]
{
  "codes": [
    {
      "code": "pprint(gph.asset_issue(10000, \"TESTS\", \"test1\", account=\"test1\"))",
      "language": "python"
    }
  ]
}
[/block]
**NH Asset**
Method: register_nh_asset_creator

Function: Register current account as a developer

Parameters: 
account：Registrar account name
Example:

[block:code]
{
  "codes": [
    {
      "code": "pprint(gph.register_nh_asset_creator(\"test2\"))",
      "language": "python"
    }
  ]
}
[/block]
Method: create_world_view

Function: Create a supported NH asset worldview and register the NH asset worldview supported by current account (generally the game account) with the blockchain system 

Parameters: 
world_view: Worldview name
account: Creator account name
Example:

[block:code]
{
  "codes": [
    {
      "code": "pprint(gph.create_world_view(\"DRBALL\", \"test1\"))",
      "language": "python"
    }
  ]
}
[/block]
Method: create_nh_asset

Function: Create a unique NH asset

Parameters: 
owner: Specify the NH asset owner (NH asset ownership account, which is defaulted as NH asset creator)
assetID: The native token used for the transaction of current NH asset
world_view：Worldview
describe: Description of the current content of the NH asset, as defined by the creator
account: creator
Example:

[block:code]
{
  "codes": [
    {
      "code": "pprint(gph.create_nh_asset(\"test2\", \"XXX\", \"FLY\", '{\"name\":\"tom\"}', \"test1\"))",
      "language": "python"
    }
  ]
}
[/block]
Method: create_nh_asset_order

Function: Sell the NH asset

Parameters: 
otcaccount： Account on OTC transaction platform for charging pending orders
pending_order_fee_amount： Amount of fees for pending orders. Pending order fees paid by users to OTC platform accounts
pending_order_fee_asset： The native token or ID of the asset used to pay for the pending order. The pending order fee paid by the user to the OTC platform account
nh_asset：NH Asset ID
memo：Pending order memo
price_amount：Price amount of pending order
price： The native token or ID used for the pending order price
account：Seller
Example:

[block:code]
{
  "codes": [
    {
      "code": "pprint(gph.create_nh_asset_order(\"official-account\", 1, \"1.3.0\", \"4.2.1\", \" \", 100, \"1.3.0\", \"test1\"))",
      "language": "python"
    }
  ]
}
[/block]
**Contract**
Method: create_contract

Function: Create a smart contract

Parameters: 
name： Contract name, regular /^[a-z][a-z0-9.-]{4,63}$/, begin with a letter + letters or numbers or dot or dash -, length 4 to 63
data：Contract lua code
con_authority：Contract authority (publicKey in a pair of public and private keys)
account：Contract creator
Example:

[block:code]
{
  "codes": [
    {
      "code": "print(gph.create_contract(\"contract.test01\", data=data, con_authority=\"COCOS6esv8d6u2eqzKyiQvCYJa6XK74c7BrmzUqL4Z7zfhtvB4dbLh4\", account=\"developer\"))",
      "language": "python"
    }
  ]
}
[/block]
Method: call_contract_function

Function: Call contract function interface

Parameters: 
contract：Contract name or contract ID
function：Function name in the contract
value_list(list)： Call the parameter list of the contract function
account：Caller account name
value_list parameters example:

[block:code]
{
  "codes": [
    {
      "code": "value_list = [\n        [2, {\"baseValue\": \"test1\"}], \n        [2, {\"baseValue\": \"100\")}]\n    ]",
      "language": "python"
    }
  ]
}
[/block]
Example:
[block:code]
{
  "codes": [
    {
      "code": "pprint(gph.call_contract_function(\"1.16.1\", \"draw\", value_list=value_list, account=\"test1\"))",
      "language": "python"
    }
  ]
}
[/block]
**Market**
Method: limit_order_create

Function: Create orders in a given market

Parameters: 
amount(int)：Amount of tokens sold
asset： Asset ID or native token sold
min_amount(int)： The minimum amount of tokens required to be obtained
min_amount_asset： Asset ID or native token required to be obtained
fill(bool)： It is defaulted as False. If this flag is set to True, then this order must be completely purchased or rejected.
account：Seller account name
Example:

[block:code]
{
  "codes": [
    {
      "code": "pprint(gph.limit_order_create(1, \"1.3.0\", 1, \"1.3.1\", account=\"test1\"))",
      "language": "python"
    }
  ]
}
[/block]
Method: limit_order_cancel

Function: Cancel the order in a given market

Parameters: 
order_number(list)：ID of the limit order to be canceled
account：Operator account name
Example:

[block:code]
{
  "codes": [
    {
      "code": "pprint(gph.limit_order_cancel([\"1.7.1\"], account=\"test1\"))",
      "language": "python"
    }
  ]
}
[/block]
**Witness**
Method: create_witness

Function: Create a witness candidate

Parameters: 
account_name：Witness candidate account
url：Witness weblink
key：Witness block signature public key
Example:


[block:code]
{
  "codes": [
    {
      "code": "pprint(gph.create_witness(\"test2\", \"\", \"COCOS5YnQru8mtYo9HkckwnuPe8fUcE4LSxdCfVheqBj9fMMK5zwiHb\"))",
      "language": "python"
    }
  ]
}
[/block]
Method: approve_witness

Function: Vote for witness candidates

Parameters: 
witnesses(list)：Witness account name or witness ID
account：Voting account name
Example:

[block:code]
{
  "codes": [
    {
      "code": "pprint(gph.disapprove_worker([\"1.14.1\"], \"test1\"))",
      "language": "python"
    }
  ]
}
[/block]
**Committee**
Method: committee_member_create

Function: Create a committee member candidate
Parameters: 
url：weblink
account：Committee member candidate's account
Example:


[block:code]
{
  "codes": [
    {
      "code": "pprint(gph.committee_member_create(\" \", \"test2\"))",
      "language": "python"
    }
  ]
}
[/block]
Method: committee_member_update

Function: Update committee member candidate

Parameters: 
new_url：New weblink
account：Updated committee member candidate’s account
Example:

[block:code]
{
  "codes": [
    {
      "code": "pprint(gph.committee_member_update(\" \", \"test2\"))",
      "language": "python"
    }
  ]
}
[/block]
**Proposal**
Method: relate_world_view

Function: To link with the worldview, the developer can create the NH asset of the worldview only after linking to a certain worldview. The operation needs to be completed through a proposal to be approved by the creator of the worldview

Parameters: 
world_view：Worldview name
account：Linked account name
Example:

[block:code]
{
  "codes": [
    {
      "code": "pprint(gph.relate_world_view(\"DRBALL\", \"test2\"))",
      "language": "python"
    }
  ]
}
[/block]
Method: approveproposal

Function: Approve proposals of other users to be linked with your worldview

Parameters: 
proposal_ids(list)：Proposal ID
account：Update proposed account
Example:

[block:code]
{
  "codes": [
    {
      "code": "pprint(gph.approveproposal([\"1.10.1\"], \"test1\"))",
      "language": "python"
    }
  ]
}
[/block]
**Example of Wallet API Call:**
Method: unlock

Function: Unlock the wallet for related wallet operations

Parameters: 
pwd：wallet password
Example:

[block:code]
{
  "codes": [
    {
      "code": "print(gph.wallet.unlock(pwd))",
      "language": "python"
    }
  ]
}
[/block]
Method: getAccounts

Function: Get account information in the wallet database

[block:code]
{
  "codes": [
    {
      "code": "print(gph.wallet.getAccounts())",
      "language": "python"
    }
  ]
}
[/block]
Method: getPrivateKeyForPublicKey

Function: Get the corresponding private key in the wallet according to the public key given

Parameters: 
pub：Public key string

[block:code]
{
  "codes": [
    {
      "code": "print(gph.wallet.getPrivateKeyForPublicKey(pub))",
      "language": "python"
    }
  ]
}
[/block]
**Example of RPC Interface Call:**
Method: get_object

Function: Get this object information

Parameters: 
object_id：Object id
Example:

[block:code]
{
  "codes": [
    {
      "code": "print(gph.rpc.get_object(\"1.2.18\")) # Get account information of id \"1.2.17\"",
      "language": "python"
    }
  ]
}
[/block]
Method: get_contract

Function: Get contract details

Parameters: 
contract_id：Contract id or contract name
Example:

[block:code]
{
  "codes": [
    {
      "code": "print(gph.rpc.get_contract(\"1.16.0\")) # Get contract details of id \"1.16.0\"",
      "language": "python"
    }
  ]
}
[/block]
## Main-Packages 
**grapheneEnhance**
Description: The sub-modules correspond to all the classes involved in the blockchain system, such as accounts, assets, blocks, proposals, contracts, etc. Each class has a corresponding method to call. The graphene module has APIs related to the operation that can be called, such as transferring funds, creating accounts, creating assets, creating contracts, and so on.

grapheneEnhance.account module
grapheneEnhance.aes module
grapheneEnhance.amount module
grapheneEnhance.asset module
grapheneEnhance.block module
grapheneEnhance.blockchain module
grapheneEnhance.committee module
grapheneEnhance.contract module
grapheneEnhance.dex module
grapheneEnhance.exceptions module
grapheneEnhance.extensions module
grapheneEnhance.graphene module
grapheneEnhance.instance module
grapheneEnhance.market module
grapheneEnhance.memo module
grapheneEnhance.notify module
grapheneEnhance.price module
grapheneEnhance.proposal module
grapheneEnhance.storage module
grapheneEnhance.transactionbuilder module
grapheneEnhance.utils module
grapheneEnhance.vesting module
grapheneEnhance.wallet module
grapheneEnhance.witness module
grapheneEnhance.worker module

grapheneEnhancebase
Description: The sub-modules involve contents related to the underlying design, such as blockchain information, object type, operation, data structure, etc., which do not need to be changed in general. The chains module needs to be modified according to the use of the blockchain when initializing.

grapheneEnhancebase.account module

grapheneEnhancebase.asset_permissions module
grapheneEnhancebase.bip38 module
grapheneEnhancebase.chains module
grapheneEnhancebase.memo module
grapheneEnhancebase.objects module
grapheneEnhancebase.objecttypes module
grapheneEnhancebase.operationids module
grapheneEnhancebase.operations module
grapheneEnhancebase.signedtransactions module
grapheneEnhancebase.transactions module