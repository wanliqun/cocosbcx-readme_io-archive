---
title: "8.1 JS-SDK"
slug: "81-js-sdk"
excerpt: "Javascript API，用于使用COCOS-BCX RPC API与基于COCOS-BCX的区块链集成。"
hidden: false
createdAt: "2019-05-17T03:29:01.682Z"
updatedAt: "2020-05-08T03:10:38.525Z"
---
## 类库引用说明
**引入API文件**
[block:code]
{
  "codes": [
    {
      "code": "<script type=\"text/javascript\" src=\"bcx.min.js\"></script>",
      "language": "javascript"
    }
  ]
}
[/block]

**实例化类库对象**
[block:code]
{
  "codes": [
    {
      "code": "var bcx=new BCX({\n            default_ws_node:”ws://XXXXXXXXX” //节点rpc地址,选填。如果没有指定此项则会自动连接ws_node_list中速度最快的节点\n            ws_node_list:[{url:\"ws://xxxxxxx\",name:\"xxxxx\"}]//API服务器节点列表，必填\n            faucet_url:\"http://xxx.xxx.xxx.xxx:xxxx\", //注册入口\n            networks:[{\n                core_asset:\"xxx\",//核心资产符号\n                chain_id:\"xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx\"//链id   \n            }], \n            auto_reconnect:false,//当RPC断开时是否自动连接，默认为true\n            app_keys:[\"xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx\"]//合约授权，不进行合约授权，则不用配置此选项\n\t })",
      "language": "javascript"
    }
  ]
}
[/block]
**调用实例-转账** 
[block:code]
{
  "codes": [
    {
      "code": "bcx.transferAsset({\n            fromAccount: 'test1',\n            toAccount: 'test2',\n            amount: amount,\n            assetId: 'COCOS',\n            feeAssetId: 'COCOS',\n            memo: memo,\n            onlyGetFee: false,\n        }).then(function (res) {\n             console.log('transferAsset res',res);\n        })",
      "language": "javascript"
    }
  ]
}
[/block]
## API说明
1.没有特殊说明均有一个可选参数callback
   callback返回的result为Object对象,结构为{code:0,message:””}。 code=1时表示成功，无message状态描述。 code!=1时意味执行失败，message为失败状态描述。
2.没有殊说明均只有一个参数，该参数为一个对象，对象包含所有相关参数，其中也包含callback
调用示例：
[block:code]
{
  "codes": [
    {
      "code": "bcl.getPrivateKey({\n     callback:res=>{}\n})",
      "language": "javascript"
    }
  ]
}
[/block]
3.除订阅类接口，其他接口在不传callback参数时均返回promise对象
4.接口的参数类型没有特殊说明均为字符串
5.接口的参数没有特殊说明均不能为空，callback为可选参数
6.查询类接口返回数据实例:{code:1,data:[]}
7.非查询类接口返回数据会多一个数据字段trxData,值为一个对象
示例：
[block:code]
{
  "codes": [
    {
      "code": "trx_data:{\n block_num:*****,//区块高度\n trx_id:\"************************\"//交易ID\n}",
      "language": "javascript"
    }
  ]
}
[/block]
8.非查询类接口若涉及关联ID业务(如创建NH资产产生的ID)返回的数据中将包含data对象
示例：
[block:code]
{
  "codes": [
    {
      "code": "data:{\n  real_running_time: 387//运行时间\n  result: \"4.2.288\"//关联业务id\n}",
      "language": "javascript"
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
## 区块链系统的互操作API
## 钱包模式
**创建账户**
方法：createAccountWithWallet
功能：钱包模式创建账户，钱包模式创建的账户不能用账户名密码登录。如果钱包模式已经存在账户，该操作会创建子账户，创建该子账户需要先成为终身会员账户
参数：
account：账户名注册规则，/^[a-z][a-z0-9.-]{5,64}$/，小写字母开头+数字或小写字母或点.或短横线-，长度5至64
password：密码
callback：回调函数

**备份钱包**
方法：backupDownload
功能：备份钱包，调用该API会生成一个钱包文件，自动下载
参数：
callback：回调函数

**加载备份钱包文件**
方法：loadWalletFile
功能：对于web来说，file input绑定change事件，读取钱包文件
参数：
file：宿主环境若在web => file input 的 change事件触发返回的事件对象event.target，files[0]
callback：回调函数

**从备份文件恢复钱包**
方法：restoreWallet
功能：备份钱包，调用该API会生成一个钱包文件，自动下载。该API调用后，钱包处于锁定状态。
参数：
password：备份文件的钱包密码
callback：回调函数

**导入私钥**
方法：importPrivateKey
功能：导入私钥到钱包
参数：
privateKey：明文私钥
password：如果是已经创建钱包或恢复钱包，此时的密码为原来钱包的密码，否则是可以随意填写的临时密码
callback：回调函数

**删除钱包**
方法：deleteWallet
功能：删除钱包，使用账户模式时，最好让用户先执行删除钱包
参数：
callback：回调函数

**获取钱包账户列表**
方法：getAccounts
功能：获取钱包账户列表
参数：
直接返回数据，格式示例：
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
**切换账户**
方法：setCurrentAccount
功能：钱包模式切换当前使用账户
参数：
account：要切换的账户 
callback：回调函数

**解锁账户**
方法：unlockAccount
功能：导入私钥或钱包模式才可以使用此方法解锁账户
参数：
password：导入私钥时设置的临时密码
callback：回调函数

**锁定账户**
方法：lockAccount
功能：锁定账户
参数：
callback：回调函数

## 账户模式
**创建账户**
方法：createAccountWithPassword
功能：账户注册。如果账户模式已经有账户登录，该操作会创建子账户，创建该子账户需要操作账户为终身会员账户
参数：
account：账户名注册规则，/^[a-z][a-z0-9.-]{4,63}$/，小写字母开头+数字或小写字母或点.或短横线-，长度4至63
password：密码
autoLogin：boolean类型，指定是否自动登录，默认值为false
callback：回调函数

**账户登录**
方法：passwordLogin
功能：账户登录
参数：
account：账户名 password：密码
callback：回调函数

**私钥登录**
方法：privateKeyLogin
功能：之前这个API只是过渡，严格上导入私钥只存在于钱包模式。现在为了兼容，此API还暂时留在这里，依然可用调用 
参数：
privateKey：私钥 
password：设置的临时密码
callback：回调函数

**退出登录**
方法：logout
功能：该方法会清除用户相关缓存，其中包括清除加密后的密文key
参数：
callback：回调函数

**修改密码**
方法：changePassword
功能：只有账户模式，才能修改密码；修改密码成功后，API将会自动调用退出登录。
参数：
oldPassword：旧密码
newPassword：新密码
callback：回调函数

**获取当前账户信息**
方法：getAccountInfo
功能：当账户处于解锁状态，返回数据中将包含账户名name
参数：无

## 账户操作
**升级成为终身会员账户**
方法：upgradeAccount
功能：购买终身会员账户后，可以创建子账户，此操作需消耗一定的手续费
参数：
onlyGetFee：是否只获取此操作手续费
callback：回调函数

**导出用户私钥**
方法：getPrivateKey
功能：获取用户active_private_key，本秘钥可用于为账户所有花费行为签名，返回的owner_private_key：可修改账户相关的各种设置，包括权限设置
参数：
callback：设置获取私钥成功后的回调函数

**查询账户记录**
方法：queryAccountOperations
功能：查询用户近期操作记录
参数：
account：账户名
limit：查询记录条数
startId:开始账户记录id,如果查询范围是整个账户记录，则最开始的账户记录则是startId 
endId:结束账户记录id,如果查询范围是整个账户记录，则最新的账户记录则是endId
callback：查看API统一参数说明

**订阅用户操作记录变更**
方法：subscribeToAccountOperations
功能：订阅用户操作记录变更
参数：
account：账户名
callback：只要用户操作记录有变化，就调用此callback：回调函数

**查询账户信息**
方法：queryAccountInfo
功能：账户信息中包含用户id用户名等信息
参数：
account：账户名
callback：查看API统一参数说明

## 代币操作接口
**代币资产转移**
方法：transferAsset
功能：向目标对象发送代币
参数：
fromAccount：发款方账户名，不是发起提议，
toAccount：收款方账号名
amount：发送的代币数量
assetId：资产ID （如：X.X.X）或 代币符号（如：BTC）
memo：转账备注
feeAssetId：支付手续费的代币资产符号
isPropose：是否发起提议
onlyGetFee（boolean）：是否只获取本次操作所需手续费
callback：设置转账后的回调函数

**创建资产**
方法：createAsset
功能：创建token
参数：
assetId：资产符号，正则^[.A-Z]+$
precision：精度(小数位数)
maxSupply：最大资产总量
description: 资产描述，可不填
onlyGetFee：设置只返回本次调用所需手续费
callback：见统一API说明
coreExchangeRate(Object)：
[block:code]
{
  "codes": [
    {
      "code": "{  \n\t\t\tquoteAmount:标价资产(即创建的代币，默认1),  \n\t\t\tbaseAmount: 基准资产(即核心资产，默认1)  \n\t\t}",
      "language": "javascript"
    }
  ]
}
[/block]
**更新资产**
方法：updateAsset
功能：更新token
参数：
assetId：资产符号，正则^[.A-Z]+$
maxSupply：最大资产总量
newIssuer：更新发行人
description：资产描述，可不填
onlyGetFee：设置只返回本次调用所需手续费
callback：见统一API说明
coreExchangeRate(Object)：手续费汇率
[block:code]
{
  "codes": [
    {
      "code": "{   \n\t\tquoteAmount:标价资产  \n\t\tbaseAmount:基准资产  \n\t}",
      "language": "javascript"
    }
  ]
}
[/block]
**资产销毁**
方法：reserveAsset
功能：销毁代币资产
参数：
assetId：资产符号 
amount：销毁数量
onlyGetFee：设置只返回本次调用所需手续费
callback：回调函数

**资产发行**
方法：issueAsset
功能：代币资产token发行
参数：
toAccount：发行对象
amount：发行数量
assetId：资产符号 
memo：备注消息，选填
onlyGetFee：设置只返回本次调用所需手续费
callback：回调函数

**注资资产手续费池**
方法：assetFundFeePool
功能：所有网络手续费最终将使用核心资产代币进行支付。手续费资金池用来承担从 二级资产代币 转换为 核心资产代币 的费用，以便用户可以使用 二级资产代币 来支付手续费。如果资金池中余额用完，用户将无法继续使用 二级资产代币 支付手续费。目前支持使用二级资产代币作为手续费的API有“转账、投票、升级终身会员、资产发行”，后续会继续扩展
参数：
assetId：需要注资的二级资产代币符号 
amount：注资核心资产代币数量
onlyGetFee：设置只返回本次调用所需手续费
callback：回调函数

**领取资产手续费**
方法：assetClaimFees
功能：资产发行人可以在这里领取累积的资产手续费。
参数：
assetId：需要领取的二级资产代币符号 
amount：二级资产代币数量
onlyGetFee：设置只返回本次调用所需手续费
callback：回调函数

**查询链上发行的资产**
方法：queryAsset
功能：代币资产查询
参数：
assetId：资产符号，此参数若为空，则查询链上发行的所有资产 
callback：回调函数

**查询账户指定资产余额**
方法：queryAccountBalances
功能：获取用户对应的数字资产，如果assetId为空，则返回用户所有代币。
参数：
assetId：资产ID或代币符号，资产ID：数字代币的唯一代币标识ID（如："X.X.X"），代币符号（如：”BTC”）
account：用户名
callback：回调函数

**查询账户所有资产余额列表**
方法：queryAccountAllBalances
功能：查询用户拥有的所有资产列表，列表中包含资产对记账单位的换算值。当账户无任何资产余额将会返回余额为0的核心资产
参数：
unit：记账单位，将会根据手续费汇率或交易市场价格换算等价的该资产，资产ID或代币符号，资产ID：数字代币的唯一代币标识ID（如："X.X.X"），代币符号（如：”BTC”）
account：用户名
callback：回调函数

## NH资产操作
**注册开发者**
方法：registerCreator
功能：将当前账户注册成为开发者

**创建世界观**
方法：creatWorldView
功能：创建支持的NH资产世界观，向区块链系统注册当前账号（通常为游戏的账号）支持的NH资产世界观
参数：
worldView：世界观名称，区分大小写;

**创造NH资产**
方法：creatNHAsset
功能：创建一个唯一的NH资产，具有唯一性。本接口仅限NH资产制造商（铁匠铺）使用。
参数：
assetId：当前NH资产交易时，适用的资产ID；
worldView：世界观；
baseDescribe：当前NH资产的具体内容描述，由制造者定义;
ownerAccount：指定NH资产拥有者(NH资产归属权账户，默认为NH资产创建者)
NHAssetsCount (Number)：创建NH资产的数量，默认值为1，只有type为0即创建同一种NH资产生效
type：创建NH资产方式的类型，默认值为0。值为0时默认创建同一种NH资产，1是创建不同NH资产。
NHAssets(Array)示例:
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
**删除NH资产**
方法：deleteNHAsset
功能：删除整条NH资产数据记录，通常在商品销毁时使用（仅能由用户自己授权处理自己想要销毁的数据）。
参数：
NHAssetIds (Array)：NH资产实例的唯一标识ID;示例：[X.X.X, X.X.X]

**转移NH资产**
方法：transferNHAsset
功能：用户可以将自己的NH资产转移到另外一个用户
参数：
toAccount：转移NH资产的目标用户名
NHAssetIds（Array）：多个NH资产id组成的数组，示例：[X.X.X, X.X.X]

**提议关联世界观**
方法：proposeRelateWorldView
功能：提议关联到某一个世界观，需要该世界观的创建人审批
参数：
worldView：需要关联的世界观名

**批准关联世界观的提议**
方法：approvalProposal
功能：批准其他用户关联自己的世界观的提议
参数：
proposalId：提议ID

**获取当前用户收到的提议**
方法：getAccountProposals
功能：获取当前操作用户收到的提议

## NH资产买卖接口
**创建NH资产出售单**
方法：creatNHAssetOrder
功能：卖出NH资产（在交易前可调用queryAccountGameItems函数，列举用户NH资产，以便用户选着卖出）
参数：
otcAccount：OTC交易平台账户，用于收取挂单费用；（OTC平台填写）
orderFee：挂单费用，用户向OTC平台账户支付的挂单费用；（OTC平台填写）
NHAssetId：NH资产实例的唯一标识ID; （用户填写）
price：商品挂单价格；（用户填写）
priceAssetId：商品挂单价格所使用的代币种类；（用户填写）
expiration：挂单时间，如3600(秒)，为1小时
memo：挂单备注信息；
callback：设置执行挂单卖出后的回调函数

**购买订单NH资产**
方法：fillNHAssetOrder
功能：买入NH资产，支付购买游戏装备的代币费用，同时修改用户拥有的商品数据。该操作是一个多步合成的原子操作，在支付费用的同时完成用户账户NH资产数据的更新，如果支付动作或账户商品数据更新动作中某一个动作不被主链区块认可，则整个交易将被回滚，避免异常交易。
参数：
orderId：订单ID
callback：回调函数

**取消NH资产出售单**
方法：cancelNHAssetOrder
功能：取消NH资产挂卖订单
参数：
orderId：订单ID
callback：回调函数

*## NH资产查询*类接口
**查询全网用户NH资产售卖订单**
方法：queryNHAssetOrders
功能：查询全网用户NH资产的售卖订单 
参数：
assetIds(array）：资产符号或id筛选条件
worldViews (array)：版本名称或版本id筛选条件
pageSize：页容量
page：页数

**查询指定用户的NH资产售卖订单**
方法：queryAccountNHAssetOrders
功能：查询指定用户的NH资产售卖订单
参数：
account：查询账户名或账户Id
pageSize：页容量
page：页数
callback：回调函数

**查询账户下所拥有的道具NH资产**
方法：queryAccountNHAssets
功能：读取当前用户账户下所有可在对应游戏中使用的NH资产
参数：
account：账户名或账户id
worldViews (array)：世界观名集合
page：页数
pageSize：页容量，每页的数据条数
callback：返回值。示例：
{status:1,data:[],total:0}

**查询开发者所关联的世界观**
方法：queryNHCreator
功能：查询开发者所关联的世界观 
参数：
account：账户名或账户ID
callback：回调函数

**查询开发者创建的NH资产**
方法：queryNHCreator
功能：查询开发者所创建的世界观 
参数：
account：账户名或账户ID
callback：回调函数

**查询NH资产详细信息**
方法：queryNHAssets
功能：查询NH资产详细信息 
参数：
NHAssetIds：NH资产id或hash
callback：回调函数

**查询世界观详细信息**
方法：lookupWorldViews
功能：查询世界观详细信息 
参数：
worldViews (array)：世界观名称或id
callback：回调函数

## 节点投票
**查询节点投票信息数据**
方法：queryVotes
功能：查询节点投票信息数据 
参数：
callback：回调函数

**用户提交投票信息**
方法：publishVotes
功能：保存的时候设置了代理账户，用户投票信息将统一跟随代理账户 
参数：
witnessesIds（array）：节点账户id集合，查询节点投票信息数据中会有每个节点的账户ID
proxyAccount：代理账户名
callback：回调函数

## 区块链浏览器类接口
**查询区块**
方法：queryBlock
功能：通过区块高度查询区块信息
参数：
block：区块高度

**查询交易**
方法：queryTransaction
功能：通过交易id（即交易hash）查询交易信息
参数：
transactionId：交易id

**查询信息通过id**
方法：queryDataByIds 功能：通过id查询相关数据信息
参数：
ids(Array)：id数组集合

**订阅区块**
方法：subscribeToBlocks
功能：监听实时出块信息
参数：
isReqTrx:订阅的区块是否包含交易信息，默认包含 callback：回调函数

**订阅区块链交易**
方法：subscribeToChainTranscation
功能：监听区块链全网发生的交易 
参数：
callback：回调函数

**查看节点出块信息**
方法：lookupWitnessesForExplorer
功能：这里重点是参照demo解析节点出块信息数据
参数：
callback：回调函数

**查看账户节点出块奖励**
方法：lookupBlockRewards
功能：参照demo解析数据
参数：
callback：回调函数

**领取节点出块奖励**
方法：claimVestingBalance
功能：领取节点出块奖励
参数：
id：奖励id，查询节点出块奖励中会有这个id
callback：回调函数

## API服务器节点相关接口
**bcx初始化**
方法：init
功能：初始化内容包括RPC连接、重新载入Indexedb数据等 
参数：
refresh:选填，第一次init后，第二次init会使用缓存信息。只有当refresh为true才会重新载入数据，重新初始化RPC模块
autoReconnect:选填，RPC断开后是否进行重连 
subscribeToRpcConnectionStatusCallback:选填，监听RPC连接状态,返回 status=>closed：rpc连接关闭,error：rpc连接错误，realopen：rpc连接成功。此监听有单独的方法提供 
callback：选填，回调函数

**查看API服务器节点列表**
方法：lookupWSNodeList
功能：查看API服务器节点列表信息
参数： 
refresh:是否刷新ping，此刷新只能刷新非当前连接节点，若想全刷新则调用init({refresh:true}) 
callback：回调函数

**连接API服务器节点**
方法：switchAPINode
功能：切换节点
参数：
url：API服务器节点地址，此地址必须是API服务器节点列表中的websoket地址
callback：回调函数

**添加新的API服务器节点**
方法：addAPINode
功能：添加新节点
参数：
name：新节点名称
url：API服务器节点websoket地址
callback：回调函数

**删除API服务器节点**
方法：deleteAPINode
功能：删除节点
参数：
url：API服务器节点websoket地址
callback：回调函数

**监听与API服务器节点的连接状态变化**
方法：subscribeToRpcConnectionStatus
功能：监听rpc连接状态变化
参数：
callback：回调会返回状态status，包括下述结果: 
closed：rpc连接关闭
error：rpc连接错误
realopen：rpc连接成功

## 合约
**一键生成私钥/公钥（随机生成）**
方法：generateKeys
功能：随机生成一对公私钥，创建带有权限的合约会用到，生成的私钥用于API初始化对合约授权，没有回调，直接返回

**合约创建**
方法：createContract
功能：创建智能合约，如果要对合约设置权限，创建合约时得加入特定的lua代码，并调用合约函数set_permissions_flag => 合约权限代码:function my_change_contract_authority( publickey) assert(is_owner()) change_contract_authority( publickey) end function set_permissions_flag(flag) assert(is_owner()) set_permissions_flag(flag) end 
参数：
authority：合约权限(一对公私钥中的公钥publicKey)，开发者在使用API初始化的时候，可以配置私钥，配置了该公钥对应的私钥才可以调用合约。
name：合约名称，正则/^[a-z][a-z0-9.-]{4,63}$/，首字母开头+字母或数字或点.或短横线-，长度4至63 data：合约lua代码
onlyGetFee：设置只返回本次操作所需手续费 
callback：见统一API说明

**合约更新**
方法：updateContract
功能：更新合约代码
参数：
nameOrId合约名称或Id，示例：contract.test02
data：合约lua代码
onlyGetFee：设置只返回本次操作所需手续费
注意：当合约内有锁定资产时，此时更新合约会提示不能更新合约，必须先解锁资产。

**合约调用**
方法：callContractFunction
功能：调用合约函数接口 
参数：
nameOrId：合约名称或Id，示例：contract.test02
functionName：合约里的函数名称，my_nht_describe_change （修改道具属性）
valueList(array)： 调用合约函数的参数列表，示例：[4.2.0,{"size":"large"}] ，这里的参数若传json字符串，则合约需调用cjson解析，若传对象则无需cjson解析
runtime：运行合约函数的时间(单位毫秒)，默认为5
onlyGetFee：设置只返回本次操作所需手续费，默认为false
callback：回调函数

**查询合约信息**
方法：queryContract
功能：查询合约信息数据
参数：
nameOrId：合约名字或Id
callback：回调函数

**查询账户合约数据**
方法：queryAccountContractData
功能：查询账户合约里产生数据
参数：
account：账户名或Id
contractNameOrId：合约名字或Id
callback：回调函数

## 其他
**取消订阅**
方法：unsubscribe
功能：取消订阅 
参数：
method(Array)：取消指定订阅的方法名，如取消订阅区块和区块链交易['subscribeToBlocks','subscribeToBlocks']，不传该参数则取消所有订阅。该方法不传callback则返回promise。 注：若需指定取消某一用户的订阅,则参数为['subscribeToAccountOperation|account'] callback：回调函数

**交易备注解密**
方法：decodeMemo
功能：无回调，直接返回结果，结果是一个对象，对象中包含备注文本text。该方法传参是直接传入，非包裹式options对象传参。 示例：bcl.decodeMemo(raw_data.memo) ,其中raw_data为交易原始数据。

**获取交易类型基础手续费**
方法：queryTransactionBaseFee
功能： 获取交易类型基础手续费 
参数：
transactionType：交易类型，示例transfer
feeAssetId：选择支付手续费的代币类型资产符号或ID
callback：见统一API说明

## transactionType列表
[block:parameters]
{
  "data": {
    "h-0": "transactionType",
    "h-1": "对应相关API",
    "0-0": "transfer",
    "1-0": "account_create",
    "2-0": "account_update",
    "3-0": "account_upgrade",
    "4-0": "asset_create",
    "5-0": "asset_issue",
    "0-1": "transferAsset",
    "1-1": "createAccountWithPassword",
    "2-1": "changePassword",
    "3-1": "upgradeAccount",
    "4-1": "createAsset",
    "5-1": "issueAsset",
    "6-0": "proposal_update",
    "7-0": "vesting_balance_withdraw",
    "8-0": "contract_create",
    "9-0": "call_contract_function",
    "10-0": "call_contract_function",
    "11-0": "register_creator",
    "12-0": "creat_world_view",
    "6-1": "submitProposal",
    "7-1": "claimVestingBalance",
    "8-1": "createContract",
    "9-1": "callContractFunction",
    "10-1": "callContractFunction",
    "11-1": "registerCreator",
    "12-1": "creatWorldView",
    "13-0": "propose_relate_world_view",
    "14-0": "creat_nh_asset",
    "15-0": "delete_nh_asset",
    "16-0": "transfer_nh_asset",
    "17-0": "transfer_nh_asset",
    "18-0": "transfer_nh_asset",
    "19-0": "creat_nh_asset_order",
    "20-0": "cancel_nh_asset_order",
    "21-0": "fill_nh_asset_order",
    "22-0": "limit_order_create",
    "23-0": "limit_order_cancel",
    "13-1": "proposeRelateWorldView",
    "14-1": "creatNHAsset",
    "15-1": "delete_nh_asset",
    "16-1": "transferNHAsset",
    "17-1": "transferNHAsset",
    "18-1": "transferNHAsset",
    "19-1": "creatNHAssetOrder",
    "20-1": "cancelNHAssetOrder",
    "21-1": "fillNHAssetOrder",
    "22-1": "createLimitOrder",
    "23-1": "cancelLimitOrder"
  },
  "cols": 2,
  "rows": 24
}
[/block]
## 开源地址
[JSSDK](https://github.com/Cocos-BCX/JSSDK)