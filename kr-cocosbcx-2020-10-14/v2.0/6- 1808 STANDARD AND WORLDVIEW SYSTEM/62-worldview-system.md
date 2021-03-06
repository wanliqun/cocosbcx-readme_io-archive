---
title: "6.2 Worldview System"
slug: "62-worldview-system"
hidden: false
createdAt: "2019-06-25T08:41:59.900Z"
updatedAt: "2019-06-25T08:42:04.667Z"
---
##Game World and the Worldview System

Different from the concept of the traditional game industry, BCX's blockchain games are not completely independent business scenarios. Each blockchain​ game can be considered a game world, and several game worlds with similar basic settings can be considered to have a common worldview.
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/9b2d420-777d2f0-3.png",
        "777d2f0-3.png",
        187,
        209,
        "#f7f8fa"
      ],
      "caption": "Game items under the same worldview used in different game worlds"
    }
  ]
}
[/block]
The concept of worldview is not created by blockchain gaming, but a feature already shared by many modern games. For example, Warcraft, World of Warcraft, Hearthstone, and The Legend of Storm share a common worldview of Blizzard universe, in which a considerable part of game props, characters, and assets are common. Although these assets have a different explanation on specific attributes, skills, etc. in each game, the design of these assets stems from the common basic rules.

The worldview of blockchain games is an identity that distinguishes between story settings and characters/items/rules settings and utility scope. Game items follow a unified specification in the worldview, and can be migrated and circulated in different game worlds under this worldview by paying the “migration fee”, which is the “travelling” of game props.


##Cross-World Item “Traveling”, Multiverse and Parallel World

Game items are a kind of non-homogeneous digital assets used in blockchain games. The process of items “travelling” across different worlds is that of applying and changing of a non-homogeneous digital asset in different games and services under the same worldview.

The 1808 standard makes it possible for on-chain games to design the multiverse/parallel universe. Different game worldviews are also different game universes, which forms the multiverse of on-chain games. The game items in each universe can be freely circulated, and are written with different attributes, skills, etc. in different games. These items do not affect each other. This is what we mentioned as the item design in the "parallel world".

Scalable custom data enables game designers to create unique game assets. Non-interfering zone data allows game assets to be given new properties that are an immune while "travelling" the world and the universe, while also making it possible of data linkage between games (such as skill gain/reduction). The image below is an example of the on-chain game assets travelling​ across the world line/parallel world:
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/ad01ddc-8643642-4.png",
        "8643642-4.png",
        482,
        278,
        "#a49f9c"
      ],
      "caption": "Example of on-chain game assets traveling across the world line"
    }
  ]
}
[/block]
According to the game operation design, the 1808 non-homogeneous assets standard support the design of paid travelling across the world line through a specific third-party. This is helpful for game operation to meet the needs of item balance and asset circulation control. It boasts the following features:

**Data management in the worldview system**

1808 non-homogeneous digital asset standard is defined on chain initially and operated via smart contract. The complicated data structure and combination design of the 1808 standard makes the design of asset data security more important. Therefore, COCOS-BCX analyzes the risks and potential dangers that may occur during the operation of data on chain, and starts to make improvement.

**Separately stored assets and contract data**

Separate data storage can ensure that the asset owner has full ownership of the asset. If the contract and the asset data are stored together, the specific contract can call the assets owned by the contract under the authority of the contract developer, which is very unsafe. In COCOS-BCX, the data of homogeneous, non-homogeneous assets and smart contracts are stored separately, which is a more data-safe design, in addition to helping to reduce data flow consumption and improve blockchain efficiency.

**Contract verification mechanism with identity authentication**

For contract functions involving sensitive operations, COCOS-BCX allows developers to define contract execution mechanisms with identity authentication. A contract function with authentication mechanism will only be executed when the caller meets the requirements, avoiding the risk of hackers maliciously executing a specific contract interface for illegal asset operations.

**Control contract permissions by zone data**

The contract is able to obtain all zone data in the 1808 standard extended asset data, but changes to the asset data will be limited to the zone marked as current contract. That is, Game A can obtain the attribute data of the asset in Game B, but the changes to the asset will only be saved in zone A, and contract A cannot modify any data in zone B.

**Asset owner management mode for zone data**

The zone data is continuously supplemented with the growth of games. The excessively added zone data or the invalid zone data added by the ​malicious contract will affect the execution efficiency of the business, resulting in asset data redundancy. To avoid this situation, the 1808 standard allows the user to delete a specific zone in the extended asset data. However, this only gives the user the right to delete the zone data without including the right to change the zone data, in case the user cheats by changing the data.