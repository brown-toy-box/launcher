# Hit the target! Part 7

## Get ready! @showdialog

Let's get your game ready for multiplayer!

## Advanced tutorial @showdialog

**Note**

This is an advanced tutorial.
We will describe the blocks that you will add to your project,
but the instructions do not walk you through every block that you need.

You can always view the hint to see the code that you are building.

Try building without the hints, though!

## Use good variable names!

Since we're going to have multiple players,
we should use a better name for our player's sprite.

1.  Find a block in your   
``||loops(noclick):on start||``   
container that uses the   
``||variables(noclick):playerSprite||``   
variable.
1.  Rename the variable to   
``||variables(noclick):p1Sprite||``.

~hint How do I rename a variable?

1.  Select any of the ``||variables(noclick):playerSprite||``
blocks. A menu appears.
1.  Near the bottom of the menu, select   
**Rename variable...**
1.  Enter the new name,   
**p1Sprite**.
1.  Select the **Ok** button.

hint~

## How many points?

Let's add some variables to make your game easy to change later.

1.  Create two variables:
    -   ``||variables(noclick):throwPoints||``
    -   ``||variables(noclick):targetPoints||``
1.  In your   
``||loops(noclick):on start||``   
container, add blocks from the   
``||variables:Variables||``   
drawer for your new variables.
    -   The ``||variables:throwPoints||`` variable
    holds the change to the player's score when they   
    **throw a football**. Set it to **-1**.
    -   The ``||variables:targetPoints||`` variable
    holds the change to the player's score when they   
    **hit a target**. Set it appropriately for your game.
1.  Use your new variables in the other blocks where appropriate.

View the hint if you need any help.

```blocks
controller.player1.onButtonEvent(ControllerButton.A, ControllerButtonEvent.Pressed, function () {
    launcher.launchFootball(1)
    // @highlight
    info.changeScoreBy(throwPoints)
})
sprites.onOverlap(SpriteKind.P1Football, SpriteKind.Target, function (sprite, otherSprite) {
    sprites.destroy(sprite)
    // @highlight
    info.changeScoreBy(targetPoints)
    launcher.increaseTargetSpeed(otherSprite)
})
let throwPoints = 0
let targetPoints = 0
targetPoints = 3
throwPoints = -1
```

## Changing blocks!

Now, we need to swap out the single-player blocks for their
multiplayer versions.

1.  Find your   
``||info(noclick):set score to (0)||``   
block in your   
``||loops(noclick):on start||``   
container.
1.  Exchange it for the   
``||info:set player 2 score to (0)||``   
block.
1.  In the new block, switch to player **1**.

Now, do the same thing for the   
``||info:change score by (1)||``   
blocks. Be sure to use your variables in the new blocks!

Lastly, swap out the controller blocks with the
multiplayer versions.

For example, instead of the  
``||controller(noclick):on A button pressed||``   
block, use the   
``||controller:on player 2 A button pressed||``.

Play your game in the simulator to make sure
**nothing has changed**.

View the hint for examples of the multiplayer blocks.

```block
let throwPoints = 0
controller.player1.onButtonEvent(ControllerButton.A, ControllerButtonEvent.Pressed, function () {
    launcher.launchFootball(1)
    info.player1.changeScoreBy(throwPoints)
})
```

## Finish @showdialog

Good work! Nothing has changed in your gameplay,
but now we're ready to add multiple players!

```template
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
info.onCountdownEnd(function () {
    if (launcher.currentRound() == launcher.numRounds()) {
        game.setGameOverEffect(true, effects.confetti)
        game.gameOver(true)
    } else {
        launcher.startNewRound()
        game.splash("Round " + launcher.currentRound() + "!")
    }
})
scene.setBackgroundImage(assets_launcher.field)
let playerSprite = sprites.create(assets_launcher.footballerRight0, SpriteKind.Player)
playerSprite.setPosition(10, 20)
launcher.setPlayerSprite(playerSprite, 1)
launcher.setMarkerColor(1, 2)
let targetSprite = sprites.create(assets_launcher.target0, SpriteKind.Target)
launcher.addTarget(targetSprite)
launcher.addRound(50, 0)
launcher.addRound(0, 50)
launcher.addRound(50, 5)
game.showLongText("Your instructions here!", DialogLayout.Bottom)
launcher.startNewRound()
info.setScore(0)
game.splash("Round " + launcher.currentRound() + "!")
```

```ghost
controller.player1.onButtonEvent(ControllerButton.A, ControllerButtonEvent.Pressed, function () {
    launcher.launchFootball(1)
    info.player1.changeScoreBy(throwPoints)
})
controller.player1.onButtonEvent(ControllerButton.Left, ControllerButtonEvent.Pressed, function () {
    launcher.increaseAngle(1)
})
controller.player1.onButtonEvent(ControllerButton.Right, ControllerButtonEvent.Pressed, function () {
    launcher.decreaseAngle(1)
})
sprites.onOverlap(SpriteKind.P1Football, SpriteKind.Target, function (sprite, otherSprite) {
    sprites.destroy(sprite)
    info.player1.changeScoreBy(targetPoints)
    launcher.increaseTargetSpeed(otherSprite)
})
info.onCountdownEnd(function () {
    if (launcher.currentRound() == launcher.numRounds()) {
        game.setGameOverEffect(true, effects.confetti)
        game.gameOver(true)
    } else {
        launcher.startNewRound()
        game.splash("Round " + launcher.currentRound() + "!")
    }
})
let throwPoints = 0
let targetPoints = 0
scene.setBackgroundImage(assets_launcher.field)
let p1Sprite = sprites.create(assets_launcher.footballerRight0, SpriteKind.Player)
p1Sprite.setPosition(10, 20)
launcher.setPlayerSprite(p1Sprite, 1)
launcher.setMarkerColor(1, 2)
let targetSprite = sprites.create(assets_launcher.target0, SpriteKind.Target)
launcher.addTarget(targetSprite)
launcher.addRound(50, 0)
launcher.addRound(0, 50)
launcher.addRound(50, 5)
game.showLongText("Your instructions here!", DialogLayout.Bottom)
launcher.startNewRound()
info.player1.setScore(0)
targetPoints = 3
throwPoints = -1
game.splash("Round " + launcher.currentRound() + "!")
```

```package
assets_launcher=github:brown-toy-box/assets_launcher
launcher=github:brown-toy-box/launcher
```