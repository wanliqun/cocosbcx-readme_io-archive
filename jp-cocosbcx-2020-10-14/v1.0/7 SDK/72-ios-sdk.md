---
title: "7.3 iOS-SDK"
slug: "72-ios-sdk"
hidden: false
createdAt: "2019-09-18T04:37:40.451Z"
updatedAt: "2019-09-18T05:07:11.399Z"
---
[block:api-header]
{
  "title": "Example"
}
[/block]
例を実行するには、repoをcloneしてから、例のディレクトリから「pod install」を実行してください。
[block:api-header]
{
  "title": "依存ライブラリ"
}
[/block]
AFNetworking
FMDB
Secp256k1_A
SocketRocket
[block:api-header]
{
  "title": "インストール"
}
[/block]
**1．CocosPodsでインテグレーション** 
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
**2．手動インストール**
CocosSDKディレクトリのClassフォルダ内すべてのファイルをします。
依存ライブラリをプロジェクトに追加します。
[block:api-header]
{
  "title": "基本機能"
}
[/block]
**初期化**
1．説明
SDKの初期化、ノードへのアクセス、ChainIdとチェーン識別子の設定

2．インターフェイス関数
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
3．コード例
[block:code]
{
  "codes": [
    {
      "code": "- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions\n{\n // テストノード\n [[CocosSDK shareInstance] Cocos_ConnectWithNodeUrl:@\"ws://39.106.126.54:8050\" Fauceturl:@\"http://47.93.62.96:3000\" TimeOut:2 CoreAsset:@\"COCOS\" ChainId:@\"53b98adf376459cc29e5672075ed0c0b1672ea7dce42b0b1fe5e021c02bda640\" ConnectedStatus:^(WebsocketConnectStatus connectStatus) {\n }];\n return YES;\n}",
      "language": "objectivec"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "ログのアウトプットを設定"
}
[/block]
1．説明
consoleでSDKのログをアウトプットするかどうかを設定します。

2．インターフェイス関数
[block:code]
{
  "codes": [
    {
      "code": "/**\n  *  Open debug log\n  *\n  *  @param isOpen YES means open，No means close\n  */\n - (void)Cocos_OpenLog:(BOOL)isOpen;",
      "language": "objectivec"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "アカウントの作成"
}
[/block]
**説明**

**ウォレットモード**
ウォレットモードでアカウントを作成します。このモードで作成した場合、アカウント名・パスワードでログインできません。

**アカウントモード**
アカウントモードでアカウントを作成します。このモードで作成した場合、アカウント名・パスワードでログインできます。

1．インターフェイス関数
[block:code]
{
  "codes": [
    {
      "code": "/**\n  Create account\n\n  @param walletMode  Mode of wallet\n  @param accountName Account\n  @param password    Password\n  @param autoLogin   Auto log in\n  */\n - (void)Cocos_CreateAccountWalletMode:(CocosWalletMode)walletMode\n      AccountName:(NSString *)accountName\n         Password:(NSString *)password\n        AutoLogin:(BOOL)autoLogin\n          Success:(SuccessBlock)successBlock\n            Error:(Error)errorBlock;",
      "language": "objectivec"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "ウォレットのログアウト/削除"
}
[/block]
1．説明
SDKで保存したログインとインポートデータをクリアします。

2．インターフェイス関数
[block:code]
{
  "codes": [
    {
      "code": "Objective-C\n/**\n  Delete wallet\n  @param accountName Account\n  */\n - (void)Cocos_DeleteWalletAccountName:(NSString *)accountName\n           Success:(SuccessBlock)successBlock\n             Error:(Error)errorBlock;",
      "language": "objectivec"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "ウォレットへのログイン"
}
[/block]
1．説明
アカウントモードでは、アカウント名とパスワードでログインします

2．インターフェイス関数
[block:code]
{
  "codes": [
    {
      "code": "/**\n  Log in by account\n\n  @param accountName Account\n  @param password    Password\n  */\n - (void)Cocos_LoginAccountWithName:(NSString *)accountName\n           Password:(NSString *)password\n             Success:(SuccessBlock)successBlock\n               Error:(Error)errorBlock;",
      "language": "objectivec"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "取引"
}
[/block]
1．説明
振込

2．インターフェイス関数
[block:code]
{
  "codes": [
    {
      "code": "/**\n  Transfer\n\n  @param fromName        Sender's account\n  @param toName          Receiver's account\n  @param password        Password\n  @param transferAsset   Asset's name(eg. COCOS)\n  @param assetAmount     assetAmount Transfer amount\n  @param feePayingAsset  Charge's currency(require)\n  @param memo            Memo String\n  */\n - (void)Cocos_TransferFromAccount:(NSString *)fromName\n               ToAccount:(NSString *)toName\n                Password:(NSString *)password\n           TransferAsset:(NSString *)transferAsset\n             AssetAmount:(NSString *)assetAmount\n          FeePayingAsset:(NSString *)feePayingAsset\n                    Memo:(NSString *)memo\n               Success:(SuccessBlock)successBlock\n                 Error:(Error)errorBlock;",
      "language": "objectivec"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "ステータスコード"
}
[/block]
**一覧と説明** 
[block:parameters]
{
  "data": {
    "h-0": "code",
    "h-1": "message",
    "h-2": "Description",
    "0-0": "300",
    "0-1": "Chain sync error, please check your system clock",
    "1-0": "301",
    "1-1": "RPC connection failed. Please check your network",
    "2-0": "1",
    "2-1": "None",
    "2-2": "Operation succeeded",
    "3-0": "0",
    "3-1": "failed",
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
    "18-1": "Account is locked or not logged in",
    "19-0": "115",
    "19-1": "There is no asset XX on block chain",
    "20-0": "116",
    "20-1": "Account receivable does not exist",
    "21-0": "117",
    "21-1": "The current asset precision is configured as X ,and the decimal cannot exceed X",
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
    "31-1": "Parameter ‘memo’ can not be empty memo",
    "32-0": "130",
    "32-1": "Please enter the correct contract name(/^a-z{4,63}$/)",
    "33-0": "131",
    "33-1": "Parameter ‘worldView’ can not be empty",
    "34-0": "133",
    "34-1": "Parameter ‘toAccount’ can not be empty toAccount",
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
    "49-1": "Key import error",
    "50-0": "151",
    "50-1": "File saving is not supported",
    "51-0": "152",
    "51-1": "Invalid backup to download conversion",
    "52-0": "153",
    "52-1": "Please unlock your wallet first",
    "53-0": "154",
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
    "59-1": "You are not the creator of the Asset XX",
    "60-0": "161",
    "60-1": "Orders do not exist",
    "61-0": "162",
    "61-1": "The asset already exists",
    "62-0": "163",
    "62-1": "The wallet already exists. Please try importing the private key",
    "63-0": "164",
    "63-1": "worldViews do not exist",
    "64-0": "165",
    "64-1": "There is no wallet account information on the chain",
    "65-0": "166",
    "65-1": "The Wallet Chain ID does not match the current chain configuration information. The chain ID of the wallet is: XX",
    "66-0": "167",
    "66-1": "The current contract version ID was not found",
    "67-0": "168",
    "67-1": "This subscription does not exist",
    "68-0": "169",
    "68-1": "Method does not exist"
  },
  "cols": 3,
  "rows": 69
}
[/block]

[block:api-header]
{
  "title": "GitHub"
}
[/block]
[iOSSDK](https://github.com/Cocos-BCX/iOSSDK)