# Hit the target! Part 2

## Let's throw some footballs! @showdialog

In this tutorial, the player will throw some footballs!

## Throw the ball!

Let's throw a football whenever the player presses **A**.

1.  From the   
``||controller:Controller||``   
drawer, add an   
``||controller:on A button pressed||``   
container to your workspace.
1.  Inside the new container, add a   
``||launcher:launch football for player (1)||``   
block from the   
``||launcher:Launcher||``   
drawer.

Try it in the simulator!
When you press **A**,
the player should throw a football in the same
direction as the marker.

View the hint if you need any help.

```block
controller.A.onEvent(ControllerButtonEvent.Pressed, function () {
    launcher.launchFootball(1)
})
```

## Where are you throwing?

Now, let's allow the player to change the direction of the marker.

1.  From the   
``||controller:Controller||``   
drawer, add an   
``||controller:on left button pressed||``   
container to your workspace.
1.  Inside the new container, add an   
``||launcher:increase angle for player (1)||``   
block from the   
``||launcher:Launcher||``   
drawer.

That takes care of the **left** button.
What about **right**?

1.  Add **another**   
``||controller:on left button pressed||``   
container to your workspace.
1.  Use the dropdown to change the button name to   
**right**.
1.  Inside the new container, add a   
``||launcher:decrease angle for player (1)||``   
block from the   
``||launcher:Launcher||``   
drawer.

Try it in the simulator!
When you press **left** and **right**,
the marker should change direction.
Try throwing some footballs, too!

View the hint if you need any help.

```blockconfig.local
controller.left.onEvent(ControllerButtonEvent.Pressed, function () {

})
```

```blocks
controller.left.onEvent(ControllerButtonEvent.Pressed, function () {
    launcher.increaseAngle(1)
})
controller.right.onEvent(ControllerButtonEvent.Pressed, function () {
    launcher.decreaseAngle(1)
})
```

## Finish @showdialog

Congratulations! Your player can now aim and throw footballs!

Now, let's add a target for the player to hit!

```template
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
```

```package
assets_launcher=github:brown-toy-box/assets_launcher
launcher=github:brown-toy-box/launcher
```