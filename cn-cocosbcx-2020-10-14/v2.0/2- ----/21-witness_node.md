---
title: "2.1 节点二进制程序详解"
slug: "21-witness_node"
hidden: false
createdAt: "2019-03-25T09:38:56.370Z"
updatedAt: "2020-04-29T11:35:48.492Z"
---
witness_node是节点启动的可执行文件，节点具有交易打包、出块、同步链数据等功能。
[block:api-header]
{
  "title": "2.1.1 同步数据节点部署"
}
[/block]

说明：这里部署的是数据同步节点，不具有出块功能。

部署有两种方式：
  * 手动部署；
  * docker镜像自动化部署

## 1. 手动部署

###  a. 准备节点运行依赖环境
  * 系统要求：Ubuntu16.04
  *  依赖库下载
[block:code]
{
  "codes": [
    {
      "code": "sudo apt-get update",
      "language": "shell"
    }
  ]
}
[/block]

[block:code]
{
  "codes": [
    {
      "code": "sudo apt-get install autoconf cmake git vim libbz2-dev libdb++-dev libdb-dev libssl-dev openssl libreadline-dev libtool libcurl4-openssl-dev libboost-all-dev",
      "language": "shell"
    }
  ]
}
[/block]
可能存在的问题说明：
* Ubuntu系统上的g++需要支持c++11;
* 有的时候使用apt-get安装一些软件或一些依赖库时，会遇到找不到这个包的情况或者速度特别慢，可以考虑把服务器的源换掉，改为国内的，大部分重新安装就能安装成功。
   
更改服务器软件源，详细操作如下：
  * 登录root用户或者使用sudo
  * 备份原来的源列表文件 
[block:code]
{
  "codes": [
    {
      "code": "mv /etc/apt/sources.list /etc/apt/sourses.list.backup",
      "language": "shell"
    }
  ]
}
[/block]
  *  新建源列表文件 
[block:code]
{
  "codes": [
    {
      "code": "vim /etc/apt/sources.list",
      "language": "shell"
    }
  ]
}
[/block]
  * 加入源地址（推荐用阿里云源） 

把下面的源地址 复制粘贴到sources.list文件里。
[block:code]
{
  "codes": [
    {
      "code": "deb http://mirrors.aliyun.com/ubuntu/ bionic main restricted universe multiverse\ndeb http://mirrors.aliyun.com/ubuntu/ bionic-security main restricted universe multiverse\ndeb http://mirrors.aliyun.com/ubuntu/ bionic-updates main restricted universe multiverse\ndeb http://mirrors.aliyun.com/ubuntu/ bionic-proposed main restricted universe multiverse\ndeb http://mirrors.aliyun.com/ubuntu/ bionic-backports main restricted universe multiverse\ndeb-src http://mirrors.aliyun.com/ubuntu/ bionic main restricted universe multiverse\ndeb-src http://mirrors.aliyun.com/ubuntu/ bionic-security main restricted universe multiverse\ndeb-src http://mirrors.aliyun.com/ubuntu/ bionic-updates main restricted universe multiverse\ndeb-src http://mirrors.aliyun.com/ubuntu/ bionic-proposed main restricted universe multiverse\ndeb-src http://mirrors.aliyun.com/ubuntu/ bionic-backports main restricted universe multiverse",
      "language": "text"
    }
  ]
}
[/block]
  * 更新软件列表 
[block:code]
{
  "codes": [
    {
      "code": "sudo apt-get update",
      "language": "shell"
    }
  ]
}
[/block]
### b.  获取可执行文件和配置

    
节点运行需获取witness_node和genesis.json、config.ini配置。cli_wallet不是必须的，在验证节点是否搭建正常和链交互时会使用到。   
 
witness_node是节点启动的可执行文件。

cli_wallet是钱包客户端可执行文件。

节点启动加载的配置文件有两个：genesis.json和config.ini。

关于genesis.json和config.ini：
  * 同一条链的节点启动时，使用的genesis.json必须是相同的。genesis.json会影响chain-id，不同的链的genesis.json通常不同。
  * 不同节点的config.ini有些参数会不同，该配置可以根据需要修改。

可执行文件和配置[仓库地址]( https://github.com/Cocos-BCX/cocos-bcx-node-bin.git)：
[block:code]
{
  "codes": [
    {
      "code": "git clone https://github.com/Cocos-BCX/cocos-bcx-node-bin.git",
      "language": "shell"
    }
  ]
}
[/block]
cocos-bcx-node-bin仓库中存在多个版本的witness_node和配置，下面以full_node/testnet v0.7.16为例说明：
* [可执行文件witness_node路径](https://github.com/Cocos-BCX/cocos-bcx-node-bin/tree/master/fullnode/testnet/0.7.16/linux)。可执行文件较大，已压缩，解压缩命令：tar -zxvf  witness_node.tar.gz。如果witness_node没有可执行权限，请执行：chmod +x witness_node
* [配置genesis.json和config.ini路径](https://github.com/Cocos-BCX/cocos-bcx-node-bin/tree/master/fullnode/testnet/0.7.16/config)。**genesis.json不允许修改**；config.ini是默认可用的示例，用户可以根据自己的需求进行修改；setup_node.sh是节点第一次启动执行的shell脚本，实际上是把节点启动执行的一些命令进行了封装。
* [cli_wallet路径](https://github.com/Cocos-BCX/cocos-bcx-node-bin/tree/master/cli/testnet/0.7.16/linux)


### c. 节点启动


把witness_node、genesis.json、config.ini和setup_node.sh放置在同一目录下

  * **第一次启动节点**

在witness_node可执行文件路径下，执行setup_node.sh

如果witness_node没有可执行权限，请执行：chmod +x witness_node
如果setup_node.sh没有可执行权限，请执行：chmod +x setup_node.sh

脚本执行命令：
[block:code]
{
  "codes": [
    {
      "code": "./setup_node.sh\n",
      "language": "shell"
    }
  ]
}
[/block]
节点以nohup形式启动，chain-id 保存在chainID.log中，节点运行log在witness_node.log中。

  * **节点安全停止运行**

异常停止节点服务，往往会产生脏数据，导致下次再次启动节点失败。

安全地停止节点服务的方式：pkill witness_node或者kill -15 PID


  * **再次启动节点**

只需要执行下面的命令：
[block:code]
{
  "codes": [
    {
      "code": "nohup ./witness_node --genesis-json genesis.json >> witness_node.log 2>&1 &",
      "language": "shell"
    }
  ]
}
[/block]

  * **脏数据清除**
[block:code]
{
  "codes": [
    {
      "code": "./witness_node --genesis-json genesis.json  --resync-blockchain",
      "language": "shell"
    }
  ]
}
[/block]
注意：执行此命令会把该节点的区块数据都清除掉。


### d. 节点启动验证
  
* witness_node节点运行log验证

节点启动后，会输出log到witness_node.log文件中，查看log出现Got block同步区块数据的内容，即可说明节点启动正常。

如果链上区块数据比较多，同步到最新区块数据会耗时比较长。

详细log如下：
[block:code]
{
  "codes": [
    {
      "code": "......\n2046508ms th_a       application.cpp:203           reset_p2p_node       ] Configured p2p node to listen on 0.0.0.0:8060\n2046511ms th_a       application.cpp:283           reset_websocket_serv ] Configured websocket rpc to listen on 0.0.0.0:8049\n2046514ms th_a       witness.cpp:118               plugin_startup       ] witness plugin:  plugin_startup() begin\n2046516ms th_a       witness.cpp:136               plugin_startup       ] No witnesses configured! Please add witness IDs and private keys to configuration.\n2046518ms th_a       witness.cpp:138               plugin_startup       ] witness plugin:  plugin_startup() end\n2046519ms th_a       main.cpp:267                  main                 ] Started node on a chain with 0 blocks.\n2046521ms th_a       main.cpp:268                  main                 ] Chain ID is 7d89b84f22af0b150780a2b121aa6c715b19261c8b7fe0fda3a564574ed7d3e9\n2062761ms th_a       application.cpp:522           handle_block         ] Got block: #10000 time: 2019-06-04T11:44:18 latency: 3520204761 ms from: init3  irreversible: 9992 (-8)\n2078184ms th_a       application.cpp:522           handle_block         ] Got block: #20000 time: 2019-06-04T17:18:14 latency: 3500184184 ms from: init9  irreversible: 19992 (-8)\n2091319ms th_a       application.cpp:522           handle_block         ] Got block: #30000 time: 2019-06-04T22:52:04 latency: 3480167319 ms from: init7  irreversible: 29992 (-8)\n2104634ms th_a       application.cpp:522           handle_block         ] Got block: #40000 time: 2019-06-05T04:26:00 latency: 3460144634 ms from: init6  irreversible: 39989 (-11)\n2118227ms th_a       application.cpp:522           handle_block         ] Got block: #50000 time: 2019-06-05T10:02:24 latency: 3439974227 ms from: init0  irreversible: 49990 (-10)\n2134949ms th_a       application.cpp:522           handle_block         ] Got block: #60000 time: 2019-06-05T15:36:14 latency: 3419960949 ms from: init3  irreversible: 59991 (-9)\n2149467ms th_a       application.cpp:522           handle_block         ] Got block: #70000 time: 2019-06-05T21:10:10 latency: 3399939467 ms from: init5  irreversible: 69991 (-9)\n2166023ms th_a       application.cpp:522           handle_block         ] Got block: #80000 time: 2019-06-06T02:44:00 latency: 3379926023 ms from: init7  irreversible: 79991 (-9)\n2182468ms th_a       application.cpp:522           handle_block         ] Got block: #90000 time: 2019-06-06T08:26:58 latency: 3359364468 ms from: init8  irreversible: 89992 (-8)\n2198981ms th_a       application.cpp:522           handle_block         ] Got block: #100000 time: 2019-06-06T14:00:54 latency: 3339344981 ms from: init7  irreversible: 99992 (-8)\n2213786ms th_a       application.cpp:522           handle_block         ] Got block: #110000 time: 2019-06-06T19:34:44 latency: 3319329786 ms from: init5  irreversible: 109992 (-8)\n2228284ms th_a       application.cpp:522           handle_block         ] Got block: #120000 time: 2019-06-07T01:08:40 latency: 3299308284 ms from: init2  irreversible: 119992 (-8)\n2244463ms th_a       application.cpp:522           handle_block         ] Got block: #130000 time: 2019-06-07T06:42:30 latency: 3279294463 ms from: init4  irreversible: 129992 (-8)\n2266002ms th_a       application.cpp:522           handle_block         ] Got block: #140000 time: 2019-06-07T12:16:26 latency: 3259280002 ms from: init3  irreversible: 139992 (-8)\n2287018ms th_a       application.cpp:522           handle_block         ] Got block: #150000 time: 2019-06-07T17:54:40 latency: 3239007018 ms from: init8  irreversible: 149989 (-11)\n2307275ms th_a       application.cpp:522           handle_block         ] Got block: #160000 time: 2019-06-07T23:28:36 latency: 3218991275 ms from: init8  irreversible: 159989 (-11)\n2327053ms th_a       application.cpp:522           handle_block         ] Got block: #170000 time: 2019-06-08T05:06:12 latency: 3198755053 ms from: init10  irreversible: 169989 (-11)\n2348915ms th_a       application.cpp:522           handle_block         ] Got block: #180000 time: 2019-06-08T10:40:02 latency: 3178746915 ms from: init10  irreversible: 179992 (-8)\n2367877ms th_a       application.cpp:522           handle_block         ] Got block: #190000 time: 2019-06-08T16:13:58 latency: 3158729877 ms from: init1  irreversible: 189990 (-10)\n2386397ms th_a       application.cpp:522           handle_block         ] Got block: #200000 time: 2019-06-08T21:47:48 latency: 3138718397 ms from: init7  irreversible: 199992 (-8)\n2406046ms th_a       application.cpp:522           handle_block         ] Got block: #210000 time: 2019-06-09T03:21:44 latency: 3118702046 ms from: init6  irreversible: 209992 (-8)\n2426167ms th_a       application.cpp:522           handle_block         ] Got block: #220000 time: 2019-06-09T08:55:34 latency: 3098692167 ms from: init2  irreversible: 219992 (-8)\n2445954ms th_a       application.cpp:522           handle_block         ] Got block: #230000 time: 2019-06-09T14:29:30 latency: 3078675954 ms from: init1  irreversible: 229992 (-8)\n2467114ms th_a       application.cpp:522           handle_block         ] Got block: #240000 time: 2019-06-09T20:03:26 latency: 3058661114 ms from: init3  irreversible: 239991 (-9)\n2489161ms th_a       application.cpp:522           handle_block         ] Got block: #250000 time: 2019-06-10T01:37:16 latency: 3038653161 ms from: init8  irreversible: 249991 (-9)\n2510115ms th_a       application.cpp:522           handle_block         ] Got block: #260000 time: 2019-06-10T07:11:12 latency: 3018638115 ms from: init2  irreversible: 259989 (-11)\n2522582ms th_a       database_api.cpp:283          database_api_impl    ] creating database api 140901296\n2522584ms th_a       database_api.cpp:283          database_api_impl    ] creating database api 140914416\n2523378ms th_a       database_api.cpp:283          database_api_impl    ] creating database api 141054768\n2523380ms th_a       database_api.cpp:304          ~database_api_impl   ] freeing database api 140914416\n2532011ms th_a       application.cpp:522           handle_block         ] Got block: #270000 time: 2019-06-10T12:47:42 latency: 2998470011 ms from: init7  irreversible: 269988 (-12)\n2554534ms th_a       application.cpp:522           handle_block         ] Got block: #280000 time: 2019-06-10T18:22:14 latency: 2978420533 ms from: init2  irreversible: 279990 (-10)\n2576437ms th_a       application.cpp:522           handle_block         ] Got block: #290000 time: 2019-06-10T23:56:04 latency: 2958412437 ms from: init10  irreversible: 289992 (-8)\n2599590ms th_a       application.cpp:522           handle_block         ] Got block: #300000 time: 2019-06-11T05:30:00 latency: 2938399590 ms from: init2  irreversible: 299992 (-8)\n......",
      "language": "text"
    }
  ]
}
[/block]
  * cli_wallet钱包命令行验证

cli_wallet是钱包命令行，用来与节点进行交互。通过交互可以查看链的一些区块信息，据此来验证节点启动是否正常。

启动cli_wallet：
[block:code]
{
  "codes": [
    {
      "code": "./cli_wallet --chain-id 7d89b84f22af0b150780a2b121aa6c715b19261c8b7fe0fda3a564574ed7d3e9 -s ws://127.0.0.1:8049 -r 127.0.0.1:8048",
      "language": "shell"
    }
  ]
}
[/block]
正常启动后，可以看到如下信息：
[block:code]
{
  "codes": [
    {
      "code": "Logging RPC to file: logs/rpc/rpc.log\n2726309ms th_a       main.cpp:131                  main                 ] key_to_wif( committee_private_key ): 5KCBDTcyDqzsqehcb52tW5nU6pXife6V2rX9Yf7c3saYSzbDZ5W \n2726315ms th_a       main.cpp:135                  main                 ] nico_pub_key: COCOS7yE9skpBAirth3eSNMRtwq1jYswEE3uSbbuAtXTz88HtbpQsZf \n2726315ms th_a       main.cpp:136                  main                 ] key_to_wif( nico_private_key ): 5KAUeN3Yv51FzpLGGf4S1ByKpMqVFNzXTJK7euqc3NnaaLz1GJm \nStarting a new wallet with chain ID 7d89b84f22af0b150780a2b121aa6c715b19261c8b7fe0fda3a564574ed7d3e9 (from CLI)\n2726319ms th_a       main.cpp:183                  main                 ] wdata.ws_server: ws://127.0.0.1:8049 \n2726329ms th_a       main.cpp:188                  main                 ] wdata.ws_user:  wdata.ws_password:  \nPlease use the set_password method to initialize a new wallet before continuing\n2727441ms th_a       main.cpp:227                  main                 ] Listening for incoming RPC requests on 127.0.0.1:8048\nnew >>> ",
      "language": "text"
    }
  ]
}
[/block]
执行info命令可以查看到该节点同步到的最新区块(head_block_num)信息：
[block:code]
{
  "codes": [
    {
      "code": "Please use the set_password method to initialize a new wallet before continuing\n2727441ms th_a       main.cpp:227                  main                 ] Listening for incoming RPC requests on 127.0.0.1:8048\nnew >>> info\ninfo\n{\n  \"head_block_num\": 368397,\n  \"head_block_id\": \"00059f0dddcff65636f9e7a374deeb162d1054b6\",\n  \"head_block_age\": \"32 days old\",\n  \"next_maintenance_time\": \"32 days ago\",\n  \"chain_id\": \"7d89b84f22af0b150780a2b121aa6c715b19261c8b7fe0fda3a564574ed7d3e9\",\n  \"participation\": \"100.00000000000000000\",\n  \"active_witnesses\": [\n    \"1.6.1\",\n    \"1.6.2\",\n    \"1.6.3\",\n    \"1.6.4\",\n    \"1.6.5\",\n    \"1.6.6\",\n    \"1.6.7\",\n    \"1.6.8\",\n    \"1.6.9\",\n    \"1.6.10\",\n    \"1.6.11\"\n  ],\n  \"active_committee_members\": [\n    \"1.5.0\",\n    \"1.5.1\",\n    \"1.5.2\",\n    \"1.5.3\",\n    \"1.5.4\",\n    \"1.5.5\",\n    \"1.5.6\",\n    \"1.5.7\",\n    \"1.5.8\",\n    \"1.5.9\",\n    \"1.5.10\"\n  ]\n}\n",
      "language": "text"
    }
  ]
}
[/block]

进一步的验证，可以通过set_password、unlock、import_key、transfer执行转账是否成功来验证。