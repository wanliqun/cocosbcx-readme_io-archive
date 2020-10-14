---
title: "8.1 Example of Betting Game"
slug: "81-example-of-betting-game"
hidden: false
createdAt: "2019-06-26T06:05:32.515Z"
updatedAt: "2019-06-26T06:05:39.966Z"
---
We’ll introduce to the development process with an example of a dice program with specific source code: [cocos-dice-sample](https://github.com/Cocos-BCX/cocos-dice-sample)。This includes contract development, deployment, debugging, and front-end contract call.

We hope the community have a complete understanding of DApp development based on Cocos-BCX.


##Game Rules

The game rules of Dice are very simple, with the following specific steps:
1.	Set the bet amount
2.	Adjust the slider to bet on the upper limit of the dice number and change the chance of winning
3.	Click “Roll” to place a bet. If the result is less than your bet number, you will be awarded immediately. The program will make the settlement based on the winning rate.


##Development Environment

[block:parameters]
{
  "data": {
    "h-0": "Environment",
    "h-1": "Version",
    "h-2": "Description",
    "0-0": "MacPro",
    "1-0": "VSCode",
    "2-0": "Node",
    "3-0": "JS SDK",
    "0-1": "10.14.2 (18C54)",
    "1-1": "1.32.3 (1.32.3)",
    "2-1": "v10.13.0",
    "3-1": "1.3.2.2"
  },
  "cols": 3,
  "rows": 4
}
[/block]