---
title: "3.2 System Architecture"
slug: "32-system-architecture"
hidden: false
createdAt: "2019-06-24T09:57:48.065Z"
updatedAt: "2019-06-24T10:03:40.638Z"
---
##Integrated Blockchain-Interactive Runtime Environment for Games
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/fdddf61-6aa4721-3-2-1Cocos-BCX.png",
        "6aa4721-3-2-1Cocos-BCX.png",
        1133,
        599,
        "#385273"
      ],
      "caption": "3-2-1 Cocos-BCX On-Chain Game Run-time Environment Architecture"
    }
  ]
}
[/block]
**Game Runtime Environment With Multi-System Compatibility**

Cocos-BCX believes the run-time environment of future blockchain game should involve the following features:
  * Full blockchain interoperable interfaces;
  * Transparent downward inheritance;
  * Packaged atomic operations;
  * Compatible with multiple operating systems.

To simplify the development process, Cocos-BCX designs an integrated run-time environment for various Apps and supporting interoperable interfaces. Combined with COCOS Creator, it simplifies the connection between game programs and the blockchain, making interactions transparent to developers, allowing traditional game developers to develop or migrate blockchain games without any barriers.

Cocos-BCX SDK is integrated into the Cocos Runtime to provide a complete blockchain interactive interface for the game. The developers can connect game content with blockchain network based on Cocos-BCX SDK for the transparent and structured interactions, which frees the game development team from investing in R&D to be compatible with the blockchain network and different devices.

The runtime environment will be compatible with Android, iOS and PC Web, mobile H5 and other systems and environments. The games in the runtime environment can be run across different platforms.


##Interactive Interfaces of Blockchain

Cocos-BCX provides an interoperable environment that allows developers to easily interact with the blockchain.

Cocos-BCX blockchain interfaces integrate with multi-system SDK, including Android, iOS, JavaScript for front-end web applications and back-end python and PHP.

Those developing environments can facilitate the development of blockchain software, and data interaction, such as account registration, user information, assets operation and user data operation. On-chain data interfaces allow users to store homogeneous or non-homogeneous asset data, featuring compatibility and customization. Blockchain system does not demand clear text of digital assets.  Game developers enjoy greater flexibility to structure on-chain data storage and guarantee safely transferrable information across Client and market plug-in parser.

Currently, the blockchain interactive environment provides mainly the packaging of functions including the search and transfer of homogeneous and non-homogeneous assets and props, changes in ownership, transaction submission, proposal and voting. 


##Exchange Gateway Supporting the Homogeneous and Non-Homogeneous Assets and Cross-Chain Transactions

Homogeneous and non-homogeneous assets are separated from the smart contract in Cocos-BCX. It is foreseeable that there will be a large number of ongoing transactions in Cocos-BCX network. It is necessary to reduce the ​computational cost of assets analysis and circulation as much as possible to achieve cross-chain exchange of non-homogeneous assets. The separation of assets and contracts proves to be a safer design.
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/6cdb29b-b312f92-3-2-2.png",
        "b312f92-3-2-2.png",
        801,
        526,
        "#f7f9fa"
      ],
      "caption": "3-2-2 Exchange Gateway"
    }
  ]
}
[/block]
Cocos-BCX provides a set of gateways for the automatic exchange of coins and props, which enables the smooth transfer of contents among different on-chain games and platforms under a unified value system. Contents that can be exchanged include​ game coins, equipment data and etc.

**Exchange of Digital Game Assets**

The exchange of game digital assets and Ethereum ERC20 digital assets is as follows:
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/5c22f96-06e5cdb-_1.png",
        "06e5cdb-_1.png",
        939,
        211,
        "#f5f5f5"
      ],
      "caption": "3-2-3 Exchange of ERC20 Digital Assets"
    }
  ]
}
[/block]
Game coins can be transferred across consortium chains and private chains through an ​exchange gateway.

**Exchange of Non-Homogeneous Digital Game Assets**
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/e0941f9-2c0ecd3-_1.png",
        "2c0ecd3-_1.png",
        939,
        198,
        "#f3f3f3"
      ],
      "caption": "3-2-4 Exchange between Cocos-BCX And ERC721 Digital Assets"
    }
  ]
}
[/block]
BCX-NHAS-1808 is a non-homogeneous digital asset standard for the decentralized and distributed ledger network in the use of COCOS tokens. Compatible with other standards for non-homogeneous assets, it features separation between assets and contracts and a scalable and customizable data zone.

The ERC875 and ERC721 standards are Ethereum's standard protocols for non-homogeneous digital assets. To some extent, ERC875 standard is more like an upgraded version of a simplified ERC721 standard, which is the very first of its kind. ERC841 and ERC821 standards are its optimized and amended versions while ERC875 standard is simpler and more direct. Its defined functions including name, symbol, balanceOf, transfer, transferFrom, totalSupply, ownerOf and trade. Compared with ERC721 standard, the function of ERC875 standard is much simpler.

Further expanding the digital asset technologies supported by the exchange gateway allows the gateway to support non-homogeneous complex contracts represented by ERC721, ERC875 and BCX-NHAS-1808 standards. The gateway is equivalent to a specific compiler in the exchange of game props and non-homogeneous contracts. By translating and exchanging structured data, it realizes two-way exchange between non-homogeneous contracts and on-chain game props. Compatible with more types of prop exchanges inside and outside the chains, it provides richer game content and user experience.


## Improvement and Extension to the Existing Blockchains
**Improved Data Structure of Non-homogeneous Assets**
Non-homogeneous digital assets are a type of digital assets applied to distributed ledger network with unique assets instance. Optimized structure of non-homogeneous digital assets facilitates more flexible service to blockchain gaming.

Cocos-BCX redesigns the data structure and adds custom data storage to accommodate possible game data and extended content. Meanwhile, consensus, witness, block generation and other crucial process are adjusted accordingly to be matched with the ​new data structure. Item data in Cocos-BCX will be recorded in full in the block data only in the case of generation and any attribute change. While in the common transaction and transfer, only the hash pointer will be recorded to prevent block size from growing too fast with the accumulation of transactions.
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/3b9a99a-b0ce604-_1.png",
        "b0ce604-_1.png",
        939,
        714,
        "#eaebed"
      ],
      "caption": "3-2-5 Relationship Between Each Part and Data Structure of Non-Homogeneous Assets"
    }
  ]
}
[/block]
The non-homogeneous digital assets data structure in the blockchain network is divided into fixed data zone and scalable data zone.

The former stores the basic information of non-homogeneous digital assets, including assets ID, worldview statement and basic data zone. The assets ID is the unique identifier of assets instance in the distributed ledger network, and the unique credential to access, check and modify the assets. Worldview statement, including the worldview ID, the type of game in which the asset is in effect and supported, the world and the currencies supporting the circulation of assets in the network. The basic data zone further consists of information including a basic description of the assets, production time, producer, owner, user, a black & white list of use right, etc.

Scalable data zone is a functional section designed for attribute extension of non-homogeneous digital assets, including zone data and data with combination relationship. Data with combination relationship describes asset portfolios, nesting and affiliations. The scalable data zone stores specific transaction data under supported worldview, the data unit of which is called “zone”. Different games or other business entities have exclusive zone IDs and a ​data area in terms of zone data, which is isolated from each other. Zone data is stored in the form of key-value pairs of zone identity and data, representing the data of specific games, such as Attack, Defense and Durability.

In addition, the design of separated use right and ownership makes the business designs of complex financial models including lease, mortgage and pledge based on on-chain permission system available.

Cocos BCX-NHAS-1808 has many advantages over other non-homogeneous digital assets standards of Ethereum, such as the separation of assets and contracts, scalable and customizable data zone and compatibility with other non-homogeneous assets standards.

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/5623f20-635f897-_1.png",
        "635f897-_1.png",
        932,
        378,
        "#b1c7d3"
      ],
      "caption": "3-2-6 Comparison of Existing Non-Homogeneous Digital Assets Standards"
    }
  ]
}
[/block]
**Separately Stored Assets and Contract Data**

Homogeneous & non-homogeneous assets data, and smart contracts are stored separately on the blockchain. 

There are a lot of continuous transactions in Cocos-BCX, which makes it necessary to reduce the computational cost of assets analysis and transfer. Separation of assets and contracts can contribute to individual execution of contracts and necessary results on chain.

Under this circumstance, the owner of the asset has full permission over the asset, and the operation of the asset can only be done by the owner's authorization. In this way, modifying the contract content to destroy assets attributes or call others’ asset can be avoided. Besides, ruling out constraints of contracts is conducive to achieving cross-chain exchange of non-homogeneous assets. Therefore, the separation of assets and contracts proves to be a safer design. 

**Improved DPoS Consensus Mechanism**
[block:image]
{
  "images": [
    {
      "image": []
    }
  ]
}
[/block]
The consensus layer of Cocos-BCX TestNet adopts the DPoS consensus algorithm. 

DPoS algorithm infers the block producers and block generating time based on the scheduled witness and allocated time slot. Usually, the time slot interval is 5 seconds. In actual application, the interval is set to 3 seconds for faster broadcasting and larger throughput. If the scheduled witness arrives in the allocated time slot but there is no normal production due to network error or equipment failure, blocks will not be generated in that time slot. The network will wait till the next time slot and select the next scheduled witness to produce blocks. 

In Cocos-BCX, stakeholders elect all scheduled witnesses by voting. The scheduled witnesses are collectively referred to as active witnesses with a number from 11 to 101. They share the same scheduled block probability in the witness-scheduling algorithm in the DPoS consensus algorithm, which ensures that their block probabilities and rewards are consistent. Graphene voting is usually updated every 24 hours. In the initial stage, for the sake of security, stability and fairness, voting to the ​network of the project usually updated at a shorter interval, probably 12 hours or less.
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/a88b9b0-e05878e-_1.png",
        "e05878e-_1.png",
        868,
        334,
        "#aab9cb"
      ],
      "caption": "3-2-7 Comparison of Existing Consensus Mechanisms"
    }
  ]
}
[/block]
Following the principles of DPoS, CocosChain delegates witnesses and time slots to predict block producers and production time. The Aws of the main chain is always more than that of the forked chains. As a result, the block height of the main chain must be higher than the forked chains. Universal voting is also used to prevent the centralization of witnesses and to enhance network security. Above [Figure 3-2-7] shows the comparison between different witness mechanisms.

**Security Provided by Modern Cryptography**
Modern mathematics-based cryptography has been widely used to various industries of the Internet. Common symmetric cryptographic technology includes AES used in Wi-Fi, the asymmetric cryptography algorithms involve RSA (public and private key cryptography) and ECC. We use elliptic-curve cryptography (ECC) on our platform. Those algorithms create an encryption and decryption system that rejects decryption computation. Attempts to breach the encryption without keys are impractical because of the massive time (nearly hundred years) required.

ECC, fully named as elliptic curve cryptography, was proposed by Neal Koblitz and Victor Miller, respectively in 1985. 

**Low Forking Risk**
Under the Proof-of-Work (“PoW”) mechanism of Bitcoin and Ethereum, forking occurs when miners simultaneously mine two blocks. The shorter blockchain will be abandoned by the “longest chain rule” after 6 blocks. However, there will be two kinds of fork (soft and hard) if the miners do not follow the same mechanism. A soft fork is triggered by system upgrades and continues to exit until the upgrade finished. In the case that a group of miners on the same block main chain start take different consensus mechanism, a hard fork takes place and two separate blockchains are formed. “The DAO” is a famous case of hard forking of Ethereum in July 2016. When Ethereum forks into Ethereum and Ethereum classics, the computing power corresponding to the original main chain will be reduced, which will have a profound influence on the security of the entire main chain network.

To assure the safety and accuracy of game data, CocosChain uses DPoS consensus mechanism with no mining involved.  Risk of forking is low compared with PoW.  A fork may only take place when more than 1/3 of the witnesses disagree to the consensus.  Forking can also be prevented upon the removal of AWs by voting.

**Multi-Chain Interoperability**
The Platform will offer multi-chain interoperability in addition to cross-chain exchange gateway. For instance, Cocos-BCX will support the large storage of smart contracts and data on IPFS in the next phase of development.

**Merges of Multi-Operations to Ensure Atomicity**
Prop producing for blockchain games is atomic. The prop producers create props based on the demands, materials and assets submitted by the players. Upon completion, the props are transferred to the players. This process engages a series of operations (OP), including generation of digital assets, setting of prop properties, and transfer of asset ownership to users. To ensure the consistency in the operational results, we combine the operations into one transaction, that is, one atomic operation. In this case, all the operations inside the transaction will succeed or fail at the same time.
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/478f46a-d776974-_1.png",
        "d776974-_1.png",
        940,
        509,
        "#dbdde0"
      ],
      "caption": "3-2-8 Atomic Merges of Operations"
    }
  ]
}
[/block]
Another application of atomic combination is dis-intermediated assets exchange of Project BCX, aimed to help seller gain more and buyers consume less. The dis-intermediated circulation platform does not store data about users’ assets but acts​ as a medium for marrying node-to-node requests. Game manufacturers can flexibly design their own data structures for game assets. When users make a request for sale on the circulation platform, the related game assets (currency or props) shall be locked and cannot be used until the request is cancelled. The request contains the mainchain ID of the seller and the content of the assets to be sold. When the request is fulfilled, the system shall automatically change the assets ownership and transfer to the seller the assets that the buyer has paid. By then, the whole circulation request is completed. 

When asset exchange begins, the sale or purchase shall be submitted to the circulation platform in the form of a request. The transfer of assets and the change of ownership shall be deemed as a one-off indivisible operation. In other words, the behaviors of both sides shall be recognized by consensus. If the mainchain block doesn’t recognize one party’s change in assets, the whole transaction shall be rolled back. That is, the change of asset ownership or transfer of assets throughout the exchange shall be packed inside one transaction. The state of the two acts shall be consistent. When the transaction is completed normally, a unique transaction ID shall be available for checking on chain.
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/099cf1e-d95ac55-_1.png",
        "d95ac55-_1.png",
        939,
        277,
        "#dde5f1"
      ],
      "caption": "3-2-9 Determining State of Atomic Transaction"
    }
  ]
}
[/block]
##BCX Testnet: High-Performance Blockchain and High-Speed Contract Virtual Machine
Cocos-BCX is competent in concurrent task processing. 

For most of the current online games, when the user scale reaches a certain level, the server needs to process a large amount of data within a short time, which is impossible for the existing Ethereum network. 

Theoretically, the improved DPoS consensus of Cocos-BCX allows a throughput up to 100,000 TPS. Under a rational data management mode, the concurrent task processing is sufficient to support the development and normal running of existing games, meets the basic operation needs of large online games on the platform and secures game experience almost the same as that of the existing centralized games. 

Large online games mean significantly high frequency in data interaction, as evidenced by DNF’s record of 600,000 people online at the same time and Steam’s even more astonishing one of 14.2 million people. If every online user’s submission of data is regarded as an application for consensus, Cocos-BCX’s maximum throughput cannot support such a magnitude of request. Hence, the development team designs various delegation templates based on the speed of witness so that single delegates need not witness and process all the run-time games at the same time but focus on witnessing and counting multiple games of the same type. Besides, under the templates, the submission of data or witnesses of different games are asynchronous. Each game will select a suitable delegation template. Data under the asynchronous templates is validated through on-chain database service. That is, users validate, store and obtain data on chain. This process is efficient enough to support operation of player data for large games.
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/8d17143-a6252a2-_1.png",
        "a6252a2-_1.png",
        939,
        406,
        "#eeeeee"
      ],
      "caption": "3-2-10 Cocos-BCX Contract"
    }
  ]
}
[/block]
Contract is a segment of program that is executed automatically as well as a system participant that fulfills scheduled tasks according to the basic algorithms of the environment (compiler algorithms). Contract can define input and output, receive and store value and send out information and value. Smart contract is designed with the “trustless principle”. All nodes believe that each other is not trustable. Each node of blockchain, which features distributed storage, keeps the same contract execution code. The execution results are witnessed by the computing power of the whole network. Whether they are recognized is decided by voting by all. Cocos-BCX smart contract supports the definition of witness delegation. 

To ensure that the contract execution efficiency allows sound game experience for the users, Cocos-BCX comes up with a high-speed contract virtual machine scheme based on LUA for on-chain games. Different from existing rivals, the scheme features custom-made and optimized run-time environment and execution efficiency as well as language and API system that are the same as those of SDK, and interoperation interfaces for the chain and game execution environment. This addresses the monotony in environment and poor flexibility and customization of blockchain contracts. The use of smart contract has gone beyond description of currency to content directly related to the games, probably including basic algorithms, setting, unit, scene and even map. The improved virtual machine not only supports more complex and flexible contract forms but greatly improve the execution efficiency of smart contracts.


##Further Enhancement of the Distributed Ledger System for Blockchain Gaming

It’s mentioned that the final form of on-chain games is the complete on-chain implementation of overall game logic. But as current blockchain technology cannot satisfy the threshold of loading whole games, several key issues are to be resolved before game algorithms can be migrated on blockchains:
	The cost and volume for nodal data synchronization 
Smart contracts can only run on full nodes. And it is unpractical for the users to host nodes that require massive system resources, networking, and time to synchronize. 
	Algorithm codes exceeding the block size
Whole backend logic is required for the contract to implement complete game logic on blockchain. The sizes of algorithm smart contracts may be larger than system block size, especially when game logics are complicated. But with current blockchain technology, the contract that cannot be held by the blocks will never work and produce any result. 
	Continuous execution of smart contract 
Whole game logic running on blockchain means continuous execution of smart contract before end of the game. That is cross-block execution, and game algorithms may run continually at time durations beyond block intervals, which is not yet available with current blockchain technology. 
	Latency of transaction executions 
Whole game running on blockchain also means that all possible executions of the game are processed on blockchain, including high-speed response. Transaction response of traditional blockchain depends on the behavior of block generation with a time interval, and the fastest confirmation is also limited by block generation cycle, making it difficult to meet the need for game contracts to instantly respond to transactions. 
	Inaccessible to randomness consensus
On-chain randomness is described by open smart contract, and different node noise needs to be added to contract operation to produce random results that cannot be calculated by the third party. However, the noises from different nodes may vary.  That is, other nodes cannot execute the contract again to validate whether the randomness is correct, which ultimately leads to the failure in consensus.
	Feasibility of critical features such as on-chain timer and heartbeat  
Timer and heartbeat, along with their sync security requirements, are necessary to execute scheduled or conditioned smart contracts. No solution is available for these building blocks today. 
	Digital assets authority
Traditional blockchain digital assets are recorded in the contract data zone, and assets are inseparable from contracts. Therefore, contract owners may damage the interest of assets holders if they are authorized to modify digital assets data.

Accordingly, CocosChain proposes these preliminary designs and features that substantially improve the existing blockchains: 
	Reduced data volume and sync time on nodes; 
	Syntax support to compartmentalized consensus processing;
	Continual execution of smart contracts; 
	Minimum latency to event execution; 
	On-chain trusted randomness; 
	On-chain timer and heartbeat; 
	Authority added in non-homogeneous digital assets data structure. 


**Light Nodes**

In Cocos-BCX, light node is in nature an environment capable of interoperation with the chain. Different from full nodes, light nodes need not synchronize data to network but necessary contract information and environmental data. Such a design significantly reduces the amount of data and time for synchronization and allows actual capacity and feasible time cost for the on-chain game software.

The games developed by Cocos-BCX are basically contracts operated locally in the light nodes. In the contract, the consensus and non-consensus parts are identified and compartmentalized separately into one or more sub-contracts that are distributed to related nodes for consensus (for details, see the Syntax Support to Compartmentalized Consensus Processing). Such a design allows enormous game contracts to be executed efficiently without latency. Separate processing of consensus and non-consensus parts secures data reliability similar to that of traditional blockchains while offering possible best user experience. Meanwhile, validation for light nodes falls on execution environment and input data (validation of trusted execution environment) rather than process and outcome as in traditional blockchains, further enhancing the overall execution efficiency.

**Continual Execution of Smart Contracts**

The light nodes make it possible for whole games as contracts on chain. Game contracts can be executed in the light nodes continually over time, independent of the block period and block size but only related to game sub-contract with consensus.

Based on the syntax identifiers of priority of consensus, the game contracts and sub-contracts adopt asynchronous and synchronous consensus respectively to validate and synchronize key steps during continual execution. In this way, a mechanism is built for continual execution of game contracts and witness of consensus on results.

**Session**

There is an on-chain interface for session. It creates a user session list with active restriction in the public data zone. The users in the session interval have the rights to push transactions to other uses in the same interval. When other users receive the notice on data changes, they shall obtain corresponding data in time.

**Support consensus tasks at the syntax level**

Cocos-BCX proposes the design of syntax support to compartmentalized consensus processing for contracts. The consensus priority of script may be adorned with specific key words so that the contract interpreter can recognize the identified contracts in need of consensus and, when scanning the whole text, compartmentalize them into sub-contracts for consensus from related nodes in the chain network. The consensus priority includes, in an ascending order, no need for consensus, normal consensus, immediate response and immediate validation.

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/f682aac-fc1d209-_1.png",
        "fc1d209-_1.png",
        939,
        935,
        "#f2f3f4"
      ],
      "caption": "3-2-11 Light Nodes and Asynchronous Smart Contract Execution"
    }
  ]
}
[/block]
Whole contract is executed locally. To execute the parts in need of consensus, consensus methods are determined based on the syntax priority identifiers. Different priority calls for different steps of consensus. The execution of game contracts is smoother, with lower possibility of block waiting and, if any, shorter waiting. 

The execution and consensus of main contracts identified as immediate validation, the highest priority, are asynchronous. For those identified as an ​immediate response, when the transaction is submitted, the nodes shall immediately return a receipt for submission, that is, the hash value (Tx ID). Transactions identified as normal consensus shall be executed following the normal procedure in blockchain. Those identified as no need of consensus shall be executed on light nodes.

In addition, contracts in need of consensus are compartmentalized into sub-contracts that are then distributed for execution. These sub-contracts shall have complete context and a design without external dependence, so that other nodes can obtain the result correctly.

**Priority of Contract Consensus** 

Cocos-BCX deals with all transactions that need consensus in the game, including those require high-speed response and immediate confirmation. Transaction response of traditional blockchain depends on block production, and the fastest confirmation is also limited by block production cycle, making it difficult to meet the need for game contracts to instantly acknowledge transactions. 

	Rapid asynchronous validation of transactions
As illustrated in [Figure 3-2-12], the senior consensus tasks are marked up, extracted, and broadcasted to the nodes for execution. The block producers receive and pool the results from the nodes. When the number of results reaches a certain threshold, the block producers confirm these tasks and write them onto the block cache.
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/795e395-14a87a8-_1.png",
        "14a87a8-_1.png",
        940,
        1022,
        "#ecf1f3"
      ],
      "caption": "3-2-12 Concurrent Task Processing"
    }
  ]
}
[/block]
Therefore, the nodes will submit, process, and broadcast transactions immediately, and block generation and transaction execution become asynchronous for rapid asynchronous validation.

	Instant response
In the Cocos-BCX design, for a contract identified as instant response, when users send a transaction request to the nodes, the nodes shall immediately broadcast it to the network and return the hash value to the users. With the design, the final record period does not differ too much from the traditional design but the response to transaction is hardly delayed. The nodes shall submit transactions immediately, which greatly increase the speed of response. 

Moreover, the hash value shall inform the users of the state of transaction. Meanwhile, the information about transaction shall be updated to the transaction history datasheet and pushed dynamically to the users, who need not wait for the transaction to be validated and used in order to receive the callback for response. With reference to hash tracking in Ethereum, we have added the mechanism for dynamic push of transaction to users. 

**Minimum Transaction Latency**

Existing blockchains confirm task results after the nodes receive, execute, validate and record the data on the blocks. A task is pended upon submission and executed in the next block production cycle, resulting in system latency.

	Prioritized consensus
Cocos-BCX comes with a syntax priority identifier for transactions. When a transaction is identified as immediate validation, the nodes will submit, process and broadcast the transaction immediately. The block generation and transaction execution become asynchronous for rapid asynchronous validation. Immediate response is another consensus priority. With it, response to transaction is hardly delayed. The nodes will submit transactions immediately, which greatly increase the response speed. 

	Partitioned witness
To improve the node utilization rate and processing efficiency, Cocos-BCX proposes the design of partitioned witness based on delegate witness. That is, some nodes focus on processing specific types of contract requests. The design works as shown in [Figure 3-2-13].
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/9f63f3b-0f2e3cb-_1.png",
        "0f2e3cb-_1.png",
        939,
        416,
        "#f4f3f3"
      ],
      "caption": "3-2-13 Partitioned Consensus Design of Cocos Chain"
    }
  ]
}
[/block]
In the game industry, compartmentalized witness allows optimization of the processing capability of related nodes based on the type of request. For instance, for centralized requests for floating-point operation, the core hashing power should be strengthened; for centralized requests for data structure processing, the storage IO capability should be enhanced. In this way, the overall efficiency and benefit are optimized.

**Delegate-Type Transaction Mechanism**

Delegate-type transactions mainly cover the transactions that are highly random and generate different results when executed by different nodes (like generating a set of random numbers). However, this type is restricted to the transaction request related to non-personal data. With the consensus identifiers, names of node clusters (node groups) that engage delegates in consensus can be defined, specifying which type of nodes shall process the transaction. When only one node is needed (N=1), the designated node cluster shall randomly choose one online node within the cluster to process the transaction, for example, processing the random event. When there is more than one delegated node (N>1) or one cluster, several nodes within the designated cluster shall be distributed to process the transaction. When the delegates that pass trusted execution environment validation received the delegated transaction, they shall validate the feasibility of the transaction, execute delegation, and, upon completion, encrypt and pack the transaction result, finally broadcast it to the chain.

The design of defining the name of the delegated node cluster is adopted for two reasons. First, to ensure security, only the name of the delegated node is defined and nodes are chosen randomly from within the cluster to process transactions. The delegates do not know the specific delegated nodes, which prevents cheating. Second, to guarantee run-time reliability, the designated node cluster ensures that the transaction is distributed to the nodes that are online.

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/5b73190-931799b-_1.png",
        "931799b-_1.png",
        939,
        634,
        "#f6f5f6"
      ],
      "caption": "3-2-14 Delegate-type compartmentalized consensus"
    }
  ]
}
[/block]
**Implementation of On-Chain Trusted Random Process**

External randomness refers to that the uncertainty of the random process occurs outside the blockchain system, while internal randomness does the opposite. External randomness has no guarantee that the generation process of random factors can be trusted by the blockchain system. Therefore, to achieve rational randomness in the blockchain system is in fact to guarantee the credibility of the random process and results trustable. 

	The nodes practically finishing the execution of the random process shouldn’t be accessible to the scenarios and objects of the random information, to avoid cheating with this part of the information. 
	The random process should not be publicized on the blockchain before completion of its invocation business behaviors, hence to prevent the ongoing business from losing impartiality due to the publicity of randomness (Eg. The composition of each gamer’s card in a round of Landlords). 
	Internal randomness should be able to prevent BP/developers from cheating. 

At present, Cocos-BCX has successfully implemented trustable on-chain randomness, and it’s available for contract developers to call the randomness by the ​interface. Simply call the random function of the contract in a general development method and you’ll obtain the internal-source random data.
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/a1fd003-5d97807-_1.png",
        "5d97807-_1.png",
        940,
        200,
        "#f0f1f2"
      ],
      "caption": "3-2-15 On-Chain Trusted Random Process"
    }
  ]
}
[/block]
**On-Chain Trusted Random Process**

Whether game algorithms on blockchains have practical value is related to on-chain randomness. Research reveals that one key problem should be solved for complete on-chain randomness. The algorithms of on-chain randomness are described by smart contracts and the contract process is public. If random results that cannot be figured out by third parties are to be generated, there should be noises from nodes in the input into the process during contract execution. However, the noises from different nodes may vary. That is, other nodes cannot execute the contract again to validate whether the randomness is correct, leading to failure in consensus.

We have proposed three feasible solutions to address this problem.

Solution Ⅰ
	One or multiple random data pools are reserved in the dynamic data zone of blockchain. The block producers wrap the random results in the encrypted data segments of the block and release the closed-source codes of encryption. In this case, all the nodes shall have the same set of random data pools whose data is in pipe form with read and write sides and which are accessible to the read and write sides in line with the algorithms and features first-in-first-out. 

	Since transaction processing is consistent across all nodes in the blockchain, applications may read the random results from the random data pools during application. Under such a mechanism for generation and distribution, the security of process and result meets the requirement from the blockchain network: 

	Any access (read and write) shall cause irreversible changes to the random data pools. 
	Writing random data shall be completed by closed-source dynamic encryption library.
	Random data generators shall not know where the random results are placed in the random data pools and who shall use the random process. 

This solution is applicable to scenes where the chain network shows consistency in the order of transaction processing. For instance, in RPG games, players open the map loot box for random props. 

Solution Ⅱ
	A delegation mechanism allows some transactions to be delegated to some trustable node cluster for processing. The cluster allocates randomly online trustable nodes to execute the transactions. After execution, the trustable nodes shall record the random results. The client shall obtain the results via the informing or polling mechanism. 
	Since this solution is based on the chain transaction delegation mechanism, the changes to chain shall be smaller than those in Solution 1. However, to ensure the feasibility of solution, the following requirements shall be met: 

	The commissioned parties shall pass trusted execution environment validation to ensure their reliability. 
	When the delegates execute the randomness and release the results, the same safe encryption library shall be used. 
	For the transfer of encrypted data, zero-knowledge proof or other schemes shall be used to prove the identity of the delegates and shall be recognizable to the clients, so as to ensure that third parties do not forge the data obtained by the clients. 

This solution is applicable to transactions that engage multiple parties but need only one batch of results of randomness, like the order of shuffle in chess and card games.

Solution Ⅲ
	The current block producers receive random transactions, generate a result via the random function, encrypt the randomness and results, write them to the block data, pack it and send it to the whole network. Other ordinary nodes accept and use the result, reaching a consensus on the random transaction. 

This solution is applicable to lottery draws in games, like throwing the dice for a random result.

**Timer and Heartbeat**

Nearly all games and applications need online detection. For Cocos-BCX blockchain games, two concepts, namely, timer and heartbeat are put forward in response to user state detection and continual session. 
Time synchronization mechanism is the premise of a timer in the blockchain network. The traditional mechanism is built with external time signal or trust center. Under the trustless logic of blockchain, the external time signal and trust center both have defects that cannot be self-validated. Hence, on-chain time synchronization can only be completed on blockchain. 

The time synchronization solution of Cocos-BCX works as: With block timestamp, the block nodes broadcast equivalent time synchronization while releasing blocks. Each node completes time synchronization operations upon receiving the block broadcast. In the end, time synchronization to the whole network is completed once in one block synchronization period. 

With such a design, two-form timer technical support is provided:
	With block period as the minimal timing granularity, the timer works according to the scheduled timing goals. Without bias caused by factors like time zone, the block timestamp is deemed as the timing standard for the whole network. The timer can be executed normally in any network zone and time zone based on the same timing rules.
	Use the messaging mechanism similar to internal-source random process to submit the parameters required by the timer to random node by delegating, and the implementation layer of the node will execute the behaviors including initialization and expiration notice for the timer. 

Heartbeat is similar to the timer. Its time pulse also comes from the block timestamp. In one heartbeat period, nodes/ends submit information about their updated connection. Absence of such information in a period indicates that the nodes/ends are offline. The timer and heartbeat provide application basis for user state detection and future sessions. 

**Standardized Non-Homogeneous Assets**

Blockchain divides non-homogeneous digital assets data structure into fixed and extensible data zone, and the latter supports attribute extension of non-homogeneous digital assets, serving as a storage zone for specific game transaction data within the supported worldview, including zone data and data with combination relationship. Flexibly structured extensible data zone of non-homogeneous allows the extension of games or other business scenarios. As the game increases, zone data will gradually be added when assets transfer across different games, and thus affect the efficiency of chain operation. Meanwhile, asset authority has to be added to prevent malicious data from being written into the contract and causing redundant: 
	Assets owners have the right to delete but cannot modify certain zone data, which can reduce data redundancy while preventing cheating, such as custom enhanced props;
	Contracts can only modify zone data in charge. The contract reads all information of the NH assets’ extensible data, but the modification permission is limited to the zone of current data. For example, in blockchain games, the contract reads the relevant assets data of the games “HEROES OF THE STORM” and “World of Warcraft”, while the weapon “Frostmourne” of “HEROES OF THE STORM” won’t be truly cut off in “World of Warcraft”, but presents the status of “cut-off”.

**Design Tools for Established Rules**

It can be found in real game scenario that the user recognizes the open rules of some game, but loses assets after joining the game, because the developer changes the rules by temporarily rewriting the contract code before the game starts, or withdrawing the raised fund while no longer provide services to the users, which is beneficial to the developer himself but hurting the users. The established tools are just developed to prevent such phenomena. Game developers can use the “design tools for established rules” for blockchain-based games to design blockchain games to enhance user trust. This is realized by locking a certain amount of homogeneous assets using smart contract, and then set unlocking requirements, time and amount. Add to contract codes the utility functions that during the assets lockup, the codes of games are not allowed to be modified. The contract codes cannot be modified during the assets lockup, so the game will operate within the initial rules.

## Cheat-proof Transaction Verification Mechanism to Prevent BP/ Developers from Cheating
 
As the core node of transaction processing and communication across the network, BP has quicker access to the results than general nodes and thus higher priority in acquiring some timely or confidential information. This also indicates the possibility of cheating. For instance, the BP may be informed of the outcome of a random process in advance and utilize contract to predict the operation outcome, which is unfair to the games in the public chain and makes them unsafe. 

The developers herein refer to individuals and organizations that are capable of executing chain interaction or transformation, including low-level and contract developers in the chain network. They are able to analyze or control chain information in depth. There is some reason to believe that they can read codes to access the encrypted or concealed details of communication technologies that may be used in transmission and design codes accordingly to obtain the information of random process and sensitive data illegally.

Therefore, BCX comes with mechanisms for transaction execution, information transmission and operation that can prevent BP and developers from cheating, which will be described in this paper. 

**Dynamic Encryption Transmission**

To prevent sensitive information from being intercepted and deciphered during broadcasting, a safe mode of transmission with dynamic encryption is integrated into the BCX chain network, as demonstrated by [Figure 3-2-16].
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/19bee22-6f122ce-_1.png",
        "6f122ce-_1.png",
        939,
        530,
        "#f8f9fa"
      ],
      "caption": "3-2-16 Transmission with Dynamic Encryption"
    }
  ]
}
[/block]
Taking random seed as an example, when a random seed is produced, the producer will encrypt the information with the dynamic data concerning time, block height and other noise input as AES key and broadcast the encrypted information. All the nodes share the same algorithm for dynamic key generation that allows them to correctly decipher the information. The eavesdropping third parties, however, will not be able to do that, which guarantees the security of sensitive data during transmission.

**Prevent Custom Nodes from Accessing the Network**

Sound transmission security alone cannot prevent node developers from revising programs to output the information they have received and deciphered. Hence, a mechanism for authentication is incorporated to prevent the revised node program from connecting to the chain network, as shown by [Figure 3-2-17].

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/fa93233-0341def-_1.png",
        "0341def-_1.png",
        939,
        571,
        "#f9f9fa"
      ],
      "caption": "3-2-17 Node Access Verification Mechanism"
    }
  ]
}
[/block]
Before release, the BCK node program will be embedded with authentication information that is not included in the open source code yet related to the version number. When a node tries to connect to the chain network and other nodes, the latter will verify whether the information is consistent with that recorded in the chain network and refuse the connection of nodes that fail to pass authentication. In this way, malicious connection from revised node program to the chain network is stopped. Besides, secondary developers can also customize the authentication information in the source code to release their own chain network, which will also be able to prevent non-official code connection.

**Concealed Process Variables**

Since the contract itself is a Turing-complete state machine system, fixed input will derive fixed output and the results will be broadcast to the whole network for synchronization under the transaction mechanism. If the broadcast information is an intermediate process of a series of behaviors, some process variables that should not have been known may be revealed. To address this problem, a contract execution logic that conceals process variables is put forward, as shown by [Figure 3-2-18]. 

With a reasonable contract design, process variables that involve sensitive data are executed in the same OP, which is completed in the memory of the executing node. What is broadcast at the end is the OP result. In this way, the process variables are concealed throughout the period, with no risk of exposure.
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/aa604ef-27b0535-_1.png",
        "27b0535-_1.png",
        940,
        609,
        "#fafbfc"
      ],
      "caption": "3-2-18 Process Variable Concealing Mechanism"
    }
  ]
}
[/block]
**Contract Mechanism with Execution Authentication**

An execution authentication mechanism is added to prevent malicious developers from predicting the possible output of the contract via test use of contract interface. To be specific, only authorized accounts can execute specific contract interface, as shown by [Figure 3-2-19].
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/545ca92-b1cbe57-_1.png",
        "b1cbe57-_1.png",
        939,
        526,
        "#fafafa"
      ],
      "caption": "3-2-19 Contract Mechanism with Execution Authentication"
    }
  ]
}
[/block]
When the contract receives an ​execution request, the signature in the request shall be verified against the execution permission specified in the contract. Only when the request passes authentication shall the contract function be executed normally. Otherwise, the contract shall be directly terminated without returning the payment to the requestor. With this mechanism, even if the developers know the code of the chain and the contract and the process and principles of execution, they shall not be able to maliciously use specific interfaces. This guarantees that the contract shall not be used at will for prediction of execution outcome.

**Internal Trusted Environment for Execution of Sensitive Processes**

For information or operation that remains sensitive during a certain period of time (like a board game), this scheme allows execution logic within the period to work in a blackbox mode with protection from the Trusted Execution Environment (TEE) mechanism. Usually, the chain network challenges or verifies the blackbox environments on a regular basis via the TEE mechanism to ensure their reliability. Besides, any of them shall be chosen randomly for the execution of the sensitive processes. When the execution is completed, traceable records and outcome shall be submitted online to ensure fair, open and transparent recording on the chain network. It works as [Figure 3-2-20] shows.

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/8759b92-d349d17-_1.png",
        "d349d17-_1.png",
        939,
        323,
        "#f5f6f6"
      ],
      "caption": "3-2-20 Mechanism for Internal Execution of Sensitive Processes"
    }
  ]
}
[/block]
This mechanism prevents developers and BP from participating in the execution of the blackbox processes, thus avoiding their cheating. With the design specified above, COCOS-BCX shall offer a trusted, reliable and safe execution environment for all the businesses that it supports.