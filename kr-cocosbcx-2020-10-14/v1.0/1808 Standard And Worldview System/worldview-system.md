---
title: "Worldview System"
slug: "worldview-system"
hidden: false
createdAt: "2019-03-15T06:31:24.917Z"
updatedAt: "2019-03-18T03:15:19.367Z"
---
**Game world and worldview system**

Different from the concepts in traditional gaming industry, blockchain games in Cocos-BCX are not completely independent transactions, i.e., one game one world. A batch of game worlds with similar basic settings associated is considered to share a common worldwide.
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/227bce9-33.png",
        "33.png",
        340,
        381,
        "#f7f8fa"
      ],
      "caption": "Worldview items used in different game worlds"
    }
  ]
}
[/block]
The concept of worldview is not initiated in blockchain games, but shared by many games in modern gaming industry. For example, Warcraft, World of Warcraft, Hearthstone, and Legend of the Storm adopt blizzard universes worldview, and some items, roles and assets are transferable across these games. Despite different attributes and skills in respective games, these assets are designed based on common rules.  

Blockchain gaming worldview is an identification to distinguish plot setting, roles, items, rules and applicability. Following a unified norm, items are transferable across different games through paying the costs of “migration”, that is, “Crossing” of game items.

**Crossing worlds, multiverse and parallel worlds**

Game items are non-homogeneous digital assets used on blockchain gaming, while the migration of items across worlds refers to the application and change of non-homogeneous digital assets in different games and transactions under the same worldview. 

 1808 standard non-homogeneous assets provide possibilities of designing multiple universes or parallel universes for on-chain games. Different game worldviews, also different game universes, consists of multiple universes for on-chain games. Game items are transferrable across those universes while embodying various attributes and skills. They co-exist in a harmonious way without interference. That is the design of items in "Parallel World".

Extensible customized data enables game developers to create distinctive game assets. Isolated zone data empowers game assets to transfer across worlds and universe with brand-new attributes, and meanwhile makes data linkage possible, such as skill strengthening and weakening. The following is an example of on-chain game assets crossing worlds/ parallel worlds: 
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/a1ce2c7-34.png",
        "34.png",
        482,
        279,
        "#a49f9c"
      ],
      "caption": "Design example of items crossing worlds"
    }
  ]
}
[/block]
According to the design of game operation, BCX-NHAS-1808 sustains paid transfer of appointed third party across worlds. This mechanism contributes to improved item balance and control of asset circulation of game operation.

**Data management in worldview system**

BCX-NHAS-1808 initiates definition and operates through smart contract on chain. Since 1808 standard contains relatively complex data structure and portfolio, the security of asset data under worldview system grow more important. Cocos-BCX analyzes potential risks in on-chain data operation, and comes up with repair and improvement.

**Separation of assets and other data**

Separately stored data ensures the ownership of assets owners, while merged storage of contract and assets is insecure, because specific contract can call other assets with the authority of contract developer. In Cocos-BCX, (non-) homogeneous assets and data of smart contract are separately stored, which are conducive to reducing the consumption of data transfer and enhancing chain efficiency in a safer way.

**Contract execution authentication mechanism with identity verification**

For contract functions involving sensitive operations, Cocos-BCX allows developers to define contract execution mechanisms with identity authentication. Therefore, contract functions with validation will only be executed by qualified caller, and avoid malicious execution of specific contracts through illegal interface performance.

**Zone control over contract authority**

All the zone data of 1808 standard extended data can be acquired by contracts, while the modification to assets data is confined to the zone of the existing contract. That is to say, attribute data of assets in game A is transparent in game B, but the modified assets will only be stored in zone A and meanwhile contract A cannot modify any data in zone B.

**Management mode of assets owners apply to zone data**

Zone data is accumulated with the increase of games, while excessive zone data or malicious contract with invalid zone data impairs the efficiency of transactions, causing redundancy of user asset data. Under the circumstances, 1808 standard allows users to delete rather than modify specific zone of extended asset data to avoid cheating.