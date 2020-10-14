---
title: "2.1 witness_node"
slug: "21-witness_node"
hidden: false
createdAt: "2019-06-24T07:22:32.431Z"
updatedAt: "2019-08-01T06:10:08.439Z"
---
Witness_node is is an executable file initiated by a node, which has functions such as generating blocks and syncing chain data.

##2.1.1 Deployment of data syncing node

Note: here we deployed is the data syncing node, which cannot generate a block.

There are two ways to deploy: 
a. Manual deployment; 
b. Automatic deployment by docker image.

###  a. Prepare the dependent environment to run the node
  * System:  Ubuntu16.04
  * Download dependent library
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
Description of possible problems:
* g++ on Ubuntu systems needs to support c++11;
* Sometimes when you use apt-get to install some software or some dependent libraries, you will find that the package cannot be found or the speed is very slow. You can consider changing the source of the server, after which the software or dependent library will be successfully installed.
   
Below is the detailed operations to change the source of server software
  * Log in as root or use sudo
  * Back up the original source list file
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
* Create a new source list file
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
  *  Add source address (it is recommended​ to use Alibaba Cloud source)

Copy and paste the source address below into the sources.list file.
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
* Update software list
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
### b.  Get the executables and configurations

    
witness_node, genesis.json and config.in configurations are required to run the node. Cli_wallet is not required but will be used when verifying whether the node is built properly and in interactions with the chain.
 
witness_node is the executable file for node start.

cli_wallet is the executable file for wallet client.

There are two configuration files for node start: genesis.json and config.ini.

About genesis.json and config.ini：
  * When starting the nodes of the same chain, the genesis.json used must be the same. genesis.json will affect chain-id, therefore the genesis.json varies with different chains.
  * Some parameters of config.ini of different nodes will be different. This configuration can be modified as needed.

Executable files and configuration[repositories address]( https://github.com/Cocos-BCX/cocos-bcx-node-bin.git):
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
There are multiple versions of the witness_node and configuration in the cocos-bcx-node-bin repository. The following is an example of full_node/testnet v0.7.16:
* [Executable file witness_node path] (https://github.com/Cocos-BCX/cocos-bcx-node-bin/tree/master/fullnode/testnet/0.7.16/linux).  The executable file is compressed, uncompress command: tar -zxvf  witness_node.tar.gz. If the witness_node does not have executable permissions, please execute: chmod +x witness_node
* [genesis.json and config.ini configuration path] (https://github.com/Cocos-BCX/cocos-bcx-node-bin/tree/master/fullnode/testnet/0.7.16/config). **genesis.json cannot be modified **; Config.ini is an example that is available by default. Users can modify it according to their own needs. setup_node.sh is the shell script executed when the node starts for the first time. It actually encapsulates some commands to be executed when the node starts.
* [cli_wallet path](https://github.com/Cocos-BCX/cocos-bcx-node-bin/tree/master/cli/testnet/0.7.16/linux)


### c. Node start

Put witness_node, genesis.json, config.ini, and setup_node.sh in the same directory

  * **Start the node for the first time**

Execute setup_node.sh in the witness_node executable file path

If the witness_node does not have executable permissions, please execute: chmod +x witness_node
If setup_node.sh does not have executable permissions, execute: chmod +x setup_node.sh

Script execution command:
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
The node is started in nohup, the chain-id is stored in chainID.log, and the node is running log in the duration_node.log.

  * **Node safely stops running**

Abnormally stopping the node service will often generate dirty data, which will cause the node to fail to restart next time.

The way to safely stop node services: pkill witness_node or kill -15 PID

  * **Restart the node**

Execute the following command:
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

  * **Remove dirty data**
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
Note: Executing this command will clear the block data of this node.


### d. Node start verification
  
* witness_node running log verification

After the node is started, a log will be output to the witness_node.log file to check the contents of the Got block sync block data in the log, which means that the node starts normally.

If there is a lot of blocks on the blockchain, it will take a long time to synchronize to the latest block.

The detailed log is as follows:
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
  * cli_wallet command line verification

Cli_wallet is the wallet command line used to interact with nodes. Block information of the chain can be viewed through the interactions, thus verifying whether the node starts normally.

Start cli_wallet: 
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
You can see the following information after cli_wallet is successfully started:
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
Run the info command to view the latest block (head_block_num) information that the node synchronizes to:
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
It can be further verified by the successful execution of set_password, unlock, import_key, and transfer.