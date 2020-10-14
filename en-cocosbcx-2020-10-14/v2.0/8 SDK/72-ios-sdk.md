---
title: "8.2 iOS-SDK"
slug: "72-ios-sdk"
hidden: false
createdAt: "2019-06-25T10:04:53.207Z"
updatedAt: "2020-03-02T09:27:05.880Z"
---
CocosSDK integration documentation


## Example
To run the sample project, the repo shall be cloned and then run the 'pod install' from the sample directory.

## Dependent Libraries

AFNetworking
FMDB
Secp256k1_A
SocketRocket

## Installation
1.Integrated installation using CocoaPods


[block:code]
{
  "codes": [
    {
      "code": "pod 'CocosSDK'",
      "language": "objectivec"
    }
  ]
}
[/block]
2.Manual integration

   Add all the files in the Class folder under the CocosSDK directory. 
   Add dependent libraries to the project.

## Basic Functions
**Initialization**
1.User guide
   Initialize SDK, connect nodes, configure ChainId and chain identifier

2.Interface function

[block:code]
{
  "codes": [
    {
      "code": "/**\n  Initialize SDK\n  @param url RPC     Node\n  @param faucetUrl   URL Address\n  @param timeOut     Timeout\n  @param coreAsset   Chain identifier\n  @param chainId     Chain ID\n  @param connectedStatus Status of connection\n  */\n - (void)Cocos_ConnectWithNodeUrl:(NSString *)url\n         Fauceturl:(NSString *)faucetUrl\n            TimeOut:(NSTimeInterval)timeOut\n         CoreAsset:(NSString *)coreAsset\n            ChainId:(NSString *)chainId\n     ConnectedStatus:(void (^)(WebsocketConnectStatus     connectStatus))connectedStatus;",
      "language": "objectivec"
    }
  ]
}
[/block]
3.Example code

[block:code]
{
  "codes": [
    {
      "code": " - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions\n{\n // Test node\n [[CocosSDK shareInstance] Cocos_ConnectWithNodeUrl:@\"ws://39.106.126.54:8050\" Fauceturl:@\"http://47.93.62.96:3000\" TimeOut:2 CoreAsset:@\"COCOS\" ChainId:@\"53b98adf376459cc29e5672075ed0c0b1672ea7dce42b0b1fe5e021c02bda640\" ConnectedStatus:^(WebsocketConnectStatus connectStatus) {\n }];\n return YES;\n}",
      "language": "objectivec"
    }
  ]
}
[/block]
## Set log output
1.User guide
   Set whether to output the log information of sdk in the console
2.Interface function


[block:code]
{
  "codes": [
    {
      "code": " /**\n  *  Open debug log\n  *\n  *  @param isOpen YES means open，No means close\n  */\n - (void)Cocos_OpenLog:(BOOL)isOpen;",
      "language": "objectivec"
    }
  ]
}
[/block]

[block:api-header]
{}
[/block]
## Create an account

**User guide**
**Wallet mode**
   Create an account in wallet mode. Accounts created in wallet mode cannot be logged in with account name and password.
**Account mode**
   Create an account in account mode. Accounts created in wallet mode can be logged in with an account name and password.
1.Interface function

[block:code]
{
  "codes": [
    {
      "code": " /**\n  Create account\n\n  @param walletMode  Mode of wallet\n  @param accountName Account\n  @param password    Password\n  @param autoLogin   Auto log in\n  */\n - (void)Cocos_CreateAccountWalletMode:(CocosWalletMode)walletMode\n      AccountName:(NSString *)accountName\n         Password:(NSString *)password\n        AutoLogin:(BOOL)autoLogin\n          Success:(SuccessBlock)successBlock\n            Error:(Error)errorBlock;",
      "language": "objectivec"
    }
  ]
}
[/block]
## Delete/logout wallet
1.User guide
   Delete the login and import records saved by the SDK

2.Interface function

[block:code]
{
  "codes": [
    {
      "code": " /**\n  Delete wallet\n  @param accountName Account\n  */\n - (void)Cocos_DeleteWalletAccountName:(NSString *)accountName\n           Success:(SuccessBlock)successBlock\n             Error:(Error)errorBlock;",
      "language": "objectivec"
    }
  ]
}
[/block]
## Login wallet
1.User guide
   Log in to the wallet with the account name and password

2.Interface function

[block:code]
{
  "codes": [
    {
      "code": " /**\n  Log in by account\n\n  @param accountName Account\n  @param password    Password\n  */\n - (void)Cocos_LoginAccountWithName:(NSString *)accountName\n           Password:(NSString *)password\n             Success:(SuccessBlock)successBlock\n               Error:(Error)errorBlock;",
      "language": "objectivec"
    }
  ]
}
[/block]
## Transfer
1.User guide
   Transfer

2.Interface function
[block:code]
{
  "codes": [
    {
      "code": " /**\n  Transfer\n\n  @param fromName        Sender's account\n  @param toName          Receiver's account\n  @param password        Password\n  @param transferAsset   Asset's name(eg. COCOS)\n  @param assetAmount     assetAmount Transfer amount\n  @param feePayingAsset  Charge's currency(require)\n  @param memo            Memo String\n  */\n - (void)Cocos_TransferFromAccount:(NSString *)fromName\n               ToAccount:(NSString *)toName\n                Password:(NSString *)password\n           TransferAsset:(NSString *)transferAsset\n             AssetAmount:(NSString *)assetAmount\n          FeePayingAsset:(NSString *)feePayingAsset\n                    Memo:(NSString *)memo\n               Success:(SuccessBlock)successBlock\n                 Error:(Error)errorBlock;",
      "language": "objectivec"
    }
  ]
}
[/block]
## Status Code
**Description**

[block:parameters]
{
  "data": {
    "0-0": "300",
    "h-0": "code",
    "h-1": "message",
    "h-2": "Description",
    "1-0": "301",
    "2-0": "1",
    "3-0": "0",
    "4-0": "101",
    "5-0": "1011",
    "6-0": "102",
    "7-0": "103",
    "8-0": "104",
    "9-0": "105",
    "10-0": "106",
    "11-0": "107",
    "12-0": "108",
    "13-0": "109",
    "14-0": "110",
    "15-0": "111",
    "16-0": "112",
    "17-0": "113",
    "18-0": "114",
    "19-0": "115",
    "20-0": "116",
    "21-0": "117",
    "22-0": "118",
    "23-0": "119",
    "24-0": "120",
    "25-0": "121",
    "26-0": "122",
    "27-0": "123",
    "28-0": "124",
    "29-0": "125",
    "30-0": "127",
    "31-0": "129",
    "32-0": "130",
    "33-0": "131",
    "34-0": "133",
    "35-0": "135",
    "36-0": "136",
    "37-0": "137",
    "38-0": "138",
    "39-0": "139",
    "40-0": "140",
    "41-0": "141",
    "42-0": "142",
    "43-0": "144",
    "44-0": "145",
    "45-0": "146",
    "46-0": "147",
    "47-0": "148",
    "48-0": "149",
    "49-0": "150",
    "50-0": "151",
    "51-0": "152",
    "52-1": "Please unlock your wallet first",
    "52-0": "153",
    "53-0": "154",
    "54-0": "155",
    "55-0": "156",
    "56-0": "157",
    "57-0": "158",
    "58-0": "159",
    "59-0": "160",
    "60-0": "161",
    "61-1": "The asset already exists",
    "61-0": "162",
    "62-0": "163",
    "63-0": "164",
    "64-0": "165",
    "65-0": "166",
    "66-0": "167",
    "67-0": "168",
    "68-0": "169",
    "2-2": "Operation succeeded",
    "3-2": "The operation failed, and the error status description is not fixed. You can directly prompt res.message or to prompt the operation failure.",
    "68-1": "Method does not exist",
    "67-1": "This subscription does not exist",
    "66-1": "The current contract version ID was not found",
    "65-1": "The Wallet Chain ID does not match the current chain configuration information. The chain ID of the wallet is: XX",
    "64-1": "There is no wallet account information on the chain",
    "63-1": "worldViews do not exist",
    "62-1": "The wallet already exists. Please try importing the private key",
    "60-1": "Orders do not exist",
    "59-1": "You are not the creator of the Asset XX",
    "58-1": "Account exists",
    "57-1": "Imported Wallet core assets can not be XX , and it should be XX",
    "56-1": "Can’t delete wallet, does not exist in index",
    "55-1": "The wallet has been imported. Do not repeat import",
    "54-1": "Your browser may not support wallet file recovery",
    "53-1": "Please restore your wallet first",
    "51-1": "Invalid backup to download conversion",
    "50-1": "File saving is not supported",
    "49-1": "Key import error",
    "48-1": "This wallet has already been imported",
    "47-1": "Request timeout, please try to unlock the account or login the account",
    "46-1": "NHAsset do not exist",
    "45-1": "The account does not contain information about the contract",
    "44-1": "XX contract not found",
    "43-1": "Your current batch creation / deletion / transfer number is X , and batch operations can not exceed X",
    "42-1": "Please check the data type of parameter NHAssets",
    "41-1": "Please check the data in parameter NHAssets",
    "40-1": "API server node address already exists",
    "39-1": "Node address must start with ws:// or wss://",
    "38-1": "Parameter ‘url’ can not be empty",
    "37-1": "Parameter ‘NHAssetHashOrIds’ can not be empty",
    "36-1": "Parameter ‘orderId’ can not be empty",
    "35-1": "Please check parameter data type",
    "34-1": "Parameter ‘toAccount’ can not be empty toAccount",
    "33-1": "Parameter ‘worldView’ can not be empty",
    "32-1": "Please enter the correct contract name(/^a-z{4,63}$/)",
    "31-1": "Parameter ‘memo’ can not be empty memo",
    "30-1": "No reward available",
    "29-1": "Users do not own XX assets",
    "28-1": "Receivables account name can not be empty",
    "27-1": "Parameter account can not be empty",
    "26-1": "Parameter blockOrTXID is incorrect",
    "25-1": "block and transaction information cannot be found",
    "24-1": "Error fetching account record",
    "23-1": "Expiry of the transaction",
    "22-1": "Encrypt memo failed",
    "21-1": "The current asset precision is configured as X ,and the decimal cannot exceed X",
    "20-1": "Account receivable does not exist",
    "19-1": "There is no asset XX on block chain",
    "18-1": "Account is locked or not logged in",
    "17-1": "Please enter the correct original/temporary password",
    "16-1": "Must have owner permission to change the password, please confirm that you imported the ownerPrivateKey",
    "15-1": "Please login first",
    "14-1": "The private key has no account information",
    "13-1": "Please enter the correct private key",
    "12-1": "User name or password error (please confirm that your account is registered in account mode, and the account registered in wallet mode cannot be logged in using account mode)",
    "11-1": "Please import the private key",
    "10-1": "The account is already unlocked",
    "9-1": "wrong password",
    "8-1": "XX not found",
    "7-1": "Please enter the correct account name(/^a-z{4,63}/$)",
    "6-1": "The network is busy, please check your network connection",
    "5-1": "Parameter error",
    "4-1": "Parameter is missing",
    "3-1": "failed",
    "2-1": "None",
    "1-1": "RPC connection failed. Please check your network",
    "0-1": "Chain sync error, please check your system clock"
  },
  "cols": 3,
  "rows": 69
}
[/block]