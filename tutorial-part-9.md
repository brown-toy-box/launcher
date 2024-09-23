# Hit the target! Part 9

## More players! @showdialog

Let's add the other two players to the game!

## Advanced tutorial @showdialog

**Note**

This is an advanced tutorial.
We will describe the blocks that you will add to your project,
but the instructions do not walk you through every block that you need.

## Lots more duplicating!

Now that you've added Player 2 to the game,
repeat the same process for the other two players!

Be sure to test your game after each of these tasks.

1.  Create and setup sprites for Players 3 and 4.
1.  Give Players 3 and 4 their starting scores.
1.  Allow Players 3 and 4 to throw footballs.
1.  Allow Players 3 and 4 to change direction.
1.  Give points to Players 3 and 4 when their footballs hit the target.

If you need help, then go back to the previous tutorial
for some reminders.

~hint How do I play as Players 3 and 4?

-   If you have game controllers compatible with your computer,
then you can connect four controllers to play with four players.
(You need one controller for each player.)
-   You can control Players 3 and 4 from the multiplayer controls in the simulator.
    -   Now that we have activated multiplayer mode, you will see
    four new buttons next to the simulator that represent the players.
        -   Player 1 is **red**.
        -   Player 2 is **blue**.
        -   Player 3 is **orange**.
        -   Player 4 is **green**.
        -   In fullscreen mode, these buttons appear below the screen.
    -   Select the **orange** avatar (the third one) to switch the controls
    to Player 3.   
    Notice the simulator changes color.
    -   Select the **green** avatar (the fourth one) to switch the controls
    to Player 4.
    -   The keys on the keyboard work the same as always.

hint~


## Finish @showdialog

Congratulations! You've built the advanced game!

Try to get the highest score! Compete with your family and friends!

Feel free to try these additional customizations.

-   Add even more rounds.
-   Try different velocities for the targets.
-   Randomize the velocities for some of the rounds.
-   Change the speed of the footballs each round.
-   Add more targets for some of the rounds.
-   Add sound effects.
-   Create your own images.

Have fun!

```template
controller.player1.onButtonEvent(ControllerButton.A, ControllerButtonEvent.Pressed, function () {
    launcher.launchFootball(1)
    info.player1.changeScoreBy(throwPoints)
})
controller.player2.onButtonEvent(ControllerButton.A, ControllerButtonEvent.Pressed, function () {
    launcher.launchFootball(2)
    info.player2.changeScoreBy(throwPoints)
})
controller.player1.onButtonEvent(ControllerButton.Left, ControllerButtonEvent.Pressed, function () {
    launcher.increaseAngle(1)
})
controller.player2.onButtonEvent(ControllerButton.Left, ControllerButtonEvent.Pressed, function () {
    launcher.decreaseAngle(2)
})
controller.player1.onButtonEvent(ControllerButton.Right, ControllerButtonEvent.Pressed, function () {
    launcher.decreaseAngle(1)
})
controller.player2.onButtonEvent(ControllerButton.Right, ControllerButtonEvent.Pressed, function () {
    launcher.increaseAngle(2)
})
sprites.onOverlap(SpriteKind.P1Football, SpriteKind.Target, function (sprite, otherSprite) {
    sprites.destroy(sprite)
    info.player1.changeScoreBy(targetPoints)
    launcher.increaseTargetSpeed(otherSprite)
})
sprites.onOverlap(SpriteKind.P2Football, SpriteKind.Target, function (sprite, otherSprite) {
    sprites.destroy(sprite)
    info.player2.changeScoreBy(targetPoints)
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
let p2Sprite = sprites.create(assets_launcher.footballerLeft2, SpriteKind.Player)
p2Sprite.setPosition(150, 20)
launcher.setPlayerSprite(p2Sprite, 2)
launcher.setMarkerColor(2, 8)
let targetSprite = sprites.create(assets_launcher.target0, SpriteKind.Target)
launcher.addTarget(targetSprite)
launcher.addRound(50, 0)
launcher.addRound(0, 50)
launcher.addRound(50, 5)
game.showLongText("Your instructions here!", DialogLayout.Bottom)
launcher.startNewRound()
info.player1.setScore(0)
info.player2.setScore(0)
targetPoints = 3
throwPoints = -1
game.splash("Round " + launcher.currentRound() + "!")
```

```ghost
controller.player1.onButtonEvent(ControllerButton.A, ControllerButtonEvent.Pressed, function () {
    launcher.launchFootball(1)
    info.player1.changeScoreBy(throwPoints)
})
controller.player2.onButtonEvent(ControllerButton.A, ControllerButtonEvent.Pressed, function () {
    launcher.launchFootball(2)
    info.player2.changeScoreBy(throwPoints)
})
controller.player3.onButtonEvent(ControllerButton.A, ControllerButtonEvent.Pressed, function () {
    launcher.launchFootball(3)
    info.player1.changeScoreBy(throwPoints)
})
controller.player4.onButtonEvent(ControllerButton.A, ControllerButtonEvent.Pressed, function () {
    launcher.launchFootball(4)
    info.player1.changeScoreBy(throwPoints)
})
controller.player1.onButtonEvent(ControllerButton.Left, ControllerButtonEvent.Pressed, function () {
    launcher.increaseAngle(1)
})
controller.player2.onButtonEvent(ControllerButton.Left, ControllerButtonEvent.Pressed, function () {
    launcher.decreaseAngle(2)
})
controller.player3.onButtonEvent(ControllerButton.Left, ControllerButtonEvent.Pressed, function () {
    launcher.increaseAngle(3)
})
controller.player4.onButtonEvent(ControllerButton.Left, ControllerButtonEvent.Pressed, function () {
    launcher.decreaseAngle(4)
})
controller.player1.onButtonEvent(ControllerButton.Right, ControllerButtonEvent.Pressed, function () {
    launcher.decreaseAngle(1)
})
controller.player2.onButtonEvent(ControllerButton.Right, ControllerButtonEvent.Pressed, function () {
    launcher.increaseAngle(2)
})
controller.player3.onButtonEvent(ControllerButton.Right, ControllerButtonEvent.Pressed, function () {
    launcher.decreaseAngle(3)
})
controller.player4.onButtonEvent(ControllerButton.Right, ControllerButtonEvent.Pressed, function () {
    launcher.decreaseAngle(4)
})
sprites.onOverlap(SpriteKind.P1Football, SpriteKind.Target, function (sprite, otherSprite) {
    sprites.destroy(sprite)
    info.player1.changeScoreBy(targetPoints)
    launcher.increaseTargetSpeed(otherSprite)
})
sprites.onOverlap(SpriteKind.P2Football, SpriteKind.Target, function (sprite, otherSprite) {
    sprites.destroy(sprite)
    info.player2.changeScoreBy(targetPoints)
    launcher.increaseTargetSpeed(otherSprite)
})
sprites.onOverlap(SpriteKind.P3Football, SpriteKind.Target, function (sprite, otherSprite) {
    sprites.destroy(sprite)
    info.player3.changeScoreBy(targetPoints)
    launcher.increaseTargetSpeed(otherSprite)
})
sprites.onOverlap(SpriteKind.P4Football, SpriteKind.Target, function (sprite, otherSprite) {
    sprites.destroy(sprite)
    info.player4.changeScoreBy(targetPoints)
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
let p2Sprite = sprites.create(assets_launcher.footballerLeft2, SpriteKind.Player)
p2Sprite.setPosition(150, 20)
launcher.setPlayerSprite(p2Sprite, 2)
launcher.setMarkerColor(2, 8)
let p3Sprite = sprites.create(assets_launcher.footballerRight1, SpriteKind.Player)
p3Sprite.setPosition(10, 110)
launcher.setPlayerSprite(p3Sprite, 3)
launcher.setMarkerColor(3, 4)
let p4Sprite = sprites.create(assets_launcher.footballerLeft3, SpriteKind.Player)
p4Sprite.setPosition(150, 110)
launcher.setPlayerSprite(p4Sprite, 4)
launcher.setMarkerColor(4, 11)
let targetSprite = sprites.create(assets_launcher.target0, SpriteKind.Target)
launcher.addTarget(targetSprite)
launcher.addRound(50, 0)
launcher.addRound(0, 50)
launcher.addRound(50, 5)
game.showLongText("Your instructions here!", DialogLayout.Bottom)
launcher.startNewRound()
info.player1.setScore(0)
info.player2.setScore(0)
info.player3.setScore(0)
info.player4.setScore(0)
targetPoints = 3
throwPoints = -1
game.splash("Round " + launcher.currentRound() + "!")
```

```package
assets_launcher=github:brown-toy-box/assets_launcher
launcher=github:brown-toy-box/launcher
```