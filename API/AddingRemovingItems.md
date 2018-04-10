# Adding & Removing items

## Finding items

Before you can add an item to the inventory you’ll need to have a reference to it first. This can be a prefab reference in the Unity inspector, or you can dynamically fetch the object through code. For example, maybe you want to add an item with the name “Sword 123”, or grab an item with ID 6.  [How to find items?](http://devdog.io/unity-assets/inventory-pro/documentation/2.5p/api/finding-items)

## Adding an item to an inventory

To add an item to an inventory you can use the manager / facade to do so. The following code adds an item to a “loot to inventory”.

```csharp
InventoryItemBase myItem; // Assign object in Unity inspector.

InventoryManager.AddItem(myItem);  // Add the item to a collection, if it was already in a collection it will now be in both.
InventoryManager.AddItemAndRemove(item);  // Add the item to a collection and remove it from it's previous collection if it was in any.

```

It’s really that simple!

## Adding an item to a specific collection

You can also add an item to a specific  [collection](http://devdog.io/unity-assets/inventory-pro/documentation/api/collections) like the bank, a specific inventory, etc.

```csharp

ItemCollectionBase myCollection; // Define collection inside class, and assign it in the inspector.

myCollection.AddItem(item); // Add the item to a collection, if it was already in a collection it will now be in both (So be careful with this).
myCollection.AddItemAndRemove(item); // Add the item to a collection and remove it from it's previous collection if it was in any.

```

## Removing an item from an inventory

```csharp

InventoryManager.RemoveItem(myItem.ID, 1, false); // (0) ItemID, (1) Amount of items, (2) Also scan bank for item.

```

## Removing an item from a specific collection

Note that if you have only 3 items with the given ID in the collection, and you try to remove 5, no errors will be thrown and only 3 items will be removed. If you want to make sure the items you’re trying to remove are present use myCollection.GetItemCount(myItem.ID); to get the total amount of items in the collection first.

```csharp

ItemCollectionBase myCollection; // Define collection inside class, and assign it in the inspector.

uint itemsRemoved = myCollection.RemoveItem(myItem.ID, 1); // (0) ItemID, (1) Amount of items to remove

```

## Adding to a reference collection

When adding a reference to a reference collection make sure that the item you’re trying to add is already in another collection. In other words when setting an Apple in the skillbar make sure the Apple is already in the inventory.

```csharp

public InventoryItemBase item; // The item we wish to store
public ItemCollectionBase referenceCollection; // The reference collection to move it to

public void Start ()
{
    var storedItems = new List();
    bool added = InventoryManager.AddItem(item, storedItems); // Add the item to an inventory (loot to collection)
    if (added)
        storedItems.First().itemCollection.MoveItem (item, i.index, referenceCollection, 0, false); // Move the item to a reference collection, a reference doesn't destroy the item from it's original location.
}

```

## Removing from a reference collection

```csharp

referenceCollection.SetItem(0, null, true); // (0) Index in collection, (1) set it to null, (2) Do a repaint?, you'll likely want to set this to true.

```

## Setting an item in a specific slot

```csharp

referenceCollection.SetItem(slot, item, true); // (Make sure item is an instance object and not a prefab)

```

This does not call the collection's event such as OnAddedItem because you're adding the item directly to a specific slot. If you want to notify the collection you can do so by calling the Notify method.

```csharp

referenceCollection.NotifyItemAdded(item, 1, false); // Notify the collection that an item has been added. Only required when using SetItem() or when directly adding an item to a wrapper.

```