---
title: "3.1 Overall Design"
slug: "31-overall-design"
excerpt: "This chapter introduces you to the Cocos-BCX’s business and operation design, which can help you quickly understand the basic situation of the overall project."
hidden: false
createdAt: "2019-06-24T09:25:06.375Z"
updatedAt: "2019-06-24T09:28:29.568Z"
---
##Complete Wallet and Blockchain Explorer

Cocos-BCX provides digital asset wallets to a variety of operating platforms, such as Android, iOS and Windows, ensuring that mainstream users can participate in assets circulation. Users can store game digital assets and ERC20 tokens imported through the exchange gateway in the wallet, making it easier for the transactions of game coins on the circulation platform. On the other hand, Cocos-BCX ensures the security of the digital assets stored by the user in the wallet with the financial-level algorithm and KYC authentication.

Cocos-BCX wallet is embedded​ with a blockchain explorer for users to search for on-chain information recorded in each block. Each blockchain system has its own explorer. Cocos-BCX offers a complete blockchain explorer with search and jump functions, for example, when a rare prop asset is generated, relevant data will be recorded on the mainchain. Users may then find relevant transactions information in the blockchain explorer. Cocos-BCX blockchain explorer also supports users to check information of atomic operation. Assets distribution is more transparent on the blockchain explorer with all data recorded on chain, which is authentic and tamper-resistant.



##Iterative Smart Contract System

For contract systems represented by Ethereum, the smart contract can't be modified once released, which makes it difficult to meet the requirements of the game logic update and bug fixes. To solve these problems, we developed an iterative contract system.
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/d894a9c-d474ad5-_1.png",
        "d474ad5-_1.png",
        939,
        388,
        "#ecf2f4"
      ],
      "caption": "Iteration of Smart Contract"
    }
  ]
}
[/block]
The system allows authorized users to update the contract with the modified one after the developers release the defined contract on the blockchain. Although the old version still exists (to ensure openness and fairness), the on-chain address will be overwritten by the new contract data, and the references of multiple-contract application will be updated automatically.


##Worldview Statement

Most items are universal in current game system. In order to reduce repeated design, increase the efficiency of game development and make it more interesting, Cocos-BCX introduces the concept of worldview. Game assets and props with the same worldview are interoperable. The worldview of blockchain games is an identification used to distinguish between story settings and characters/items/rules settings and utility scope. Game items follow unified specification in the worldview, where the game assets and items with the same worldview can be migrated and circulated in different games under this worldview by paying the “migration fee”, which can be regarded as the “travelling​” of game props.

In Cocos-BCX, the worldview defines the application scenarios, circulation rules and registration for the NH assets, as well as the basic information of the worldview (worldview ID) and the symbol of circulative tokens.

Taking TYPE-MOON as an example, the worldview is unified. Therefore, the system will be updated once new games sharing this worldview.  Its works include:
	Tsukihime, the doujin game;
	Kara no Kyoukai, the novel;
	Fate/Stay Night；Fate/Stay Night, the first commercial game;
	Fan disc Fate/Hollow Ataraxia of Fate/Stay Night;
	Melty Blood series, the scenario-based fighting game.

The characters, items and plot settings in each work with the same worldview are universal, and it's common in the real world that game makers develop various works in the same worldview.

Cocos-BCX allows game developers to declare a worldview at the time of creation. In addition, the worldview is allowed to have its own governance committee (and consensus committee), which may further be allowed to have its independent blockchain environment in the future.



##Cross-World Item “Traveling”

Game assets and props under the same worldview are interoperable across different games. For example, the props of game B can be used in game A and game C as shown in Figure 3-4-1 below.
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/06b71d3-3bb45a4-_1.png",
        "3bb45a4-_1.png",
        708,
        794,
        "#f7f8fa"
      ],
      "caption": "Circulation of Game Items under the Same or Similar Worldview"
    }
  ]
}
[/block]
The game props following the unified rules in the worldview can be transferred across different games by paying migration fee, which is the "travelling​" of game props. Props are a non-homogeneous digital asset for blockchain-based games. The "travelling" of props is the process of applying the asset under the same worldview in different games. The modification to the asset by different games is stored in each game's zone data. The data of different games is independent of each other under the default setting, and only internal modification to zone data is allowed.
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/e8d974d-5f57c31-_1.png",
        "5f57c31-_1.png",
        940,
        542,
        "#a59f9c"
      ],
      "caption": "Examples of On-Chain Game Assets Migrating across Different Games under the Same Worldview"
    }
  ]
}
[/block]
##Smithy Mechanism

The Smithy is a series of accounts with the right to generate props and equipment, and a series of contracts. As one of the core functions of all games, the Smithy can be managed by game makers or by game guilds and designer studios. Players convert game coins and materials into props or purchase items directly in the Smithy. This open and transparent process endows props with uniqueness as other props, which can be retrieved and searched in the blockchain explorer.
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/7d24059-601ac4c-_2.png",
        "601ac4c-_2.png",
        940,
        500,
        "#fbfbfb"
      ],
      "caption": "The Smithy Forges Assets and Supports Assets Circulation"
    }
  ]
}
[/block]
The combination of props in the Smithy mechanism is an atomic operation to ensure the atomicity. All operations of the transaction will either succeed or fail simultaneously. The core of “player-the Smithy-player” consists of two parts, that is, the player submits materials to the Smithy, and the latter returns the finished props to the players, which together can be regarded as a complete transaction. The information of the two parts will be recorded on-chain to ensure that users’ asset transfer is true, reliable and tamper-resistant. In doing so, circulated materials, tokens and other digital assets released by players are free from being manipulated in the same way as that in a ​centralized game system, and data loss can also be prevented, thereby protecting the interest of the players.

The Smithy has the following features:
	It is a series of accounts with the right to generate props and equipment, and a series of contracts;
	It is where props can be generated independently of the game;
	Props generated here are unique;
	Props generation, attributes setting and ownership transfer to users are all combined into one atomic operation;
	It is managed by worldview management committee (game developer, player guilds and the union of designers)

Cocos-BCX empowers the Smithy with props generation right under the worldview. For example, Excalibur can be circulated across works in Arthur Legendary worldview or in TYPE MOON worldview, with the homogeneous asset under a unified worldview as the transfer standard.



##Nested Props Combination

Game props and equipment may be composed of multiple components and items. In Cocos-BCX, non-homogeneous digital assets of the blockchain game, i.e., props, can also be nested and contained.
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/2a7b51e-ec6ad7f-_1.png",
        "ec6ad7f-_1.png",
        940,
        861,
        "#f7f7f8"
      ],
      "caption": "Nested Props Combination"
    }
  ]
}
[/block]
Each prop may involve multiple items. The parent asset may contain one or more child assets, and child asset can have other child assets. For example, Nested props combination below, “Red Comet” in Figure consists of three sub-props, “Engine”, “Wheel” and “Weapon”, and the sub-props “Engine” and “Wheel” are respectively composed of other sub-props – “Fuel”, “Filter” and “Gear”, “Tire”.


##Props Circulation Platform

In Cocos-BCX, props transactions are mainly implemented by two functions:
The purchase of props is a multi-step atomic operation, where the props data of the user account is updated while paying the fee. If any action in the updating of the assets data is not recognized by the block of the mainchain, the entire transaction will be rolled back.

For the transfer of the props, the functions provided by Cocos-BCX do not directly change the ownership of specific assets, but send a request for assets transfer to the OTC asset circulation platform (centralized or decentralized). In principle, users can only operate (transfer or sell) on their own assets, which should not be controlled by any third party, such as the platform. The OTC asset circulation platform needs to record orderObject after the function is executed successfully. Or the getItems function is called before the request is sent to list user props for the ​user to select. It is essentially a peer-to-peer matching of the requests after the purchase request is received.

Unlike traditional game transaction platforms, there’s no intermediary on Cocos-BCX’s decentralized digital assets circulation platform, which improves transaction efficiency of both parties. On the other hand, fees go directly to sellers rather than the intermediary, allowing sellers to gain more benefits and buyers to consume less.
Players can make transfer and purchase of non-homogenous assets, such as game coins and in-game prop assets, on props circulation platform. The platform adopts a smart contract for the automatic matching of orders to provide a more efficient exchange service throughout the process of circulation.

The circulation platform will be connected with game data running on multiple platforms. With optimal compatibility and customization, game makers can flexibly and independently design their own on-chain game storage structure and connect game data to the circulation platform. Therefore, users can easily access the coins and prop assets of various games on the platform, providing strong support for asset circulation within the game.

After being authorized to log in to the platform, users may submit their game prop assets to the platform through orders. The purchase and sell orders that meet the requirements will be automatically matched by the system. The transaction covers both homogeneous and non-homogeneous assets, such as in-game currencies, props, equipment, and game data.

The order information will be written into blockchain upon release. The corresponding assets in the game will also be frozen at the same time.

A typical asset transaction process is shown as:

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/4388df3-18f525d-_1.png",
        "18f525d-_1.png",
        940,
        83,
        "#abc4e3"
      ],
      "caption": "Process of Digital Assets Circulation"
    }
  ]
}
[/block]
##An Example of Props Circulation Platform

The exchange platform supports the free transactions of COCOS, independently issued “game coins” (homogenous digital assets), and prop assets (non-homogeneous assets).  

The services provided by the exchange platform includes the exchange of COCOS for other game coins, and the exchanges of different game coins, the price of which is determined by their exchange rate against COCOS. The exchange platform can improve the game industry liquidity while providing a unified evaluation basis for the value of different game coins.

Game contents circulation on the platform mainly indicates the exchange and circulation among COCOS, game coins and props. As data of game items are highly customizable, the data of different game props may be possibly inconsistent, so that it requires the game makers to authorize and provide an analytic method for contents of the games to be connected to the circulation platform.

When users submit a transaction order on the content exchange platform, the related game assets (coins or props) will be locked and cannot be used. The order contains the account ID of the seller and the content of the assets to be sold. When the order is matched, the system will automatically transfer the ownership of the assets and release to the seller the fees paid by the buyer. In the process of the transaction, the transfer of digital assets between the two parties will be merged as an atomic operation, which is to pack the operations of the two parties into one transaction. The state of these actions is consistent. The normal completion of the transaction will result in a unique transaction ID that can be checked on the blockchain, as shown in the ​following figure:

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/76e8b58-2bb8d63-_1.png",
        "2bb8d63-_1.png",
        939,
        402,
        "#dfeaf7"
      ],
      "caption": "Process of Game Content Request/Match"
    }
  ]
}
[/block]
##Enhanced Permission System

**Specified Permission System and On-Chain Operations to Support more Business Segments**

Cocos-BCX’s design of separating the assets ownership from the right to use specifies existing permission system of the assets. The use right determines whether the user has the permission on most operations, while the ownership determines whether the user has the actual ownership and key rights to operate the assets. Certain operations are required to be co-signed by the owner and user.
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/5a68311-e723f2f-_1.png",
        "e723f2f-_1.png",
        854,
        496,
        "#f9f9f9"
      ],
      "caption": "Separation of Assets Ownership and Use Right"
    }
  ]
}
[/block]
With specified operations, Cocos-BCX provides operations that can be called by the contract. The operations can support the transfer of ownership and use right, and enable the creation of a timed task. The operations of creating a timed task can specify the tasks to be executed upon expiration (if one contract function is called).
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/74f174e-e8a7175-_1.png",
        "e8a7175-_1.png",
        940,
        523,
        "#f1f2f2"
      ],
      "caption": "Specified On-Chain Operations"
    }
  ]
}
[/block]
**Implementation of New Business Models by Contract and OP**

Improved Cocos-BCX chain adds a variety of atomic operations and data structures for possible new-type business. Based on BCX contract system, developers can easily deliver the business logic​ unable to be implemented with traditional blockchain/contract system, such as asset leasing, mortgages and pledges.

  *  Lease

The functions for each process of the leasing business are defined in the smart contract. When the lease agreement is reached, the contract functions implement the behaviors including paying rents and transferring the permissions by combining the ownership change OP and the general transaction OP. The blockchain-based timed task OP defines business activities such as reclaiming the use right upon expiration.
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/5c9c74f-040a1d3-_1.png",
        "040a1d3-_1.png",
        939,
        160,
        "#f5f5f6"
      ],
      "caption": "Process of Assets Lease"
    }
  ]
}
[/block]
  *  Pledge

The functions for each process of the pledge business are defined in the smart contract. When a pledge occurred, the contract functions implement the behaviors including paying the pledge and transferring the permissions by combining the ownership change OP and the general transaction OP. The blockchain-based timed task OP defines business activities such as reclaiming the use right upon expiration or returning ownership in the case of redemption during pledge.
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/c48ecf2-3301fec-_1.png",
        "3301fec-_1.png",
        939,
        259,
        "#f6f6f7"
      ],
      "caption": "Process of Assets Pledge"
    }
  ]
}
[/block]
  * Pawn

The functions for each process of the pawn business are defined in the smart contract. When a pawn agreement is reached, the contract functions will implement the behaviors including paying the pawn fee and transferring the permissions by combining the ownership change OP and the general transaction OP. The blockchain-based timed task OP defines business activities such as reclaiming the use right upon expiration or returning use right in the case of redemption during pawn.
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/717573f-28a267c-_1.png",
        "28a267c-_1.png",
        940,
        293,
        "#f7f7f7"
      ],
      "caption": "Process of Assets Pawn"
    }
  ]
}
[/block]
##Player Autonomy and Assets Security

Cocos-BCX’s node toolkit will be open sourced, where game developers, operators, player guilds and designer studios can be nodes and participate in the election of council nodes.

Due to the openness and transparency of the blockchain network, in-game digital assets information is accessible to everyone through the blockchain explorer. Since the accounts with high-value non-homogeneous assets in the games tend to be the preferred target for hackers, Cocos-BCX attaches great importance to the security of the player account, and provides the following security mechanisms:

	Operation permission
The ownership and disposal right of in-game props are solely owned by the player, therefore the operation to destroy any item shall be handled or permitted by the player himself;
	Atomization of key operations
When an order to exchange or create an asset is submitted to the platform or the Smithy, all operations in the process are considered as an indivisible atomic transaction. This means that ​participation in these processes can only be approved by consensus. If any of the operations are not recognized by the blockchain network, the entire operation will be rolled back to avoid any abnormal transaction.
	Scalable multi-step verification
In addition to the blockchain transaction verification password, the game maker also provides password authenticator and random code verification to further improve the security of player’s assets.


##Visualized Smart Contract Editor

Cocos-BCX provides a visualized contract editor for developers to edit smart contracts, which is simplified from a user-friendly point of view. The editor graphically presents the functions and methods commonly used in the contract to the user, allowing users who do not have the ability to write scripts to easily compile a contract as needed while advanced features are available for programmers with proficiency in script languages.

Visualized editor is an editing tool that assists developers in rapid development with graphical interfaces. Taking Click Wizar as an example, the software efficiently displays most of the common methods on the toolbar, which enables developers to compile and insert the script code in an interactive environment by simply clicking, dragging and filling in the parameters.