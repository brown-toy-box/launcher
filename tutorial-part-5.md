# Hit the target! Part 5

## Penalty! @showdialog

Now, let's give the player some incentive to play wisely.

## That's a lot of footballs!

To earn a high score, some players will throw as many footballs
as possible. Let's penalize a player for each football thrown.

1.  Locate your   
``||controller(noclick):on A button pressed||``   
container.
1.  Inside that container, add a   
``||info:change score by (1)||``   
block.
1.  Change the value to **-1**,
which will decrease the score with each
football thrown.

Test your game to make sure the score decreases
each time a football is thrown.

View the hint if you need any help.

```block
controller.A.onEvent(ControllerButtonEvent.Pressed, function () {
    launcher.launchFootball(1)
    // @highlight
    info.changeScoreBy(-1)
})
```

## More points!

Now, we should give more points when hitting the target.

1.  Locate your   
``||sprites:on||``
``||variables(sprites):sprite||``
``||sprites:of kind P1Football overlaps||``
``||variables(sprites):otherSprite||``
``||sprites:of kind Target||``   
container.
1.  **Change** the number of points earned when hitting a target.   
What value makes sense to you?

Test your game and see if the value that you selected
makes sense for your game.

Feel free to try different values to see how the strategy changes.

View the hint if you need any help.

```blocks
sprites.onOverlap(SpriteKind.P1Football, SpriteKind.Target, function (sprite, otherSprite) {
    sprites.destroy(sprite)
    // @highlight
    info.changeScoreBy(3)
})
```

## Go faster!

We also can make the target faster whenever the player hits it.

1.  Add an   
``||launcher:increase speed for target ()||``   
block to your   
``||sprites(noclick):on overlap||``   
container.
1.  Drag an   
``||variables(noclick):otherSprite||``   
block from the top of your   
``||sprites(noclick):on overlap||``   
container into the empty spot in the   
``||launcher(noclick):increase speed for target ()||``   
block.

Play your game in the simulator and the target should speed up
each time you hit it!

View the hint if you need any help.

```blocks
sprites.onOverlap(SpriteKind.P1Football, SpriteKind.Target, function (sprite, otherSprite) {
    sprites.destroy(sprite)
    info.changeScoreBy(3)
    // @highlight
    launcher.increaseTargetSpeed(otherSprite)
})
```

## Finish @showdialog

Congratulations! You've made your game more challenging!

Now, let's have multiple rounds!

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

```ghost
controller.A.onEvent(ControllerButtonEvent.Pressed, function () {
    launcher.launchFootball(1)
    info.changeScoreBy(-1)
})
controller.left.onEvent(ControllerButtonEvent.Pressed, function () {
    launcher.increaseAngle(1)
})
controller.right.onEvent(ControllerButtonEvent.Pressed, function () {
    launcher.decreaseAngle(1)
})
sprites.onOverlap(SpriteKind.P1Football, SpriteKind.Target, function (sprite, otherSprite) {
    sprites.destroy(sprite)
    info.changeScoreBy(3)
    launcher.increaseTargetSpeed(otherSprite)
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