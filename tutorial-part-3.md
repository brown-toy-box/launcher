# Hit the target! Part 3

## Did I hit it? @showdialog

Now, let's add a target that the player should try to hit.

## Bullseye!

Let's add a sprite for the target.

1.  To the **bottom**   
of your   
``||loops(noclick):on start||``   
container, add a   
``||variables(sprites):set targetSprite to||``
``||sprites:sprite [] of kind Target||``   
block.
1.  Select an image from the gallery.
We have provided two targets for you.
Feel free to draw your own!

Nice! Now we have a target for the player.

View the hint if you need any help.

```blockconfig.local
let targetSprite = sprites.create(img`.`, SpriteKind.Target)
```

```blocks
scene.setBackgroundImage(assets_launcher.field)
let playerSprite = sprites.create(assets_launcher.footballerRight0, SpriteKind.Player)
playerSprite.setPosition(10, 20)
launcher.setPlayerSprite(playerSprite, 1)
launcher.setMarkerColor(1, 2)
// @highlight
let targetSprite = sprites.create(assets_launcher.target0, SpriteKind.Target)
```

## Get moving!

Now, let's get the target moving!

-   To the **bottom**   
of your   
``||loops(noclick):on start||``   
container, add these blocks
from the   
``||launcher(noclick):Launcher||``   
drawer:
    1.  ``||launcher:add target||`` ``||variables(launcher):targetSprite||``
    1.  ``||launcher:add round with target vx (50) vy (0)||``
    1.  ``||launcher:start new round||``

Check the simulator to see that target move
up and down the field!

Try different numbers for **vx** and **vy**.
See how you can make the target move differently!

View the hint if you need any help.

```blockconfig.local
launcher.addTarget(targetSprite)
launcher.addRound(50, 0)
```

```blocks
scene.setBackgroundImage(assets_launcher.field)
let playerSprite = sprites.create(assets_launcher.footballerRight0, SpriteKind.Player)
playerSprite.setPosition(10, 20)
launcher.setPlayerSprite(playerSprite, 1)
launcher.setMarkerColor(1, 2)
let targetSprite = sprites.create(assets_launcher.target0, SpriteKind.Target)
// @highlight
launcher.addTarget(targetSprite)
// @highlight
launcher.addRound(50, 0)
// @highlight
launcher.startNewRound()
```

## Finish @showdialog

Congratulations! You now have a target that the player can hit!

Now, let's give the player some points for hitting the target!

```template
controller.A.onEvent(ControllerButtonEvent.Pressed, function () {
    launcher.launchFootball(1)
})
controller.left.onEvent(ControllerButtonEvent.Pressed, function () {
    launcher.increaseAngle(1)
})
controller.right.onEvent(ControllerButtonEvent.Pressed, function () {
    launcher.decreaseAngle(1)
})
scene.setBackgroundImage(assets_launcher.field)
let playerSprite = sprites.create(assets_launcher.footballerRight0, SpriteKind.Player)
playerSprite.setPosition(10, 20)
launcher.setPlayerSprite(playerSprite, 1)
launcher.setMarkerColor(1, 2)
```

```ghost
controller.A.onEvent(ControllerButtonEvent.Pressed, function () {
    launcher.launchFootball(1)
})
controller.left.onEvent(ControllerButtonEvent.Pressed, function () {
    launcher.increaseAngle(1)
})
controller.right.onEvent(ControllerButtonEvent.Pressed, function () {
    launcher.decreaseAngle(1)
})
scene.setBackgroundImage(assets_launcher.field)
let playerSprite = sprites.create(assets_launcher.footballerRight0, SpriteKind.Player)
playerSprite.setPosition(10, 20)
launcher.setPlayerSprite(playerSprite, 1)
launcher.setMarkerColor(1, 2)
let targetSprite = sprites.create(assets_launcher.target0, SpriteKind.Target)
launcher.addTarget(targetSprite)
launcher.addRound(50, 0)
launcher.startNewRound()
```

```package
assets_launcher=github:brown-toy-box/assets_launcher
launcher=github:brown-toy-box/launcher
```