---
title: "5.2 Lua Virtual Machine"
slug: "lua虚拟机"
hidden: false
createdAt: "2019-04-01T03:22:33.906Z"
updatedAt: "2019-06-04T09:28:43.568Z"
---
In the blockchain 1.0 era represented by Bitcoin, blockchain is a distributed ledger. With the technology evolving to the 2.0 era represented by Ethereum, it is not simply a ledger, but a super cloud computer. The core is to add virtual machines to the underlying chain system to execute smart contract procedures.

The introduction of virtue machine essentially adds a trusted execution environment to the blockchian system. The developer deploys the developed program to the blockchain system and initiates a contract API call in the form of transaction.

In terms of basic implementation technology, the virtue machine of blockchain system, such as the EVM of Ethereum, are fundamentally similar to our traditional virtual machine, such as Java and Python virtual machines. In the Java virtual machine, the programmer compiles the program in Java into bytecode for running directly on the virtual machine.

Since developers in the game field are more familiar with Lua scripts, Cocos-BCX adopts Lua virtual machine. In doing so, game developers do not need to learn the Ethereum Solidity language, neither do they have to write contracts in C++ like in EOS. It greatly lowers the barrier for developers by writing with Lua language directly. 

Cocos-BCX makes some deletions and interface expansions on the original Lua virtual machine while embedding.