# Lootables and generators

Assume you want to create a lootable corpse, after you’ve killed a badass monster, well, then this tutorial is for you.

## First things first:

The loot window can be accessed using the InventoryManager’s singleton (see code below).

```csharp
InventoryManager.instance.loot.SetItems(myItems); // Set a bunch of items in the loot window
```

The code above will set the items in the loot window, note that if there were already items in the window, they’ll now be removed and replaced with the new items. So be careful, you’ve been warned.

## Generating some random loot

To generate items there’s a basic item generator that handles the standard types and considers it’s fields, called the BasicItemGenerator. The basic item generator generates items based on a fixed set that you can supply, so for example:

```csharp
var generator = new BasicItemGenerator();
generator.SetItems(ItemManager.database.items); // Consider all items when generating our loot 
generator.minRequiredLevel = 5; // Minimal level of generates items has to be 5. 
var myLoot = generator.Generate(2,4); // Generate 2 to 4 items, note that there's also .Generate(count); for a fixed amount
```

## Setting the items in the loot window

Next you can set the loot in the loot window using the following code:

```csharp
InventoryManager.instance.loot.SetItems(myLoot); // Set a bunch of items in the loot window
```

## Solving infinite loot

Alright, almost done , note that when looting an item from the loot window, it won’t actually be removed from the actual location, the corpse. So when the user would loot some items, close the window, and try to loot again, the system would call SetItems(myLoot) again, and you’d have infinite loot. To solve this problem, you can use the LootWindow’s events, such as OnRemovedItem, when the item is removed from the loot window (aka looted), you can also remove it from the original location, the corpse.

```csharp
public InventoryItemBase[] myGeneratedItems;

public void Start()
{
    InventoryManager.instance.loot.OnRemovedItem += OnRemovedItem;

    var generator = new BasicItemGenerator(); 
    generator.SetItems(ItemManager.database.items); // Consider all items when generating our loot
    generator.minRequiredLevel = 5; // Minimal level of generates items has to be 5.
    myGeneratedItems = generator.Generate(2,4); // Generate 2 to 4 items, note that there's also .Generate(count); for a fixed amount
}

public void OnDestroy()
{
    InventoryManager.instance.loot.OnRemovedItem -= OnRemovedItem;
}

private void OnRemovedItem(InventoryItemBase item, uint itemID, uint slot, uint amount)
{
    myGeneratedItems[slot] = null; // Setting to null fine, you're also allowed to remove it from the array if you prefer. Keep in mind that if you remove the item from the array, the slot (index) will change, and you have to re-call .SetItems() on the loot window.
}
```