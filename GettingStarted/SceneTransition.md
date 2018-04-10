# Scene Transition

When moving between scenes there are a few solutions to keep your player data.

1. You can place a "DontDestroyOnLoad" component to the _Managers object, the Player and the Canvas. This will prevent the objects from being destroyed between scene loads and will keep all your player and inventory data.

2. Another option would be to create a 2nd scene that contains your player data (_Manager, Player and Canvas), and never unload this scene. As of Unity 5.4 it's possible to load multiple scenes at once, so you can utilise 1 for all the player data.

3. And the last option would be to save all data, destroy it, load the next scene and load all data back into memory. Although this is an option I personally don't prefer to use it, as you're just re-creating everything you just threw away a second ago.  [More about saving and loading.](http://devdog.io/unity-assets/inventory-pro/documentation/2.5p/components/saving-and-loading)

Generally, option 1 or option 2 are recommended, as they're the fastest, safest, and generally easiest to implement.