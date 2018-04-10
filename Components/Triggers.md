# Triggers

<iframe width="560" height="315" src="https://www.youtube.com/embed/KJ1nP0Y6wDw" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen></iframe>

Triggers can be used to trigger a window and bound them to a location in the world. For example, when the player opens a bank it is done so at a specific location in your game. When the player walks away the bank window will auto. be closed and won't be able to be re-opened until the player is in range of the bank again.

!!! note
	The trigger distance can be managed in the general settings object.

- **Trigger mouse click** activates the window when the triggerer is clicked.
- **Trigger hover key code**  triggers the window when the object is in the center of the screen and the keycode is pressed (useful for first person games).
- **The animations and audio**  clips are for the object that triggers the window (such as a NPC), not the window itself.

**ITriggerInputHandler:** The Input handler is responsible for handling the input of the trigger. This allows you to replace just the input if you'd like to use your own system. If you're using an asset like Rewired you can simply swap out the input handler for a rewired input handler, and voila, the trigger is now using rewired's input system.

**ITriggerRangeHandler:** The range handler handles the range for this trigger. When none is set the player's range handler is used by default. If you'd like to create an object which has a different range than the global use distance (the distance your player's trigger is using), you can do so by adding the TriggerRangeHandler and specifying the use distance on the newly added component.

**Note:** **you don't have to use a trigger range handler on a component, by default your player's range handler is used.**

![](Assets/Trigger.png)

## Integrating triggers

Triggers can of course be re-used for other aspects of your game. In many cases you'll want to receive a callback when a trigger is used or unused; This can be done using the  [trigger callbacks interface.](TriggerCallbacks.md)