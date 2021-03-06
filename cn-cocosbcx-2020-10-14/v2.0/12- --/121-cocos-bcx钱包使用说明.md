---
title: "12.1 COCOS-BCX钱包使用说明"
slug: "121-cocos-bcx钱包使用说明"
hidden: false
createdAt: "2020-01-01T05:13:19.983Z"
updatedAt: "2020-01-02T10:47:13.168Z"
---
12月12日，Cocos-BCX 宣布主网1.0版本“冈仁波齐”正式上线。同期，官方手机钱包也支持主网。方便大家使用和资产安全，请大家仔细阅读下方官方钱包使用指引。

#一、账号体系

##**1.1 下载并安装手机钱包**
首先识别下方二维码，下载并安装 Cocos-BCX 手机钱包。
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/20be0a4-_20191216191934.png",
        "微信截图_20191216191934.png",
        196,
        200,
        "#9c9c9c"
      ]
    }
  ]
}
[/block]
##**1.2 注册账号步骤**
* 第一步：点击首页的【立即登录/创建账号】
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/57b2a0a-_20191216192839_1.png",
        "微信截图_20191216192839 (1).png",
        750,
        684,
        "#a3a9e0"
      ]
    }
  ]
}
[/block]
* 第二步：点击右上角【注册】
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/03b6a96-_20191216192946.png",
        "微信截图_20191216192946.png",
        484,
        346,
        "#fdfafb"
      ]
    }
  ]
}
[/block]
* 第三步：注册账号

注册基本账号满足以下条件之一即可：
1. 含有数字0~9
2. 含有特殊字符- 
3. 不含有a,e,i,o,u,y字母的

注册账号模式有两种：【账户模式】和【钱包模式】。
【账户模式】：可支持账号加密码及私钥两种登录方式，请务必管理好账号信息及私钥，确保钱包安全。（私钥是通过账户名和密码通过算法加密生成）
【钱包模式】：仅支持私钥登录，请务必备份好私钥，确保钱包安全。（私钥的生成和账户信息无关的随机生成）
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/e63d652-_20191231113707.png",
        "微信截图_20191231113707.png",
        491,
        513,
        "#e7e7f4"
      ]
    }
  ]
}
[/block]
* 第四步：保存私钥。注册完账号之后需务必保存私钥
【注意】Cocos-BCX 私钥分两种，各自权限不一样。
资产私钥（active ）活跃权限用来设定拥有花费本账户资金权限的账户名或公钥。
账户私钥（owner）账户权限设定谁可以控制本账户。控制人（账户名或者公钥）可修改账户相关的各自设置，包括权限设置。
[block:image]
{
  "images": [
    {
      "image": []
    }
  ]
}
[/block]
##**1.3 登录账号（导入钱包）**

* 第一步：点击立即登录
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/0f96057-_20191216192839_1.png",
        "微信截图_20191216192839 (1).png",
        750,
        684,
        "#a3a9e0"
      ]
    }
  ]
}
[/block]
* 第二步：输入账号密码或者钱包私钥进行登录

因为在注册的时候分为【账户模式】和【钱包模式】，而上面我们介绍了【账户模式】支持账户密码和私钥登录，【钱包模式】只支持私钥登录。所以在登录的时候依然有两种选择。

选择【账户模式登录】直接填写账户名和密码即可，这种情况只支持在【账户模式】下创建的账号。
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/98a14f3-_20191231140324.png",
        "微信截图_20191231140324.png",
        730,
        763,
        "#eae7f4"
      ]
    }
  ]
}
[/block]
【已有钱包，去导入】需要导入【资产私钥】或【账户私钥】任意一种即可。然后设置一个临时密码，该密码可以为你的账号密码，是为了加密导入的私钥进行存储。
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/21b10a9-_20191231140812.png",
        "微信截图_20191231140812.png",
        557,
        888,
        "#f1eff7"
      ]
    }
  ]
}
[/block]
## **1.4 多账户管理**
Cocos-BCX 手机钱包具有多账户管理功能，如需查看或者添加更多钱包，可先点击右上角，然后点击“+”,即可添加。
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/5d57f2a-_20191231141837.png",
        "微信截图_20191231141837.png",
        503,
        854,
        "#868593"
      ]
    }
  ]
}
[/block]
# 二、“钱包”页功能
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/7cdc72e-_20191231142759.png",
        "微信截图_20191231142759.png",
        495,
        875,
        "#c3c4e6"
      ]
    }
  ]
}
[/block]
从钱包页，我们可以看到总资产、转账、收款、资源、投票和我的资产（COCOS）。下面一一解释。

##**2.1 总资产**
目前注册一个主网账号，即可获得0.1COCOS，按照市场价，所以显示为0.000413（￥）。

##**2.2 转账** 
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/500af58-1.png__original",
        "1.png__original",
        498,
        417,
        "#fbf7f8"
      ]
    }
  ]
}
[/block]
转账需要注意的一点是，接收方的地址不是我们常见的一长串地址，只需要填写对方的账户名即可。

##**2.3 收款**
复制账户名或者提供收款二维码给转账方即可。
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/c00e473-_20191231145056.png",
        "微信截图_20191231145056.png",
        593,
        892,
        "#c6c7dd"
      ]
    }
  ]
}
[/block]
##**2.4 资源**
在手续费的设计上，Cocos-BCX 采取 GAS 资源模型。引入一种特化资产GAS，用于系统内多种事务的执行驱动计量。GAS 资产本身不可交易或转账。

通过冻结 COCOS 资产余额获得 GAS，冻结部分的 COCOS 不可以任何形式转账和交易，直到解冻。GAS 资产使用后按时间线性恢复，24h 后恢复至冻结量的100%，账户需执行领取操作才可获得恢复的 GAS。

在抵押时，用户可以选择给自己或者他人。
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/f0795b9-_20191231150352.png",
        "微信截图_20191231150352.png",
        497,
        830,
        "#f3f3f8"
      ]
    }
  ]
}
[/block]
##**2.5 投票**
在 Cocos-BCX 主网中，Cocos-BCX 继续采用改进的 DPos 算法，开启节点招募，候选人需要获得前11名投票才可以当选为活跃BP或理事会。为了方便用户进行投票，在钱包中也可以进行。
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/e55d247-_20191231151310.png",
        "微信截图_20191231151310.png",
        499,
        879,
        "#f3f2f3"
      ]
    }
  ]
}
[/block]
##**2.6 我的资产**
在“我的资产”中，可以进行转账和收款，已查看具体交易记录。
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/521601c-_20191231152145.png",
        "微信截图_20191231152145.png",
        713,
        837,
        "#bbc5ee"
      ]
    }
  ]
}
[/block]
#三、“发现”页功能
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/1877186-_20191231152600.png",
        "微信截图_20191231152600.png",
        491,
        869,
        "#ded8d9"
      ]
    }
  ]
}
[/block]
在“发现页”我们可以查看 Cocos-BCX 官网、区块链浏览器、生态产品和体验热门游戏。如果热门游戏没有展示你想体验的游戏，请在右上角输入已上线 Cocos-BCX 主网的 DApp官网，进行体验。

#四、“我的”页功能
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/6c1817a-_20191231153448.jpg",
        "微信图片_20191231153448.jpg",
        750,
        742,
        "#fafafb"
      ]
    }
  ]
}
[/block]
在“我的”页具有资产总览、钱包管理、系统设置、联系人和关于我们五个功能。以下进行简单讲解。

##**4.1 资产总览** 
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/5fffbdd-_20191231154547.png",
        "微信截图_20191231154547.png",
        731,
        685,
        "#bdc8f0"
      ]
    }
  ]
}
[/block]
在资产总览可以查看总资产、数字资产和非同质资产。

##**4.2 钱包管理 * 
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/9b90ed9-_20191231155019.png",
        "微信截图_20191231155019.png",
        490,
        407,
        "#f9f9fb"
      ]
    }
  ]
}
[/block]
点钱包管理，可以看到多个账户。
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/eca6677-_20191231155053.png",
        "微信截图_20191231155053.png",
        492,
        790,
        "#e2e3f4"
      ]
    }
  ]
}
[/block]
点开任意一个账户，可以查看公钥和私钥、重置密码和退出账号等。
导出私钥：如果用私钥导入模式，可以用临时密码解密查看导入时的私钥。
如果是账户登录模式，就可以用账户的密码查看用户的资产私钥和账户私钥。

##**4.3 系统设置** 
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/9751949-_20191231155518.jpg",
        "微信图片_20191231155518.jpg",
        750,
        465,
        "#fcfcfc"
      ]
    }
  ]
}
[/block]
在系统设置可以进行多种操作，比如语言，可以设置为中文和英文；网络设置可以为主网和测试网；货币单位可以设置为CNY和USD。

##**4.4 联系人**
我们在转账的时候提到了联系人，如果经常给某些人转账的话，我们可以把他们的账号添加进联系人，这样可以减免某些操作。在添加联系人时需要填写：联系人名称、备注和钱包地址（联系人的账户名）即可。
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/a110533-_20191231155952.jpg",
        "微信图片_20191231155952.jpg",
        750,
        680,
        "#fdfdfd"
      ]
    }
  ]
}
[/block]
#五、重要提示
账号密码一旦丢失将无法找回；
账号密码可以根据旧密码修改为新密码；
修改账户密码，随之账户私钥和资产私钥也会变化；
目前 Cocos-BCX 移动版钱包是支持主网的，跟测试网账号不通用，需要重新注册；
目前Cocos-BCX 移动版钱包是支持主网的，可以存放主网 COCOS，不支持 ERC20的COCOS，请勿往钱包转账；
Cocos-BCX主网 COCOS 映射将在后期进行，请注意官方渠道消息；
加密骑士团游戏需要抵押主网 COCOS 获取 GAS 才可以进行体验，如不能体验请联系客服（cocosbcx03）；
体验游戏需要导入资产私钥，领取 GAS 需要导入账户私钥，请勿搞混；
如仍有其他问题，请联系客服（cocosbcx03）。