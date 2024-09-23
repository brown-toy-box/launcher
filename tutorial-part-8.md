# Hit the target! Part 8

## Showdown! @showdialog

Let's add another player to the game!

## Advanced tutorial @showdialog

**Note**

This is an advanced tutorial.
We will describe the blocks that you will add to your project,
but the instructions do not walk you through every block that you need.

You can always view the hint to see the code that you are building.

Try building without the hints, though!

## Introducing Player 2!

First, we need to add a new sprite for the player.

1.  **Right after** the blocks in   
``||loops(noclick):on start||``   
that create the first player, insert a   
``||variables(sprites):set mySprite to||``
``||sprites:sprite [] of kind Player||``   
block to create a sprite for the second player.
1.  Give the sprite an appropriate name, like   
``||variables(noclick):p2Sprite||``
1.  Select an image for the player's sprite,
or create your own!
1.  Add blocks similar to those for the first player.
    -   Set Player 2's sprite to a location in the
    top-right of the field.
    -   Tell the game about the new sprite for Player 2.
    -   If you wish, change the marker color.

We also should give Player 2 their starting score.

-   **Right after** you give Player 1 their starting score of zero,
do the same for Player 2.

Check the simulator to make sure your new player appears
and that they have a score of zero.

View the hint if you need any help.

```blocks
let p1Sprite = sprites.create(assets_launcher.footballerRight0, SpriteKind.Player)
p1Sprite.setPosition(10, 20)
launcher.setPlayerSprite(p1Sprite, 1)
launcher.setMarkerColor(1, 2)
// @highlight
let p2Sprite = sprites.create(assets_launcher.footballerLeft2, SpriteKind.Player)
// @highlight
p2Sprite.setPosition(150, 20)
// @highlight
launcher.setPlayerSprite(p2Sprite, 2)
// @highlight
launcher.setMarkerColor(2, 8)
let targetSprite = sprites.create(assets_launcher.target0, SpriteKind.Target)
info.player1.setScore(0)
// @highlight
info.player2.setScore(0)
```

## Let's toss the ball around!

Now, let's get Player 2 throwing footballs!

1.  Find your   
``||controller(noclick):on player 1 A button pressed||``   
container.
1.  **Duplicate** the entire container.
1.  In the duplicate container,
change all of the blocks to use Player 2 instead.

Give it a try! See if your program allows Player 2 to throw footballs!

View the hint if you need any help.

~hint How do I play as Player 2?

-   You can control Player 2 with the keyboard.
    -   **U** is the **A** button.
    -   **O** is the **B** button.
-   If you have game controllers compatible with your computer,
then you can connect two controllers to play with two players.
(You need one controller for each player.)
-   You can control Player 2 from the multiplayer controls in the simulator.
    -   Now that we have activated multiplayer mode, you will see
    four new buttons next to the simulator that represent the players.
        -   Player 1 is **red**.
        -   Player 2 is **blue**.
        -   In fullscreen mode, these buttons appear below the screen.
    -   Select the **blue** avatar (the second one) to switch the controls
    to Player 2.   
    Notice the simulator changes color.
    -   The keys on the keyboard work the same as always.
    -   Select the **red** avatar (the first one) to switch back to Player 1.
    Notice again that the simulator changes color.

hint~

~hint How do I duplicate a block?

If your mouse has multiple buttons,
then you can **right-click** (or "alt-click")
on a block. From the menu that appears,
select **Duplicate**.

If your mouse only has one button,
then select the block. On your keyboard,
press **Ctrl+C** (on a Mac, press **Command+C**)
to copy the block, and then **Ctrl+V**
(or **Command+V**) to paste a duplicate
to your workspace.

hint~

## Changing directions

We need to let Player 2 change the direction of their throws.

1.  **Duplicate** your existing   
``||controller(noclick):on player 1 left button pressed||``   
container.
1.  Also duplicate your existing   
``||controller(noclick):on player 1 right button pressed||``   
container.
1.  Change the blocks in the new containers to use Player 2 instead.

Give it a try! See if your program allows Player 2 to throw footballs
in different directions!

**Note**: You might feel like the controls are backward for Player 2.
If you feel that way, swap them!

~hint How do I change directions for Player 2 with the keyboard?

-   **I** is the **up** button.
-   **J** is the **left** button.
-   **K** is the **down** button.
-   **L** is the **right** button.

hint~

View the hint if you need any help.

```blocks
controller.player2.onButtonEvent(ControllerButton.Left, ControllerButtonEvent.Pressed, function () {
    launcher.decreaseAngle(2)
})
controller.player2.onButtonEvent(ControllerButton.Right, ControllerButtonEvent.Pressed, function () {
    launcher.increaseAngle(2)
})
```

## Gimme some points!

Our final task is to give Player 2 points for hitting the target.

1.  **Duplicate** your existing   
``||sprites(noclick):on||``
``||variables(noclick):sprite||``
``||sprites(noclick):of kind P1Football overlaps||``
``||variables(noclick):otherSprite||``
``||sprites(noclick):of kind Target||``   
container.
1.  Switch all of the blocks to use Player 2 instead.
    -   **Remember** to switch the **sprite kind**   
    at the top of the block to   
    ``||sprites(noclick):P2Football||``!

Give it a try! See if your program allows Player 2 earns points for
hitting the target!

View the hint if you need any help.

```blocks
sprites.onOverlap(SpriteKind.P2Football, SpriteKind.Target, function (sprite, otherSprite) {
    sprites.destroy(sprite)
    info.player2.changeScoreBy(targetPoints)
    launcher.increaseTargetSpeed(otherSprite)
})
```

## Finish @showdialog

Good work! Now you can play with two players!

You can even play on separate computers over the Internet!
Details are in the leader guide.

Head to the last tutorial to have up to four players!

```template
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

```ghost
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

```package
assets_launcher=github:brown-toy-box/assets_launcher
launcher=github:brown-toy-box/launcher
```