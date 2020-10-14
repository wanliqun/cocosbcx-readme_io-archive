---
title: "8.2 iOS-SDK"
slug: "75-ios-sdk"
excerpt: "CocosSDK 集成使用文档"
hidden: false
createdAt: "2019-03-25T09:31:37.504Z"
updatedAt: "2019-12-12T09:40:15.158Z"
---
## Example
要运行示例项目，请克隆repo，然后首先从示例目录运行’pod install’。

## 依赖库

AFNetworking
FMDB
Secp256k1_A
SocketRocket

## 安装
1.使用 CocoaPods 集成安装

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
2.手动集成

   添加 CocosSDK 目录下 Class 文件夹所有文件。
   添加依赖库到项目中。

## 基础功能
**初始化**
1.说明和用途
   初始化 SDK 基础，连接节点、配置 ChainId 和链标识

2.接口函数
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
3.示例代码
[block:code]
{
  "codes": [
    {
      "code": " - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions\n{\n // 测试节点\n [[CocosSDK shareInstance] Cocos_ConnectWithNodeUrl:@\"ws://39.106.126.54:8050\" Fauceturl:@\"http://47.93.62.96:3000\" TimeOut:2 CoreAsset:@\"COCOS\" ChainId:@\"53b98adf376459cc29e5672075ed0c0b1672ea7dce42b0b1fe5e021c02bda640\" ConnectedStatus:^(WebsocketConnectStatus connectStatus) {\n }];\n return YES;\n}",
      "language": "objectivec"
    }
  ]
}
[/block]
## 设置日志输出
1.说明和用途
   设置是否在console输出sdk的log信息
2.接口函数
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
{
  "title": ""
}
[/block]
## 创建账户

**说明和用途**
**钱包模式**
     钱包模式创建账户，钱包模式创建的账户不能用账户名密码登录
**账户模式**
     账户模式创建账户，钱包模式创建的账户可以用账户名密码登录
1.接口函数
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
## 删除/退出钱包
1.使用说明
   清除 SDK 保存的登录和导入记录

2.接口函数
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
## 登录钱包
1.使用说明
   账户模式下，使用账户名和密码登录钱包

2.接口函数
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
## 转账
1.使用说明
   转账

2.接口函数
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
## 状态码
**状态码说明** 
[block:parameters]
{
  "data": {
    "0-0": "300",
    "0-1": "Chain sync error, please check your system clock",
    "0-2": "链同步错误，请检查您的系统时钟",
    "h-0": "code",
    "h-1": "message",
    "h-2": "说明",
    "1-0": "301",
    "1-1": "RPC connection failed. Please check your network",
    "1-2": "连接RPC失败，请检查你的网络",
    "2-0": "1",
    "2-1": "无",
    "2-2": "操作成功",
    "3-0": "0",
    "3-1": "failed",
    "3-2": "操作失败，返回错误状态描述不固定，可直接提示res.message或统一提示为操作失败",
    "4-0": "101",
    "4-1": "Parameter is missing",
    "4-2": "参数缺失",
    "5-0": "1011",
    "5-1": "Parameter error",
    "5-2": "参数错误",
    "6-0": "102",
    "6-1": "The network is busy, please check your network connection",
    "6-2": "网络繁忙，请检查你的网络连",
    "7-0": "103",
    "7-1": "Please enter the correct account name(/^a-z{4,63}/$)",
    "7-2": "请输入正确的账户名(正则/^a-z{4,63}/$)",
    "8-0": "104",
    "8-1": "XX not found",
    "8-2": "XX 不存在",
    "9-0": "105",
    "9-1": "wrong password",
    "9-2": "密码错误",
    "10-0": "106",
    "10-1": "The account is already unlocked",
    "10-2": "账户已经处于解锁状态",
    "11-0": "107",
    "11-1": "Please import the private key",
    "11-2": "请先导入私钥",
    "12-0": "108",
    "12-1": "User name or password error (please confirm that your account is registered in account mode, and the account registered in wallet mode cannot be logged in using account mode)",
    "12-2": "用户名或密码错误(请确认你的账户是通过账户模式注册的，钱包模式注册的账户不能使用账户模式登录)",
    "13-0": "109",
    "13-1": "Please enter the correct private key",
    "13-2": "请输入正确的私钥",
    "14-0": "110",
    "14-1": "The private key has no account information",
    "14-2": "该私钥没有对应的账户信息",
    "15-0": "111",
    "15-1": "Please login first",
    "15-2": "请先登录",
    "16-0": "112",
    "16-1": "Must have owner permission to change the password, please confirm that you imported the ownerPrivateKey",
    "16-2": "必须拥有owner权限才可以进行密码修改,请确认你导入的是ownerPrivateKey",
    "17-0": "113",
    "17-1": "Please enter the correct original/temporary password",
    "17-2": "请输入正确的原始密码/临时密码",
    "18-0": "114",
    "18-1": "Account is locked or not logged in",
    "18-2": "帐户被锁定或未登录",
    "19-0": "115",
    "19-1": "There is no asset XX on block chain",
    "19-2": "区块链上不存在资产 XX",
    "20-0": "116",
    "20-1": "Account receivable does not exist",
    "20-2": "收款方账户不存在",
    "21-0": "117",
    "21-1": "The current asset precision is configured as X ,and the decimal cannot exceed X",
    "21-2": "当前资产精度配置为 X ，小数点不能超过 X",
    "22-0": "118",
    "22-1": "Encrypt memo failed",
    "22-2": "备注加密失败",
    "23-0": "119",
    "23-1": "Expiry of the transaction",
    "23-2": "交易过期",
    "24-0": "120",
    "24-1": "Error fetching account record",
    "24-2": "获取帐户记录错误",
    "25-0": "121",
    "26-0": "122",
    "27-0": "123",
    "25-1": "block and transaction information cannot be found",
    "25-2": "查询不到相关区块及交易信息",
    "26-1": "Parameter blockOrTXID is incorrect",
    "26-2": "参数blockOrTXID不正确",
    "27-1": "Parameter account can not be empty",
    "27-2": "参数account不能为空",
    "28-0": "124",
    "29-0": "125",
    "30-0": "127",
    "30-1": "No reward available",
    "30-2": "没有可领取的奖励",
    "29-1": "Users do not own XX assets",
    "29-2": "用户未拥有 XX 资产",
    "28-1": "Receivables account name can not be empty",
    "28-2": "收款方账户名不能为空",
    "31-0": "129",
    "32-0": "130",
    "33-0": "131",
    "31-1": "Parameter ‘memo’ can not be empty\tmemo",
    "31-2": "不能为空",
    "32-1": "Please enter the correct contract name(/^a-z{4,63}$/)",
    "32-2": "请输入正确的合约名称(正则/^a-z{4,63}$/)",
    "33-1": "Parameter ‘worldView’ can not be empty",
    "33-2": "世界观名称不能为空",
    "34-0": "133",
    "35-0": "135",
    "36-0": "136",
    "34-1": "Parameter ‘toAccount’ can not be empty\ttoAccount",
    "34-2": "不能为空",
    "35-1": "Please check parameter data type",
    "35-2": "请检查参数数据类型",
    "36-1": "Parameter ‘orderId’ can not be empty",
    "36-2": "orderId不能为空",
    "37-0": "137",
    "38-0": "138",
    "39-0": "139",
    "40-0": "140",
    "37-1": "Parameter ‘NHAssetHashOrIds’ can not be empty",
    "37-2": "NHAssetHashOrIds不能为空",
    "38-1": "Parameter ‘url’ can not be empty",
    "38-2": "接入点地址不能为空",
    "39-1": "Node address must start with ws:// or wss://",
    "39-2": "节点地址必须以 ws:// 或 wss:// 开头",
    "40-1": "API server node address already exists",
    "40-2": "API服务器节点地址已经存在",
    "41-0": "141",
    "42-0": "142",
    "43-0": "144",
    "44-0": "145",
    "41-1": "Please check the data in parameter NHAssets",
    "41-2": "请检查参数NHAssets中的数据",
    "42-1": "Please check the data type of parameter NHAssets",
    "42-2": "请检查参数NHAssets的数据类型",
    "43-1": "Your current batch creation / deletion / transfer number is X , and batch operations can not exceed X",
    "43-2": "您当前批量 创建/删除/转移 NH资产数量为 X ，批量操作数量不能超过 X",
    "44-1": "XX contract not found",
    "44-2": "XX 合约不存在",
    "45-0": "146",
    "46-0": "147",
    "48-0": "149",
    "49-0": "150",
    "47-0": "148",
    "45-2": "账户没有该合约相关的信息",
    "45-1": "The account does not contain information about the contract",
    "46-2": "非同质资产不存在",
    "46-1": "NHAsset do not exist",
    "47-2": "请求超时，请尝试解锁账户或登录账户",
    "47-1": "Request timeout, please try to unlock the account or login the account",
    "48-2": "此私钥已导入过钱包",
    "48-1": "This wallet has already been imported",
    "49-2": "导入私钥失败",
    "49-1": "Key import error",
    "50-0": "151",
    "51-0": "152",
    "52-0": "153",
    "53-0": "154",
    "54-0": "155",
    "50-2": "您的浏览器不支持文件保存",
    "50-1": "File saving is not supported",
    "51-1": "Invalid backup to download conversion",
    "51-2": "无效的备份下载转换",
    "52-1": "Please unlock your wallet first",
    "52-2": "请先解锁钱包",
    "53-1": "Please restore your wallet first",
    "53-2": "请先恢复你的钱包",
    "54-1": "Your browser may not support wallet file recovery",
    "54-2": "浏览器不支持钱包文件恢复",
    "55-0": "156",
    "56-0": "157",
    "57-0": "158",
    "58-0": "159",
    "59-0": "160",
    "55-2": "该钱包已经导入，请勿重复导入",
    "55-1": "The wallet has been imported. Do not repeat import",
    "56-1": "Can’t delete wallet, does not exist in index",
    "56-2": "请求超时，请尝试解锁账户或登录账户",
    "57-1": "Imported Wallet core assets can not be XX , and it should be XX",
    "57-2": "导入的钱包核心资产不能为 XX ，应为 XX",
    "58-1": "Account exists",
    "58-2": "账户已存在",
    "59-1": "You are not the creator of the Asset XX .",
    "59-2": "你不是该资产的创建者",
    "60-0": "161",
    "61-0": "162",
    "62-0": "163",
    "63-0": "164",
    "64-0": "165",
    "60-1": "Orders do not exist",
    "60-2": "订单不存在",
    "61-1": "The asset already exists",
    "61-2": "资产已存在",
    "62-1": "The wallet already exists. Please try importing the private key",
    "62-2": "钱包已经存在，请尝试导入私钥",
    "63-1": "worldViews do not exist",
    "63-2": "世界观不存在",
    "64-1": "There is no wallet account information on the chain",
    "64-2": "链上没有该钱包账户信息",
    "65-0": "166",
    "66-0": "167",
    "67-0": "168",
    "68-0": "169",
    "68-2": "API方法不存在",
    "68-1": "Method does not exist",
    "67-1": "This subscription does not exist",
    "67-2": "当前没有订阅此项",
    "66-2": "当前合约版本id没有找到 X",
    "66-1": "The current contract version ID was not found",
    "65-2": "该钱包链id与当前链配置信息不",
    "65-1": "The Wallet Chain ID does not match the current chain configuration information. The chain ID of the wallet is: XX"
  },
  "cols": 3,
  "rows": 69
}
[/block]
## 合作项目
CocosBCXWallet

## 开源地址
[iOSSDK](https://github.com/Cocos-BCX/iOSSDK)