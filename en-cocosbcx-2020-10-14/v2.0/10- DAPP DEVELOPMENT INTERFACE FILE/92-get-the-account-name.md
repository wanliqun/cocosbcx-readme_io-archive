---
title: "10.2 How to Develop a Game on Cocos-BCX with Cocos Creator"
slug: "92-get-the-account-name"
hidden: false
createdAt: "2019-06-24T08:04:25.900Z"
updatedAt: "2020-03-02T09:34:33.364Z"
---
## Program a Dgame with [Cocos Creator](https://www.cocos.com/creator) that is named Pick Up the Stars 

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/c119ca0-1.gif",
        "1.gif",
        960,
        544,
        "#405a6c"
      ]
    }
  ]
}
[/block]
## How to play:
By pressing the A and D keys to manipulate an obtuse monster that never stops jumping to touch the continuously appearing stars. The game is over when the stars disappear.

## Download the source code:
Click below link to experience the game (which is not integrated with Cocos-BCX):
http://fbdemos.leanapp.cn/star-catcher/

[Click here to download the source code](https://github.com/cocos-creator/tutorial-first-game/releases/download/v2.0/start_project.zip)

[See the complete source code that has not been integrated with Cocos-BCX](https://github.com/cocos-creator/tutorial-first-game/releases/download/v2.0/complete_project.zip)

[See the complete source code that has been integrated with Cocos-BCX](https://github.com/Cocos-BCX/star-project.git)
Note: Please open the on-chain game through​ Google Chrome and install CocosPay Plugin before you start the game.

## Open the source code of the project
If you still don't know how to get and start Cocos Creator, please read the Installation and Start section.
1. First, start Cocos Creator and select Open Project.
2. In the folder selection dialog box that pops up, select start_project just downloaded and decompressed, and click the Open button. 
3. The main window of the Cocos Creator editor will be opened and you will see the project status as follows:
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/93795e4-2-2.png",
        "2-2.png",
        1278,
        718,
        "#414141"
      ]
    }
  ]
}
[/block]
## Create a scene
In Cocos Creator, the Scene is the core to organize the game contents in development, which is also the vehicle to present all the game content to players. A Scene typically includes the following contents:
  * Scene image and text (Sprite,  ​Label)
  * Characters
  * Gameplay scripts attached to the scene nodes as components
The game scene will be loaded when the player runs the game. After that, the game scripts of all the components included will automatically run to implement various logical functions set by developers. Therefore, apart from resources, the game scene is also the foundation of all content creation. Now, let's create a new scene.
1. Select the Assets directory in explorer to ensure that our scenes will be created in this directory.
2. Click + button in the top left corner of Assets panel and select Scene from the popup menu.
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/285b50f-3-3.png",
        "3-3.png",
        206,
        329,
        "#3c3c3c"
      ]
    }
  ]
}
[/block]
3. Create a Scene file named New Scene. Right-click it and choose Rename to rename it as a game. 
4. Double click on the ​game to open the scene in the Scene Editor and the Node Tree.

## Set up a scene image 
**Add a background**
Find the background image resource through Assets/Textures/Background in explorer, then click and drag this resource to Canvas node in Node Tree. Don't release the mouse until the Canvas node is highlighted orange, indicating that a sub-node​ of image resource called background is added.
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/d82c083-4-4.png",
        "4-4.png",
        207,
        329,
        "#989799"
      ]
    }
  ]
}
[/block]
Release the mouse, and you’ll see the background node that has been added under Canvas. When we add a node by dragging, the node is automatically named as the name of the image resource.
When we edit and modify the scene, we can save our modifications via main menu File -> Save Scene. Or we can save it by keyboard shortcut Ctrl + S (Windows) or Cmd + S (Mac).

## Add a ground
The character needs a ground to jump on. Drag the Assets/Textures/Ground in explorer to the Canvas in Node Tree in the same way as adding the background. In addition, we can select the sequence relationship between the newly added node and background. While dragging the resource, move the mouse pointer to under the background until the Canvas is displayed in the orange square. The green line represents the position the node will be inserted which is displayed below background. Then release the mouse. In this way, the ground will be put under background in the scene Node Tree, which is also a sub-node of Canvas. 
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/d9001ef-5-5.png",
        "5-5.png",
        305,
        117,
        "#5c4b3b"
      ]
    }
  ]
}
[/block]
In Node Tree, the rendering order of the nodes displayed below is after the upper nodes. That is, the lower nodes are drawn after the upper nodes. Therefore, the ground is located at the bottom and is displayed at the top of Node Tree in the scene editor. In addition, the child node will always be displayed before the parent node. The relationship and rendering order of the nodes can be adjusted in Node Tree. We can also keep dragging node up and down to change the order of node in the list.
According to the method of modifying the background, we can also use the Rectangle Transform Tool to set an appropriate size for the ground. When using the Rectangle Transform Tool, we can change the node position by dragging its anchor and edges. The status of the ground has illustrated below:
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/8996622-7-7.png",
        "7-7.png",
        1238,
        763,
        "#34393d"
      ]
    }
  ]
}
[/block]
In addition to the Rectangle Transform Tool, we can use the Move Tool to change the node position. Hold the move tool and drag the arrow shown on the node to change its position on a single axis at one time.
The value does not need to be precise when setting the position and size of background and ground. If you prefer precise value, you can input the values of position and size directly as shown in the screenshot.

## Add the main character
Next, it's the turn of the main character, little monster. Drag Assets/Texture/PurpleMonster from explorer to Canvas in Node Tree, and make sure it is placed below the ground. In this way, our main character will be shown at the very front. PurpleMonster, which parallels to the ground node, should be a child node of Canvas.
To make the main character stand out in the scene node, right-click the newly added PurpleMonster to rename it as Player.
Then, we need to set up some properties of the main character. First, change the position of Anchor. The Anchor will be at the center of any node by default, which means that the node's center is also the location of the node. We hope to control the bottom of the main character to simulate the effect of jumping on the ground. Therefore, we need to set up an Anchor at the character’ foot first. Find Anchor in the Properties panel and set up the value of y as 0. We will see the arrow of Move Tool that represents the position of the main character appears under the foot of the main character in the scene editor.
When the value of Anchor is (0,0), it means the Anchor is in the lower-left​ corner of the node; when the value of Anchor is (1,1), it means the Anchor is in the upper right corner of the node; when the value of Anchor is (0.5, 0.5), it means the Anchor is in the center of the node. The rest can be done in the same manner.
Next, drag the Player in the scene editor and place it on the ground. The effect is as illustrated below:
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/ec8a107-8-8.png",
        "8-8.png",
        1168,
        459,
        "#2c303a"
      ]
    }
  ]
}
[/block]
In this way we have the basic scene graphic content configured. In the next section, we will write code to make the game come alive.

## Write the script for the main character
One of the core philosophy to develop games through Cocos Creator is to make the content creation and function development collaborate smoothly. In the section above, we focused on graphic content. Next, we will write a script to develop the flow of functions, and we will see that the finished program script can be used by content creators easily. 
Even if you have never written a program before, there's no need to worry. We will provide all the necessary codes in the tutorial. Copy and paste them to the correct position. Then you can ask programmer partners for help. Next, let's start creating script that drives the main character to act. 

## Create a script
1. Right-click the Assets Folder in explorer and select Create- -> Folder
2. Right-click New Folder and select rename to rename it as scripts, where will store all the scripts of the game.
3. Right-click the scripts folder and select Create -> JavaScript to create a JavaScript script
4. Rename the new script to Player and double click the script to open the code editor
**Attention：** The script name in Cocos Creator is the name of the component, and its name is case-sensitive! If the case of the component name is incorrect, you will not be able to use the component correctly!

## Write component property
There are already some pre-set code blocks in the open Player script, as shown below:
[block:code]
{
  "codes": [
    {
      "code": "cc.Class({\n    extends: cc.Component,\n\n    properties: {\n        // foo: {\n        //     // ATTRIBUTES:\n        //     default: null,        // The default value will be used only when the component attaching\n        //                           // to a node for the first time\n        //     type: cc.SpriteFrame, // optional, default is typeof default\n        //     serializable: true,   // optional, default is true\n        // },\n        // bar: {\n        //     get () {\n        //         return this._bar;\n        //     },\n        //     set (value) {\n        //         this._bar = value;\n        //     }\n        // },\n    },\n    // LIFE-CYCLE CALLBACKS:\n\n    // onLoad () {},\n\n    start () {\n\n    },\n    // update (dt) {},\n});\n",
      "language": "javascript"
    }
  ]
}
[/block]
Let's take a look at the role of these codes. First,​ we can see a global cc.Class() method. What is cc? Cc is short for Cocos. The main namespace of the Cocos engine. All classes, functions, properties, and constants in the engine code are defined in this namespace. Class() is a method under the cc module that declares classes in Cocos Creator. To make it easier to distinguish, we call the class declared with cc.Class called CCClass. The argument to the Class() method is a prototype object. You can create the required class by setting the required type parameters in the prototype object as key-value pairs.
E.g:
[block:code]
{
  "codes": [
    {
      "code": "var Sprite = cc.Class({\n        name: \"sprite\"\n    });\n",
      "language": "javascript"
    }
  ]
}
[/block]
The above code creates a type with cc.Class() method and assigns it to the Sprite variable. Set the class name to sprite. Class names are used for serialization, which can generally be omitted.
For a detailed study of cc.Class, refer to  [Declare class with cc.Class.](http://docs.cocos.com/creator/manual/zh/scripting/class.html)。
Now let's go back to the script editor and look back at the previous code, which is a structure needed to write a component script. A script with such a structure is a component in Cocos Creator that can be mounted on a node in the scene to provide various functions of the control node. Let's set some properties first, then see how to adjust them in the scene.
Find the properties section in the ​Player script, change it to the following and save it:
[block:code]
{
  "codes": [
    {
      "code": "// Player.js\n    //...\n    properties: {\n        // main character's jump height\n        jumpHeight: 0,\n        // main character's jump duration\n        jumpDuration: 0,\n        // maximal movement speed\n        maxMoveSpeed: 0,\n        // acceleration\n        accel: 0,\n    },\n    //...\n",
      "language": "javascript"
    }
  ]
}
[/block]
Cocos Creator specifies that all properties that a node has need to be written in the properties code block. These properties will specify how the main character moves. We don't need to care about the values in the code, because we will set these values directly in the Property inspector. We can put properties that need to be adjusted at any time in the properties later during the game production process.
Now we can add Player component to the node of the main character. Select Player in Node Tree, click the Add Component button in the Property panel. Select User’s Script Component -> Player, and add Player component to the main character node.
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/b9009fc-9-9.png",
        "9-9.png",
        476,
        230,
        "#808895"
      ]
    }
  ]
}
[/block]
Now we can see the newly added Player component in the Properties panel of Player. Set up properties related to the jumping and movement of the main character according to the image below:
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/c8738eb-10-10.png",
        "10-10.png",
        293,
        189,
        "#414140"
      ]
    }
  ]
}
[/block]
The jumpDuration's unit is seconds. The other unit of the values is pixels. According to the current setting of the Player component: Our main character will have a jump height of 200 pixels. The time needed for jumping to the highest point is 0.3 seconds. Its maximum horizontal movement speed is 400 pixels per second. The horizontal acceleration is 350 pixels per second.
All the value is for reference only. When the game is running, you can modify value in the Properties panel at any time according to your preference. There is no need to change any codes. 

## Write the Jumping and Moving logic
Now, let's add an function called setJumpAction to make role jump, and put it below the properties: {...}, code block:
The method to setJumpAction function:
[block:code]
{
  "codes": [
    {
      "code": "// Player.js\n    properties: {\n        //...\n    },\n\n    setJumpAction: function () {\n        // jump up\n        var jumpUp = cc.moveBy(this.jumpDuration, cc.v2(0, this.jumpHeight)).easing(cc.easeCubicActionOut());\n        // jump down\n        var jumpDown = cc.moveBy(this.jumpDuration, cc.v2(0, -this.jumpHeight)).easing(cc.easeCubicActionIn());\n        // repeat\n        return cc.repeatForever(cc.sequence(jumpUp, jumpDown));\n    },\n",
      "language": "javascript"
    }
  ]
}
[/block]
Now, you need to know about Cocos Creator's Action system. Since the action system is much more complicated, here is a brief introduction.
In Cocos Creator, the action is simply the displacement, scaling, and rotation of a node.
For example, in the code above, the method of the moveBy() is to move the specified distance within the specified time. The first parameter is the jump time we defined in the main character properties. The second parameter is a Vec2 (representing 2D vector and coordinate) type objects. For a better understanding, we can look at the official method Reference:
[block:code]
{
  "codes": [
    {
      "code": "/**\n * !#en\n * Moves a Node object x,y pixels by modifying its position property.                                  <br/>\n * x and y are relative to the position of the object.                                                 <br/>\n* Several MoveBy actions can be concurrently called, and the resulting                                <br/>\n * movement will be the sum of individual movements.\n * !#zh Moves the specified distance。\n * @method moveBy\n * @param {Number} duration duration in seconds\n * @param {Vec2|Number} deltaPos\n * @param {Number} [deltaY]\n * @return {ActionInterval}\n * @example\n * // example\n * var actionTo = cc.moveBy(2, cc.v2(windowSize.width - 40, windowSize.height - 40));\n */\ncc.moveBy = function (duration, deltaPos, deltaY) {\n    return new cc.MoveBy(duration, deltaPos, deltaY);\n};\n",
      "language": "javascript"
    }
  ]
}
[/block]
As you can see, the method moveBy can set three parameters. We already know the first two parameters; the third parameter is the Y coordinate of the Number type. The second parameter can be set in two types, the first is the Number type, the second is the Vec2 type. If we set the Number type here, then the default parameter is X coordinate. In this case, the third parameter is required, which is the Y coordinate. In the above example, cc.moveBy(this.jumpDuration, cc.v2(0, this.jumpHeight)) is a type of cc.v2 object constructed using the Vec2 type, which represents a coordinate, that is, X coordinates also have Y coordinates, because you don't need to pass in the third parameter. At the same time, pay attention to the official statement x and y are relative to the position of the object. This sentence means that the incoming X and Y coordinates are relative to the current coordinate position of the node, rather than the absolute coordinates of the entire coordinate system.
After understanding the meaning of the parameters, let's focus on the return value of the moveBy() function. As you can see from the official description, this method returns an object of type ActionInterval. ActionInterval is a class in Cocos that represents the time interval action, which is completed within a certain time. Now we can understand the meaning of the previous part of the code cc.moveBy(this.jumpDuration, cc.v2(0, this.jumpHeight)).easing(cc.easeCubicActionOut()), which means to construct an ActionInterval type. The object, which represents the coordinate position of (0, this.jumpHeight) relative to the current node during the jumpDuration time. In short, it is simply an upward jump action.
So what is the role of easing (cc.easeCubicActionOut()) in the second half? Easing is a funtion under the ActionInterval class that allows the interval action to be rendered as an easing motion. The set parameter is an easing object that returns an ActionInterval type object, which is set by using the easeCubicActionInOut function. EaseCubicInOut is an action that continually enters and exits in a cubic function. For the specific curve, refer to the following figure:
[block:image]
{
  "images": [
    {
      "image": []
    }
  ]
}
[/block]
See the details in [API](http://docs.cocos.com/creator/api/zh/modules/cc.html?h=easecubicactionout()。
Next, call the setJumpAction method just added in the onLoad method, then execute the runAction to start the action:
[block:code]
{
  "codes": [
    {
      "code": "// Player.js\n    onLoad: function () {\n        // initialize jump action\n        this.jumpAction = this.setJumpAction();\n        this.node.runAction(this.jumpAction);\n    },\n",
      "language": "javascript"
    }
  ]
}
[/block]
The onLoad method will be immediately implemented after loading the scene. So we will put operations and logic concerning initialization into it. We first pass the action of the loop jump to the jumpAction variable, then call the runAction method under the node mounted by this component, and pass the action of the loop jump to let the node (main character) jump all the time. Save the script, and then we can start running the game for the first time!
Click the Preview button at the top of Cocos Creator editor. which will automatically open your default browser and start running the game in it. Now we can see the main character - the purple monster is jumping lively and continuously in the scene.

## Manipulation of movement
A main character that can only jump foolishly up and down on the same spot is not very promising. Let us add keyboard input for the main character, using A and D to manipulate its jump direction. Add the Keyboard event response function below the setJumpAction method:
[block:code]
{
  "codes": [
    {
      "code": "// Player.js\n    setJumpAction: function () {\n        //...\n    },\n\n    onKeyDown (event) {\n        // set a flag when key pressed\n        switch(event.keyCode) {\n            case cc.macro.KEY.a:\n                this.accLeft = true;\n                break;\n            case cc.macro.KEY.d:\n                this.accRight = true;\n                break;\n        }\n    },\n\n    onKeyUp (event) {\n        // unset a flag when key released\n        switch(event.keyCode) {\n            case cc.macro.KEY.a:\n                this.accLeft = false;\n                break;\n            case cc.macro.KEY.d:\n                this.accRight = false;\n                break;\n        }\n    },\n",
      "language": "javascript"
    }
  ]
}
[/block]
Then modify the onLoad function, into which we add the switch of accelerating to the left/right and the current horizontal speed of the main character. Finally, call cc.systemEvent and start listening for keyboard input after the scene has been loaded:
[block:code]
{
  "codes": [
    {
      "code": "// Player.js\n    onLoad: function () {\n        // initialize jump action\n        this.jumpAction = this.setJumpAction();\n        this.node.runAction(this.jumpAction);\n\n        // switch of acceleration direction\n        this.accLeft = false;\n        this.accRight = false;\n        // current horizontal speed of main character\n        this.xSpeed = 0;\n\n        // Initialize the keyboard input listening\n        cc.systemEvent.on(cc.SystemEvent.EventType.KEY_DOWN, this.onKeyDown, this);\n        cc.systemEvent.on(cc.SystemEvent.EventType.KEY_UP, this.onKeyUp, this);   \n    },\n\n    onDestroy () {\n        // initialize keyboard input listener\n        cc.systemEvent.off(cc.SystemEvent.EventType.KEY_DOWN, this.onKeyDown, this);\n        cc.systemEvent.off(cc.SystemEvent.EventType.KEY_UP, this.onKeyUp, this);\n    },\n",
      "language": "javascript"
    }
  ]
}
[/block]
It's better to understand if you have Android development experience. The listener here is essentially the same as the OnClickListener in Android. In cocos, systemEvent is used to listen to system global events.（For details on listening and dispatching of mouse, touch, and custom events, see details in  [Monitor and launch events](https://docs.cocos.com/creator/manual/zh/scripting/events.html）Here registered a keyboard response function to systemEvent, in which the switch is used to determine whether the keyboard is A and D pressed or not, and if pressed, performs the corresponding operation.
Finally, modify the content of the update method by adding settings for the acceleration, speed and the current position of the main character:
[block:code]
{
  "codes": [
    {
      "code": "// Player.js\n    update: function (dt) {\n        // update speed of each frame according to the current acceleration direction\n        if (this.accLeft) {\n            this.xSpeed -= this.accel * dt;\n        } else if (this.accRight) {\n            this.xSpeed += this.accel * dt;\n        }\n        // restrict the movement speed of the main character to the maximum movement speed\n        if ( Math.abs(this.xSpeed) > this.maxMoveSpeed ) {\n            // if speed reach limit, use max speed with current direction\n            this.xSpeed = this.maxMoveSpeed * this.xSpeed / Math.abs(this.xSpeed);\n        }\n\n        // update the position of the main character according to the current speed\n        this.node.x += this.xSpeed * dt;\n    },\n",
      "language": "javascript"
    }
  ]
}
[/block]
Update will be called once per frame after the scene is loaded. We usually put the logical content that needs to be calculated or updated in time. In our game, after obtaining the direction of acceleration based on the keyboard input, we need to calculate the speed and position of the main character in update every frame.
After saving the script, click Preview Game to see our latest results. After the browser opens the preview, click on the game screen with the mouse (this is the browser limit, you can click the game screen to accept the keyboard input), then you can press the A and D keys to control the main character to move left and right!

Is the movement a little bit too slow? Does the main character jump not high enough? Hope to extend jump duration? No problem! All these can be adjusted at any time. Just set up different property value for the Player component, then you can adjust the game at your will. Here is a set of settings for reference:
Jump Height: 150
Jump Duration: 0.3
Max Move Speed: 400
Accel: 1000
This set of properties will make the main character become more flexible, as to how to choose, it depends on what style of game you want to do.

## Make stars
The main character can jump freely now so we need to set up a goal for players. The stars will appear continuously in the scene and players need to manipulate the monster to touch the stars to collect points. The star touched by the main character will disappear and a new one will be immediately re-created at a random position.

## Create Prefab
For node that needs to be regenerated, we can save it as Prefab resource, which can be a template for dynamic generation node.Learn more information about Prefab [Prefab resources（Prefab）](https://docs.cocos.com/creator/manual/zh/asset-workflow/prefab.html)。
First, drag the Assets/textures/Star texture from the Explorer into the scene. The location is arbitrary. We just need to use the scene as the operating platform creating Prefab. After the product is complete, we will remove this node from the scene.
We don't need to modify the position or rendering properties of the stars, but to make the stars disappear after being touched by the main character, we need to add a special component to the stars. Add a JavaScript script called Star to Assets/Scripts in the same way as adding a Player script.
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/2640c38-11-11.png",
        "11-11.png",
        304,
        456,
        "#393e43"
      ]
    }
  ]
}
[/block]
Next, double click this script to start editing. Only one property is needed for the star component to stipulate the distance for collecting points by the main character. Modify properties and add the following content:
[block:code]
{
  "codes": [
    {
      "code": "// Star.js\n    properties: {\n        // When the distance between the star and main character is less than this value, collection of the point will be completed\n        pickRadius: 0,\n    },\n",
      "language": "javascript"
    }
  ]
}
[/block]
Add this script to star you just created, select star in Node Tree, then click the Add Component button in the Property Inspector. Select User Script Component -> Star. The script will be added to the newly created star on the node. Then set the Pick Radius property value to 60 in the Property Inspector:
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/495be0a-12-12.png",
        "12-12.png",
        757,
        495,
        "#454646"
      ]
    }
  ]
}
[/block]
The settings required by Star Prefab are finished. Now drag star from Node Tree to the assets folder in Explorer to generate a Prefab resource named star.
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/84a59b4-13-13.png",
        "13-13.png",
        299,
        395,
        "#383a3b"
      ]
    }
  ]
}
[/block]
Now star can be deleted from the scene. We can double click star Prefab resource to edit directly .
Next we will dynamically generate stars using the Prefab resource in the script. 

## Add game control script
Star generation is part of the game's main logic, so we're going to add a script called Game as the main logic script for the game, which will add logic for scoring, game failure, and restart.
Add the Game script to the assets/scripts folder. Double click to open the script. First add the property needed for generating stars:
[block:code]
{
  "codes": [
    {
      "code": "// Game.js\n    properties: {\n        // this property quotes the PreFab resource of stars\n        starPrefab: {\n            default: null,\n            type: cc.Prefab\n        },\n        // the random scale of disappearing time for stars\n        maxStarDuration: 0,\n        minStarDuration: 0,\n        // ground node for confirming the height of the generated star's position\n        ground: {\n            default: null,\n            type: cc.Node\n        },\n        // player node for obtaining the jump height of the main character and controlling the movement switch of the main character\n        player: {\n            default: null,\n            type: cc.Node\n        }\n    },\n",
      "language": "javascript"
    }
  ]
}
[/block]
Beginners here may wonder why property like starPrefab are enclosed in {}, and there are new "properties" in parentheses. In fact, this is a complete declaration of the property. Our property declarations were incomplete before. In some cases, we need to add parameters to the property declaration. These parameters control how the properties are displayed in Property Inspector, and the properties are in the behavior of the scene during serialization. E.g:
[block:code]
{
  "codes": [
    {
      "code": "properties: {\n    score: {\n        default: 0,\n        displayName: \"Score (player)\",\n        tooltip: \"The score of player\",\n    }\n}\n",
      "language": "javascript"
    }
  ]
}
[/block]
The code above sets three parameters: default, displayName, and tooltip for the score property. These parameters specify the default value of the score (default) to 0. In the Property inspector, the property name (displayName) will be displayed as Score (player), and the corresponding tooltip is displayed when the mouse is moving on the parameter.
The following are common parameters:
Default：Sets the default value of the property. This default value is only used when the component is first added to the node.
Type：To qualify the data type of a property，see details in [CCClass Advanced Reference: type attribute](https://docs.cocos.com/creator/manual/zh/scripting/reference/class.html#type-%E5%8F%82%E6%95%B0)
Visible：set to false to not display this property in the Property Inspector panel
Serializable： set to false to not serialize (save) this property
DisplayName：Displayed as the specified name in the Property Inspector panel
Tooltip：in the Property Inspector panel
[block:code]
{
  "codes": [
    {
      "code": "starPrefab: {\n    default: null,\n    type: cc.Prefab\n},\n",
      "language": "javascript"
    }
  ]
}
[/block]
It's easy to understand. First, the starPrefab property is declared under the Game component. The default value of this property is null. The type that can be passed in must be the Prefab resource type. After that, the properties of ground and player can also be understood.
After saving the script, add the Game component to Canvas in Node Tree (after selecting Canvas drag the script onto the Property inspector, or click the Add Component button of the Property inspector and select Game from the User Script component.)
Next, drag the star's Prefab resource from the Explorer to the Star Prefab property of the Game component. This is the first time we've set a reference for a property. Only when the property declaration specifies that type is a reference type (such as the cc.Prefab type we wrote here) can we drag a resource or node onto that property.
Next, drag the star's Prefab resource from the Explorer to the Star Prefab property of the Game component. This is the first time we've set a reference for a property. Only when the property declaration specifies that type is a reference type (such as the cc.Prefab type we wrote here) can we drag a resource or node onto that property.
Then set the Min Star Duration and Max Star Duration properties to value of 3 and 5. When we generate the stars, we randomly take value between the two, which is the time elapsed before the stars disappear.

## Generate stars at random position
Next, we continue to modify the Game script to add logic to generate stars after the onLoad function:
[block:code]
{
  "codes": [
    {
      "code": "// Game.js\n    onLoad: function () {\n        // obtain the anchor point of ground level on the y axis\n        this.groundY = this.ground.y + this.ground.height/2;\n        // generate a new star\n        this.spawnNewStar();\n    },\n\n    spawnNewStar: function() {\n        // generate a new node in the scene with a preset template\n        var newStar = cc.instantiate(this.starPrefab);\n        // put the newly added node under the Canvas node\n        this.node.addChild(newStar);\n        // set up a random position for the star\n        newStar.setPosition(this.getNewStarPosition());\n    },\n\n    getNewStarPosition: function () {\n        var randX = 0;\n        // According to the position of the ground level and the main character's jump height, randomly obtain an anchor point of the star on the y axis\n        var randY = this.groundY + Math.random() * this.player.getComponent('Player').jumpHeight + 50;\n        // according to the width of the screen, randomly obtain an anchor point of star on the x axis\n        var maxX = this.node.width/2;\n        randX = (Math.random() - 0.5) * 2 * maxX;\n        // return to the anchor point of the star\n        return cc.v2(randX, randY);\n    },\n",
      "language": "javascript"
    }
  ]
}
[/block]
There are a few issues to be aware of here:
1. The y property under the node corresponds to the y coordinate of Anchor, because it defaults to the center of the node, so the y coordinate of the ground needs to add half of the ground height.
2. The purpose of the instantiate method is to clone the specified object of any type, or instantiate a new node from Prefab. The return value is Node or Object.
3.  The addChild method under Node is to establish the new node at the next level of the node, so the new node is displayed above the node.
4. The role of setPosition method under Node is to set the position of the node in the parent coordinate system. You can set the coordinate point in two ways. One is to pass in two values x and y, and the second is to pass cc.v2(x, y) (object of type cc.Vec2)
5. Get the component reference mounted on the node via the getComponent method under Node.
After saving the script, click the Preview Game button and you can see it in the browser. After the game starts, a star is dynamically generated! In the same way, you can dynamically generate any pre-set Prefab-based nodes in the game.
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/f2e3114-13.png__original",
        "13.png__original",
        1003,
        560,
        "#0c2734"
      ]
    }
  ]
}
[/block]
## Add the action of the main character's touching and collecting of stars
Now we need to add the action logic of the main character to collect stars. The point here is that stars should be able to get the position of the main character’s node at any time. In order to judge whether the distance between them is shorter than the collectable distance. How to get the reference of the main character’s node? Don't forget the two things we did before:
1. The Game component has a property called player that holds a reference to the main character’s node.
2. Each star is dynamically generated in Game script.
Therefore, we just need to pass the instance of Game component to stars and save it when the Game script generates  Star  instance, then we can access the main character’s node at any time via game.player. Let's open Game script and add a newStar.getComponent('Star').game = this; at the end of the spawnNewStar method, as follows:
[block:code]
{
  "codes": [
    {
      "code": "// Game.js\n    spawnNewStar: function() {\n        // ...\n        // Staging a reference of Game object on a star component\n        newStar.getComponent('Star').game = this;\n    },\n",
      "language": "javascript"
    }
  ]
}
[/block]
After saving, open the Star script. Now we can use the player node referenced in the Game component to determine the distance. Add the methods named getPlayerDistance and onPicked after the onLoad method:
[block:code]
{
  "codes": [
    {
      "code": "// Star.js\n    getPlayerDistance: function () {\n        // judge the distance according to the position of the player node\n        var playerPos = this.game.player.getPosition();\n        // calculate the distance between two nodes according to their positions\n        var dist = this.node.position.sub(playerPos).mag();\n        return dist;\n    },\n\n    onPicked: function() {\n        // When the stars are being collected, invoke the interface in the Game script to generate a new star\n        this.game.spawnNewStar();\n        // then destroy the current star's node\n        this.node.destroy();\n    },\n",
      "language": "javascript"
    }
  ]
}
[/block]
The getPosition() function under Node returns the position (x, y) of the node in the parent coordinate system, which is a Vec2 type object. Also note that calling the destroy() method under Node will destroy the node.
Then add the judgment distance of each frame in the update method. If the distance is shorter than the collection distance specified by the pickRadius property, then the collection behavior is performed:

[block:code]
{
  "codes": [
    {
      "code": "// Star.js\n    update: function (dt) {\n        // judge if the distance between the star and main character is shorter than the collecting distance for each frame\n        if (this.getPlayerDistance() < this.pickRadius) {\n            // invoke collecting behavior\n            this.onPicked();\n            return;\n        }\n    },\n",
      "language": "javascript"
    }
  ]
}
[/block]
Save the script, by pressing A and D key to control the main character to move around, You can see that when the main character gets close to the star, the star will disappear and a new one will be generated at a random position!

## Add score
The little monster makes a great effort to collect the stars, does not have the reward how to line? Now, let's add the logic and display of scoring when collecting stars.

## Add a score label（Label）
The score will start from 0 when the game is started. 1 point will be added for 1 star collected. To display the score, we should first create a Label node. Choose Canvas in Node Tree, right click and choose Create -> Create Renderer Nodes -> Node With Label. A new label node will be created under Canvas, and it will be located at the bottom. Next we will use the following steps to set up this label node:
1. Change the node's name to score.
2. Select score, and set the X,Y of the position property to (0, 180).
3. Edit the String property of the Label component and input Score: 0.
4. Set the Font Size property of the Label component to 50.
5. Drag the assets/mikado_outline_shadow bitmap font resource from the Assets (pay attention! the icon is bmfont) into the Font property of the Label component, replace the font of the text with the bitmap font in our project resource
**Attention：** The text of Score: 0 is recommended to use the English colon, because the Chinese character's colon will not be recognized after the String property of the Label component is added with the bitmap font.
After the completion, the effect is as shown below:
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/75cc6b7-14.png__original",
        "14.png__original",
        1321,
        688,
        "#383b3d"
      ]
    }
  ]
}
[/block]
## Add scoring logic to the Game script
We will put the logic of the scoring and update score display in the Game script, open the Game script and start editing. First add the score at the end of the properties block to display the reference property of Label:
[block:code]
{
  "codes": [
    {
      "code": "// Game.js\n    properties: {\n        // ...\n        // quotation of score label\n        scoreDisplay: {\n            default: null,\n            type: cc.Label\n        }\n    },\n",
      "language": "javascript"
    }
  ]
}
[/block]
Next, add the initialization of variables for scoring in the onLoad method：
[block:code]
{
  "codes": [
    {
      "code": "// Game.js\n    onLoad: function () {\n        // ...\n        // initialize scoring\n        this.score = 0;\n    },\n",
      "language": "javascript"
    }
  ]
}
[/block]
Then add a new method named gainScore to the back of the update method: 
[block:code]
{
  "codes": [
    {
      "code": "// Game.js\n    gainScore: function () {\n        this.score += 1;\n        // update the words of the scoreDisplay Label\n        this.scoreDisplay.string = 'Score: ' + this.score;\n    },\n",
      "language": "javascript"
    }
  ]
}
[/block]
After saving the Game script, go back to Node Tree, select Canvas, and drag the previously added score node to the Score Display property of the Game component in the Property Inspector.

## Call the scoring logic in Game in a Star script
Open the Star script below and add the gainScore call to the onPicked method:
[block:code]
{
  "codes": [
    {
      "code": "// Star.js\n    onPicked: function() {\n        // when the stars are being collected, invoke the interface in the Game script to generate a new star\n        this.game.spawnNewStar();\n        // invoke the scoring method of the Game script\n        this.game.gainScore();\n        // then destroy the current star's node\n        this.node.destroy();\n    },\n",
      "language": "javascript"
    }
  ]
}
[/block]
Preview after saving. You will see that when collecting stars, the scores displayed at the top of screen will increase now! 
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/68e21bc-15.png__original",
        "15.png__original",
        1000,
        558,
        "#0d2835"
      ]
    }
  ]
}
[/block]
## Judgement of failure and restarting 
Now our game has taken shape. But no matter how many scores one may get, a game without the possibility of failure won't give players any fulfillment. Now let's add the action of the stars' regular disappearance. And if all the stars disappear, the game will be viewed as failed. In other words, players need to finish collecting the star before the star disappears and repeat this procedure unceasingly to finish the loop of play method. 

## Add the logic of disappearing in a limited time to the star
Open the Game script, and add the variable declaration needed for counting time before invoking spawnNewStar of the onLoad method:
[block:code]
{
  "codes": [
    {
      "code": "// Game.js\n    onLoad: function () {\n        // ...\n        // initialize timer\n        this.timer = 0;\n        this.starDuration = 0;\n        // generate a new star\n        this.spawnNewStar();\n        // initialize scoring\n        this.score = 0;\n    },\n",
      "language": "javascript"
    }
  ]
}
[/block]
Then add the logic of resetting the timer to the end of the spawnNewStar method, in which this.minStarDuration and this.maxStarDuration are properties of the Game component that was declared at the beginning. They are used to stipulate the random scale of star duration:
[block:code]
{
  "codes": [
    {
      "code": "// Game.js\n    spawnNewStar: function() {\n        // ...\n        // reset timer, randomly choose a value according the scale of star duration\n        this.starDuration = this.minStarDuration + Math.random() * (this.maxStarDuration - this.minStarDuration);\n        this.timer = 0;\n    },\n",
      "language": "javascript"
    }
  ]
}
[/block]
Add the logic of updating the timer and judgement of exceeding the duration to the update method:
[block:code]
{
  "codes": [
    {
      "code": "// Game.js\n    update: function (dt) {\n        // update timer for each frame, when a new star is not generated after exceeding duration\n        // invoke the logic of game failure\n        if (this.timer > this.starDuration) {\n            this.gameOver();\n            return;\n        }\n        this.timer += dt;\n    },\n",
      "language": "javascript"
    }
  ]
}
[/block]
In the end, add the gameOver method. Reload the scene when failure occurs.
[block:code]
{
  "codes": [
    {
      "code": "// Game.js\n    gameOver: function () {\n        this.player.stopAllActions(); // stop the jumping action of the player node\n        cc.director.loadScene('game');\n    }\n",
      "language": "javascript"
    }
  ]
}
[/block]
What you need to know here is that cc.director is a singleton object that manages your game's logic flow. Since cc.director is a singleton, you don't need to call any constructor or create a method. The standard way to use it is by calling cc.director.methodName(), for example cc.director.loadScene('game') Reload the game scene game, where the game restart. The stopAllActions method under the node is obvious. This method will invalidate all the actions on the node.
Above, the modification of the Game script is complete, save the script, and then open the Star script, we need to add a simple visual hint effect for the stars that are about to disappear, add the following code at the end of the update method:
[block:code]
{
  "codes": [
    {
      "code": "// Star.js\n    update: function() {\n        // ...\n        // update the transparency of the star according to the timer in the Game script\n        var opacityRatio = 1 - this.game.timer/this.game.starDuration;\n        var minOpacity = 50;\n        this.node.opacity = minOpacity + Math.floor(opacityRatio * (255 - minOpacity));\n    }\n",
      "language": "javascript"
    }
  ]
}
[/block]
Save the Star script, and the logic of this game's play method now is completely finished. Now click the Preview Game button, we will see a qualified game with a core play method, incentive mechanism and failure mechanism in the browser. 

## Access to the Cocos-BCX chain
Currently we use Cocos Creator to implement a complete star picking game. Next, we need to record the scores obtained during the game on the Cocos-BCX chain. Just three simple steps:

First, import a toolkit that interacts with the Cocos-BCX chain. View the Toolkit documentation and import the toolkit provided by Cocos-BCX. 
Attention: Since the code in the toolkit refer to each other, it needs to be imported in the following order:
[block:code]
{
  "codes": [
    {
      "code": "import \"https://jdi.cocosbcx.net/static/js/bcx.min.js\"\nimport \"https://jdi.cocosbcx.net/static/js/core.min.js\"\nimport \"https://jdi.cocosbcx.net/static/js/plugin.min.js\"\n",
      "language": "javascript"
    }
  ]
}
[/block]
Second, initialize the configuration parameters linked to Cocos-BCX. The following provides two connectable socket addresses. When auto_reconnect is set to true, socket will be reconnected automatically.
[block:code]
{
  "codes": [
    {
      "code": "var _configParams={\n  default_ws_node:\"ws://39.106.126.54:8049\",\n  ws_node_list:[\n    {url:\"ws://39.106.126.54:8049\",name:\"COCOS node 1\"},\n    {url:\"ws://47.93.62.96:8049\",name:\"COCOS node 2\"}\n  ],\n  networks:[\n    {\n      core_asset:\"COCOS\",\n      chain_id:\"7d89b84f22af0b150780a2b121aa6c715b19261c8b7fe0fda3a564574ed7d3e9\" \n    }\n  ], \n  faucet_url:\"http://47.93.62.96:8041\",\n  auto_reconnect:true,\n  worker:false\n};\n",
      "language": "javascript"
    }
  ]
}
[/block]
When we record data, we not only record the content of the data, but also the source of the data, the time when the data was generated, etc., so that the data record makes sense.
Based on blockchain technology, Cocos-BCX provides wallet tools in PC, browser and mobile phone. It provides functions such as creating data source accounts, recording data, querying data, etc. Only by downloading one of these tools can we build the link with the account management tool. We can record and query the data information generated by each play of the game. The data is permanent and cannot be changed or deleted.
Third, download the Install Wallet tool and create a link to the Wallet tool. [Click here to download Wallet tool ](https://www.cocosbcx.io/product)
Here's the link code for building a wallet tool:
[block:code]
{
  "codes": [
    {
      "code": "  initSDK (callback) {\n          this.contractName = \"contract.starproject\";       \n            if (window.BcxWeb) {\n                this.bcl =  window.BcxWeb;\n                console.log(\"===bcl---\")\n                if (callback) {\n                    callback(true);\n                }\n            }else{\n                console.log(\"===bcl--cocos-\")\n                let self = this\n                self.bcl = new BCX(_configParams);\n                Cocosjs.plugins(new CocosBCX())\n                //connect pc-plugin between sdk\n                Cocosjs.cocos.connect('My-App').then(connected => {\n                    console.log(\"connected==\"+connected)\n                    if (!connected) {\n                        self.checkWindowBcx(function(is_success){\n                            console.log(\"is_success==\",is_success)\n                            if(is_success){\n                                if (callback) {\n                                    console.log(\"is_success==222\")\n                                    callback(true)\n                                }\n                            }else{\n                                console.log(\"no_cocos_pay\")\n                                callback(false)\n                            }\n                        })\n                        return false\n                    }\n                    const cocos = Cocosjs.cocos\n                    self.bcl = cocos.cocosBcx(self.bcl);\n                    if(self.bcl){\n                        if (callback) {\n                            callback(true);\n                        }  \n                    }else{\n                        if (callback) {\n                            callback(null);\n                        }\n                    }\n                }).catch(function(e){\n                    console.log(\"connect error---\"+JSON.stringify(e))\n                })\n    \n            }\n    },\n\n\n    checkWindowBcx(callback){\n        let check_count = 0\n        let self = this\n        let sdk_intervral = setInterval(function(){\n            console.log(\"checkWindowBcx\",window.BcxWeb)\n            if (window.BcxWeb){\n                self.bcl = window.BcxWeb\n                if(callback){\n                    callback(true)\n                }\n                clearInterval(sdk_intervral);\n            }\n           \n            if(check_count>=3){\n                clearInterval(sdk_intervral);\n                if(callback){\n                    callback(false)\n                }\n            }\n            check_count = check_count + 1\n\n        }, 1000);\n    },\n",
      "language": "javascript"
    }
  ]
}
[/block]
Through the three steps above, we have completed the link with the Cocos-BCX chain. Download the complete project example [view the source code](https://github.com/Cocos-BCX/star-project.git).