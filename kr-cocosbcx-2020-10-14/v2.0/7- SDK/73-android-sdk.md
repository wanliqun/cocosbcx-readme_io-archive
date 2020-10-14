---
title: "7.3 Android-SDK"
slug: "73-android-sdk"
hidden: false
createdAt: "2019-06-26T03:57:49.571Z"
updatedAt: "2019-06-26T04:38:29.801Z"
---
## Application Scope
This document is for Android COCOS wallet development. 
The SDK is applicable for Android 4.0 (API Level 14) or later, and the SDK currently chooses version 27 for beta compilation. 
**Note:**
Android P (version 27) limits the http network requests. However, http request is used in the SDK.

## Class Library Reference
 1. Copy bcx_sdk.aar to the project directory, select New Moudule in Project Structure (note that it is not to add module dependency), select Import JAR/arr Package, click Next, select the path where the arr file is located, click Finish, and add the bcx_sdkMoudle to the project by selecting Module dependency. 
This will not compile third-party dependencies into aar files, you need to add the following dependencies:

[block:code]
{
  "codes": [
    {
      "code": "// implenment websocket\n    implementation 'com.neovisionaries:nv-websocket-client:1.30'\n    // implenment bitcoinj\n    implementation 'org.bitcoinj:bitcoinj-core:0.14.7'\n    implementation group: 'com.google.code.gson', name: 'gson', version: '2.8.5'\n    implementation group: \"org.tukaani\", name: \"xz\", version: \"1.6\"\n    implementation 'com.squareup.okhttp3:okhttp:3.12.1'\n    // spongycastle\n    implementation 'com.madgag.spongycastle:core:1.58.0.0'\n    implementation 'com.madgag.spongycastle:prov:1.58.0.0'\n    implementation 'com.madgag.spongycastle:pkix:1.54.0.0'\n    implementation 'com.madgag.spongycastle:pg:1.54.0.0'\n    // fasterxml\n    implementation 'com.fasterxml.jackson.core:jackson-databind:2.9.7'",
      "language": "java"
    }
  ]
}
[/block]
2. Maven mode (not supported for the moment) 

[block:code]
{
  "codes": [
    {
      "code": "//Normal dependency\nimplementation 'com.cocos.android:cocos-sdk:1.0.0'\n\n//Turn off all dependency transit - method 1\nimplementation 'com.cocos.android:cocos-sdk:1.0.0@aar'\n\n//Turn off all dependency transit - method 2\nimplementation('com.cocos.android:cocos-sdk:1.0.0') {\n        transitive = false\n}\n",
      "language": "java"
    }
  ]
}
[/block]
## Note:
    1. Avoid creating a database of the same name:cocos_bcx_android_sdk.db;
    2.ERROR：INSTALL_FAILED_NO_MATCHING_ABIS
Solution
Add the following code to the app module's build.gradle android: 

[block:code]
{
  "codes": [
    {
      "code": "packagingOptions {\n        exclude 'lib/x86_64/darwin/libscrypt.dylib'\n        exclude 'lib/x86_64/freebsd/libscrypt.so'\n        exclude 'lib/x86_64/linux/libscrypt.so'\n    }",
      "language": "java"
    }
  ]
}
[/block]
## SDK initialization (items must be initialized before calling other interfaces, otherwise a null pointer error will be reported)

[block:code]
{
  "codes": [
    {
      "code": "List<String> mListNode = Arrays.asList(\"ws://47.93.62.96:8050\", \"ws://39.96.33.61:8080\", \"ws://39.96.29.40:8050\", \"ws://39.106.126.54:8050\");\n       String[] faucetUrl = {\"http://47.93.62.96:3000/api/v1/accounts\"};\n       String chainId = \"53b98adf376459cc29e5672075ed0c0b1672ea7dce42b0b1fe5e021c02bda640\";\n       String coreAsset = \"COCOS\";\n       boolean isOpenLog = true;\n       CocosBcxApiWrapper.getBcxInstance().init(this, chainId, mListNode, faucetUrl, coreAsset, isOpenLog,\n               new IBcxCallBack() {\n                   @Override\n                   public void onReceiveValue(String value) {\n                       Log.i(\"initBcxSdk\", value);\n                 }\n               });",
      "language": "java"
    }
  ]
}
[/block]
## SDK API User Guide
Callback data is a unified string type; 
The API call object is a singleton column object; Below is an example of an API call: 

[block:code]
{
  "codes": [
    {
      "code": " /**\n    * account model  create account\n    *\n    * @param strAccountName accountName\n    * @param strPassword    Password\n    * @param isAutoLogin    true :   log in， false:just register\n    * @param callBack\n    */           \nCocosBcxApiWrapper.getBcxInstance().create_password_account(\"*****\", \"*****\", true, new IBcxCallBack() {\n               @Override\n               public void onReceiveValue(String value) {\n                   Log.i(\"createaccwithpassword\", value);\n                   ToastUtils.showShort(value);\n               }\n           });",
      "language": "java"
    }
  ]
}
[/block]
## Status Code
**Description** 

[block:parameters]
{
  "data": {
    "h-0": "code",
    "h-1": "Message",
    "h-2": "Description",
    "0-0": "300",
    "0-1": "Chain sync error, please check your system clock",
    "1-0": "301",
    "1-1": "RPC connection failed. Please check your network",
    "2-0": "1",
    "2-1": "None",
    "3-0": "0",
    "3-1": "failed",
    "2-2": "Operation succeeded",
    "3-2": "The operation failed, and the error status description is not fixed. You can directly prompt res.message or to prompt the operation failure.",
    "4-0": "101",
    "4-1": "Parameter is missing",
    "5-0": "1011",
    "5-1": "Parameter error",
    "6-0": "102",
    "6-1": "The network is busy, please check your network connection",
    "7-0": "103",
    "7-1": "Please enter the correct account name(/^a-z{4,63}/$)",
    "8-0": "104",
    "8-1": "XX not found",
    "9-0": "105",
    "9-1": "wrong password",
    "10-0": "106",
    "10-1": "The account is already unlocked",
    "11-0": "107",
    "11-1": "Please import the private key",
    "12-0": "108",
    "12-1": "User name or password error (please confirm that your account is registered in account mode, and the account registered in wallet mode cannot be logged in using account mode)",
    "13-0": "109",
    "13-1": "Please enter the correct private key",
    "14-0": "110",
    "14-1": "The private key has no account information",
    "15-0": "111",
    "15-1": "Please login first",
    "16-0": "112",
    "16-1": "Must have owner permission to change the password, please confirm that you imported the ownerPrivateKey",
    "17-0": "113",
    "17-1": "Please enter the correct original/temporary password",
    "18-0": "114",
    "18-1": "Account is locked or not logged in.",
    "19-0": "115",
    "19-1": "There is no asset XX on block chain",
    "20-0": "116",
    "20-1": "Account receivable does not exist",
    "21-0": "117",
    "21-1": "The current asset precision is configured as X, and the decimal cannot exceed X",
    "22-0": "118",
    "22-1": "Encrypt memo failed",
    "23-0": "119",
    "23-1": "Expiry of the transaction",
    "24-0": "120",
    "24-1": "Error fetching account record",
    "25-0": "121",
    "25-1": "block and transaction information cannot be found",
    "26-0": "122",
    "26-1": "Parameter blockOrTXID is incorrect",
    "27-0": "123",
    "27-1": "Parameter account can not be empty",
    "28-0": "124",
    "28-1": "Receivables account name can not be empty",
    "29-0": "125",
    "29-1": "Users do not own XX assets",
    "30-0": "127",
    "30-1": "No reward available",
    "31-0": "129",
    "31-1": "Parameter ‘memo’ can not be empty",
    "32-0": "130",
    "32-1": "Please enter the correct contract name(/^a-z{4,63}$/)",
    "33-0": "131",
    "33-1": "Parameter ‘worldView’ can not be empty",
    "34-0": "133",
    "34-1": "Parameter ‘toAccount’ can not be empty",
    "35-0": "135",
    "35-1": "Please check parameter data type",
    "36-0": "136",
    "36-1": "Parameter ‘orderId’ can not be empty",
    "37-0": "137",
    "37-1": "Parameter ‘NHAssetHashOrIds’ can not be empty",
    "38-0": "138",
    "38-1": "Parameter ‘url’ can not be empty",
    "39-0": "139",
    "39-1": "Node address must start with ws:// or wss://",
    "40-0": "140",
    "40-1": "API server node address already exists",
    "41-0": "141",
    "41-1": "Please check the data in parameter NHAssets",
    "42-0": "142",
    "42-1": "Please check the data type of parameter NHAssets",
    "43-0": "144",
    "43-1": "Your current batch creation / deletion / transfer number is X , and batch operations can not exceed X",
    "44-0": "145",
    "44-1": "XX contract not found",
    "45-0": "146",
    "45-1": "The account does not contain information about the contract",
    "46-0": "147",
    "46-1": "NHAsset do not exist",
    "47-0": "148",
    "47-1": "Request timeout, please try to unlock the account or login the account",
    "48-0": "149",
    "48-1": "This wallet has already been imported",
    "49-0": "150",
    "50-0": "151",
    "49-1": "Key import error",
    "50-1": "File saving is not supported",
    "51-0": "152",
    "51-1": "Invalid backup to download conversion",
    "52-0": "153",
    "53-0": "154",
    "52-1": "Please unlock your wallet first",
    "53-1": "Please restore your wallet first",
    "54-0": "155",
    "54-1": "Your browser may not support wallet file recovery",
    "55-0": "156",
    "55-1": "The wallet has been imported. Do not repeat import",
    "56-0": "157",
    "56-1": "Can’t delete wallet, does not exist in index",
    "57-0": "158",
    "57-1": "Imported Wallet core assets can not be XX , and it should be XX",
    "58-0": "159",
    "58-1": "Account exists",
    "59-0": "160",
    "59-1": "You are not the creator of the Asset XX .",
    "60-0": "161",
    "60-1": "Orders do not exist",
    "61-0": "162",
    "61-1": "The asset already exists",
    "62-0": "163",
    "62-1": "The wallet already exists. Please try importing the private key",
    "63-0": "164",
    "63-1": "worldViews do not exist",
    "64-0": "165",
    "65-0": "166",
    "66-0": "167",
    "67-0": "168",
    "68-0": "169",
    "64-1": "There is no wallet account information on the chain",
    "68-1": "MethodMethod does not exist\t does not exist",
    "65-1": "The Wallet Chain ID does not match the current chain configuration information. The chain ID of the wallet is: XX",
    "66-1": "The current contract version ID was not found",
    "67-1": "This subscription does not exist"
  },
  "cols": 3,
  "rows": 69
}
[/block]
## API Examples
1. Wallet mode - create an account


[block:code]
{
  "codes": [
    {
      "code": " /**\n     * wallet model  create account\n     *\n     * @param strAccountName accountName\n     * @param strPassword    Password\n     * @param isAutoLogin    true :   log in， false:just register\n     * @param callBack\n     */\n  CocosBcxApiWrapper.getBcxInstance().create_wallet_account(\"testtest3\", \"111111\", true, new IBcxCallBack() {\n                @Override\n                public void onReceiveValue(String value) {\n                    Log.i(\"create_wallet_account\", value);\n                }\n            });",
      "language": "java"
    }
  ]
}
[/block]

[block:code]
{
  "codes": [
    {
      "code": "Return data 1 ：{\"code\":1,\"data\":{\"account\":{\"active_key\":\"COCOS6BGnotPV3232ZJBvp5FgZuZ5cGPqNgqaSHnbSoaJLjaKmV8LLE\",\"name\":\"testtest3\",\"owner_key\":\"COCOS8F9BeMjVqBVakgJhTm2pQoMido4ZBksfHL6oQb1ZWXtpmpBJF5\"}}}\n",
      "language": "java"
    }
  ]
}
[/block]

[block:code]
{
  "codes": [
    {
      "code": "Return data 2：{\"code\":159,\"message\":account exist}",
      "language": "java"
    }
  ]
}
[/block]

[block:code]
{
  "codes": [
    {
      "code": "Return data 3：{\"code\":102,\"message\":It doesn't connect to the server.}",
      "language": "java"
    }
  ]
}
[/block]
2.Transfer

[block:code]
{
  "codes": [
    {
      "code": " /**\n     * transfer\n     * @param password (Temporary password/account password)\n     * @param strFrom transfer from\n     * @param strTo transfer to\n     * @param strAmount transfer amount\n     * @param strAssetSymbol transferred asset symbol\n     * @param strMemo Memo\n     */\n CocosBcxApiWrapper.getBcxInstance().transfer(\"111111\", \"testtest3\", \"gnkhandsome1\", \"10\", \"COCOS\", \"testting\", new IBcxCallBack() {\n                @Override\n                public void onReceiveValue(String value) {\n                    Log.i(\"transfer\", value);\n                }\n            });",
      "language": "java"
    }
  ]
}
[/block]

[block:code]
{
  "codes": [
    {
      "code": "###Return data1 ：{\"code\":1,\"message\":bf3c058914399136d384de714a3c57d2966e1513}\nNOTE： hash : bf3c058914399136d384de714a3c57d2966e1513",
      "language": "java"
    }
  ]
}
[/block]

[block:code]
{
  "codes": [
    {
      "code": " Return data2: {\"code\":105,\"message\":wrong password}",
      "language": "java"
    }
  ]
}
[/block]
3. Export private key (The account logged in through the private key import can only export the private key imported at login.)

[block:code]
{
  "codes": [
    {
      "code": "CocosBcxApiWrapper.getBcxInstance().export_private_key(\"gnkhandsome1\", \"123456\", new IBcxCallBack() {\n                            @Override\n                            public void onReceiveValue(final String value) {\n                                   Log.i(\"export_private_key\", value);\n                                \n                            }\n                        });",
      "language": "java"
    }
  ]
}
[/block]
Return data (public key (Key), private key (Value)): 

[block:code]
{
  "codes": [
    {
      "code": "{\"code\":1,\"data\":{\"COCOS6G55VgR94GZmELS4UHEf2eVggmhPRnWLTWgGiEmzuBKdvEwoAB\":\"5Hy7aVcZFyHa7UKURN22m9gB7xp4KS7Bo1dibWSVZZYAg6Br1bu\",\"COCOS8Dw7QjWVFggYCvp9c8XbsXssqizN1MqkwPfSAVTQppQLhUcTC2\":\"5JgPmrWHevyH4ZzLkgZL3yAaddXE6phrKJYCfKyAJmhhjbmZyF7\"},\"message\":\"\"}",
      "language": "java"
    }
  ]
}
[/block]
4. Get the account balance (parameter 1:  user ID, parameter 2:  the asset ID whose balance is to be gotten, if it is empty, get the balance information of all assets in the account)

[block:code]
{
  "codes": [
    {
      "code": "List<Object> assetSymbolOrId = new ArrayList<>();\n      // todo default asset symbol\nassetSymbolOrId.add(\"1.3.0\");\nCocosBcxApiWrapper.getBcxInstance().get_account_balances(\"1.2.76\", unit, new IBcxCallBack() {\n          @Override\n          public void onReceiveValue(final String value) {\n                  Log.i(\"get_account_balances\", value);\n          }\n      });",
      "language": "java"
    }
  ]
}
[/block]
Return data:
[block:code]
{
  "codes": [
    {
      "code": "{\"id\":1,\"data\":[{\"amount\":55362897,\"asset_id\":\"1.3.0\"}]}",
      "language": "text"
    }
  ]
}
[/block]
## Interoperable API for Blockchain Systems
## Wallet mode
**Create an account**
Method: createAccountWithWallet

Function: To create an account with a wallet. The account created with the wallet cannot be logged in with account name and password. If an account already exists with the wallet, this operation will create a sub-account, which requires the account to be a lifetime member first.

Parameters: 
account: Account name registration rules, /^[a-z][a-z0-9.-]{4,63}$/, begin with lowercase letters + digits or lowercase letters or dots or dashes -, with a length of 4 to 63 characters
password: password
callback: callback function

**Backup wallet**
Method: backupDownload

 Function: To back up the wallet. Calling this API will generate a wallet file, which will be downloaded automatically 

Parameters: 
 callback: callback function

**Load backup wallet file **
Method: loadWalletFile

Function: For the web, the change event is bound to the file input to read the wallet file.

Parameters: 
 file: The host environment triggers the returned event object event.target, files[0] if the change event in web => file input
callback: callback function

**Restore wallet from backup file **
Method: restoreWallet

Function: To back up the wallet. Calling this API will generate a wallet file, which will be downloaded automatically. After the API is called, the wallet is locked.

Parameters: 
password: the wallet password of the backup file
callback: callback function

**Import private key **
Method: importPrivateKey

Function: To import private key to the wallet

Parameters: 
privateKey: unencrypted private key
password: If the wallet has been created or the wallet has been restored, the password is that of the original wallet, otherwise it is a temporary password that can be filled in freely.
callback: callback function

**Delete wallet**
Method: deleteWallet

Function: To delete the wallet. In the account mode, it’s better to delete the wallet first

Parameters: 
callback: callback function

**Get a list of wallet accounts **
Method: getAccounts

Function: To get a list of wallet accounts

Parameters: 
Return data directly, the example format is: 

[block:code]
{
  "codes": [
    {
      "code": "{  \n\t\t\"accounts\": [\"tom0002\"],  \n\t\t\"currentAccount\": {  \n\t\t\t\"account_id\": \"1.2.20\",  \n\t\t\t\"locked\": true,  \n\t\t\t\"account_name\": \"tom0002\"  \n\t\t}\n  }",
      "language": "javascript"
    }
  ]
}
[/block]
**Switch account**
Method: setCurrentAccount

Function: To switch current account in wallet mode

Parameters: 
account: the account to be switched to
callback: callback function

**Unlock account**
Method: unlockAccount

Function: This method can be used to unlock your account by importing private key or in the wallet mode.

Parameters: 
Password:  the temporary password set when importing the private key
Callback:  callback function

**Lock account**
Method: lockAccount

Function: Lock the account

Parameters:  
callback: callback function

## Account Mode
**Create an account**
Method: createAccountWithPassword

Function: To create an account. If there’s already an account logged in under account mode, this operation will create a sub-account, which requires the account to be a lifetime member first.

Parameters:  
account: Account name registration rules, /^[a-z][a-z0-9.-]{4,63}$/, begin with lowercase letters + digits or lowercase letters or dots or dashes -, with a length of 4 to 63 characters
password: password
autoLogin: Boolean type. it specifies whether to log in automatically with the default value of false
callback: callback function

**Account login**
Method: passwordLogin

Function: To login the account

Parameters: 
account: account name
password: password
callback: callback function

**Private key login**
Method: privateKeyLogin

Function: Previously, this API was just a transition. Strictly speaking, importing a private key exists only in the wallet mode. Now, this API is temporarily left here and is still available for calling for compatility.

Parameters: 
privateKey: Private key
password: Temporary password 
callback: callback function

**Logout**
Method: logout

Function: This method will clear the user-related cache, including clearing the encrypted ciphertext key.

Parameters: 
callback: callback function

**Change password**
Method:  changePassword

Function: The password can be changed only in the account mode; after the password is successfully changed, the API will automatically call the logout.

Parameters: 
oldPassword: old password
newPassword: new password
callback: callback function

**Get current account information**
Method: getAccountInfo

Function: When the account is unlocked, the return data will contain the account name

Parameters: None

## Account operation

**Upgrade to a lifetime membership account**
Method: upgradeAccount

Function: After purchasing a lifetime membership account, you can create a sub-account, which requires a certain fee.

Parameters:  
onlyGetFee: Whether to get this operation fee only
callback: callback function

**Export user private key**
Method: getPrivateKey

Function: Get the user’s active_private_key. This key can be used to sign all the expenditures of the account. The returned owner_private_key:  can modify various settings related to the account, including permission settings.

Parameters:  
callback: Set the callback function after successfully get the private key

**Query account record**
Method: queryAccountOperations

Function: To query user’s recent operation history

Parameters:  
account: account name
limit: Number of records queried
startId: The first account record id to be queried. If the query scope is the entire account record, the initial account record is startId
endId: The last account record id to be queried. If the scope of the query is the entire account record, the latest account record is the endId.
callback: See the unified API parameter description

**Subscribe to operation record changes**
Method: subscribeToAccountOperations

Function: To subscribe to operation record changes

Parameters:  
account: account name
callback: Call this callback whenever the user action record changes: callback function

**Query account information**
Method: queryAccountInfo

Function: The account information includes information such as the user id username.

Parameters:  
account: account name
callback: See the unified API parameter description

## Token operation interface

**Token asset transfer**
Method: transferAsset

Function: Send tokens to the recipient

Parameters:  
fromAccount: The sender's account name. it is not a proposal
toAccount: The recipient’s account name
amount: Amount of tokens sent
assetId: Asset ID (e.g. X.X.X) or token symbol (e.g. BTC)
memo: Transfer memo
feeAssetId: Token asset symbol used to pay for transfer fee
isPropose: Whether to propose
onlyGetFee（boolean）: Whether to get the transaction fee for this operation
callback: Set the callback function after the transfer

**Create an asset**
Method: createAsset

Function: To create a token

Parameters:  
assetId: Asset symbol, regular ^[.A-Z]+$
precision: precise to decimal digit
maxSupply: Maximum asset supply
description: Asset description, optional
onlyGetFee: Set to return only the fee required for this call
callback: See the unified API parameter description
coreExchangeRate(Object): 

[block:code]
{
  "codes": [
    {
      "code": "{  \n\t\t\tquoteAmount: quote asset(Created token, default 1),  \n\t\t\tbaseAmount: base asset (Core asset, default 1)  \n\t\t}",
      "language": "javascript"
    }
  ]
}
[/block]
**Update assets**
Method: updateAsset

Function: Update token

Parameters:  
assetId: Asset symbol, regular ^[.A-Z]+$
maxSupply: Maximum asset supply
newIssuer: Update issuer
description: Asset description, optional
onlyGetFee: Set to return only the fee required for this call
callback: See the unified API parameter description
coreExchangeRate(Object): Fee exchange rate

[block:code]
{
  "codes": [
    {
      "code": "{   \n\t\tquoteAmount: quote asset\n\t\tbaseAmount: base asset\n\t}",
      "language": "javascript"
    }
  ]
}
[/block]
**Burn asset**
Method: reserveAsset

Function: Burn token assets

Parameters:  
assetId: Asset symbol
amount: Amount to be destroyed
onlyGetFee: Set to return only the fee required for this call
callback: callback function

**Issue asset**
Method: issueAsset

Function: To issue token asset

Parameters:  
toAccount: Issue object
amount: Amount to be issued
assetId: Asset symbol
memo: memos, optional
onlyGetFee: Set to return only the fee required for this call
callback: callback function

**Asset fund fee pool**
Method: assetFundFeePool

Function: All fees will eventually be paid using the core asset token. The fee pool is used to cover the fee for the exchange from the secondary asset token to the core asset token so that the user can use the secondary token to pay the fee. If the balance in the funds pool is used up, the user will not be able to continue to use the secondary asset token to pay the transaction fee. Currently, the APIs that supports the use of secondary asset tokens as a fee include “transfer, vote, lifetime membership upgrade, asset issuance”, which will be expanded.

Parameters:  
assetId: Secondary asset token symbol requiring fund injection
amount: Amount of core asset tokens to be injected
onlyGetFee: Set to return only the fee required for this call
callback: callback function

**Collect asset fees**
Method: assetClaimFees

Function: The asset issuer can collect the accumulated fees here.

Parameters:  
assetId: Secondary asset token symbol to be collected
amount: Amount of secondary asset tokens
onlyGetFee: Set to return only the fee required for this call
callback: callback function

**Query the assets issued on the blockchain**
Method: queryAsset

Function: Token asset query

Parameters:  
assetId: Asset symbol, if this parameter is empty, all assets issued on the chain will be queried
callback: callback function

**Query specified asset balance of the account**
Method: queryAccountBalances

Function: Get the digital asset corresponding to the user. If the assetId is empty, all the tokens of the user will be returned.

Parameters:  
assetId: Asset ID or token symbol. Asset ID:  the unique token ID of the digital token (e.g. "X.X.X"), token symbol (e.g. "BTC")
account: Account name
callback: callback function

**Query the list of all asset balances in the account**
Method: queryAccountAllBalances

Function: Query the list of all assets owned by the user, including the conversion value of the asset to the unit of account. Core asset with a balance of 0 will be returned when the account has no asset balance

Parameters:  
unit: the unit of account will be exchanged to the asset, asset ID or token symbol based on the fee rate or the market price. Asset ID:  The unique token ID of the digital token (e.g. "X.X.X"), token symbol (e.g. "BTC")
account: account name
callback: callback function

## NH asset operation
**Register as a developer**
Method: registerCreator

Function: Register your current account as a developer

**Create a worldview**
Method: creatWorldView

Function: Create a supported NH asset worldview and register the current account (usually the game's account) with the blockchain system to support the NH asset worldview

Parameters:  
worldView: Worldview name, case sensitive

**Create NH asset**
Method: creatNHAsset

Function: Create a unique NH asset. This interface is for use only by NH asset manufacturers (blacksmiths).

Parameters:  
assetId: The applicable asset ID when the current NH asset is traded;
worldView: worldview
baseDescribe: The specific content description of the current NH assets, as defined by the creator;
ownerAccount: Specify the NH asset owner (NH asset ownership account, the default is NH asset creator) 
NHAssetsCount (Number):  Create the amount of NH assets, the default value is 1, only type 0 to create the same NH asset to take effect
type: Create the type of NH asset mode. The default value is 0. A value of 0 creates the same NH asset by default, and a value of 0 creates a different NH asset.
NHAssets (Array) example: 

[block:code]
{
  "codes": [
    {
      "code": "[{  \n\t \"assetId\": \"X.X.X\",  \n\t \"worldView\": \"TEST\",  \n\t \"baseDescribe\": \"{name:\\\"预言家\\\"}\",  \n\t \"ownerAccount\": \"test2\"  \n\t}, {  \n\t \"assetId\": \"X.X.X\",  \n\t \"worldView\": \"TEST\",  \n\t \"baseDescribe\": \"{name:\\\"女巫\\\"}\",  \n\t \"ownerAccount\": \"test2\"  \n\t}, {  \n\t \"assetId\": \"X.X.X\",  \n\t \"worldView\": \"TEST\",  \n\t \"baseDescribe\": \"{name:\\\"猎人\\\"}\",  \n\t \"ownerAccount\": \"test2\"  \n\t}]",
      "language": "javascript"
    }
  ]
}
[/block]
**Delete NH assets**
Method: deleteNHAsset

Function: Delete the entire NH asset data record, which is usually used when the product is to be destroyed (only the user can authorize the destruction of the data).

Parameters:  
NHAssetIds (Array): Unique ID of the NH asset instance; example:  [X.X.X, X.X.X]

**Transfer of NH assets**
Method: transferNHAsset

Function: Users can transfer their NH assets to another user

Parameters:  
toAccount: Account name the NH asset is transferred to
NHAssetIds（Array）: An array of multiple NH asset ids, example:  [X.X.X, X.X.X]

**Propose to link worldviews**
Method: proposeRelateWorldView

Function: Propose to link to a certain worldview, which requires the approval of the creator of the worldview

Parameters:  
worldView: Worldview to be linked

**Approve the proposal to link a worldview**
Method: approvalProposal

Function: Approve proposals of other users to link with the worldview

Parameters:  
proposalId: Proposal ID

**Get the proposal received by the current user**
Method: getAccountProposals

Function: Get the proposal received by the current operation user

## NH asset transaction interface
**Create an NH asset sales order**
Method: creatNHAssetOrder

Function: Sell NH assets (you can call the queryAccountGameItems function before the transaction, listing the user's NH assets so that the user can choose an asset to sell)

Parameters:  
otcAccount: OTC transaction platform account, used to collect the pending order fee; (filled in the OTC platform)
orderFee: Pending order fee, the pending order fee paid by the user to the OTC platform account; (filled in the OTC platform)
NHAssetId: The unique identifier ID of the NH asset instance; (filled in by users)
price: Pending order price; (filled in by users)
priceAssetId: The token type for the price of the pending order; (filled in by users)
expiration: Order time, such as 3600 (seconds), is 1 hour
memo: Memo for the pending order
callback: Set the callback function after executing the pending order 

**Purchase order NH assets**
Method: fillNHAssetOrder

Function: Buy NH assets, pay the token for purchasing game equipment, and modify the product data owned by the user. This is a multi-step atomic operation, where the NH asset data of the user account is updated while paying the fee. If any action in the updating of the assets data is not recognized by the block of the main chain, the entire transaction will be rolled back to avoid abnormal transaction.

Parameters:  
orderId: order ID
callback: callback function

**Cancel the NH asset sales order**
Method: cancelNHAssetOrder

Function: Cancel NH asset sale order

Parameters:  
orderId: order ID
callback: callback function

## NH asset query interfaces
**Query the NH asset sales orders of the network users**
Method: queryNHAssetOrders

Function: Query the NH asset sales orders of the network users

Parameters:  
assetIds(array): Asset symbol or id screening 
worldViews (array): Version name or version id screening
pageSize: Page size
page: Number of pages

**Query the NH asset sales order of the specified user**
Method: queryAccountNHAssetOrders

Function: Query the NH asset sales order of the specified user

Parameters:  
account: Query account name or account ID
pageSize: Page size
page: Number of pages
callback: callback function

**Query the NH assets of the item under the account**
Method: queryAccountNHAssets

Function: Read all NH assets under the current user account that can be used in the corresponding game

Parameters:  
account: Account name or account ID
worldViews (array): Set of worldviews
page: Number of pages
pageSize: Page size, number of data per page
callback: Return value. Example: 
{status: 1,data: [],total: 0}

**Query the worldview linked with the developer**
Method: queryNHCreator

Function: Query the worldview linked with the developer

Parameters:  
account: Account name or account ID
callback: callback function

**Query the NH assets created by the developer**
Method: queryNHCreator

Function: Query the NH assets created by the developer

Parameters:  
account: Account name or account ID
callback: callback function

**Query the details of NH asset**
Method: queryNHAssets

Function: Query the details of NH asset

Parameters:  
NHAssetIds: NH asset id or hash
callback: callback function

**Query the details of worldview**
Method: lookupWorldViews

Function: Query the details of worldview

Parameters:  
worldViews (array): Worldview name or id
callback: callback function

## Node vote
**Query the data of node votes**
Method: queryVotes

Function: Query the data of node votes

Parameters:  
callback: callback function

**User submits voting information**
Method: publishVotes

Function: The proxy account is set when saving, which will be followed by the user’s voting information.

Parameters:  
witnessesIds（array）: Set of node account ids. The query node vote data will have the account ID of each node
proxyAccount: Proxy account name
callback: callback function

## Blockchain explorer interface
**Query the block**
Method: queryBlock

Function: Query block information by block height

Parameters:  
block: Block height

**Query the transaction**
Method: queryTransaction

Function: Query transaction information by transaction id (ie transaction hash)

Parameters:  
transactionId: Transaction id

**Query information by ids**
Method: queryDataByIds 

Function: Query related data by id

Parameters:  
ids(Array): Set of ID array 

**Subscribe to the blocks**
Method: subscribeToBlocks

Function: Monitor real-time block information

Parameters:  
isReqTrx: Whether the subscribed block contains transaction information, which is included by default.
callback: callback function

**Subscribe to blockchain transactions**
Method: subscribeToChainTranscation

Function: Monitor blockchain transactions across the network

Parameters:  
callback: callback function

**View the block generation information of the node**
Method: lookupWitnessesForExplorer

Function: The key point is to refer to the demo parsing block generation data of the node.

Parameters:  
callback: callback function

**View block rewards of the account node**
Method: lookupBlockRewards

Function: Analyze data with reference to demo

Parameters:  
callback: callback function

**Collect block reward**
Method: claimVestingBalance

Function: Collect block reward

Parameters:  
id: Reward ID. The ID will be included in the query block rewards.
callback: callback function

## API server node related interface
**BCX initialization**
Method: init

Function: Initialization includes RPC connection, reloading Indexedb data, etc.

Parameters:  
refresh: Optional, after the first init, the second init will use the cache information. Data will be reloaded and the RPC module will be reinitialized only if the refresh is true
autoReconnect: Optional, whether to reconnect after the RPC is disconnected
subscribeToRpcConnectionStatusCallback: Optional, monitor RPC connection status, return status=>closed:  rpc connection is closed, error:  rpc connection error, realopen:  rpc connection is successful. There will provide a separate method for monitoring.
callback: optional, callback function

**View the list of API server nodes**
Method: lookupWSNodeList

Function: View the list of API server nodes

Parameters:  
refresh: Whether to refresh the ping. This can only refresh the non-current connection node, if you want to refresh all, call init({refresh: true})
callback: callback functioncallback function

**Connect to the API server node**
Method: switchAPINode

Function: Switch node

Parameters:  
url: API server node address, this address must be the websoket address in the API server node list
callback: callback function

*Add a new API server node**
Method: addAPINode

Function: Add a new API server node

Parameters:  
name: New node name
url: API server node websoket address
callback: callback function

**Delete API server node**
Method: deleteAPINode

Function: Delete node

Parameters:  
url: API server node websoket address
callback: callback function

**Monitor connection state changes with API server nodes**
Method: subscribeToRpcConnectionStatus

Function: Monitor rpc connection status changes

Parameters:  
callback: The callback returns status, including the following results: 
closed: Rpc connection closed
error: Rpc connection error
realopen: Rpc connection succeeded

## Contract
**Generate private key/public key (randomly generated)**
Method: generateKeys

Function: Randomly generate a pair of public and private keys, which will be used when creating a contract with permissions. The generated private key is used for API initialization to authorize the contract, which will be returned directly without callback

**Create a contract**
Method:  createContract

Function:  Create a smart contract. If you want to set permissions on the contract, you must add a specific lua code when creating the contract, and call the contract function set_permissions_flag => contract authority code:  function my_change_contract_authority( publickey) assert(is_owner()) change_contract_authority( publickey) end function set_permissions_flag(flag) assert(is_owner()) set_permissions_flag(flag) end

Parameters:  
authority: Contract authority (public key publicKey in a pair of public and private keys), the developer can configure the private key when using the API initialization, and configure the private key corresponding to the public key to call the contract.
name: Contract name, regular /^[az][a-z0-9.-]{4,63}$/, beginning with the letter + letters or numbers or dot. or dash -, length 4 to 63 data:  contract lua Code
onlyGetFee: Set to return only the fee required for this operation
callback: See the unified API parameter description

**Update the contract**
Method: updateContract

Function: Update contract code

Parameters:  
nameOrId: Contract name or Id，Example: contract.test02
data: Contract lua code
onlyGetFee: Set to return only the fee for this operation

**Contract call**
Method: callContractFunction

Function: Call contract function interface

Parameters:  
nameOrId: Contract name or Id，Example: contract.test02
functionName: Function name in the contract，my_nht_describe_change（Modify item properties）
valueList(array): Call the parameter list of the contract function, example: [4.2.0,{"size": "large"}] , If the parameter passes a json string, the contract needs to call cjson parsing. If the object is passed, no cjson parsing is required.
runtime: The time (in milliseconds) to run the contract function with a default of 5
onlyGetFee: Set to return only the fee for this operation with a default of false
callback: callback function

**Query contract information**
Method: queryContract

Function: Query contract information data

Parameters:  
nameOrId: Contract name or Id
callback: callback function

**Query account contract data**
Method: queryAccountContractData

Function: Query data generated in the account contract

Parameters:  
account: Account name or Id
contractNameOrId: Contract name or Id
callback: callback function

## Others
**Unsubscribe**
Unsubscribe Method: unsubscribe

Function: Unsubscribe

Parameters:  
method(Array): Cancel the method name of the specified subscription, such as unsubscribing to block and blockchain transactions ['subscribeToBlocks', 'subscribeToBlocks'], without passing this parameter, cancel all subscriptions. This method returns a promise without passing a callback. Note:  If you need to specify to cancel a user's subscription, the parameter is ['subscribeToAccountOperation|account']
callback: callback function

**Decode transaction memo**
Method: decodeMemo

Function: There is no callback, the result is returned directly, and the result is an object containing the memo text. The method is passed directly, but not the wrapped options object parameter. Example:  bcl.decodeMemo(raw_data.memo) where raw_data is the transaction raw data.

**Get the transaction base fee**
Method: queryTransactionBaseFee

Function: Get the transaction type base fee

Parameters:  
transactionType: transaction type, example: transfer
feeAssetId: Select the token type asset symbol or ID to pay the fee
callback: See the unified API description

## transactionType list

[block:parameters]
{
  "data": {
    "h-0": "transactionType",
    "h-1": "Corresponding API",
    "0-0": "transfer",
    "0-1": "transferAsset",
    "1-0": "account_create",
    "1-1": "createAccountWithPassword",
    "2-0": "account_update",
    "2-1": "changePassword",
    "3-0": "account_upgrade",
    "3-1": "upgradeAccount",
    "4-0": "asset_create",
    "4-1": "createAsset",
    "5-0": "asset_issue",
    "5-1": "issueAsset",
    "6-0": "proposal_update",
    "6-1": "submitProposal",
    "7-0": "vesting_balance_withdraw",
    "7-1": "claimVestingBalance",
    "8-0": "contract_create",
    "8-1": "createContract",
    "9-0": "call_contract_function",
    "9-1": "callContractFunction",
    "10-0": "register_creator",
    "10-1": "registerCreator",
    "11-0": "creat_world_view",
    "11-1": "creatWorldView",
    "12-0": "propose_relate_world_view",
    "12-1": "proposeRelateWorldView",
    "13-0": "creat_nh_asset",
    "13-1": "creatNHAsset",
    "14-0": "delete_nh_asset",
    "14-1": "delete_nh_asset",
    "15-0": "transfer_nh_asset",
    "15-1": "transferNHAsset",
    "16-0": "creat_nh_asset_order",
    "16-1": "creatNHAssetOrder",
    "17-0": "cancel_nh_asset_order",
    "17-1": "cancelNHAssetOrder",
    "18-0": "fill_nh_asset_order",
    "18-1": "fillNHAssetOrder",
    "19-0": "limit_order_create",
    "20-0": "limit_order_cancel",
    "19-1": "createLimitOrder",
    "20-1": "cancelLimitOrder"
  },
  "cols": 2,
  "rows": 21
}
[/block]