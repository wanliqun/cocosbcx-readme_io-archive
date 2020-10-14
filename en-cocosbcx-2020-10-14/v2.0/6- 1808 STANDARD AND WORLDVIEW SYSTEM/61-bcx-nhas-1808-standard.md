---
title: "6.1 BCX-NHAS-1808 Standard"
slug: "61-bcx-nhas-1808-standard"
excerpt: "This chapter focuses on the definition of BCX-NHAS-1808, the non-homogeneous digital assets standard, proposed after reviewing a number of existing non-homogeneous digital asset standards and combining with the needs of game industry. The standard is used to standardize all non-homogeneous digital assets that will be released and distributed on the BCX chain."
hidden: false
createdAt: "2019-06-25T08:37:28.423Z"
updatedAt: "2019-08-12T03:13:01.258Z"
---
##Features

**Universally used unique value expression**

The non-homogeneous digital assets defined by the 1808 standard support a variety of data customizing and scaling approaches. They are compatible with different asset types in various games, and can be used as a general expression for various game data.


**Cross use cases without affecting each other (world wall)**

The extended data area is combined in the unit of zone. Each zone is bound to one or several contracts that are only responsible for itself. It represents a data area that is unique to the use case (game world). The key-value pair information after the zone is unfolded represents a series of game business-related data. Data between different zones can be read but not written mutually, that is, data changes in different use cases do not affect each other. The "world wall" of the game will prevent these properties from affecting other worlds, which will not result in the situation of "equipment downgraded in game A is also downgraded in game B".


**Worldview compatible design**

The non-homogeneous digital assets defined by the 1808 standard allow digital assets under the same worldview to be used in different business scenarios. Therefore, there requires certain rules to balance the asset value (capability value) among different business entities.

As for the 1808 standard, when an asset instance is referenced in a new business scenario, a relative attribute is determined, which takes a certain other zone data as references, representing the basic value of the asset. The data can be identified in other business entities under the same worldview. When the asset instance enters different business entities, the value in the business entity is determined according to this attribute, and other attributes such as equipment skills are supplemented by the zone data form of the business entity.


**Cross-network and cross-standard compatible design**

The digital assets defined in this standard are designed to be compatible with other network non-homogeneous digital asset standards, including ERC-721, ERC-1155, ERC-998, etc. For a single non-homogeneous digital asset type defined by contracts (ERC-721, etc.), the asset instance can be compatible by defining an asset type with the same custom data structure. For nested/combined asset types defined by contracts (ERC-998, etc.), compatibility can be achieved by adding portfolio relationship data to the extended data area.


**Asset owners are allowed to discard specific zone data**

The zone data of the 1808 standard digital asset will be left with a record of the game as the number of games experienced increases. When the owner no longer needs the data generated in a certain game because of props reinforcement errors, being given negative attributes or wishing to re-challenge the game, etc., the owner can choose to delete the zone data corresponding to the game, allowing the assets to reenter the game in the initial state.

The asset owner's control over the asset zone data is limited to the complete deletion of the specified zone data, rather than the change of zone data to prevent the owner from cheating. In addition, the deletion of zone data can also effectively prevent malicious contracts from writing large amounts of junk data to specific assets, resulting in data redundancy.


**Assets used as an embedded or combined module on the blockchain**
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/d1c2a0b-a25551d-6.png",
        "a25551d-6.png",
        240,
        220,
        "#f7f7f8"
      ],
      "caption": "Nested Combination of 1808 Standard Non-Homogeneous Assets"
    }
  ]
}
[/block]
Game props and equipment may be composed of multiple components and items. Therefore, the non-homogeneous digital assets of blockchain games should also be able to be nested and contained. In this case, each non-homogeneous asset can be composed of multiple non-homogeneous assets. The parent asset can contain one or more child assets, and the child assets can further contain other child assets.

For game scenarios with equipment construction or combination, the 1808 standard provides a design that supports asset portfolios. The extended data contains the zone that records the combination relationship. The zone data records the information of the nested relationship when the asset is combined. Before the relationship is terminated, the ownership of nested child assets will not be able to be transferred.

##Comparison of non-homogeneous assets

At present, ERC-721、ERC-1155 and ERC-998 of Ethereum network are the popular non-homogeneous digital asset standards, which are used in different scenarios and for different needs on the Ethereum network:

**ERC-721**
It is an officially accepted non-homogeneous digital asset standard defined by smart contracts in the Ethereum network. It has a customizable data zone, which makes it possible to digitize items or records. Typical applications are: Crypto Kitties, Crypto Celebrities, etc.

**ERC-1155**
It is a standard interface proposed by Enjin to define multiple non-homogenous assets in Ethereum's single smart contract, serving mainly the virtual props in blockchain games. Typical application: War of Crypto.

**ERC-998**
It is a combination of non-homologous tokens (CNFT, Composable NFTs) defined in Ethereum's smart contracts proposed by Matt Lockyer.
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/2b5e12a-71643cf-29.png",
        "71643cf-29.png",
        482,
        196,
        "#b5c7d2"
      ],
      "caption": "Comparison of non-homogeneous assets"
    }
  ]
}
[/block]
The figure shows the comparison of the above three non-homogeneous asset standards with NHAS-1808, which briefly compares the essentials that may be involved in blockchain and gaming. The differences marked in red are the features of the 1808 standard designed by COCOS-BCX for the game running on-chain. These features are related to the data structure design of the 1808 standard asset in addition to the characteristics of the BCX chain network itself.


##Data Structure
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/bb60e76-9371cbe-30.png",
        "9371cbe-30.png",
        982,
        620,
        "#c5dae9"
      ],
      "caption": "Data Structure of 1808 standar non-homogeneous digital asset"
    }
  ]
}
[/block]
The non-homogeneous digital assets data structure in the blockchain network is divided into fixed data zone and scalable data zone.

The fixed data zone stores the basic information of non-homogeneous digital assets, including asset ID, worldview statement and basic data zone; While the scalable data zone is a functional section designed for attribute extension of non-homogeneous digital assets, including zone data and combination relationship data.

The fixed data zone defines asset ID, worldview statement and other basic data. The asset ID is the unique identifier of assets instance in the ​distributed ledger network, and the unique credential to access, check and modify the assets. Worldview statement, including the worldview ID, the type of game in which the asset is in effect and supported, the world and the currencies supporting the circulation of assets in the network. The basic data zone further consists of information including a basic description of the assets, production time, producer, owner, user, black & white list of use right, etc.

The data includes the asset owner ID, producer ID, production time, and basic attributes of the asset (eg, equipment descriptions, etc.). The scalable data zone stores different business data in the worldview supported by the asset. Different business entities have exclusive zone IDs and data area in the zone, which is isolated from each other. Zone data is stored in the form of key-value pairs of the zone identity and data. The scalable data zone also contains a data zone to show the relationship of asset combination and nesting, which are used to describe the combination and affiliation of the assets.



## Data Structure Reference

The field types and identification reference tables of the fixed data zone of non-homogeneous digital assets defined in this standard.
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/c2b649d-cf939fa-31.png",
        "cf939fa-31.png",
        1026,
        370,
        "#e7e7e7"
      ]
    }
  ]
}
[/block]
The asset_id_type is designed to maintain the uniqueness in the network, which requires little for the ID length. However, from the perspective of multi-network compatibility, the maximum sample size of the ID should cover the maximum expected number of non-homogeneous digital asset instances in the existing decentralized distributed account-based network. For example, if the asset ID in the Ethereum network is a 40-byte hash address and the maximum number of samples that can be supported is 1.462*10^48, hash addresses or other unique identification approaches with a sample size greater than this value is considered when designing the asset ID in the network to which this standard is applied.

The world_view_type contains the worldview ID applied to the asset and the world currency corresponding to the worldview, where the Worldview ID is a unique identifier for the network, and the currency in circulation is the unique symbol of the currency (the network using the symbol as a unique credential) or the address (the network using the address as the unique credential).

The Asset_owner and Asset_creator fields type is account_id_type, which should be of a unique and sufficient sample size.

The Asset_create_time field type is time_point_sec, which is used to identify the date when this asset instance is created. It is determined by the timestamp of the ledger when the instantiation transaction is completed.

The asset_description field type is a string, which is a piece of data that can be used to express the basic attributes of an asset instance. The data can be processed in a custom parsing or encryption manner to match specific business entities and application scenarios.
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/d30f13c-cf939fa-31.png",
        "cf939fa-31.png",
        1026,
        370,
        "#e7e7e7"
      ]
    }
  ]
}
[/block]
 The Mod_data field type is an id list, which is a relationship table consisting of a list of identifiers of parent asset IDs and child asset IDs, which are used to describe the combination and nesting relationship of assets in different business entities.

 The World_view field type is a map, which is a key-value pair mapping table composed of zone identifiers and zone data. The zone identifier is a type identifier of the business entity, corresponding to one or several contracts, and all data interactions of the business instance for this asset instance will be performed in this zone.

 The Session_key field type is contract_id_type, which is the id of one or more core contracts that the business should contain. The id should be as unique and sufficient as the other unique identifiers.

 The session_data field type is a ​map, which consists of the inner_key and the inner_value. The specific data of the key and value is defined by the business entity responsible for this zone, which may include structured or encrypted strings as its data according to its needs.