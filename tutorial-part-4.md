# Hit the target! Part 4

## Points! @showdialog

Now, let's give the player some points for hitting the target.

## What do I do?

First, let's give the player some instructions on how to play.

1.  Locate your   
``||loops(noclick):on start||``   
container.
1.  **Just above** the   
``||launcher(noclick):start new round||``   
block, add a   
``||game:show long text () bottom||``   
block from the   
``||game:Game||``   
drawer.
1.  In the new block, type some instructions for the player
so that they know how to play.

View the hint if you need any help.

```blocks
scene.setBackgroundImage(assets_launcher.field)
let playerSprite = sprites.create(assets_launcher.footballerRight0, SpriteKind.Player)
playerSprite.setPosition(10, 20)
launcher.setPlayerSprite(playerSprite, 1)
launcher.setMarkerColor(1, 2)
let targetSprite = sprites.create(assets_launcher.target0, SpriteKind.Target)
launcher.addTarget(targetSprite)
launcher.addRound(50, 0)
// @highlight
game.showLongText("Your instructions here!", DialogLayout.Bottom)
launcher.startNewRound()
```

## I hit it!

Now, let's give the player some points when they hit the target.

1.  Add a   
``||info:set score to (0)||``   
block from the   
``||info:Info||``   
drawer to your   
``||loops(noclick):on start||``   
container.
1.  From the   
``||sprites:Sprites||``   
drawer, add an   
``||sprites:on||``
``||variables(sprites):sprite||``
``||sprites:of kind P1Football overlaps||``
``||variables(sprites):otherSprite||``
``||sprites:of kind Target||``   
container to your workspace.
1.  Inside this new container, add these blocks:
    -   ``||sprites:destroy||`` ``||variables(sprites):sprite||``
    -   ``||info:change score by (1)||``

Play your game in the simulator.
You should get points each time you hit the target!

View the hint if you need any help.

```blockconfig.local
sprites.onOverlap(SpriteKind.P1Football, SpriteKind.Target, function (sprite, otherSprite) {

})
sprites.destroy(sprite)
```

```block
sprites.onOverlap(SpriteKind.P1Football, SpriteKind.Target, function (sprite, otherSprite) {
    sprites.destroy(sprite)
    info.changeScoreBy(1)
})
```

## Finish @showdialog

Congratulations! You have completed the introductory game!

How many points can you get?

There are additional tutorials in the skillmap that can enhance your game.

Have fun!

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
let targetSprite = sprites.create(assets_launcher.target0, SpriteKind.Target)
launcher.addTarget(targetSprite)
launcher.addRound(50, 0)
launcher.startNewRound()
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
sprites.onOverlap(SpriteKind.P1Football, SpriteKind.Target, function (sprite, otherSprite) {
    sprites.destroy(sprite)
    info.changeScoreBy(1)
})
scene.setBackgroundImage(assets_launcher.field)
let playerSprite = sprites.create(assets_launcher.footballerRight0, SpriteKind.Player)
playerSprite.setPosition(10, 20)
launcher.setPlayerSprite(playerSprite, 1)
launcher.setMarkerColor(1, 2)
let targetSprite = sprites.create(assets_launcher.target0, SpriteKind.Target)
launcher.addTarget(targetSprite)
launcher.addRound(50, 0)
game.showLongText("Your instructions here!", DialogLayout.Bottom)
launcher.startNewRound()
info.setScore(0)
```

```package
assets_launcher=github:brown-toy-box/assets_launcher
launcher=github:brown-toy-box/launcher
```