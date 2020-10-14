---
title: "Command Line Tools"
slug: "command-line-tools"
hidden: false
createdAt: "2019-03-15T06:17:14.863Z"
updatedAt: "2019-03-16T15:51:56.566Z"
---
This section will introduce the use of cli_wallet (command line tool), which is an interoperable command line client based on encapsulated interfaces of Cocos-BCX RPC.
[block:api-header]
{
  "title": "Basic Operations"
}
[/block]
**Log in command line wallet
Acquire executable files: cli_wallet, copy it to predetermined directory and repeat the first step:
./cli_wallet --chain-id 81003974d328ff17b64076928ab87b24d7dffbc87df3d4cde89d2fa1877e4f6a -s ws://127.0.0.1:8070 -r 127.0.0.1:8099
--chain-id: Chain ID
-s: Witness node RPC address
-r: Command line wallet RPC listen address (skip it when there is no external call) 
In this section all the operations are executed within the command line wallet
Command line wallet should be unlocked for most operations, and players have to log in and unlock the wallet for account-related operation.

**Unlock command line wallet 
Set password and unlock wallet** 
set_password xxxx (xxx is passcode)   unlock xxxx(xxxx is passcode)

Import account
Syntax import_key   user name   private key

[block:code]
{
  "codes": [
    {
      "code": "import_key name KaVpJa9G4oqA5WHcSGitauFRuzdHcPVEAaESaA",
      "language": "text"
    }
  ]
}
[/block]
**Transfer** 
transfer from to amount asset_symblo memo_info true
Log in and unlock wallet with sufficient balance
[block:api-header]
{
  "title": "Account Related"
}
[/block]
Register 
Register  Log in and unlock wallet with sufficient balance 
[block:code]
{
  "codes": [
    {
      "code": "register_account name owner_key active_key registrar_account referrer_account referrer_percent true",
      "language": "text"
    }
  ]
}
[/block]
Return to a set of secure mnemonic code, public key and private key 
suggest_brain_key 
Print account operations history 
get_account_history account limit
[block:api-header]
{
  "title": "Acquire Account Information"
}
[/block]
List imported account in the wallet
list_my_accounts
Acquire account information 
get_account account_name_or_id
List account balance
list_account_balances account
Acquire object 
get_object object_id
Acquire private key
get_private_key public_key
Acquire account ID
get_account_id account_name_or_id
Return to token information 
get_asset asset_name_or_id
Acquire token ID
get_asset_id asset_name_or_id
Account upgrade
Account upgraded to member 
upgrade_account name true
Sufficient balance in the account and command line wallet will grant upgrading to permanent membership rather than annual membership
Registered as committee member 
create_committee_member account url true
The registered committee member changes from candidate to an official member by winning polls registered as witness 
create_witness account url true
The registered witness changes from candidate to an official witness by winning polls
[block:api-header]
{
  "title": "Vote"
}
[/block]
When counting votes in maintenance cycle, users have to vote for at least two or more nodes to be approved as valid votes.
Voters need to log in and unlock the wallet, the appointed member must be a lifetime member and an alternative witness/alternative committee member.  
Vote for witness  vote_for_witness name witness true true Vote for committee members  vote_for_committee_member name committee true true
[block:api-header]
{
  "title": "Configuration Modification"
}
[/block]
**Committee members propose to modify the overall configuration of blockchain**
import_key committee private key #import committee members
propose_parameter_change committee"2018-07-24T06:55:40" {"committee_proposal_review_period": 300} true #Committee suggest to modify review duration of the overall configuration of blockchain  
transfer name committee-account 100 COCOS "message" true #transfer to the proposal executor
approve_proposal 见证人 1.10.0 {"active_approvals_to_add" : ["见证人"]} true #approve proposal
committee-account（1.10.0）The real executor of the proposal, the initial amount of the account is 0, modifying the chain requires transferring service charge to the account 
Proposed executor account committee-account, Each committee member takes up a certain active authority weight according to his obtained votes. The proposal can only be executed when the weight of all the committee members who approve the proposal exceeds the threshold of committee-account.   
System automatically determines whether to execute the proposal upon the expiration, and updates operation rates after the closing time of the next maintenance time.

**Committee members propose to modify operating rates**
import_key Committee members private key #import committee members
propose_fee_change committee "2018-07-24T06:55:40" {"transfer" : {"fee": 244000, "price_per_kbyte": 100000}} true #Propose to modify transfer operation rate
transfer name committee-account 100 COCOS "message" true #transfer to the proposed performer
approve_proposal witness 1.10.0 {"active_approvals_to_add":  ["witness"]} true #approval proposal
committee-account (1.10.0) is the real executor of the proposal, the initial amount of the account is 0, modifying the chain requires transferring service charge to the account.
Proposed executor account committee-account, Each committee member takes up a certain active authority weight according to his obtained votes. The proposal can only be executed when the weight of all the committee members who approve the proposal exceeds the threshold of commit-account.
System automatically determines whether to execute the proposal upon the expiration, and updates operation rate after the closing time of the next maintenance time.
[block:api-header]
{
  "title": "Chain Parameter Acquisition"
}
[/block]
Acquire information of chain IDs, current active witnesses and committee members
Acquire designated block information get_block block_num  Acquire the total number of on-chain registered accounts  get_account_count  List on-chain tokens  list_assets lowerbound limit Return results and rank token symbols, lowerbound refers to minimum quota, and limit stands for the greatest number of return – the greatest number of token symbols is no less than that of lowerbound token  Return chain operating costs and other invariable attributes  get_global_properties Return chain header block ID, time and next maintenance cycle and other variable attributes get_dynamic_global_properties  List witnesses  list_witnesses lowerbound limit Return witnesses through ranking witness accounts, lowerbound refers to minimum quota, and limit stands for the greatest number of return List committee members  list_committee_members lowerbound limit Return committee members through ranking member accounts, lowerbound refers to minimum quota, and limit stands for the greatest number of return  Return witness information  get_witness witness_name_or_id Return committee members information  get_committee_member committee_member_name_or_id
[block:api-header]
{
  "title": "Acquire Information of Local Nodes"
}
[/block]
Return information, such as Client, compilation time, boost, and openssl  
about
[block:api-header]
{
  "title": "Other"
}
[/block]
List information of account incentives
 get_vesting_balances account_name 
Receive incentives (witness members only) 
 withdraw_vesting witness_name amount asset_symbol true
 Lock wallet 
lock