---
title: "2.1 Witness_node"
slug: "2-1-witness_node"
hidden: false
createdAt: "2019-08-26T04:48:34.442Z"
updatedAt: "2019-08-26T05:02:01.753Z"
---
Witness_node는 노드에서 시작한 실행 파일이며 블록 생성 및 체인 데이터 동기화와 같은 기능이 있습니다.

##2.1.1 데이터 동기화 노드 배포

Note: 우리는 블록을 생성 할 수없는 데이터 동기화 노드를 배포했습니다.

배포하는 두 가지 방법이 있습니다: 
a. 수동배포
b. 도커 이미지에 의한 자동 배포

###  a. 노드를 실행할 종속 환경 준비
  * 시스템:  Ubuntu16.04
  * 종속 라이브러리 다운로드
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
발상가능한 문제에 대한 기술:
* g++ Ubuntu systems은 c++11의 지원이 필요로 함
* apt-get을 사용하여 특정 소프트웨어 또는 특정 종속 라이브러리를 설치할 때, 패키지를 찾을 수 없거나 속도가 매우 느려질 수 있습니다. 서버 소스 변경을 고려한 이후에는 소프트웨어 또는 종속 라이브러리가 성공적으로 설치치 될 수 있습니다.
   
다음은 서버 소프트웨어의 소스를 변경하는 자세한 운영법입니다
  * 루트로 로그인하거나 sudo를 사용하십시오
  * 원본 소스 목록 파일을 백업하십시오
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
* 새로운 소스목록파일을 생성하십시오 
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
  *  소스 주소 추가 (Alibaba Cloud 소스를 사용하는 것이 좋습니다)

아래 소스 주소를 복사하여 소스 목록 파일에 붙여 넣으십시오.
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
* 소프트웨어 목록 업데이트
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
### b.  실행 파일 및 구성 가져 오기

    
노드를 실행하려면 witness_node, genesis.json 및 config.in 구성이 필요합니다. Cli_wallet은 필요하지 않지만 노드가 올바르게 구축되어 있고 체인과 상호 작용하는지 확인할 때 사용됩니다.
 
witness_node는 노드 시작을위한 실행 파일입니다.

cli_wallet은 wallet 클라이언트의 실행 파일입니다.

노드 시작을위한 두 개의 구성 파일 (genesis.json 및 config.ini)이 있습니다.

genesis.json 및 config.ini 정보 ：
   * 같은 체인의 노드를 시작할 때 사용 된 genesis.json은 같아야합니다. genesis.json은 chain-id에 영향을 미치므로 genesis.json은 체인마다 다릅니다.
   * 다른 노드의 config.ini의 일부 매개 변수가 다릅니다. 이 구성은 필요에 따라 수정할 수 있습니다.

실행 파일 및 구성 [저장소 주소] (https://github.com/Cocos-BCX/cocos-bcx-node-bin.git):
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
cocos-bcx-node-bin 저장소에는 여러 버전의 witness_node 및 구성이 있습니다. 다음은 full_node / testnet v0.7.16의 예입니다.

* [Executable file witness_node path] (https://github.com/Cocos-BCX/cocos-bcx-node-bin/tree/master/fullnode/testnet/0.7.16/linux). 실행 파일이 압축되어 압축 해제 명령 인 tar -zxvf witness_node.tar.gz입니다. witness_node에 실행 권한이 없으면 chmod + x witness_node를 실행하십시오.

* [genesis.json and config.ini configuration path] (https://github.com/Cocos-BCX/cocos-bcx-node-bin/tree/master/fullnode/testnet/0.7.16/config). **genesis.json cannot be modified **; Config.ini는 기본적으로 사용 가능한 예입니다. 사용자는 자신의 필요에 따라 수정할 수 있습니다. setup_node.sh는 노드가 처음 시작될 때 실행되는 쉘 스크립트입니다. 실제로 노드가 시작될 때 실행될 일부 명령을 캡슐화합니다.


* [cli_wallet path](https://github.com/Cocos-BCX/cocos-bcx-node-bin/tree/master/cli/testnet/0.7.16/linux)


### c. Node 개시

witness_node, genesis.json, config.ini 및 setup_node.sh를 동일한 디렉토리에 두십시오. 

  * **노드를 처음 시작하십시오**

witness_node 실행 파일 경로에서 setup_node.sh를 실행하십시오.

witness_node에 실행 권한이 없으면 chmod + x witness_node를 실행하십시오.
setup_node.sh에 실행 권한이 없으면 chmod + x setup_node.sh를 실행하십시오.

스크립트 실행 명령:
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
노드는 nohup에서 시작되고 chain-id는 chainID.log에 저장되며 노드는 duration_node.log에서 로그를 실행 중입니다.

   * ** 노드 안전하게 실행 중지 **

비정상적으로 노드 서비스를 중지하면 더티 데이터가 생성되어 다음에 노드가 다시 시작되지 않습니다.

노드 서비스를 안전하게 중지하는 방법: pkill witness_node 또는 kill -15 PID

   * ** 노드를 다시 시작하십시오 **

다음 명령을 실행하십시오:
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

  * **오염 데이터 제거**
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
참고: 이 명령을 실행하면이 노드의 블록 데이터가 지워집니다.


### d. Node 개시 인증
  
* 로그 검증을 실행하는 witness_node

노드가 시작된 후 로그에서 Got 블록 동기화 블록 데이터의 내용을 확인하기 위해 witness_node.log 파일에 로그가 출력됩니다. 이는 노드가 정상적으로 시작됨을 의미합니다.

블록 체인에 많은 블록이있는 경우 최신 블록과 동기화하는 데 시간이 오래 걸립니다.

자세한 로그는 다음과 같습니다:
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
* cli_wallet 명령행 확인

Cli_wallet은 노드와 상호 작용하는 데 사용되는 월렛 명령힝입니다. 상호 작용을 통해 체인의 블록 정보를 볼 수 있으므로 노드가 정상적으로 시작하는지 확인할 수 있습니다.

cli_wallet을 시작하십시오:
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
cli_wallet이 성공적으로 시작된 후 다음 정보를 볼 수 있습니다:
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
info 명령을 실행하여 노드가 동기화하는 최신 블록 (head_block_num) 정보를보십시오.
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
set_password, unlock, import_key 및 transfer의 성공적인 실행을 추가로 확인할 수 있습니다.