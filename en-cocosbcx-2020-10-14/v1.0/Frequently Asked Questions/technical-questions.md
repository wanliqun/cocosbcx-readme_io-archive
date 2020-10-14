---
title: "Technical Questions"
slug: "technical-questions"
hidden: false
createdAt: "2019-03-18T03:11:27.255Z"
updatedAt: "2019-03-18T03:13:29.396Z"
---
Cocos-BCX aims to provide game developers with an easy-to-use and improved blockchain gaming infrastructure, including visual development kits and on-chain ecosystem, to achieve quick and efficient blockchain gaming development with low barriers in a visualized, graphical way. 

Cocos-BCX tries to provide a fair and open gaming environment with transparent data and rules for players without items manipulation or maliciously inducted consumption.
[block:api-header]
{
  "title": "What is the relationship between witness-id and private-key in config.ini?"
}
[/block]
witness-id is the ID of witness who owns the node. At least one witness (several witnesses are OK but not recommended) for one block generation node. private-key maps upon public key and private key of the witness.
[block:api-header]
{
  "title": "How To Operate And Maintain Nodes?"
}
[/block]
**Node file upgrading** 

Terminate node file under operation and change the name of the existing node

mv witness_node witness_node.bak

**Node file backup**

tar -zcvf witness_node_data_dir.tar.gz witness_node_data_dir

Import new node file into the original content and restart operation.

Switch to the original Client if new node cannot operate or perform unstably. 

**Node data backup**

Enter the content of node file

tar -zcvf witness_node_data_dir.tar.gz witness_node_data_dir

witness_node_data_dir.tar.gz is backup file (suggest to add date to make distinguish)

**Node data restore**

Enter the content of node file, modify the name of the existing data file and unzip the original backup file

mv witness_node_data_dir witness_node_data_dir.bak
tar -zxvf witness_node_data_dir.tar.gz

Restart operation of witness_node file
[block:api-header]
{
  "title": "What Is The Origin of BCX-NHAS-1808?"
}
[/block]
It refers to the standard for non-homogeneous digital assets in Cocos-BCX. Since it is released on August 2018, and thus gets the name.