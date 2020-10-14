---
title: "Overall Design Concept"
slug: "overall-design-concept"
hidden: false
createdAt: "2019-03-15T06:26:36.940Z"
updatedAt: "2019-04-04T07:07:06.420Z"
---
This section introduces Cocos-BCX project’s business model and operation design, which will help you get a quick start with the basic information of the whole project. 
[block:api-header]
{
  "title": "Wallet And Blockchain Explorer"
}
[/block]
Cocos-BCX provides digital assets wallet for multi-systems, such as Android, iOS and Windows, and ensures mainstream users to fully participate in assets transfer. Digital assets wallets store game digital assets and ERC20, which is imported by the exchange gateway, and facilitate the purchasing and token transfers on the platforms. On the other hand, Cocos-BCX conducts financial-level algorithm cryptography on digital assets, and guarantees the safety of assets through KYC authentication. 

Cocos-BCX wallet in imbedded with a blockchain explorer to help search for on-chain information, and thus content recorded on each block will be searchable. Each blockchain system has its own explorer. Cocos-BCX offers a complete blockchain explorer with search and jump functions, for example, when a rare prop asset is generated, relevant data will emerge on the mainchain and thus users can search for transactions and related information. Cocos-BCX blockchain explorer also supports atomic search. Assets distribution is more transparent on the blockchain explorer, and on-chain recorded data is authentic and tamper-resistant.
[block:api-header]
{
  "title": "Iterative Smart Contract System"
}
[/block]
For contract systems represented by Ethereum, the smart contract can't be modified once defined and released, which makes it difficult to meet the requirements of on-chain game logic update and bug fixes. To solve these problems, we developed interoperable smart contract.
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/255baeb-2.png",
        "2.png",
        482,
        199,
        "#eef2f4"
      ],
      "caption": "Iterative updates of smart contract"
    }
  ]
}
[/block]
The system allows authorized users to update the contract based on the modified contract after contract developers release defined contract to the chain network. Although the original contract still exist (to ensure openness and fairness), the on-chain address will be overwritten by the new contract data, and referential relationship of multiple-contract application will be updated automatically.
[block:api-header]
{
  "title": "Game Worldview"
}
[/block]
The worldview of blockchain game is an identification to distinguish plot setting, roles, props, rules and applicability. 

 Different from the concepts in traditional gaming industry, blockchain games in Cocos-BCX are not completely independent transactions, i.e., one game one world. A batch of game worlds with similar basic settings are associated based on certain communication and linkage modes. These game worlds are considered to share a common worldwide.

The concept of worldview is not initiated in blockchain games, but shared by many games in  the modern gaming industry. For example, Warcraft, World of Warcraft, Hearthstone, and Legend of the Storm adopt blizzard universes worldview, and some props, roles and assets are transferrable across these games. Despite different attributes and skills in respective games, these assets are designed based on common rules.

Blockchain gaming worldview is an identification to distinguish plot setting, roles, props, rules and applicability. Following a unified norm, props are transferrable across different games by paying the costs of “migration”, that is, “migration” of game props. 

Cocos-BCX allows game developers to declare worldview in creation with its own governance committee (and consensus committee). In the future, worldview will be allowed to have independent chain environment.
[block:api-header]
{
  "title": "Game Props \"Cross\" Worlds"
}
[/block]
Game assets and props under the same worldview can be circulated across different games. For example, props of game B in the figure below can be used in game A and game C.
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/363f5d3-3.png",
        "3.png",
        187,
        209,
        "#f7f8fa"
      ],
      "caption": "Circulation of game game items under the same or similar worldview is supported"
    }
  ]
}
[/block]
Game props follow unified norms in the worldview,  and they are transferrable across different games by paying migration fee, which is the "crossing" of game props. Props are non-homogeneous digital assets for blockchain-based games, and props "crossing" means the transfer process of assets under the same worldview. The modification of assets in different games is stored as separate zone data. Data of the games is independent from each other under default setting, and only internal modification of zone data is allowed.
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/0914343-4.png",
        "4.png",
        482,
        278,
        "#a49f9c"
      ],
      "caption": "Examples of on-chain game assets migrating across different games under the same worldview"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "The Smithy"
}
[/block]
The Smithy is a series of accounts with props, equipment and a series of contracts. As one of the core functions of all the games, the Smithy can be managed by game developers, game guilds and designer studios. Through the Smithy, players convert tokens and materials into props or purchase props directly. This open and transparent process endows props with uniqueness like other props, and props can be retrieved and searched by the blockchain explorer. 
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/2f23b67-5.png",
        "5.png",
        482,
        257,
        "#fbfbfb"
      ],
      "caption": "The Smithy forge assets and supports assets circulation"
    }
  ]
}
[/block]
The Smithy combines multiple props to ensure atomic operation, and thus transactions succeed or fail synchronously. The core of “player-the Smiths-player” consists of two parts, that is, players submit materials to the Smithy, and the latter returns completed props, and is regarded as a complete transaction. Information is recorded on-chain to guarantee true, reliable and tamper-resistant assets transfer. In doing so, circulated materials, tokens and other digital assets released by players as well as data loss can be prevented from being manipulated like what have been done in centralized game system, and thus the interest of players can thus be protected.

The Smithy has the following features:

• Accounts with props and equipment production right and a set of contracts

• Independent of game prop output

• Uniqueness  of the Props 

• Atomically operate the generation, attributes setting of props and transfer prop ownership to users
• Managed by worldview management committee (game developer, player guilds and the union of designers)  

Cocos-BCX empowers the Smiths with prop output right under the worldview. For example, Excalibur transfers across Arthur Legendary and TYPE MOON, and uses homogeneous assets under a unified worldview as transfer standard.
[block:api-header]
{
  "title": "Nested Props Combination"
}
[/block]
Game props and equipment may consist of multiple components and items. For Cocos-BCX, non-homogeneous digital assets, i.e., props, in blockchain gaming also feature being nested.
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/374f627-6.png",
        "6.png",
        240,
        220,
        "#f7f7f8"
      ],
      "caption": "Props Nesting"
    }
  ]
}
[/block]
A prop may involve multiple props, parent asset may contain one or more child assets, and child asset can have other child assets. For example, Red Comet is composed of three child props, i.e., engine, wheel and weapon, and child props - Engine and Wheel consist of other child props - Fuel, Filter and Gear and Tire.
[block:api-header]
{
  "title": "Props And Assets Circulation Platform"
}
[/block]
In Cocos-BCX, props transactions are mainly achieved by two functions. 

Prop purchase is an atomic operation consisting of multiple steps, and updates prop data of user account while paying the fee. If the blocks of the mainchain reject any behaviors, the entire transaction will be rolled back. 

For props sales, functions provided by Cocos-BCX do not directly change the ownership of specific assets, but instead initiates a request for assets transfer to the OTC asset circulation platform (central or decentralized). Theoretically, users can only operate on their own assets, and should not be controlled by any third party, such as actual assets custody by the platform and escrow transfer. OTC asset circulation platform needs to record orderObject after the function is executed successfully. Or, OTC calls getItems function and list user prop so that user can choose to transfer. A purchase arrival request means point-to-point request. 

Unlike traditional game trading platforms, Cocos-BCX’s decentralized digital assets distribution platform does not have an intermediary. On one hand, it improves circulation efficiency of both parties. On the other hand, fees go directly to sellers rather than the intermediary, and thus achieving  growing profits gained by sellers and reduced consumption of buyers.

Players can complete transfer and purchase of non-homogenous assets, such as game tokens and in-game prop assets on prop circulation platform. During the process, the platform automatically adopts a smart contract to provide efficient transfer service.

The circulation platform will connect multi-system data in games. With an optimal compatibility and customization, game developers flexibly and independently structure on-chain game storage and connect game data to the circulation platform. Therefore, users will find it convenient to search for tokens and prop assets of multiple games.

After being authorized to log in the platform, users can request to submit game prop assets to the platform. Purchase and transfer requests that meet the requirements will be automatically matched by the system. The content includes both homogeneous and non-homogeneous assets, such as in-game currencies, props, equipment, and game data.

Request information will be written on-chain after releasing requests, and meanwhile, corresponding in-game assets will be frozen. 

A typical asset circulation process is shown below: 
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/12510cb-7.png",
        "7.png",
        482,
        35,
        "#d6d6d6"
      ],
      "caption": "Process of digital assets circulation"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "Player Autonomy And Assets Safety"
}
[/block]
Open node toolkit, game developers, operators, player guilds, designer studios and etc. of Cocos-BCX can be nodes and participate in the election of council nodes.

Blockchain network is open and transparent, and thus in-game digital assets information is accessible to everyone through the blockchain explorer. Since highly valuable accounts with non-homogeneous assets in the games tend to be the top priority for hackers, Cocos-BCX greatly emphasizes asset security of player account, and thus provides the following security mechanisms: 

• Operation permission
The ownership and disposition of in-game props are only possessed by the player, and so is item destruction.

• Atomized key operations 
When requests for assets circulation and creation are submitted to the platform or the Smiths, all the operations in the process are considered as atomic transactions. That is to say, participation can only be approved under consensus. If any operations are not recognized by the chain network, the entire operation will be rolled back to avoid any abnormal transaction.

• Extensible multi-step verification 
In addition to providing blockchain transaction verification password, game manufacturers also provide confirmation password and random code verification to further enhance assets security. 
[block:api-header]
{
  "title": "About Distributed Ledger System"
}
[/block]
We have mentioned that the ultimate form of on-chain games is key game algorithms on blockchains. Yet, the existing blockchain technology still lacks critical features to carry the complete logic of games, which includes:

**Volume and time cost of synchronizing node data**  
Contracts can only be executed by a complete node, which stores large amount of data (all the transaction data) in the whole network, and is time-consuming to establish another node to synchronize the data.

**Game algorithms on blockchain support large contracts**
 To achieve on-chain game algorithms, contracts need to incorporate all the ManageBean and thus become very large and even exceed the general size of a block. However, the current blockchain technology cannot operate contracts that are too large to hold and give computational results. 
Continuously executable contract  Game algorithms on blockchain mean that game contract continuously execute before any application ends. That is to say, the operating time of cross-block game contract is far longer than block generation period. However, the existing blockchain technology cannot support this contract operation mode. 
Low latency  Game algorithms on blockchain mean that all possible transactions are executed on chain, including transactions in need of quick response. Traditional response to blockchain transactions is determined by block generation, and the fastest speed of confirmation is also limited by block generation cycle. Therefore, it is difficult to meet the demand for instant response to a game contract. 

**Randomness cannot reach consensus**  
On-chain randomness is described by open smart contract, and node noise is required to operate contracts if random results that cannot be estimated by the third party are needed. Yet, noises of different nodes cannot be the same. That is to say, other nodes cannot verify whether randomness is right through operating the contract again, leading to failure of consensus.

**On-chain timer and heartbeat**  
Timer and heartbeat mechanisms are prerequisites for all the on-chain contracts, game content to achieve scheduled, automatic operation under certain conditions. This feature also implies time synchronization and synchronized security, a completely blank area for Blockchain technology
Digital assets permission  Traditional blockchain digital assets are recorded in the contract data area, while assets and contract being inseparable. Therefore, the modification of digital assets data may cause losses to assets owners. 

In response to these problems, Cocos-BCX proposes further development of the existing distributed ledger system, and develops the following features and mechanism, in order to achieve the implementation of on-chain games:

• Reduced data volume and time cost

• Syntax support to consensus processing

• Contracts continually executable across blocks

• Low latency

• On-chain trustable randomness

• On-chain timer and keep-alive

• Permission added to non-homogeneous digital assets structure