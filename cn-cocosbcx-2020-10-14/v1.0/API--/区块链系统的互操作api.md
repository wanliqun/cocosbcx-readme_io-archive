---
title: "区块链系统的互操作API"
slug: "区块链系统的互操作api"
hidden: true
createdAt: "2018-12-14T14:34:44.266Z"
updatedAt: "2018-12-14T15:45:00.996Z"
---
[block:api-header]
{
  "title": "钱包模式"
}
[/block]
创建账户
方法：createAccountWithWallet
功能：钱包模式创建账户，钱包模式创建的账户不能用账户名密码登录。如果钱包模式已经存在账户，该操作会创建子账户，创建该子账户需要先成为终身会员账户
参数：
account：用户名
password：密码
callback ：回调函数

备份钱包
方法：backupDownload
功能：备份钱包，调用该API会生成一个钱包文件，自动下载
参数：
callback ：回调函数

加载备份钱包文件
方法：loadWalletFile
功能：对于web来说，file input绑定change事件，读取钱包文件  
参数：
  file：宿主环境若在web => file input 的 change事件触发返回的事件对象event.target,files[0]
callback ：回调函数

从备份文件恢复钱包
方法：restoreWallet
功能：备份钱包，调用该API会生成一个钱包文件，自动下载。该API调用后，钱包处于锁定状态。
参数：
password: 备份文件的钱包密码
callback ：回调函数

导入私钥
方法：importPrivateKey
功能：导入私钥到钱包
参数：
 privateKey：明文私钥
password: 如果是已经创建钱包或恢复钱包，此时的密码为原来钱包的密码，否则是可以随意填写的临时密码
callback ：回调函数

删除钱包
方法：deleteWallet
功能：删除钱包，使用账户模式时，最好让用户先执行删除钱包
参数：
callback ：回调函数 

获取钱包账户列表
方法：getAccounts
功能：获取钱包账户列表
参数：
直接返回数据格式示例: 
"accounts": ["tom0002"],
"currentAccount": {
"userId": "1.2.20",
"isLocked": true,
"name": "tom0002"
}

切换账户
方法：setCurrentAccount
功能：钱包模式切换当前使用账户
参数：
account:要切换的账户 
callback: 

解锁账户
方法：unlockAccount
功能：导入私钥或钱包模式才可以使用此方法解锁账户
参数：
password:导入私钥时设置的临时密码
callback: 

锁定账户
方法：lockAccount
功能：锁定账户
参数：callback
[block:api-header]
{
  "title": "账户模式"
}
[/block]
创建账户
方法：createAccountWithPassword
功能：账户注册。如果账户模式已经有账户登录，该操作会创建子账户，创建该子账户需要操作账户为终身会员账户
参数：
account：用户名
password：密码
autoLogin:  boolean类型，指定是否自动登录，默认值为false
callback ：回调函数

账户登录
方法：passwordLogin
功能：账户登录
参数：
account：用户名
password：密码
callback ：回调函数

私钥登录
方法：privateKeyLogin
功能：之前这个API只是过渡，严格上导入私钥只存在于钱包模式。现在为了兼容，此API还暂时留在这里,依然可用调用 
参数：
privateKey：私钥 
password：设置的临时密码
callback 

退出登录
方法：logout
功能：该方法会清除用户相关缓存,其中包括清除加密后的密文key
参数：
callback 

修改密码
方法：changePassword
功能：只有账户模式，才能修改密码；修改密码成功后,API将会自动调用退出登录。
参数：
oldPassword：旧密码
newPassword：新密码
callback：

获取当前账户信息
方法：getUserInfo
功能：当账户处于解锁状态，返回数据中将包含账户名name
参数：
无callback，直接返回
[block:api-header]
{
  "title": "账户操作"
}
[/block]
升级成为终身会员账户
方法：upgradeAccount
功能：购买终身会员账户后，可以创建子账户，此操作需消耗一定的手续费
参数：
onlyGetFee：是否只获取此操作手续费
callback

导出用户私钥
方法：getPrivateKey
功能：获取用户Active PrivateKey,本秘钥可用于为账户所有花费行为签名
参数：
callback: 设置获取私钥成功后的回调函数，回调参数:result,为Object对象,
对象结构为：
{status:1,data:{activePrivateKey:”***********”}},其中：activePrivateKey为私钥串

查询账户记录
方法：queryUserOperations
功能：查询用户近期操作记录
参数：
account:账户名
limit:查询记录条数
callback:查看API统一参数说明

订阅用户操作记录变更
方法：subscribeToUserOperations
功能：订阅用户操作记录变更
参数：
account:账户名
callback:只要用户操作记录有变化，就调用此callback
[block:code]
{
  "codes": [
    {
      "code": "",
      "language": "text"
    }
  ]
}
[/block]
查询账户信息
方法：queryUserInfo
功能：账户信息中包含用户id用户名等信息
参数：
account:账户名
callback:查看API统一参数说明
[block:api-header]
{
  "title": "数据结构"
}
[/block]
本产品支持自定义数据结构的链上存储。
对于游戏定制版而言，数据在链上的存储结构分为数据头、数据内容两部分。
数据头由游戏数字资产(assetId)、道具版本(itemVER)、道具唯一标识(itemId)组成，数据内容用于描述道具详细信息由制造者定义，通常为游戏角色、游戏装备等等游戏信息。
需要注意的是，任何数据的写操作，都将在区块中留下记录。
[block:api-header]
{
  "title": "代币操作接口"
}
[/block]
代币资产转移
方法：transferAsset
功能：向目标对象发送代币
参数：
 fromAccount:发款方账户名,不是发起提议，
toAccount: 收款方账号名
amount：发送的代币数量
assetId ：资产ID （如：1.3.0）或 代币符号（如：BTC）
memo: 转账备注
feeAssetId:支付手续费的代币资产符号
isPropose:是否发起提议
onlyGetFee（boolean）：是否只获取本次操作所需手续费
callback: 设置转账后的回调函数

创建资产
方法：createAsset
功能：创建token
参数：
assetId: 资产符号,正则^[.A-Z]+$
precision: 精度(小数位数)
maxSupply: 最大资产总量
[block:code]
{
  "codes": [
    {
      "code": "coreExchangeRate(Object): {\n      quoteAmount:标价资产(即创建的代币，默认1),\n      baseAmount: 基准资产(即核心资产,默认1)\n}\ndescription: 资产描述，可不填\nonlyGetFee: 设置只返回本次调用所需手续费\ncallback: 见统一API说明\n",
      "language": "javascript"
    }
  ]
}
[/block]
更新资产
方法：updateAsset
功能：更新token
参数：
[block:code]
{
  "codes": [
    {
      "code": "assetId: 资产符号,正则^[.A-Z]+$\nmaxSupply: 最大资产总量\nnewIssuer：更新发行人\n\ncoreExchangeRate(Object):{ 手续费汇率\nquoteAmount:标价资产\nbaseAmount:基准资产\n}\ndescription: 资产描述，可不填\nonlyGetFee: 设置只返回本次调用所需手续费\ncallback: 见统一API说明\n",
      "language": "text"
    }
  ]
}
[/block]
资产销毁
方法：reserveAsset
功能：销毁代币资产
参数：
assetId：资产符号 
amount：销毁数量
onlyGetFee：设置只返回本次调用所需手续费
callback

资产发行
方法：issueAsset
功能：代币资产token发行
参数：
toAccount：发行对象
amount：发行数量
assetId：资产符号 
memo：备注消息，选填
onlyGetFee：设置只返回本次调用所需手续费
callback

注资资产手续费池
方法：assetFundFeePool
功能：所有网络手续费最终将使用核心资产代币进行支付。手续费资金池用来承担从 二级资产代币 转换为 核心资产代币 的费用，以便用户可以使用 二级资产代币 来支付手续费。如果资金池中余额用完，用户将无法继续使用 二级资产代币 支付手续费。目前支持使用二级资产代币作为手续费的API有“转账、投票、升级终身会员、资产发行”，后续会继续扩展
参数：
assetId：需要注资的二级资产代币符号 
amount：注资核心资产代币数量
onlyGetFee：设置只返回本次调用所需手续费
callback
[block:api-header]
{}
[/block]

[block:api-header]
{}
[/block]
领取资产手续费
方法：assetClaimFees
功能：资产发行人可以在这里领取累积的资产手续费。
参数：
assetId：需要领取的二级资产代币符号 
amount：二级资产代币数量
onlyGetFee：设置只返回本次调用所需手续费
callback

查询链上发行的资产
方法：queryAsset
功能：代币资产查询
参数：
assetId：资产符号,此参数若为空，则查询链上发行的所有资产	
callback

查询账户指定资产余额
方法：queryAccountBalances
功能：获取用户对应的数字资产，如果assetId为空，则返回用户所有代币。
参数：
assetId：资产ID或代币符号，资产ID：数字代币的唯一代币标识ID（如：”1.3.0”），代币符号（如：”BTC”）
account: 用户名
callback：

查询账户所有资产余额列表
方法：queryAccountAllBalances
功能：查询用户拥有的所有资产列表，列表中包含资产对记账单位的换算值。当账户无任何资产余额将会返回余额为0的核心资产
参数：
unit：记账单位，将会根据手续费汇率或交易市场价格换算等价的该资产，资产ID或代币符号，资产ID：数字代币的唯一代币标识ID（如：”1.3.0”），代币符号（如：”BTC”）
account:用户名
callback：

[block:api-header]
{
  "title": "NH资产操作"
}
[/block]
注册开发者
方法：registerCreator
功能：将当前账户注册成为开发者

创建世界观
方法：creatWorldView
功能：创建支持的NH资产世界观，向区块链系统注册当前账号（通常为游戏的账号）支持的NH资产世界观
参数：
worldView：世界观名称,区分大小写;

创造NH资产
方法：creatNHAsset
功能：创建一个唯一的NH资产，具有唯一性。本接口仅限NH资产制造商（铁匠铺）使用。
参数：
assetId:当前NH资产交易时，适用的资产ID；
worldView：世界观；
baseDescribe：当前NH资产的具体内容描述，由制造者定义;
ownerAccount:指定NH资产拥有者(NH资产归属权账户，默认为NH资产创建者)
NHAssetsCount (Number):创建NH资产的数量，默认值为1，只有type为0即创建同一种NH资产生效
type:创建NH资产方式的类型：默认值为0，0是创建同一种NH资产，1是创建不同NH资产

[block:code]
{
  "codes": [
    {
      "code": "NHAssets(Array):示例: [{\"assetId\":\"1.3.0\",\"worldView\":\"TEST\",\"baseDescribe\":\"{name:\\\"预言家\\\"}\",\"ownerAccount\":\"test2\"},{\"assetId\":\"1.3.0\",\"worldView\":\"TEST\",\"baseDescribe\":\"{name:\\\"女巫\\\"}\",\"ownerAccount\":\"test2\"},{\"assetId\":\"1.3.0\",\"worldView\":\"TEST\",\"baseDescribe\":\"{name:\\\"猎人\\\"}\",\"ownerAccount\":\"test2\"}]",
      "language": "javascript"
    }
  ]
}
[/block]
删除NH资产
方法：deleteNHAsset
功能：删除整条NH资产数据记录,通常在商品销毁时使用（仅能由用户自己授权处理自己想要销毁的数据）。
参数:
NHAssetIds (Array): NH资产实例的唯一标识ID;示例：[3.2.195,3.2.194]

转移NH资产
方法：transferNHAsset
功能：用户可以将自己的NH资产转移到另外一个用户
参数:
toAccount:转移NH资产的目标用户名
NHAssetIds（Array）:多个NH资产id组成的数组，示例:[3.2.332,3.2.333]。

提议关联世界观
方法：proposeRelateWorldView
功能：提议关联到某一个世界观，需要该世界观的创建人审批
参数:
worldView:需要关联的世界观名
viewOwner:需要关联的世界观创建者

批准关联世界观的提议
方法：approvalProposal
功能：批准其他用户关联自己的世界观的提议
参数:
proposalId:提议Id

获取当前用户收到的提议
方法：getAccountProposals
功能：获取当前操作用户收到的提议
[block:api-header]
{
  "title": "NH资产买卖接口"
}
[/block]
创建NH资产出售单
方法：creatNHAssetOrder
功能：卖出NH资产（在交易前可调用queryAccountGameItems函数，列举用户NH资产，以便用户选着卖出）
参数：
otcAccount：OTC交易平台账户，用于收取挂单费用；（OTC平台填写）
orderFee：挂单费用，用户向OTC平台账户支付的挂单费用；（OTC平台填写）
NHAssetId：NH资产实例的唯一标识ID; （用户填写）
price：商品挂单价格；（用户填写）
priceAssetId：商品挂单价格所使用的代币种类；（用户填写）
expiration:挂单时间，如60*60=3600(秒)，为1小时
memo: 挂单备注信息；
callback: 设置执行挂单卖出后的回调函数

购买订单NH资产
方法：fillNHAssetOrder
功能：买入NH资产，支付购买游戏装备的代币费用，同时修改用户拥有的商品数据。该操作是一个多步合成的原子操作，在支付费用的同时完成用户账户NH资产数据的更新，如果支付动作或账户商品数据更新动作中某一个动作不被主链区块认可，则整个交易将被回滚，避免异常交易。
参数：
orderId:订单ID
callback

取消NH资产出售单
方法：cancelNHAssetOrder
功能：取消NH资产挂卖订单
参数：
orderId：订单ID
callback
[block:api-header]
{
  "title": "NH资产查询类接口"
}
[/block]
查询全网用户NH资产售卖订单
方法：queryNHAssetOrders
功能：查询全网用户NH资产的售卖订单	
参数：
assetSymbolsOrIds(array）:资产符号或id筛选条件
worldViews (array):版本名称或版本id筛选条件
pageSize：页容量
page:页数
查询指定用户的NH资产售卖订单
方法：queryAccountNHAssetOrders
功能：查询指定用户的NH资产售卖订单
参数：
account:查询账户名或账户Id
pageSize：页容量
page:页数
callback：

查询账户下所拥有的道具NH资产
方法：queryAccountNHAssets
功能：读取当前用户账户下所有可在对应游戏中使用的NH资产
参数：
account:账户名或账户id
worldViews (array):世界观名集合
page:页数
pageSize:页容量，每页的数据条数
callback：返回值示例{status:1,data:[],total:0}

查询开发者所关联的世界观
方法：queryNHCreator
功能：查询开发者所关联的世界观	
参数：
account:账户名或账户ID
callback

查询开发者创建的NH资产
方法：queryNHCreator
功能：查询开发者所创建的世界观	
参数：
account:账户名或账户ID
callback
查询NH资产详细信息
方法：queryNHAssets
功能：查询NH资产详细信息	
参数：
NHAssetHashOrIds:NH资产id或hash
callback
查询世界观详细信息
方法：lookupWorldViews
功能：查询世界观详细信息	
参数：
worldViewNameOrIds (array):世界观名称或id
callback
[block:api-header]
{
  "title": "节点投票"
}
[/block]
查询节点投票信息数据
方法：queryVotes
功能：查询节点投票信息数据	
参数：
callback

用户提交投票信息
方法：publishVotes
功能：保存的时候设置了代理账户，用户投票信息将统一跟随代理账户	
参数：
witnessesIds（array）:节点账户id集合,查询节点投票信息数据中会有每个节点的账户ID
proxyAccount:代理账户名
callback
[block:api-header]
{
  "title": "区块链浏览器类接口"
}
[/block]
查询区块
方法：queryBlock
功能：通过区块高度查询区块信息
参数：
block: 区块高度

查询交易
方法：queryTransaction
功能：通过交易id（即交易hash）查询交易信息
参数：
transactionId: 交易id

订阅区块
方法：subscribeToBlocks
功能：监听实时出块信息
参数：
callback

订阅区块链交易
方法：subscribeToChainTranscation
功能：监听区块链全网发生的交易 
参数：
callback

查看节点出块信息
方法：lookupWitnessesForExplorer
功能：这里重点是参照demo解析节点出块信息数据
参数：
callback

查看账户节点出块奖励
方法：lookupBlockRewards
功能： 参照demo解析数据
参数：
Callback

领取节点出块奖励
方法：claimVestingBalance
功能： 领取节点出块奖励
参数：
id：奖励id,查询节点出块奖励中会有这个id
callback
[block:api-header]
{
  "title": "API服务器节点相关接口"
}
[/block]
查看API服务器节点列表
方法：lookupWSNodeList
功能：查看API服务器节点列表信息
参数： 
callback

连接API服务器节点
方法：switchAPINode
功能：切换节点
参数： 
url：API服务器节点地址，此地址必须是API服务器节点列表中的websoket地址
callback

添加新的API服务器节点
方法：addAPINode
功能：添加新节点
参数： 
name:新节点名称
url：API服务器节点websoket地址
callback

删除API服务器节点
方法：deleteAPINode
功能：删除节点
参数： 
url：API服务器节点websoket地址
callback

监听与API服务器节点的连接状态变化
方法：subscribeToRpcConnectionStatus
功能：监听rpc连接状态变化
参数： 
callback：回调会返回状态status: closed：rpc连接关闭,error：rpc连接错误，realopen：rpc连接成功。

[block:api-header]
{
  "title": "合约"
}
[/block]
一键生成私钥/公钥（随机生成）
方法：generateKeys
功能：随机生成一对公私钥，创建带有权限的合约会用到,生成的私钥用于API初始化对合约授权，没有回调，直接返回

合约创建
方法：createContract
功能：创建智能合约，如果要对合约设置权限，创建合约时得加入特定的lua代码，并调用合约函数set_permissions_flag => 合约权限代码： function my_change_contract_authority( publickey) assert(is_owner()) change_contract_authority( publickey) end function set_permissions_flag(flag) assert(is_owner()) set_permissions_flag(flag) end	
参数：
authority：合约权限(一对公私钥中的公钥publicKey)，开发者在使用API初始化的时候，可以配置私钥，配置了该公钥对应的私钥才可以调用合约。
name: 合约名称,规则/^[a-z][a-z0-9\.-]{4,}/
data: 合约lua代码
onlyGetFee: 设置只返回本次操作所需手续费	
callback: 见统一API说明

合约更新
方法：updateContract
功能：更新合约代码
参数：
nameOrId合约名称或Id，示例：contract.test02
data: 合约lua代码
onlyGetFee: 设置只返回本次操作所需手续费	

合约调用
方法：callContractFunction
功能：调用合约函数接口	
参数：
nameOrId：合约名称或Id，示例：contract.test02
functionName:合约里的函数名称，my_nht_describe_change （修改道具属性）
valueList(array)：	调用合约函数的参数列表,示例：[‘4.2.2’,’name’,’女巫’] 
runtime: 运行合约函数的时间(单位毫秒),默认为5
onlyGetFee: 设置只返回本次操作所需手续费	默认为false
callback

查询合约信息
方法：queryContract
功能：查询合约信息数据
参数：
nameOrId：合约名字或Id
callback

查询账户合约数据
方法：queryAccountContractData
功能：查询账户合约里产生数据
参数：
userNameOrId：账户名或Id
contractNameOrId: 合约名字或Id
callback
[block:api-header]
{
  "title": "其他"
}
[/block]
获取交易类型基础手续费
方法：getTransactionBaseFee
功能：	获取交易类型基础手续费 
参数：
transactionType：交易类型,示例transfer
feeAssetId:选择支付手续费的代币类型资产符号或ID
callback：见统一API说明

transactionType列表

[block:parameters]
{
  "data": {
    "0-0": "transfer\nlimit_order_create\nlimit_order_cancel\n\naccount_create\n\n\naccount_update\naccount_upgrade\nasset_create\nasset_issue\nproposal_update\nvesting_balance_withdraw\ncontract_create\ncall_contract_function\nregister_creator\ncreat_world_view\npropose_relate_game_version\ncreat_nh_asset    \nupdata_nh_asset\ndelete_nh_asset\ntransfer_nh_asset\ncreat_nh_asset_order\ncancel_nh_asset_order\nfill_nh_asset_order",
    "h-1": "对应相关API",
    "h-0": "transactionType",
    "0-1": "transferAsset\ncreateLimitOrder\ncancelLimitOrder\n\ncreateAccountWithPassword，createAccountWithWallet\n\nchangePassword\nupgradeAccount\ncreateAsset\nissueAsset\nsubmitProposal\nclaimVestingBalance\ncreateContract\ncallContractFunction\ncreateGameVersion\ncreateGameItem\nproposeRelateGameVersion\ncreateGameItem\nupdateGameItem\ndeleteGameItem\ntransferGameItem\ncreatGameItemOrder\ncancelGameItemOrder\nfillGameItemOrder"
  },
  "cols": 2,
  "rows": 1
}
[/block]