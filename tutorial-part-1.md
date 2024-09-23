# Hit the target! Part 1

## Set the scene @showdialog

In this tutorial, we will create the scenery for our game.

## Where are we playing?

Let's add a background for our game.

1.  From the   
``||scene:Scene||``   
drawer, add a   
``||scene:set background image to []||``   
block to your   
``||loops(noclick):on start||``    
container.
1.  We have provided a background that you can use.
You also can draw your own!

Check the simulator to make sure your project works correctly.

View the hint if you need any help.

```blocks
scene.setBackgroundImage(assets_launcher.field)
```

## Put me in, coach!

Now, let's add our football player!

1.  Add a   
``||variables(sprites):set playerSprite to||``
``||sprites:sprite [] of kind Player||``   
block to your   
``||loops(noclick):on start||``   
container.
1.  Select an image from the gallery for your sprite.
You also can draw your own!
1.  Add a   
``||sprites:set||``
``||variables(sprites):playerSprite||``
``||sprites:position x to (10) y (20)||``   
block to the   
**bottom** of your   
``||loops(noclick):on start||``   
container.

Check the simulator to make your football player is in the 
top-left corner of the field.

View the hint if you need any help.

```blockconfig.local
let playerSprite = sprites.create(img`.`, SpriteKind.Player)
playerSprite.setPosition(10, 20)
```

```blocks
scene.setBackgroundImage(assets_launcher.field)
// @highlight
let playerSprite = sprites.create(assets_launcher.footballerRight0, SpriteKind.Player)
// @highlight
playerSprite.setPosition(10, 20)
```

## Where am I throwing?

We need to tell the game that this sprite belongs to the player.
This will add a marker to the sprite that shows where the
football will be thrown.

-   From the   
``||launcher:Launcher||``   
drawer, add a   
``||launcher:set sprite||``
``||variables(launcher):playerSprite||``
``||launcher:for player(1)||``   
block to the   
**bottom** of your   
``||loops(noclick):on start||``   
container.

Check the simulator to see the marker that has been added
to your player's sprite.

Want a different color? Add another block!

1.  From the   
``||launcher:Launcher||``   
drawer, add a   
``||launcher:set marker color for player (1) to ()||``
block to the   
**bottom** of your   
``||loops(noclick):on start||``   
container.
1.  Select a different color.

View the hint if you need any help.

```blockconfig.local
launcher.setPlayerSprite(playerSprite, 1)
```

```blocks
scene.setBackgroundImage(assets_launcher.field)
let playerSprite = sprites.create(assets_launcher.footballerRight0, SpriteKind.Player)
playerSprite.setPosition(10, 20)
// @highlight
launcher.setPlayerSprite(playerSprite, 1)
//@ highlight
launcher.setMarkerColor(1, 2)
```

## Finish @showdialog

Congratulations! You completed the scenery for your game.

Now, let's throw some footballs!

```ghost
scene.setBackgroundImage(assets_launcher.field)
let playerSprite = sprites.create(assets_launcher.footballerRight0, SpriteKind.Player)
playerSprite.setPosition(10, 20)
launcher.setPlayerSprite(playerSprite, 1)
launcher.setMarkerColor(1, 2)
```

```package
assets_launcher=github:brown-toy-box/assets_launcher
launcher=github:brown-toy-box/launcher
```