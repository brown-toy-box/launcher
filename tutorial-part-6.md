# Hit the target! Part 6

## Encore! @showdialog

Now, let's have multiple rounds in the game.

## Extra rounds!

Let's tell the game about our new rounds.

1.  Locate your   
``||loops(noclick):on start||``   
container.
1.  Find your   
``||launcher(noclick):add round with target vx (50) vy (0)||``   
block.
1.  Add more
``||launcher(noclick):add round with target vx (50) vy (0)||``   
blocks with   
**different** values for   
**vx** and **vy**.

Each time you add a block, you add another round to the game.

Now that we have told the game about the rounds, we need to run them!

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
launcher.addRound(0, 50)
// @highlight
launcher.addRound(50, 5)
game.showLongText("Your instructions here!", DialogLayout.Bottom)
launcher.startNewRound()
info.setScore(0)
```

## Next round!

Our code is in good shape!

We just need to start a new round when the timer ends.

1.  Add an   
``||info:on countdown end||``   
block to your workspace.
1.  Inside the new container, add an   
``||logic:if (true) then [] else []||``   
block.
1.  Use blocks from the   
``||logic:Logic||`` and the   
``||launcher:Launcher||`` drawer
so the ``||logic(noclick):if||`` block says this:
    -   ``||logic(noclick):if||``
    ``||launcher:get current round||``
    ``||logic:=||``
    ``||launcher:number of rounds||``
    ``||logic(noclick):then||``

If we have played all of the rounds, then we should end the game.   

-   Add a
``||game:game over||`` ``||loops(game):win||``   
block to the correct branch of the   
``||logic(noclick):if||`` block.
-   Feel free to use add an effect to the game over screen.

If we have not played all of the rounds, then we should start the next one.

-   Add a   
``||launcher:start new round||``   
block to the correct branch of the   
``||logic(noclick):if||`` block.

Test your game in the simulator to see if you can play multiple rounds!

View the hint if you need any help.

```block
info.onCountdownEnd(function () {
    if (launcher.currentRound() == launcher.numRounds()) {
        game.setGameOverEffect(true, effects.confetti)
        game.gameOver(true)
    } else {
        launcher.startNewRound()
    }
})
```

## Which round is it?

We should display a message before the round starts
so that players can get ready.

1.  To the **bottom** of your   
``||loops(noclic):on start||``   
block, add a   
``||game:splash ("")||``   
block.
1.  Use a   
``||text:join||`` **join**   
block from the   
``||text:Text||`` **Text**   
drawer with a   
``||launcher:get current round||``   
block to display a message
like "Round 1!"

Test your game to make sure the message appears
at the start of the game.

1.  Make a duplicate of the   
``||game(noclick):splash ("")||``   
block that you just created.
1.  Add the new block to the appropriate place
in your   
``||info(noclick):on countdown end||``   
container.

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

View the hint if you need any help.

```block
info.onCountdownEnd(function () {
    if (launcher.currentRound() == launcher.numRounds()) {
        game.setGameOverEffect(true, effects.confetti)
        game.gameOver(true)
    } else {
        launcher.startNewRound()
        // @highlight
        game.splash("Round " + launcher.currentRound() + "!")
    }
})
```

## Finish @showdialog

Congratulations! You've built the intermediate game!

Try to get the highest score!

Feel free to try these additional customizations.

-   Add even more rounds.
-   Try different velocities for the targets.
-   Change the speed of the footballs each round.
-   Add more targets for some of the rounds.
-   Create your own images.

There are additional tutorials in the skillmap that enhance your game even further.

Have fun!

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

```package
assets_launcher=github:brown-toy-box/assets_launcher
launcher=github:brown-toy-box/launcher
```