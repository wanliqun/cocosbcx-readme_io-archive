---
title: "18.1 Technical Problems"
slug: "171-technical-problems"
hidden: false
createdAt: "2019-06-24T06:01:11.621Z"
updatedAt: "2020-03-02T09:32:25.602Z"
---
## What's the use of Cocos-BCX? What problems can it solve?

Cocos-BCX hopes to provide game developers an easy-to-use, comprehensive blockchain gaming infrastructure that includes visual development kits and on-chain ecosystem. In this way, the developers need not focus on the implementation of blockchain technology but develop the blockchain games directly with low threshold and high speed and efficiency in a graphical way.

Cocos-BCX wants to provide a fair, just and open game environment which equipped with transparent data and rules, as well as zero tolerance to backstage manipulation of props drop rate and malicious induced consumption, hoping that the assets of game players can be preserved in a long, safe and decentralized way.


## What is the relationship between witness-id and private-key in config.ini?

A witness-id is the witness ID owned by the node. A block-generating node must have at least one witness (multiple witnesses are allowed but not recommended). The private-key corresponds to the public and private keys of the witness.

## How to maintain nodes?

**Upgrading the node file**

Terminate the running node file and change the existing node file name.

mv witness_node witness_node.bak

**Node file backup**

tar -zcvf witness_node_data_dir.tar.gz witness_node_data_dir

Put the new node file in the original directory and run it again.

Switch back to the original terminal if the new node is not working or unstable.

**Node data backup**

Enter the directory of the node file.

tar -zcvf witness_node_data_dir.tar.gz witness_node_data_dir

The backup file is witness_node_data_dir.tar.gz (recommend to enter the date for identification).

**Node data restoration**

Enter the directory of the node file, change the existing data folder name and extract the original backup file.

mv witness_node_data_dir witness_node_data_dir.bak
tar -zxvf witness_node_data_dir.tar.gz

Rerun the node file witness_node. 

## The origin of BCX-NHAS-1808 standard number?
The Cocos-BCX  Non-Homogeneous Asset Standard is named after the issuing date, August 2018.