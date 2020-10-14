---
title: "System Architecture"
slug: "system-architecture"
hidden: false
createdAt: "2019-03-15T06:26:48.439Z"
updatedAt: "2019-03-16T16:55:16.322Z"
---
[block:api-header]
{
  "title": "Run-Time Environment With Interoperable Interfaces And Multi-System"
}
[/block]

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/745ff1f-8.png",
        "8.png",
        482,
        255,
        "#bcc3cc"
      ],
      "caption": "Cocos-BCX on-chain games and operation architecture"
    }
  ]
}
[/block]
**Run-time environment for multi-system**

Cocos-BCX believes the future run-time environment of blockchain game should involve the following features:

• Full blockchain operating interfaces

• Downward transparency inheritance

• Encapsulated atomic operations

• Compatibility to multiple operating systems

To simplify the development process, Cocos-BCX designs a run-time environment for various Apps and interoperable interfaces, combines COCOS Creator, simplifies the connection between game process and blockchain, and makes interactions transparent to developers and enables traditional game developers to have no difficulty in dealing with developing or transferring blockchain games.

Cocos-BCX SDK is integrated into Runtime, providing complete chain interfaces. Developers connect game content with blockchain network based on Cocos-BCX SDK, and thus making chain interactions transparent and structured. Game development teams no longer have to invest in R&D to match chain network and equipment.

Android, iOS, PC Web and HTML5 are compatible in run-time environment, and thus games are transferrable across different platforms.
[block:api-header]
{
  "title": "Blockchain Interfaces"
}
[/block]
Cocos-BCX provides interactive environment to facilitate development on chain.

Cocos-BCX blockchain interoperable run-time environment provides compatible multi-systems, such as Android, SDK, javaScript and python and PHP. 

These developing environments facilitate blockchain software, and achieve data interaction, such as account registration, user information, assets operation and user data operation. On-chain data interfaces facilitate the storage of homogeneous or non-homogeneous digital data, featuring compatibility and customization. Blockchain system does not demand clear text of digital assets, and game developers enjoy greater flexibility to structure on-chain data storage and guarantee safely transferrable information across Client and market plug-in parser. 

Currently, chain interoperable environment mainly provides homogeneous digital assets, non homogeneous digital assets, props search, transfer, changes in ownership, transaction submission, proposal and other encapsulated functions.
[block:api-header]
{
  "title": "Multi-chain Riveted Exchange Gateway"
}
[/block]
Homogeneous and non-homogeneous assets are separated from smart contracts in Cocos-BCX. It can be predicted that massive and continuous transactions will exist in Cocos-BCX network. Therefore, it needs to reduce computational costs of assets parsing and transfer as much as possible to achieve cross-chain exchange of non-homogeneous assets. The separation of assets and contracts proves to be a safer design.
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/28a9b63-9.png",
        "9.png",
        397,
        261,
        "#f7f8f9"
      ],
      "caption": "Exchange Gateway"
    }
  ]
}
[/block]
Cocos-BCX provides a set of gateways to automatically exchange tokens and props, and achieves smooth transfer of content among different on-chain games and platforms under a unified value system. Exchangeable content includes data tokens, equipment data and etc.
[block:api-header]
{
  "title": "Optimization and Extension to the Existing Blockchain System"
}
[/block]
**Improved data structure of non-homogeneous digital assets** 

Non-homogeneous digital assets are a type of digital assets applied to distributed ledger network with unique assets instance, and its optimized type will serve blockchain gaming with more flexibility.

Cocos-BCX redesigns data structure, and adds custom data storage to contain potential game data and the extended content. Meanwhile, it adjusts some critical processes, such as consensus, witness and block generation to match new data structure. Cocos-BCX props data keeps full record in block data when generation and attributes change. In the common transaction and transfer, only Hush Pointer will be recorded, preventing block data size from growing too fast from accumulated transactions. 

Cocos-BCX blockchain divides non-homogeneous digital assets data structure into fixed data zone and extensible data zone. The former stores the basic information of non-homogeneous digital assets, including assets ID, worldview statement and basic data zone. Assets ID is the unique identification of assets instance in distributed ledger account, and the unique proof to visit, check and modify the assets. Worldview statement includes worldview ID, supported game and world, and currencies supporting assets circulation in the network. Basic data field consists of assets owners, producers, production time and assets basic attributes, such as prop strength. 

Extensible data field supports attribute extension of non-homogeneous digital assets, and stores specific transaction data under supported worldview, including zone data and Data  with combination relationship. Different games or other business entities have exclusive zone identity and data area in terms of zone data, which is isolated from each other. Zone data is stored in the form of key-value pairs of zone identity and data, representing the data of specific games, such as Attack, Defense and Durability. Extensible data field stores Data  with combination relationship, describing asset portfolio, and it also stores nested and affiliated relations.

Based on a set of structures of non-homogeneous digital assets, the first extensible non-homogeneous digital assets – BCX-NHAS-1808 is created. 

**Data separation of assets and contracts** 

Homogeneous, non-homogeneous assets and smart contract data are stored separately.

Massive and continuous transactions exist in Cocos-BCX network. Therefore, it needs to reduce transactional cost and computational costs of assets parsing as much as possible. The separation of assets and contracts is conducive to separately performing parsing and operating necessary results on chain.

Separately stored assets and contract data empower asset owner all privileges over the assets, prevent contract modification from destroying asset attributes or calling other assets, and easily realize cross-chain gateway of non-homogeneous assets without considering the constraints of contracts. Therefore, the separation of assets and contracts proves to be a safer design.

**Improved consensus mechanism**
DpoS consensus algorithm is used for the Cocos-BCX TestNet consensus layer.

DpoS algorithm infers block producers and block time based on the scheduled witness and allocated time slot, of which the interval is usually 5 seconds. In reality, the interval is set at 3 seconds for faster broadcasting and larger throughput. If the scheduled witness arrives in the allocated time slot but there is no normal production due to network problem or equipment failure, blocks will not be produced in that time slot. The network will wait until the next time slot and select the next scheduled witness to produce blocks. 

In Cocos-BCX, all scheduled witnesses are elected by stakeholders through voting. The scheduled witnesses are called active witnesses whose quantity ranges from 11 to 101. They share the same scheduled block probability as the witness scheduling algorithm in the DpoS consensus algorithm, which ensures that their block probabilities and rewards are consistent. GrapheneTM voting is usually updated every 24 hours. For security, stability and fairness concerns, voting for network allocation of the projects is updated at a shorter interval, usually 12 hours or less.
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/3fbd36d-10.png",
        "10.png",
        482,
        185,
        "#aeb8c9"
      ],
      "caption": "Comparison of existing consensus mechanisms"
    }
  ]
}
[/block]
In the DPoS algorithm, block producers and block time are inferred based on the scheduled witness and allocated time slot. The mainchain has more active witnesses than the sidechains, thus greater block height. Meanwhile, the mechanism of voting for network allocation avoids the centralization of witnesses, which ensures the security of the network. The strengths and weaknesses of the witness mechanisms are displayed in the following figure.
[block:api-header]
{
  "title": "Light Node"
}
[/block]
In Cocos-BCX, light nodes are interoperable environments with the chain. Different from full nodes, light nodes need not synchronize data to network but necessary contract information and environmental data. Such a design significantly reduces the amount of data and time for synchronization and allows actual capacity and feasible time cost for on-chain game softwares.
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/ae5bee4-11.png",
        "11.png",
        1218,
        600,
        "#3a4b56"
      ]
    }
  ]
}
[/block]
The games developed by Cocos-BCX are basically contracts operated locally on the light nodes, while some parts are compartmentalized separately into one or more sub-contracts that are distributed to related nodes for consensus (see Syntax Support to Compartmentalized Consensus Processing). Such a design allows enormous game contracts to be executed efficiently without latency. Separate processing of consensus and non-consensus parts secures data reliability similar to that of traditional blockchains while offering possible best user experience. Meanwhile, validation for light nodes falls on execution environment and input data (validation of trusted execution environment) rather than process and outcome as in traditional blockchains, further enhancing the overall execution efficiency.
[block:api-header]
{
  "title": "Timer And Heartbeat"
}
[/block]
Nearly all games and applications need online detection. For Cocos-BCX blockchain games, timer and heartbeat are put forward in response to user state detection and continual session.
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/7018d29-12.png",
        "12.png",
        482,
        251,
        "#3f4b58"
      ]
    }
  ]
}
[/block]
The time synchronization mechanism is the premise of a timer in the blockchain network. The traditional mechanism is built with external time signal or trust center. Under the trustless logic of blockchain, the external time signal and trust center both have defects that cannot be self-validated. Hence, on-chain time synchronization can only be completed inside the chain. 

The time synchronization solution of Cocos-BCX works as follows. With block timestamp, the block nodes broadcast equivalent time synchronization while releasing blocks. Each node completes time synchronization operations upon receiving the block broadcast. In the end, time synchronization to the whole network is completed once each block synchronization is completed.

With such a design, the timer is successfully created. With block period as the minimal timing granularity, the timer works according to the scheduled timing goals. Without bias caused by factors like time zone, the block timestamp is deemed as the timing standard for the whole network. The timer can be executed normally in any network zone and time zone based on the same timing rules. 

Heartbeat is similar to the timer. Its time pulse also comes from the block timestamp. In one heartbeat period, nodes/ends submit information about their updated connection. Absence of such information in a period indicates that the nodes/ends are offline. The timer and heartbeat provide application basis for user state detection and future sessions.
[block:api-header]
{
  "title": "High-Speed Virtual Machine"
}
[/block]
Cocos-BCX is capable of concurrent task processing.

Most of the existing games are played online. When there are a certain number of users, the server needs to process a large amount of data within a short time, which is impossible for the existing Ethereum network.

Theoretically, the improved DPoS consensus of Cocos-BCX allows a throughput up to 100,000 tps. Under a rational data management mode, the concurrent task processing is sufficient to support the development and processing existing games, meet the basic operation needs of large online games on the platform and secures game experience almost as good as that of the existing centralized games. 

Large online games mean significantly higher frequency in data interaction, as evidenced by DNF’s record of 600,000 people online at the same time and Steam’s even more astonishing record of 14.2 million people. If every online user’s submission of data is regarded as an application for consensus, Cocos-BCX’s maximum throughput cannot support such a magnitude of requests. Hence, the development team designs various delegation templates based on the speed of witness so that single delegates need no witness to process all the run-time games at the same time, but focus on witnessing and counting multiple games of the same type. Besides, under the templates, the submission of data or witness of different games is asynchronous. Each game will select a suitable delegation template. Data under the asynchronous templates is validated through on-chain database service. That is, users validate, store and obtain data on chain. This process is efficient enough to support operation of player data for large games.
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/24aa522-13.png",
        "13.png",
        482,
        224,
        "#cad8ef"
      ],
      "caption": "Cocos-BCX Smart Contract"
    }
  ]
}
[/block]
Contract is a segment of program that is executed automatically as well as a system of participants that fulfills scheduled tasks according to the basic algorithms of the environment (compiler algorithms). Contract can define input and output, receive and store value and send out information and value. Smart contract is designed with the “trustless principle”. All nodes believe that each other is not trustable. Each node of the blockchain, which features distributed storage, keeps the same contract execution code. The execution results are witnessed by the computing power of the whole network. Whether they are recognized is decided by everyone’s vote. Cocos-BCX smart contract supports the definition of witness delegation.

To ensure that the contract execution efficiency allows fluid gaming experience for the users, Cocos-BCX has come up with a virtual machine scheme based on Lua for on-chain games. Different from existing rivals, the scheme features custom-made and optimized run-time environment and execution efficiency as well as language and API system that are the same as those of SDKs, and interoperation interfaces for the chain and game execution environment. All this addresses the monotony in environment, poor flexibility and customization of blockchain contracts. The use of smart contract has gone beyond description of currency to content directly related to the games, probably including basic algorithms, setting, unit, scene and even maps. The improved virtual machine not only supports more complex and flexible contract forms but greatly improve the execution efficiency of smart contracts.