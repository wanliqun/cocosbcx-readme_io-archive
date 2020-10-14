---
title: "Technical Features"
slug: "technical-features"
hidden: false
createdAt: "2019-03-15T06:27:05.479Z"
updatedAt: "2019-03-16T17:43:29.430Z"
---
[block:api-header]
{
  "title": "On-Chain Trustable Randomness"
}
[/block]
Whether game algorithms on blockchains have practical value is related to on-chain randomness. Research reveals that one key problem should be solved for complete on-chain randomness. The algorithms of on-chain randomness are described by smart contracts and the contract process is public. If random results that cannot be figured out by third parties are to be generated, there should be noises from nodes in the input into the process during contract execution. However, the noises from different nodes may vary. That is, other nodes cannot execute the contract again to validate whether the randomness is correct, leading to failure in consensus.

**We propose three feasible solutions to address this problem. **

**Solution Ⅰ**:  One or multiple random data pools are reserved in the dynamic data zone of blockchain. The block producers wrap the random results in the encrypted data segments of the block and release the closed-source codes of encryption. In this case, all the nodes shall have the same set of random data pools whose data is in pipe form with read and write sides and which are accessible to the read and write sides in line with the algorithms and first-in first-out. 

Since transaction processing is consistent across all nodes in the blockchain, applications may read the random results from the random data pools during application. Under such a mechanism for generation and distribution, the security of process and result meets the requirement from the blockchain network:

•   Since transaction processing is consistent across all nodes in the blockchain, applications may read the result of randomness from the random data pools during application. Under such a mechanism for generation and distribution, the security of process and results meets the requirement from the blockchain network.  

•  Any access (read and write) shall cause irreversible changes to the random data pools. l

•  Writing random data shall be completed by closed-source dynamic encryption library.  

Random data generators shall not know where the random results are placed in the random data pools and who shall use the random process.  

This solution is applicable to scenes where the chain network shows consistency in the order of transaction processing. For instance, in RPG games, players open the map treasure chest for random items. 

**Solution Ⅱ**
A delegation mechanism allows some transactions to be delegated to some trustable node cluster for processing. The cluster allocates randomly online trustable nodes to execute the transactions. After execution, the trustable nodes shall record the random results. The client shall obtain the results via the informing or polling mechanism. 

Since this solution is based on the chain transaction delegation mechanism, the changes to chain shall be smaller than those in solution. However, to ensure the feasibility, the following requirements shall be met:  

•  The trustee shall pass trusted execution environment validation to ensure their reliability.

•  When the trustee execute the randomness and release the results, the same safe encryption library shall be used. For the transfer of encrypted data, zero-knowledge proof or other schemes shall be used to prove the identity of the delegates and shall be recognizable to the clients, so as to ensure that the data obtained by the clients are not forged by third parties.  

This solution is applicable to transactions that engage multiple parties but need only one batch of results of randomness, like the order of shuffle in chess and card games. 

**Solution Ⅲ**
The current block producers receive random transactions, generate a result via the random function, encrypt the randomness and results, write them to the block data, pack it and send it to the whole network. Other ordinary nodes accept and use the result, reaching a consensus on the random transaction.  This solution is applicable to lottery draws in games, like throwing the dice for a random result.
[block:api-header]
{
  "title": "Continual Execution of Smart Contract"
}
[/block]
The light nodes make it possible for whole games as contracts on chain. The local game contracts can be executed in the light nodes continually over time, independent of the block period and block size. The execution is only related to the sub-contracts that include consensus in the game contracts.
 
Based on the syntax identifiers of priority of consensus, the game contracts and sub-contracts adopt asynchronous and synchronous consensus respectively to validate and synchronize key steps during continual execution. In this way, a mechanism is built for continual execution of game contracts and witness of consensus on results.
[block:api-header]
{
  "title": "Smart Contract Session"
}
[/block]
here is an on-chain interface for session. It creates a user session list with active restriction in the public data zone. The users in the session interval have the power to push transactions to other uses in the same interval. When other users receive the notice on data changes, they shall obtain corresponding data in time.
[block:api-header]
{
  "title": "Priority of Smart Contract's Consensus"
}
[/block]
For traditional blockchain, transaction execution is validated by writing the results to block data when the nodes receive block data, interpret and run the transaction, and obtain the validation of results. When a transaction is submitted, it actually joins the pending queue. It will not be executed until the next block period. Such a mechanism prevents transactions from being responded to and processed in time.

**Prioritized consensus** 
 Cocos-BCX comes with a syntax priority identifier for transactions. When a transaction is identified as immediate validation, the nodes will submit, process and broadcast the transaction immediately. The block generation and transaction execution become asynchronous for rapid asynchronous validation. Immediate response is another consensus priority. With it, response to transaction is hardly delayed. The nodes will submit transactions immediately, which greatly increase the response speed.

**Compartmentalized witness**
To improve the node utilization rate and processing efficiency, Cocos-BCX proposes the design of compartmentalized witness based on delegate witness. That is, some nodes focus on processing specific types of contract requests. The design works as follows.
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/abcd5ae-14.png",
        "14.png",
        482,
        210,
        "#f4f3f3"
      ],
      "caption": "Compartmentalized Witness Mechanism"
    }
  ]
}
[/block]
In the game industry, compartmentalized witness allows optimization of the processing capability of related nodes based on the type of request. For instance, for centralized requests for floating-point operation, the core hashing power should be strengthened; for centralized requests for data structure processing, the storage IO capability should be enhanced. In this way, the overall efficiency and benefit are optimized.

**Low transaction latency**   
Cocos-BCX allows all the transactions in need of consensus to be processed on chain, including those identified as rapid response and immediate validation. The response to transactions on traditional blockchain depends on block production while the speed of validation is confined by the block period. These fail to meet the requirement from game contracts on immediate validation.

** Rapid asynchronous validation**  
Smart contract supports syntax consensus identifier. When the contract is executed, the transactions that are identified as immediate validation shall be elicited and broadcast immediately. Any nodes that receive the broadcast information shall immediately run the process to get the result and broadcast it. Meanwhile, the block producers in the period shall store the result into the result pool. When the quantity of the same result reaches the threshold for pass, the block producers shall broadcast the result of validation and write the transaction to block cache. The whole process is as follows.
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/a470d82-15.png",
        "15.png",
        482,
        463,
        "#eef1f4"
      ],
      "caption": "Data processing under asynchronous consensus"
    }
  ]
}
[/block]
Under such a design, the nodes will submit, process and broadcast the transaction immediately. The block generation and transaction execution become asynchronous for rapid asynchronous validation. 

**Immediate response** 
In the Cocos-BCX, for a contract identified as immediate response, when users send a transaction request to the nodes, the nodes shall immediately broadcast it to the network and return the hash value to the users. With the design, the final record period does not differ too much from the traditional design but the response to transaction is hardly delayed. The nodes shall submit transactions immediately, which greatly increase the speed of response. Moreover, the hash value shall inform the users of the state of transaction. Meanwhile, the information about transaction shall be updated to the transaction history datasheet and pushed dynamically to the users, who need not wait for the transaction to be validated and used in order to receive the callback for response. With reference to hash tracking in Ethereum, we have added the mechanism for dynamic push of transaction to users.
[block:api-header]
{
  "title": "Syntax Support To Compartmentalized Consensus Processing"
}
[/block]
Cocos-BCX proposes the design of syntax support to compartmentalized consensus processing for contracts. The consensus priority of script may be adorned with specific key words so that the contract interpreter can recognize the identified contracts in need of consensus and, when scanning the whole text, compartmentalize them into sub-contracts for consensus from related nodes in the chain network. The consensus priority includes, in an ascending order, no need for consensus, normal consensus, immediate response and immediate validation.
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/61ae3bc-16.png",
        "16.png",
        381,
        376,
        "#f3f3f4"
      ],
      "caption": "Light nodes and Principles of contract compartmentalization",
      "sizing": "smart"
    }
  ]
}
[/block]
Whole contract is executed locally. To execute the parts in need of consensus, consensus methods are determined based on the syntax priority identifiers. Different priority calls for different steps of consensus. The execution of game contracts is smoother, with lower possibility of block waiting and, if any, shorter waiting. The execution and consensus of main contracts identified as immediate validation, the highest priority, are asynchronous. For those identified as immediate response, when the transaction is submitted, the nodes shall immediately return a receipt for submission, that is, the hash value (Tx ID). Transactions identified as normal consensus shall be executed following the normal procedure in blockchain. Those identified as no need of consensus shall be executed on light nodes.    

In addition, contracts in need of consensus are compartmentalized into sub-contracts that are then distributed for execution. These sub-contracts shall have complete context and a design without external dependence, so that other nodes can obtain the result correctly. 
[block:api-header]
{
  "title": "Transaction Delegation Mechanism"
}
[/block]
Delegate-type transactions mainly cover the transactions that are highly random and generate different results when executed by different nodes (like generating a set of random numbers). However, this type is restricted to the transaction request related to non-personal data. With the consensus identifiers, names of node clusters (node groups) that engage delegates in consensus can be defined, specifying which type of nodes shall process the transaction. When only one node is needed (N=1), the designated node cluster shall randomly choose one online node within the cluster to process the transaction, for example, processing the random event. When there is more than one delegated node (N>1) or one cluster, several nodes within the designated cluster shall be distributed to process the transaction. When the delegates that pass trusted execution environment validation received the delegated transaction, they shall validate the feasibility of the transaction, execute delegation, and, upon completion, encrypt the transaction result and broadcast it to the chain.  

 The design of defining the name of the delegated node cluster is adopted for two reasons. First, to ensure security, only the name of the delegated node is defined and nodes are chosen randomly from within the cluster to process transactions. The delegates do not know the specific delegated nodes, which prevents cheating. Second, to guarantee run-time reliability, the designated node cluster ensures that the transaction is distributed to the nodes that are online.  Under this mechanism, the on-chain randomness becomes possible. Users can delegate trustable nodes to generate a random number and delegate trustable nodes to maintain public data of contract. Moreover, the developers shall set up function callback mechanism within the contract under the mechanism. 
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/ccf3714-17.png",
        "17.png",
        385,
        254,
        "#f6f5f6"
      ],
      "caption": "Compartmentalized consensus"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "Exchange of Digital Game Assets"
}
[/block]
Exchange of homogeneous digital assets  

The exchange of digital game assets and Ethereum ERC20 digital assets is as follows.
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/724e538-18.png",
        "18.png",
        1056,
        237,
        "#f5f5f5"
      ],
      "caption": "Exchange relationship between ERC20 digital assets"
    }
  ]
}
[/block]
Game currency supports transfer of assets via mapping gateway to other consortium chains and independent chains. 

Exchange of Non-Homogeneous Digital Assets 
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/24171ca-19.png",
        "19.png",
        1022,
        216,
        "#f3f3f3"
      ],
      "caption": "Exchange relationship between Cocos-BCX and ERC721 digital assets"
    }
  ]
}
[/block]
BCX-NHAS-1808 is the standard for non-homogeneous digital assets applicable to decentralized distributed ledger network in the use of COCOS tokens. Compatible with other standards for non-homogeneous assets, it allows separation between assets and contracts and features expandable and definable data zones. 

RC875 and ERC721 standards are protocols for non-homogeneous digital assets in Ethereum. To some extent, ERC875 standard is more like an upgraded version of a simplified ERC721 standard, which is the very first of its kind. ERC841 and ERC821 standards are its optimized and amended versions while ERC875 standard is simpler and more direct. Its defined functions include name, symbol, balanceOf, transfer, transferFrom, totalSupply, ownerOf and trade. Compared with ERC721 standard, ERC875 standard has simpler functions. 

 Further expanding the digital asset technologies supported by exchange gateway allows the gateway to support non-homogeneous complex contracts represented by ERC721 and ERC875 standards. The gateway is equivalent to a specific compiler in the exchange of game items and non-homogeneous contracts. By translating and exchanging structured data, it realizes two-way exchange between non-homogeneous contracts and on-chain game items. Compatible with more types of prop exchanges inside and outside the chains, it provides richer game content and user experience. 
[block:api-header]
{
  "title": "Atomic Merges of Operation"
}
[/block]
Prop producing for blockchain games is atomic. The prop producers create items based on the demands, materials and assets submitted by the players. Upon completion, the items are transferred to the players. This process engages a series of operations (OP), including generation of digital assets, setting of prop attributes, and transfer of asset ownership to users. To ensure the consistency in the operational results, we combine the operations into one transaction, that is, one atomic operation. In this case, all the operations inside the transaction will succeed or fail at the same time.
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/3ddcd63-21.png",
        "21.png",
        482,
        261,
        "#dbdddf"
      ],
      "caption": "Atomic merges of multi-operation"
    }
  ]
}
[/block]
Another application of atomicity is dis-intermediated assets exchange of Project BCX, aimed to help seller gain more and buyers consume less. The dis-intermediated circulation platform does not store data about users’ assets but act as a medium for marrying node-to-node requests. Game manufacturers can flexibly design their own data structures for game assets. The exchangeable content goes beyond homogeneous assets within games to cover items, equipment, game data and other non-homogeneous assets. When users make a request for sale on the circulation platform, the related game assets (currency or items) shall be locked and cannot be used until the request is cancelled. The request contains the mainchain ID of the seller and the content of the assets to be sold. When the request is fulfilled, the system shall automatically change the assets ownership and transfer to the seller the assets that the buyer has paid. By then, the whole circulation request is completed.    

When asset exchange begins, the sale or purchase shall be submitted to the circulation platform in the form of a request. The transfer of assets and the change of ownership shall be deemed as a one-off indivisible operation. In other words, the behaviors of both sides shall be recognized by consensus. If one party’s change in assets is not recognized by the mainchain block, the whole transaction shall be rolled back. That is, the change of asset ownership or transfer of assets throughout the exchange shall be packed inside one transaction. The state of the two acts shall be consistent. When the transaction is completed normally, a unique transaction ID shall be available for checking on chain. 
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/5080784-22.png",
        "22.png",
        482,
        142,
        "#dee5f0"
      ],
      "caption": "Determining state of atomic transaction"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "Cheating-Proof Transaction Authentication Mechanism"
}
[/block]
As the core node of transaction processing and communication across the network, BP has quicker access to the results than general nodes and thus higher priority in acquiring some timely or confidential information. This also indicates the possibility of cheating. For instance, the BP may be informed of the outcome of a random process in advance and utilize contract to predict the operation outcome, which is unfair to the games in the public chain and makes them unsafe.

The developers herein refer to individuals and organizations that are capable of chain interaction or transformation, including low-level and contract developers in the chain network. They are able to analyze or control chain information in depth. There is some reason to believe that they can read codes to access the encrypted or concealed details of communication technologies that may be used in transmission and design codes accordingly to obtain the information of random process and sensitive data illegally.

Therefore, BCX comes with mechanisms for transaction execution, information transmission and operation that can prevent BP and developers from cheating, which will be introduced in the following text. 

**Transmission with dynamic encryption**
To prevent sensitive information from being intercepted and deciphered during broadcasting, a safe mode of transmission with dynamic encryption is integrated into the BCX chain network, as demonstrated by the following figure. 
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/b67b8ae-23.png",
        "23.png",
        482,
        271,
        "#f8f9fa"
      ],
      "caption": "Transmission mechanism with dynamic encryption"
    }
  ]
}
[/block]
Take random seed as an example. When a random seed is produced, the producer will encrypt the information with the dynamic data concerning time, block height and other noise input as AES key and broadcast the encrypted information. All the nodes share the same algorithm for dynamic key generation that allows them to correctly decipher the information. The eavesdropping third parties, however, will not be able to do that, which guarantees the security of sensitive data during transmission.

**Prevention of connection from custom nodes**
Sound transmission security alone cannot prevent node developers from revising programs to output the information they have received and deciphered. Hence, a mechanism for authentication is incorporated to prevent the revised node program from connecting to the chain network, as shown in the following figure. 
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/07cc4d3-24.png",
        "24.png",
        482,
        293,
        "#f9f9fa"
      ],
      "caption": "Node access authentication mechanism"
    }
  ]
}
[/block]
Before release, the BCX node program will be embedded with authentication information that is not included in the open source code yet related to the version number. When a node tries to connect to the chain network and other nodes, the latter will verify whether the information is consistent with that recorded in the chain network and refuse the connection of nodes that fail to pass authentication. In this way, malicious connection from revised node program to the chain network is stopped. Besides, secondary developers can also customize the authentication information in the source code to release their own chain network, which will also be able to prevent non-official code connection.
[block:api-header]
{
  "title": "Concealed process variables"
}
[/block]
Since the contract itself is a Turing-complete state machine system, fixed input will derive fixed output and the results will be broadcast to the whole network for synchronization under the transaction mechanism. If the broadcast information is an intermediate process of a series of behaviors, some process variables that should not have been known may be revealed. To address this problem, a contract execution logic that conceals process variables is put forward, as shown in the following figure.
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/8f8d5be-25.png",
        "25.png",
        482,
        312,
        "#fafbfb"
      ],
      "caption": "Process variable concealing mechanism"
    }
  ]
}
[/block]
With a reasonable contract design, process variables that involve sensitive data are executed in the same OP, which is completed in the memory of the executing node. What is broadcast is then the OP outcome. In this way, the process variables are concealed throughout the period, with no risk of exposure.
[block:api-header]
{
  "title": "Contract mechanism with execution authentication"
}
[/block]
An execution authentication mechanism is added to prevent malicious developers from predicting the possible output of the contract via test use of contract interface. To be specific, only authorized accounts can execute specific contract interface, as shown in the following figure.
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/5e69308-26.png",
        "26.png",
        482,
        269,
        "#f9f9f9"
      ],
      "caption": "Contract mechanism with execution authentication"
    }
  ]
}
[/block]
When the contract receives execution request, the signature in the request shall be verified against the execution permission specified in the contract. Only when the request passes authentication shall the contract function be executed normally. Otherwise, the contract shall be directly terminated without returning the payment to the requestor. With this mechanism, even if the developers know the code of the chain and the contract and the process and principles of execution, they shall not be able to maliciously use specific interfaces. This guarantees that the contact shall not be used at will for prediction of execution outcome.
[block:api-header]
{
  "title": "Internal trusted environment for execution of sensitive processes"
}
[/block]
For information or operation that remains sensitive during a certain period of time (like a board game), this scheme allows execution logic within the period to work in a blackbox mode with protection from the Trusted Execution Environment (TEE) mechanism. Usually the chain network challenges or verifies the blackbox environments on a regular basis via the TEE mechanism to ensure their reliability. Besides, any of them shall be chosen randomly for the execution of the sensitive processes. When the execution is completed, traceable records and outcome shall be submitted online to ensure fair, open and transparent recording on the chain network. It works as follows.
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/18237e0-27.png",
        "27.png",
        482,
        165,
        "#f5f5f6"
      ],
      "caption": "Mechanism for internal execution of sensitive processes"
    }
  ]
}
[/block]
This mechanism prevents developers and BP from participating in the execution of the blackbox processes, thus avoiding their cheating. With the design specified above, COCOS-BCX shall offer a trusted, reliable and safe execution environment for all the businesses that it supports.