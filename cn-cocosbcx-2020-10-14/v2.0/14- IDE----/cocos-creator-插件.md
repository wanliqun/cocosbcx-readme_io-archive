---
title: "14.1 Cocos Creator 插件"
slug: "cocos-creator-插件"
hidden: false
createdAt: "2019-03-25T03:44:08.684Z"
updatedAt: "2019-12-13T03:19:32.575Z"
---
## Cocos Creator 介绍
[Cocos Creator ](https://www.cocos.com/creator)是以内容创作为核心的游戏开发工具，在 Cocos2d-x 基础上实现了彻底脚本化、组件化和数据驱动等特点。 

[Cocos Creator](https://www.cocos.com/creator) 基于开源框架 Cocos2d-x，实现了一体化、可扩展、可自定义工作流的编辑器，并在Cocos 系列产品中第一次引入了组件化编程思想和数据驱动的架构设计，简化了 Cocos2d-x 开发工作流中的场景编辑、UI设计、资源管理、游戏调试和预览、多平台发布等工作，是使用 Cocos2d-x 进行团队协作开发的良好选择。

## 工程结构
Cocos-BCX 的 Github 上已对此插件进行了开源，详情可访问：[Cocos-BCX For Cocos Creator](https://github.com/Cocos-BCX/bcx-sdk-creator)。该工程提供给用户可使用的 BCX For Cocos Creator 插件, 以及一个在 Cocos Creator 上联接 BCX 的 Sample 工程。
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
bcx : 这是 BCX For Cocos Creator 的插件包. (可以直接把这个文件夹安装到工程中的 packages 中, 即可使用)

sample : 这是 Sample 工程, 里面有调用 BCX 的基本方式.

## 版本要求
CocosCreator 2.0+

## 插件使用  
* 将 bcx 文件夹放在 Creator 工程的 packages 目录下
  * 安装好后, 在 Creator 的菜单中, 可以找到如下菜单 
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/5c45428-bcx_menu.png",
        "bcx_menu.png",
        279,
        110,
        "#798391"
      ]
    }
  ]
}
[/block]
  * 点击菜单 Install, 就会在 assets 目录下生成一个文件夹 bcx
  * 关闭并重新打开工程，bcx 文件夹出现在 assets 下 
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
  * 现在就可以在自己的代码中调用 bcx 相关的接口了. 

## sample 的说明 
  * 如果你是 Mac 系统, 可以用 CocosCreator 2.0+ 直接打开 sample/bcx-creator, 运行此示例工程
  * 如果你是 Win 系统, 请将 sample/bcx-creator/packages/bcx 删除, 然后再把工程根目录下的 bcx 文件夹拷到 sample/bcx-creator/packages/ 即可, 然后用 CocosCreator 2.0+ 打开, 运行. 

## 版本对应 
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
如上第一行说明, BCX For Creator 0.0.1 是基于 BCX JS SDK 1.3.0.2 而生成的.