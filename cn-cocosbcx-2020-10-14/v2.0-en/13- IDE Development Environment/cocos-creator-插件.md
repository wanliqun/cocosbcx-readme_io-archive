---
title: "13.1 Cocos Creator Plug in"
slug: "cocos-creator-插件"
hidden: false
createdAt: "2019-03-25T03:44:08.684Z"
updatedAt: "2019-06-05T13:27:11.775Z"
---
## Cocos Creator Introduction
Cocos Creator (https://www.cocos.com/creator)is a Cocos2d-x-based game development tool with fully scripted, componentized and data-driven features, and a focus on content creation. 

Based on the open source framework Cocos2d-x, Cocos Creator implements an all-in-one, extensible, customizable workflow editor and, for the first time, as a Cocos range product，introduces componentized programming ideas and data-driven architecture design. It simplifies the work like scene editing, UI design, resource management, game debugging and previewing, and multi-platform publishing in the Cocos2d-x development workflow, making a good choice for team collaboration development that using Cocos2d-x.


## Project Structure
Cocos-BCX has open sourced the plug-in at Github, for further info: Cocos-BCX For Cocos Creator(https://github.com/Cocos-BCX/bcx-sdk-creator). A BCX For Cocos Creator plug-in and a Sample project that connecting BCX on Cocos Creator are provided for the users.


[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/617af9f-Cocos-BCX.png",
        "Cocos-BCX.png",
        294,
        254,
        "#3f2f30"
      ],
      "caption": "For Cocos Creator 的插件包"
    }
  ]
}
[/block]

bcx: the plug-in package of BCX For Cocos Creator(the folder shall be available after being installed to Project’s packages.)

sample: the project that contains the basic method of calling BCX.

## Required Version
CocosCreator 2.0+

## Installation

* Move the bcx folder to the packages directory of Creater project;
  * The following menu shall be shown in the Creator menu after installation;
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/c49fd2e-bcx_menu.jpeg",
        "bcx_menu.jpeg",
        279,
        110,
        "#798391"
      ]
    }
  ]
}
[/block]

  * Click the Install button, asset menu will generate a new folder bcx;
  * Shut down and reopen the project, the bcx folder shall be in the asset menu;

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/64d8c40-bcx_assets.png",
        "bcx_assets.png",
        414,
        658,
        "#38383a"
      ]
    }
  ]
}
[/block]
* Now bcx-related interfaces can be called with users‘ own codes.

## sample instruction
    * For Mac users, please open and run sample/bcx-creator with CocosCreator 2.0+.
   * For Windows users, please delete sample/bcx-creator/packages/bcx and copy the bcx file in project root directory to sample/bcx-creator/packages/, then open and run it with CocosCreator 2.0+.

##Corresponding Version
[block:parameters]
{
  "data": {
    "h-0": "BCX For Creator",
    "h-1": "BCX JS SDK",
    "0-0": "0.0.1",
    "0-1": "1.3.0.2"
  },
  "cols": 2,
  "rows": 1
}
[/block]
As stated in the 1st line, BCX For Creator 0.0.1 is generated on the base of  BCX JS SDK 1.3.0.2.