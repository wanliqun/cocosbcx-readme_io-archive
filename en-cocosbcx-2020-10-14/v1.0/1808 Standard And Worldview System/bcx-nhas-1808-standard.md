---
title: "BCX-NHAS-1808 Standard"
slug: "bcx-nhas-1808-standard"
hidden: false
createdAt: "2019-03-15T06:30:59.027Z"
updatedAt: "2019-03-17T03:04:43.571Z"
---
In this section, we discuss many standards of non-homogeneous digital assets to support Cocos-BCX, and define BCX-NHAS-1808 that is applied to norms and released and issued on BCX blockchain based on the requirements of gaming industry.
[block:api-header]
{
  "title": "Characteristics of 1808 Standard"
}
[/block]
**Unique Value Expression of Widespread Use**
BCX-NHAS-1808 supports data custom and extension, and is compatible with assets types in various games, and thus can be a universe expression of game data.

**Crossing Multiple Usage Scenarios Without Disturbances (world wall)** 
Extensible data field is composed of zones, and each zone connects one or several contracts in charge, representing the exclusive data field owned by a certain setting (game world). The information of key-value pairs of extended zone is a series of game transaction-related data. Data of different zones can be read but cannot be written, that is, the change of data among different settings will not cause disturbances, and in-game “world wall” will stop the entrance. There is no such thing as "degraded equipment in game A is found to have been demoted in game B".

**Worldview Compatibility**
BCX-NHAS-1808 allows digital assets under the same worldview to be used in different transactions, where rules are needed to balance the assets value (ability).  In 1808 standard, the introduction of an asset instance in a new transaction will determine a relative attribute, which takes certain zone data as reference and represents the basic value of the asset, and the data can also be identified by other business entities under the same worldview. That is to say, the attribute will determine asset value when the asset instance enters into different business entities. Other attributes, such as equipment and skill, are supplemented by zone data of business entities.

**Cross Network and Cross Standard Compatibility** 
The digital assets defined by 1808 standard are compatible with other non-homogeneous digital assets standards, such as ERC-721, ERC-1155 and ERC-998. ERC-721, the single non-homogeneous digital assets defined by contract, can achieve compatibility of asset instance through defining an asset type with identical custom data structure. For nested/ composable assets, such as ERC-998, compatibility can be achieved through adding assets composable relations in extensible data field. 

**Abandon Specific Zone Data** 
The zone data of digital assets defined by 1808 standard will leave gaming record as game experience increases. When game owners do not need certain data, such as item strengthening error, endowed with negative attributes and another challenge to the game, they can delete corresponding zone data, and reboot the asset.  The control over asset zone data is confined to the deletion rather than the modification of appointed zone data in case of cheating. In addition, the right to delete zone data can effectively avoid data redundancy due to maliciously written contract into specific assets.

**Assets as nested items or modules on blockchain** 
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/4d9bc4c-6.png",
        "6.png",
        240,
        220,
        "#f7f7f8"
      ],
      "caption": "Nested composable data defined by 1808 standard"
    }
  ]
}
[/block]
Take games as example, equipment may be composed of more modules and items, and thus non-homogeneous digital assets in blockchain gaming should have the characteristics that can be nested. In this situation, each non-homogeneous asset can be made up of multiple non-homogeneous assets. Parent assets involve one or more child assets, while child assets can also include many other child assets. 

For game settings with equipment build-up or composiition, 1808 standard supports composable assets and extensible data which contain zones for recording composable relations. Zone data records the nested relations in assets composition, and the ownership of nested child assets cannot be transferred before removing the relations.
[block:api-header]
{
  "title": "Comparison of Non-Homogeneous Assets Standards"
}
[/block]
Currently, well-received non-homogeneous digital assets standards include Ethereum ERC-721, ERC-1155 and ERC-998, which are applied to different settings for various requirements:

ERC-721
ERC-721 is a non-homogeneous digital assets standard defined by smart contract and officially recognized in Ethereum Network. It has custom data zone and make it possible to digitalize items and records. Examples: Cryptokitties, CryptoCelebrities and etc.

ERC-1155
Proposed by Enjin, ERC-1155  is a standard interface for multiple non-homogeneous assets defined by single smart contract in Ethereum Network, and mainly serves virtual items in blockchain gaming. Examples: War of Crypto

ERC-998
Proposed by Matt Lockyer, ERC-998  is a composable non-homogeneous fungible tokens(CNFT) defined by smart contract in Ethereum.
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/5cb0fbb-29.png",
        "29.png",
        482,
        196,
        "#b5c7d2"
      ],
      "caption": "Comparisons of non-homogeneous assets standards"
    }
  ]
}
[/block]
The comparison of three non-homogeneous assets standards above with 1808 standard briefly introduces essential points of non-homogeneous assets involved in blockchain and games, and the red part shows the characteristics of Cocos-NHAS-1808 operated on blockchain gaming. These features are related to the data structure of 1808 standard, in addition to the characteristics of BCX blockchain network.
[block:api-header]
{
  "title": "Data Structure"
}
[/block]

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/21b5423-30.png",
        "30.png",
        982,
        620,
        "#c5dae9"
      ],
      "caption": "Data structure  of BCX-1808-NHAS Standard"
    }
  ]
}
[/block]
As shown above, the data structure of BCX-NHAS-1808 consists of two basic functions: fixed data field for storing the basic information of non-homogeneous digital assets, including asset ID, worldview statement and basic data; extensible data field, a functional data zone specially designed to extend attributes of non-homogeneous digital assets, involving Data  with combination relationship and zone data. 

Fixed data defines the asset ID, worldview and other basic data of non-homogeneous digital assets. Asset ID is the unique identification of assets instance in distributed ledger network, and the unique proof to visit, check and modify the assets. Worldview includes game types and worlds validated and supported by the assets, and currencies circulated for assets in the network. Basic data consists of the identification of assets owners, creators ID, creation time and basic attributes of the assets, such as equipment description.

Data includes IDs of assets owners, ID of producers, creation time and basic attributes of the assets, such as equipment description. Extensible data field is a storage zone for transaction data under the worldview supported by the assets, and thus different business entities embrace exclusive zone identify and data zone. Data is stored separately in various business entities, and zone data is stored in the form of zone identity and key-value pairs. Meanwhile, extensible zone includes a zone for composable assets with nested relations, in order to show the composable and affiliated relationships.
[block:api-header]
{
  "title": "Data Structure Comparison"
}
[/block]
Zones and identifications comparison table of BCX-1808-NHAS fixed data field: 
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/0092ccb-31.png",
        "31.png",
        1026,
        370,
        "#e7e7e7"
      ]
    }
  ]
}
[/block]
The field type of Asset_ID is asset_id_type, which is designed to keep network uniqueness rather than require ID length. With regard to multi-network compatibility, the maximum sample quantity of ID should cover the maximum expected quantity of non-homogeneous digital assets instances in the existing decentralized distributed ledger network. For example, the asset ID in Ethereum network is a 40-byte hash address, and the maximum sample quantity is 1.462*10^48. Therefore, greater sample quantity (greater than hash address) or other unique identification should be taken into consideration when applying this standard to design the asset ID.

The field type of World_view is world_view_type, which involves worldview IB applied to the asset and world currencies in response to the worldview. The former is unique network identification, while the latter is the unique symbol of the currency (use symbol as unique certificated network) or address (use address as unique certificated network).

The field type of Asset_owner and Asset_creator is account_id_type, which should employ data with uniqueness and sufficient sample size.

The field type of Asset_create_time is time_point_sec, which identifies creation date of the asset instance, and is determined by ledger timestamp when the instantiated transaction is completed.

The field type of Asset_description is string, a piece of data used to display the basic attributes of asset instance, and can use customized parse or encryption to deal with the piece of data to match with specific business entities and settings. 
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/58c9e02-31.png",
        "31.png",
        1026,
        370,
        "#e7e7e7"
      ]
    }
  ]
}
[/block]
•  The field type of Mod_data is id list, which is a relationship table composed of identity parent asset ID and child asset ID, and describes the composable and nested assets relations among various business entities. 

•  The field type of World_view is map, a map of key-value pair composed of zone identity and data. Zone identity is the identification of the types of business entities, and map onto one or several contracts. Data interaction between the transaction and asset instance is undergone within the zone.

•  The field type of Session_key is contract_id_type. This transaction should contain the ID of one or more contracts, and the ID should enjoy uniqueness and sufficient sample size with other unique identification. 

•  The field type of Session_data is map, which is composed of key-value pair, i.e., inner_key and inner_value. Specific data of key and value is customized by business entities in charge. Structuralized or encrypted character string can be used as data if necessary.