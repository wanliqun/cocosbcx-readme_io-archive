---
title: "3.3 Technical Features"
slug: "33-technical-features"
hidden: false
createdAt: "2019-06-24T10:04:17.044Z"
updatedAt: "2019-06-24T10:06:16.875Z"
---
##Advanced Technical Highlights
Cocos-BCX project has a number of technical highlights, including iterative smart contract system, the Smithy mechanism, nested items combination, exchange gateway that support multi-chain and asset riveting, improved DPoS consensus mechanism, visualized contract editor, high-performance network and contract VM, multi-chain connected transaction verification mechanism to prevent BP/developer from cheating, Cocos-BCX economy principle design and an asset circulation platform that supports the circulation of multiple digital assets. The technical features mentioned here are detailed below.

Targeting at the pain points of the game industry, Cocos-BCX proposes the vision of value uniformity between the producers and consumers of contents in combination with the development opportunities of blockchain technology. Based on the overall technical framework, every technical segment and organization has its own target and logic, on which basis many improved multi-module technical solutions or mechanisms.

## Optimization of “Impossible Triangle”
The “Impossible Triangle” represents three features that are difficult to be balanced in blockchain system. Cocos-BCX is also unable to make the best of the three features at the same time, but we have made the “length” of the impossible triangle as short as possible through our design principles.

（1）	Decentralization
	Improved DpoS mechanism
The consensus layer of CocosChain is improved based on the traditional DPoS consensus algorithm. All active witnesses share the same scheduled block generation probability in the witness scheduling algorithm of the DPoS consensus algorithm, which ensures consistent block generation probabilities and rewards for all witnesses;
	Low Risk of Forking
Cocos-BCX Chain uses DPoS consensus mechanism that involves no miners, effectively lowering the risk of forking caused by the centralization of computing power. A fork may only take place when more than 1/3 of the witnesses disagree to the consensus under DPoS mechanism.  
	Light Nodes
In Cocos-BCX, a light node is essentially an environment with interoperability with the chain. Different from full nodes, a light node do not need to synchronize data of the entire network but necessary contract information and environmental data. Such a design significantly reduces the amount of data to be synchronized and time for synchronization, so that the game software on the blockchain has a feasible actual capacity and time cost.

（2）	Security
Player Autonomy and Asset Security: Due to the openness and transparency of the blockchain network, the information of digital assets obtained by the player in the game can be browsed through blockchain explorer, providing a protection mechanism for the security of the game assets.
	Assets operation permission
In-game props are owned and can be disposed of only by the player, and the destruction of items will be allowed only with user authorization;
	Atomization of key operations on-chain
Actions such as assets creation/circulation are submitted to the Smithy or the circulation platform. All operations in the process of creation/circulation are regarded as an indivisible atomic transaction.
	Scalable multi-step verification
In addition to the verification password for blockchain transaction, the game developer will further set a 2-step authenticator and random code verification to further improve the security of the player's assets;
	Secured by modern cryptography
Cocos-BCX chain uses ECC (elliptic curve cryptography) for encryption to ensure blockchain information security;
	Transaction verification mechanism to prevent BP/developer from cheating
Cocos-BCX designs a set of transaction execution, message transmission and running mechanisms to prevent BP and developers from cheating;
	Iterable smart contract system
Cocos-BCX supports logic updates and bug fixes for on-chain smart contract to ensure security and timeliness of the smart contract.

（3）	Scalability
The top layer is designed to be scalable to build a business ecosystem with an overall solution for the making of the decentralized game and the running of the game economy, through the combination of the game engine, development environment and Cocos-BCX based game chain, hence to connect the global game ecosystem. The key participants of the ecosystem include developers, users, content creation and the blockchain system.

The scalability designed for the top-layer includes​ Multi-platform game runtime environment, blockchain interactive interfaces, exchange gateways that support multi-chain and asset riveting, multi-chain connected and optimization and expansion of existing blockchain systems.

The design of top-layer scalability brings about a diversified ecosystem and continued possibilities. In addition, it expands the project’s fusion boundary through at least five technologies and solutions including the integrated multi-platform game runtime environment and blockchain interactive interface.