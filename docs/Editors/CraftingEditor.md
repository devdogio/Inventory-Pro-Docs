# Crafting Editor

The crafting manager has categories that allow you to create any time of “crafting”, be it cooking, blacksmithing or leatherworking. Let’s create a new category, and start to create some blueprints.

![](Assets/CraftingEditor.png)

## Crafting blueprints

1.  By default the result item’s name – the item received after a successful craft – will be used as the blueprint name, but you can of course, like always, configure this.
2.  The chance factor indicates how likely the craft is to succeed, a craft chance of 0.5 has a 50% chance, and a chance factor of 1.0 has 100% chance of succeeding.
    1.  The speedup factor goes paired with the crafting time duration, in many games ( like WoW ) crafting the same item becomes faster when creating an entire batch at once. For example when crafting 10 Rotten apple’s, the first item takes 5 seconds, the 2nd is 1.1 (10%) faster, which comes down to 5/(1.1^n).
3.  The required items indicate how many items are required to craft the given item, this is separate from the layouts, that can be defined at the bottom.

Once you’ve defined the blueprints you can create a standard or layout based crafting window to allow the user to craft the item in-game.

![](Assets/CraftingBlueprints.png)