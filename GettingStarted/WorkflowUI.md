# Workflow UI

<iframe width="560" height="315" src="https://www.youtube.com/embed/sSy7s3cEnBQ" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen></iframe>

## UIWindow

The UI Window is responsible for the management of windows as well as animating them. Optionally you can define a key combination to trigger the window, for example “i” to open the Inventory window.

When assigning animations, don’t forget the controller on the Animator component.

## Draggable windows

And last but not least, we can also make our windows draggable, simply go to Add component/InventorySystem/UI Helpers/Draggable window.

And that’s all there’s to it, we should now a have working Inventory, but no items yet, so for the next chapter we’ll dive into the item creator for a bit.

## Positioning your windows

When the game starts windows are reset to position 0,0. It does this to allow you to design windows outside the viewport, so that you don’t have to throw them on 1 large pile inside the viewport.

You can manipulate the window’s position using the pivot x and y coordinates.A X pivot of 1.1 means 10% offset on the right side of the window. While -0.1 would mean 10% offset on the left.