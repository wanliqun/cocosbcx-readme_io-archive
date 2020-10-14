---
title: "1.1.4 Technical Requirements"
slug: "114-technical-requirements"
hidden: false
createdAt: "2019-06-24T06:04:40.143Z"
updatedAt: "2019-06-24T06:39:47.314Z"
---
##Lua Programming

Given the extensive use of Lua language in the traditional game development and its accessibility, our contract virtual machine currently supports Lua (Lua 5.3), and will further cover other languages such as JavaScript, Solidity and so on.

It’s easy to get started with Lua by reading the Lua 5.3 Reference Manual

[Lua 5.3 Reference Manual](https://www.lua.org/manual/5.3/)

##Front-End Development

Blockchain applications can be distinguished from traditional ones by the following two formulas:
App =  Fronted + Server
DApp = Fronted + Contracts
In the Cocos-BCX contract with Lua, there are the following three options for the front-end:

**1. Original Web JS**
This is a traditional web development method, which is to call the JS SDK provided by Cocos-BCX to interact with the blockchain system.

**2. Native**
This is similar to developing a traditional iOS/Android app, which is to call the Native API provided by Cocos-BCX.

**3. Creator**
This is a model that game developers are familiar with, and we have integrated the Cocos-BCX development environment into Creator. This makes it easy to release multi-platform applications.


##Command Line
Command line operations are required for the node deployment and wallet command line tools. Therefore, it is recommended to have a systematic understanding and learning of the Linux Shell.