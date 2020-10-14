---
title: "Design of Requirements And Authentication"
slug: "design-of-requirements-and-authentication"
hidden: false
createdAt: "2019-03-15T06:31:14.541Z"
updatedAt: "2019-03-17T03:15:03.213Z"
---
BCX-NHAS-1808 Requirements and authentication
[block:api-header]
{
  "title": "Non-Homogeneous Digital Assets Requirements"
}
[/block]
**Differences** 

•  Assets of different types

•  Assets of the same type have unique identification within fixed data field

•  Assets of the same type have different worldview statements within fixed data field

•  Assets of the same type have different zones within extensible data field

•  Assets of the same type have different specific data in the same zone within extensible data field 

**Confidentiality of assets zone data** 

In principle, digital assets data of distributed ledger network is open and transparent, while BCX-NHAS-1808 supports customized encrypted data considering the requirements of game development and operation. 

**Security of assets data**

•  The security of assets data in distributed ledger network includes the following:

•  The basic data, such as assets worldview, cannot be modified once released

•  Extensible data owner of a certain zone can only modify its own data

•  The modification to extended data in contract is reflected by the change of zone of the contract

•  For non-homogeneous digital assets in portfolio, transaction-induced change in ownership should be valid on the whole portfolio, and composable assets cannot perform this operation separately before being involved in portfolio.

•  Assets owners have the right to delete the zone of extensible data

**Confidentiality of authentication information**

Contract ownership authentication should involve ECC and AES to ensure confidentiality

**Circulation of cross-network digital assets** 

Non-homogeneous digital assets issued by 1808 standard is compatible with other non-homogeneous digital assets in distributed ledger network through certain ways, such as ERC 721 or ERC 875.
[block:api-header]
{
  "title": "Authentication"
}
[/block]
**Requirements Authentication**

Digital assets should involve: 

•  Fixed data authentication after the creation of digital assets
•  Contract modification authentication of digital assets
•  Owner modification authentication of digital assets
•  Composable and nested relationship authentication of digital assets

**Authentication Mode**

Authentication reference model of non-homogeneous digital assets in distributed ledger network .
The authentication of non-homogeneous digital assets defined by 1808 standard in distributed ledger network includes release authentication, visit/ execute authentication, ownership authentication and zone authority authentication.
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/eea040c-32.png",
        "32.png",
        482,
        378,
        "#f3f3f3"
      ]
    }
  ]
}
[/block]
**Authentication model of non-homogeneous digital assets in distributed ledger network
** 

•  Release authentication is used to authenticate defined and released assets in network, including releaser identity and operation authority. 
•  Visit/ execute authentication refers to the authentication done by business entities when visiting or modifying assets data, such as visit or modification of transaction data, operation authority authentication and identity authentication. 
•  Ownership authentication is used to determine the identity of those who own asset instance in settings, such as  asset transfer, transaction, and zone data deletion.  
•  Zone authority authentication is used to predict whether business entities qualify for modifying the authority of certain zone data in settings, such as the operation of business entities on asset instance data. 
• For digital assets in portfolio, ownership change in parent asset is bound up with child asset, which cannot modify ownership before unbounding. 

•  Requirements of authentication information
•  Private information for authentication, such as private key, authority and provisional authority and other derivative keys of releases, business entities, assets owners as well as temporary identity of business entities, should be stored in respective secure medium. 
•  Signing information should be safely stored in distributed ledger network and can only be searched through network authority. 
•  Transaction signing should be conducted in sage and isolated environment as much as possible, such as off-line environment. 
•  Provisional and derivative authority information should be anti-guessing redundancy.