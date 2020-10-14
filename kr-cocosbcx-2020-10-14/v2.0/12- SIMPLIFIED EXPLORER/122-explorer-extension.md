---
title: "12.2 Explorer Extension"
slug: "122-explorer-extension"
hidden: false
createdAt: "2019-06-24T07:09:19.086Z"
updatedAt: "2019-06-24T07:09:23.938Z"
---
## What is CocosPay?
CocosPay is the explorer extension for Cocos-BCX.

##Configuration
Node.js 8.9.3 version or higher.

## Creation
Use npm install to install local dependencies.
Run building npm run dev.
Use the building to issue npm run build.
The unpacked building shall be at ./build.

## Start
As a very useful extension to dapp and web, CocosPay shall inject BcxWeb’s object into the current document after installation and login, as in the example below:

[block:code]
{
  "codes": [
    {
      "code": "  if (window.BcxWeb && window.BcxWeb.BCX) { \n      bcx = window.BcxWeb.BCX\n    }",
      "language": "javascript"
    }
  ]
}
[/block]
## Open Source Address:
https://github.com/Cocos-BCX/CocosPay（to be updated）