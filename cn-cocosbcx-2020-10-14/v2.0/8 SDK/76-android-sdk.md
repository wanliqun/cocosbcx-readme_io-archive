---
title: "8.3 Android-SDK"
slug: "76-android-sdk"
hidden: false
createdAt: "2019-03-25T09:32:06.209Z"
updatedAt: "2019-12-13T03:13:18.950Z"
---
## 适用范围
该文档适用于Android cocos 钱包开发.
SDK适用于Android4.0 (API Level 14)及以上版本，SDK目前测试版编译版本选择27.
**注意：**
Android P(版本27以上) 对网络请求http限制，SDK中有使用http请求

## 类库引用说明
 1.将bcx_sdk.aar复制到项目目录下，在Project Structure里选择New Moudule(注意不是添加Module dependency), 选择Import JAR/arr Package，点击Next,选择arr文件所在的路径, 点击Finish,选择Module dependency里将bcx_sdkMoudle添加到项目里即可
这种方式不会将第三方依赖编译进aar文件，需要添加以下依赖：
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
2.Maven 方式引入（暂不支持） 
[block:code]
{
  "codes": [
    {
      "code": "//正常依赖\nimplementation 'com.cocos.android:cocos-sdk:1.0.0'\n\n//关闭全部依赖传递-方法1\nimplementation 'com.cocos.android:cocos-sdk:1.0.0@aar'\n\n//关闭全部依赖传递-方法2\nimplementation('com.cocos.android:cocos-sdk:1.0.0') {\n        transitive = false\n}\n",
      "language": "java"
    }
  ]
}
[/block]
## 注意：
    1.避免创建同名数据库：cocos_bcx_android_sdk.db;
    2.ERROR：INSTALL_FAILED_NO_MATCHING_ABIS
解决方案
    在app模块的build.gradle android下添加以下代码：
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
## SDK 初始化 （调用其他接口前必须初始化项目 ，否则会报空指针错误） 
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
## SDK API 使用说明
回调数据为统一string 类型；
API 调用对象为单列对象；

下面给出API调用示例：
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
## 状态码
**状态码说明** 
[block:parameters]
{
  "data": {
    "0-0": "300",
    "h-0": "code",
    "h-2": "说明",
    "h-1": "message",
    "1-0": "301",
    "2-0": "1",
    "3-0": "0",
    "4-0": "101",
    "0-2": "链同步错误，请检查您的系统时钟",
    "0-1": "Chain sync error, please check your system clock",
    "1-2": "连接RPC失败，请检查你的网络",
    "1-1": "RPC connection failed. Please check your network",
    "2-2": "操作成功",
    "2-1": "无",
    "3-2": "操作失败，返回错误状态描述不固定，可直接提示res.message或统一提示为操作失败",
    "3-1": "failed",
    "4-2": "参数缺失",
    "4-1": "Parameter is missing",
    "5-0": "1011",
    "6-0": "102",
    "7-0": "103",
    "8-0": "104",
    "9-0": "105",
    "5-2": "参数错误",
    "5-1": "Parameter error",
    "6-2": "网络繁忙，请检查你的网络连接",
    "6-1": "The network is busy, please check your network connection",
    "7-2": "请输入正确的账户名(正则/^a-z{4,63}/$)",
    "7-1": "Please enter the correct account name(/^a-z{4,63}/$)",
    "8-2": "XX 不存在",
    "8-1": "XX not found",
    "9-2": "密码错误",
    "9-1": "wrong password",
    "10-0": "106",
    "11-0": "107",
    "12-0": "108",
    "13-0": "109",
    "14-0": "110",
    "10-2": "账户已经处于解锁状态",
    "10-1": "The account is already unlocked",
    "12-2": "用户名或密码错误(请确认你的账户是通过账户模式注册的，钱包模式注册的账户不能使用账户模式登录)",
    "12-1": "User name or password error (please confirm that your account is registered in account mode, and the account registered in wallet mode cannot be logged in using account mode)",
    "11-2": "请先导入私钥",
    "11-1": "Please import the private key",
    "13-2": "请输入正确的私钥",
    "13-1": "Please enter the correct private key",
    "14-2": "该私钥没有对应的账户信息",
    "14-1": "The private key has no account information",
    "15-0": "111",
    "16-0": "112",
    "17-0": "113",
    "18-0": "114",
    "19-0": "115",
    "20-0": "116",
    "15-2": "请先登录",
    "15-1": "Please login first",
    "16-2": "必须拥有owner权限才可以进行密码修改,请确认你导入的是ownerPrivateKey",
    "16-1": "Must have owner permission to change the password, please confirm that you imported the ownerPrivateKey",
    "17-2": "请输入正确的原始密码/临时密码",
    "17-1": "Please enter the correct original/temporary password",
    "18-2": "帐户被锁定或未登录",
    "18-1": "Account is locked or not logged in.",
    "19-2": "区块链上不存在资产 XX",
    "19-1": "There is no asset XX on block chain",
    "20-2": "收款方账户不存在",
    "20-1": "Account receivable does not exist",
    "21-0": "117",
    "22-0": "118",
    "23-0": "119",
    "24-0": "120",
    "25-0": "121",
    "26-0": "122",
    "27-0": "123",
    "21-2": "当前资产精度配置为 X ，小数点不能超过 X",
    "21-1": "The current asset precision is configured as X ,and the decimal cannot exceed X",
    "22-2": "备注加密失败",
    "22-1": "Encrypt memo failed",
    "23-2": "交易过期",
    "23-1": "Expiry of the transaction",
    "24-2": "获取帐户记录错误",
    "24-1": "Error fetching account record",
    "25-2": "查询不到相关区块及交易信息",
    "25-1": "block and transaction information cannot be found",
    "26-2": "参数blockOrTXID不正确",
    "26-1": "Parameter blockOrTXID is incorrect",
    "27-2": "参数account不能为空",
    "27-1": "Parameter account can not be empty",
    "28-0": "124",
    "29-0": "125",
    "30-0": "127",
    "31-0": "129",
    "32-0": "130",
    "33-0": "131",
    "34-0": "133",
    "28-2": "收款方账户名不能为空",
    "28-1": "Receivables account name can not be empty",
    "29-2": "用户未拥有 XX 资产",
    "29-1": "Users do not own XX assets",
    "30-2": "没有可领取的奖励",
    "30-1": "No reward available",
    "31-2": "memo不能为空",
    "31-1": "Parameter ‘memo’ can not be empty",
    "32-2": "请输入正确的合约名称(正则/^a-z{4,63}$/)",
    "32-1": "Please enter the correct contract name(/^a-z{4,63}$/)",
    "33-2": "世界观名称不能为空",
    "33-1": "Parameter ‘worldView’ can not be empty",
    "34-2": "toAccount不能为空",
    "34-1": "Parameter ‘toAccount’ can not be empty",
    "35-0": "135",
    "36-0": "136",
    "37-0": "137",
    "38-0": "138",
    "39-0": "139",
    "40-0": "140",
    "35-2": "请检查参数数据类型",
    "35-1": "Please check parameter data type",
    "36-2": "orderId不能为空",
    "36-1": "Parameter ‘orderId’ can not be empty",
    "37-2": "NHAssetHashOrIds不能为空",
    "37-1": "Parameter ‘NHAssetHashOrIds’ can not be empty",
    "38-2": "接入点地址不能为空",
    "38-1": "Parameter ‘url’ can not be empty",
    "39-2": "节点地址必须以 ws:// 或 wss:// 开头",
    "39-1": "Node address must start with ws:// or wss://",
    "40-2": "API服务器节点地址已经存在",
    "40-1": "API server node address already exists",
    "41-0": "141",
    "42-0": "142",
    "43-0": "144",
    "44-0": "145",
    "47-0": "148",
    "41-2": "请检查参数NHAssets中的数据",
    "41-1": "Please check the data in parameter NHAssets",
    "42-2": "请检查参数NHAssets的数据类型",
    "42-1": "Please check the data type of parameter NHAssets",
    "43-2": "您当前批量 创建/删除/转移 NH资产数量为 X ，批量操作数量不能超过 X",
    "43-1": "Your current batch creation / deletion / transfer number is X , and batch operations can not exceed X",
    "45-0": "146",
    "46-0": "147",
    "44-2": "XX 合约不存在",
    "44-1": "XX contract not found",
    "45-2": "账户没有该合约相关的信息",
    "45-1": "The account does not contain information about the contract",
    "46-2": "非同质资产不存在",
    "46-1": "NHAsset do not exist",
    "47-2": "请求超时，请尝试解锁账户或登录账户",
    "47-1": "Request timeout, please try to unlock the account or login the account",
    "48-0": "149",
    "49-0": "150",
    "50-0": "151",
    "51-0": "152",
    "52-0": "153",
    "53-0": "154",
    "48-2": "此私钥已导入过钱包",
    "48-1": "This wallet has already been imported",
    "49-2": "导入私钥失败",
    "49-1": "Key import error",
    "50-2": "您的浏览器不支持文件保存",
    "50-1": "File saving is not supported",
    "51-2": "无效的备份下载转换",
    "51-1": "Invalid backup to download conversion",
    "52-2": "请先解锁钱包",
    "52-1": "Please unlock your wallet first",
    "53-2": "请先恢复你的钱包",
    "53-1": "Please restore your wallet first",
    "54-0": "155",
    "55-0": "156",
    "56-0": "157",
    "57-0": "158",
    "58-0": "159",
    "59-0": "160",
    "54-2": "浏览器不支持钱包文件恢复",
    "54-1": "Your browser may not support wallet file recovery",
    "55-2": "该钱包已经导入，请勿重复导入",
    "55-1": "The wallet has been imported. Do not repeat import",
    "56-2": "请求超时，请尝试解锁账户或登录账户",
    "56-1": "Can’t delete wallet, does not exist in index",
    "57-2": "导入的钱包核心资产不能为 XX ，应为 XX",
    "57-1": "Imported Wallet core assets can not be XX , and it should be XX",
    "58-2": "账户已存在",
    "58-1": "Account exists",
    "59-2": "你不是该资产的创建者",
    "59-1": "You are not the creator of the Asset XX .",
    "60-0": "161",
    "61-0": "162",
    "62-0": "163",
    "63-0": "164",
    "64-0": "165",
    "65-0": "166",
    "66-0": "167",
    "67-0": "168",
    "68-0": "169",
    "68-2": "API方法不存在",
    "68-1": "MethodMethod does not exist\t does not exist",
    "67-2": "当前没有订阅此项",
    "67-1": "This subscription does not exist",
    "66-2": "当前合约版本id没有找到 X",
    "66-1": "The current contract version ID was not found",
    "65-2": "该钱包链id与当前链配置信息不匹配，该钱包的链id为： XXX",
    "65-1": "The Wallet Chain ID does not match the current chain configuration information. The chain ID of the wallet is: XX",
    "64-2": "链上没有该钱包账户信息",
    "64-1": "There is no wallet account information on the chain",
    "63-2": "世界观不存在",
    "63-1": "worldViews do not exist",
    "62-2": "钱包已经存在，请尝试导入私钥",
    "62-1": "The wallet already exists. Please try importing the private key",
    "61-2": "资产已存在",
    "61-1": "The asset already exists",
    "60-2": "订单不存在",
    "60-1": "Orders do not exist"
  },
  "cols": 3,
  "rows": 69
}
[/block]
## API 使用示例
1.钱包模式-创建账户
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
      "code": "返回数据1 ：{\"code\":1,\"data\":{\"account\":{\"active_key\":\"COCOS6BGnotPV3232ZJBvp5FgZuZ5cGPqNgqaSHnbSoaJLjaKmV8LLE\",\"name\":\"testtest3\",\"owner_key\":\"COCOS8F9BeMjVqBVakgJhTm2pQoMido4ZBksfHL6oQb1ZWXtpmpBJF5\"}}}\n",
      "language": "java"
    }
  ]
}
[/block]

[block:code]
{
  "codes": [
    {
      "code": "返回数据 2：{\"code\":159,\"message\":account exist}",
      "language": "java"
    }
  ]
}
[/block]

[block:code]
{
  "codes": [
    {
      "code": "返回数据 3：{\"code\":102,\"message\":It doesn't connect to the server.}",
      "language": "java"
    }
  ]
}
[/block]
2.转账
[block:code]
{
  "codes": [
    {
      "code": " /**\n     * transfer\n     * @param password 密码 (临时密码/账户密码)\n     * @param strFrom 转出账户\n     * @param strTo 转入账户\n     * @param strAmount 转账金额\n     * @param strAssetSymbol 转账币种\n     * @param strMemo 备注信息\n     */\n CocosBcxApiWrapper.getBcxInstance().transfer(\"111111\", \"testtest3\", \"gnkhandsome1\", \"10\", \"COCOS\", \"testting\", new IBcxCallBack() {\n                @Override\n                public void onReceiveValue(String value) {\n                    Log.i(\"transfer\", value);\n                }\n            });",
      "language": "java"
    }
  ]
}
[/block]

[block:code]
{
  "codes": [
    {
      "code": "###返回数据1 ：{\"code\":1,\"message\":bf3c058914399136d384de714a3c57d2966e1513}\n注： hash : bf3c058914399136d384de714a3c57d2966e1513",
      "language": "java"
    }
  ]
}
[/block]

[block:code]
{
  "codes": [
    {
      "code": "返回数据2: {\"code\":105,\"message\":wrong password}",
      "language": "java"
    }
  ]
}
[/block]
3.导出私钥 (私通过钥导入登录的账户只能导出登陆时导入的私钥)

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
返回数据 (公钥（Key）,私钥(Value))：
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
4.获取账户余额（参数1:用户ID, 参数2：获取余额的资产ID，为空则获取账户的所有资产余额信息）
[block:code]
{
  "codes": [
    {
      "code": "List<Object> assetSymbolOrId = new ArrayList<>();\n      // todo 默认币种类型\nassetSymbolOrId.add(\"1.3.0\");\nCocosBcxApiWrapper.getBcxInstance().get_account_balances(\"1.2.76\", unit, new IBcxCallBack() {\n          @Override\n          public void onReceiveValue(final String value) {\n                  Log.i(\"get_account_balances\", value);\n          }\n      });",
      "language": "java"
    }
  ]
}
[/block]
返回数据:
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
## 合作项目
CocosWallet

## 开源地址
[AndroidSdk](https://github.com/Cocos-BCX/AndroidSdk)