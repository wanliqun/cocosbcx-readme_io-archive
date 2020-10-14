---
title: "1.2.3 Docker方式部署-推荐"
slug: "124-docker安装"
hidden: false
createdAt: "2019-04-10T09:40:57.106Z"
updatedAt: "2020-04-29T11:28:26.994Z"
---
[block:api-header]
{
  "title": "运行安装脚本"
}
[/block]
curl https://raw.githubusercontent.com/Cocos-BCX/cocos-bcx-node-bin/master/fullnode/mainnet/v1.1.3/build_chain.sh | bash

下载运行安装脚本，该脚本会从阿里云拉取镜像，取主网的配置文件config和genesis创世文件，并运行镜像。

该脚本启动后把日志和配置文件及区块数据映射到/mnt/witness下面，可以实时查看。

查看日志，大约几秒后会出现got block的字样.

详细可以参照wiki：
https://github.com/Cocos-BCX/cocos-mainnet/wiki/Run-With-Docker