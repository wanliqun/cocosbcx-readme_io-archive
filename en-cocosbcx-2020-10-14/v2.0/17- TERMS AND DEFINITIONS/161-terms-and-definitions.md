---
title: "17.1 Terms and Definitions"
slug: "161-terms-and-definitions"
hidden: false
createdAt: "2019-06-24T06:17:14.592Z"
updatedAt: "2020-03-02T09:32:44.438Z"
---
## distributed ledger
A distributed ledger (also called a shared ledger or distributed ledger technology or DLT) is an information recording method of sharing digital data through synchronized mechanism across multiple ledgers. With ledger communicate through P2P connection and data verified and agreed through consensus, there is no central administrator or centralized data storage. Each ledger stores exactly the same data.

## consensus
Consensus refers to a decision-making method and process for affairs and data through the majority approval method, generally including the process of decision-completing and completing this decision through consensus.

## decentralized game
Decentralized game is the type of game in which the main logic and code of the software are stored in and driven by the distributed ledger network. The main logic or even all logic of the game are determined by the smart contract in the distributed ledger network, which makes central service unnecessary.

## smart contract
A smart contract is a kind of script with Turing completeness. By running contract virtual machine in the distributed ledger network, it realizes the functions of running transaction logic, network data interaction, and information transmission.

## blockchain
A blockchain is a data recording method that encrypts and links distributed ledger transaction data through cryptography. Each group of transaction data is a block, usually validated by Merkel's proof，and each block contains encrypted hash, timestamp, etc. of the previous block, featuring the characteristic of being hard to tamper with. 

## homogeneous digital assets
Homogeneous digital assets are a type of digital assets that applied to the distributed ledger network. There is no difference between assets instance, which can be counted together when they sharing the same measuring units and types, and their number can be divided according to the set accuracy.

## non-homogenous digital assets
Non-homogeneous digital assets are a type of digital assets applied to distributed ledger network with unique assets instance, which have different data items and contents except the unique identifiers, and those of the same type cannot be directly combined and cannot be compartmentalized.

## world view
A worldview is an identification used to distinguish between story settings and characters/items/rules settings and utility scope.

## authentication procedure
Authentication procedure refers to the process of authorization confirming between business entities and digital assets, as well as establishing a trust relationship between business entities and distributed ledger networks.

## digital signature
The digital signature is an authentication mechanism to guarantee non-repudiation of identity information by public and private key algorithm, usually based on ECC in distributed ledger networks. The digital signature used in this paper meets the requirements of Article 13 of the Electronic Signature Law of the People's Republic of China on the reliability of electronic signatures.

## decentralized database
In decentralized distributed ledger network, data is structured to store the same copy on all ledgers. Its storage can be abstracted as a distributed decentralized database, enabling contracts or other business entities to store their structured data through declared data tables in the distributed network.

## basic identity
The basic identity of homogeneous digital asset data described in this paper refers to the identity defined by the asset publisher and meets the requirements of the distributed ledger network with the uniqueness of the universal network. It is mainly used in the scenarios of identification, authentication, reading, and modification of digital assets.

## session identity
The session identity of homogeneous extensible data of digital assets described in this paper is the identity defined by contract publisher and meets the requirements of the distributed ledger network with the uniqueness of the universal network. It is mainly used for scenarios such as digital asset extension data identification, authentication, reading and modification in specific game world and stage.

##  inherent data field
Divided by basic identification, the inherent data field is the section used to describe the basic information(unique ID, basic attributes, worldview, etc.) of non-homogeneous digital assets in this standard. 

## scalable data field
The scalable data field is the section used to describe the game world and stage information of non-homogeneous digital assets in this standard, including the business data of related games and contracts. The accessible data areas of different game worlds/contracts are divided by zone identity.

## active privilege
Active privilege refers to the executable action privilege of digital assets, such as editable and operable permissions within a certain range, including modification of specified domain in the asset scalable data area, asset sending and transferring out, etc.

## owner privilege
Owner privilege refers to the digital assets’ owner's authority used to identify an account's ownership of the asset. With a higher priority, in addition to the scope of the action permissions, owner privilege also has the authority to delete the specified domain in the scalable data area.

## data structure
Data structure refers to the specific data mode of data storage and circulation in distributed ledger network, including but not limited to: point-to-point transmission, unit data, digital assets data, smart contract data, intermediate data, etc.

## service provider
A service provider is an object that provides services, including external operation interfaces, contracts with access rights, user interfaces, etc.

## cross-net mapping
Cross-net mapping is the digital asset data with specific data structure can be mapped to different distributed ledger networks through business entities. 

[block:api-header]
{
  "title": "Abbreviations and Symbols(BCX-NHAS-1808 Standard)"
}
[/block]
## Abbreviations 
[block:parameters]
{
  "data": {
    "h-0": "Names",
    "h-1": "Explanation",
    "0-0": "IP（Internet Protocol）",
    "1-0": "HTTP（Hyper Text Transfer Protocol）",
    "2-0": "P2P（peer-to-peer）",
    "3-0": "RPC（Remote Procedure Call）",
    "5-0": "AES（Advanced Encryption Standard）",
    "6-0": "BP （Block Producer）",
    "7-0": "OP（Operation）",
    "8-0": "MS （Multisignature）",
    "0-1": "Internet Protocol",
    "1-1": "Hyper Text Transfer Protocol",
    "2-1": "An Internet system that exchanges information between peers without central servers",
    "3-1": "A computer communication protocol for completing remote procedure call",
    "5-1": "An advanced encryption standard, also known as Rijndael, is a block encryption standard widely used in symmetric encryption",
    "6-1": "A participant who packs block data and synchronizes it to other books",
    "4-0": "ECC（Elliptic Curve Cryptography）",
    "4-1": "A key algorithm for asymmetric encryption based on elliptic curve mathematics",
    "7-1": "An indivisible (atomic) action on asset data",
    "8-1": "Multi-signature, which refers to a plural authorization confirmation method that signature object needs to be completed by multiple participants"
  },
  "cols": 2,
  "rows": 9
}
[/block]
## Symbols


[block:parameters]
{
  "data": {
    "4-1": "An Ethereum's non-homogeneous digital asset contract standard that supports nested combinations between non-homogeneous digital assets",
    "3-1": "An Ethereum non-homogeneous digital asset contract standard that supports the definition of multiple asset types within a single contract",
    "2-1": "Ethereum simplified non-fungible token standard based on ERC 721",
    "1-1": "Non-fungible token standard of Ethereum",
    "0-1": "Smart homogeneous digital asset contract standard of Ethereum",
    "0-0": "ERC 20",
    "1-0": "ERC 721",
    "2-0": "ERC 875",
    "3-0": "ERC 1155",
    "4-0": "ERC 998"
  },
  "cols": 2,
  "rows": 5
}
[/block]