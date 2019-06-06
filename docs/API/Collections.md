# Collections

All windows containing items are collections, for example, the inventory, bank, vendor, loot window, etc. Each collection has a set of methods to modify its contents. Items can be added through AddItem(item), removed with RemoveItem(item), and so forth.

When creating your own collection you can override each of these behaviors and tailor them to your need. Collections contain an array of ICollectionItem objects, which in turn contain the items. These "wrappers" are the slots you see in the interface.

```csharp
// This does the same as myCollectionItem.item.Use(), but allows for UI specific control through the ICollectionItem.
myCollectionItem.TriggerUse(); // Uses the item through the wrapper.

if(myCollectionItem.item != null)
{
    myCollectionItem.item.Use(); // Example, use the item directly.
}

```

## Custom collection

Creating a custom collection is a simple process. Simply create a new class and implement the ItemCollectionBase class. Almost all ItemCollectionBase's methods are marked virtual, allowing you, the developer, to override their behavior.

```csharp
[RequireComponent(typeof(UIWindow))] // Require a UIWindow to show the actual collection.
public class MyCustomCollection : ItemCollectionBase
{
    public override void Awake()
    {
        base.Awake();

        // Custom initialization code
    }

    public override bool CanSetItem(uint slot, InventoryItemBase item)
    {
        // Add custom set behavior (check types, categories, etc).

        return base.CanSetItem(slot, item);
    }
}

```

### Currency

To add currency to an inventory you can use the manager / facade to do so. The following code adds an item to a loot to inventory.

```csharp
InventoryManager.AddCurrency(currencyID, myAmount);  // Add currency to an inventory. currencyID:uint (ID of the currency as defined in editor), myAmount: float.

```

#### Adding currency to a specific collection

You can also add currency to a specific ollection like the bank, a specific inventory, etc.

```csharp
ItemCollectionBase myCollection; // Define collection inside class, and assign it in the inspector.

myCollection.AddCurrency(currencyID, myAmount);

```

#### Removing currency from an inventory

The following code removes currency from a loot to inventory.

```csharp
bool currencyRemoved = InventoryManager.RemoveCurrency(currencyID, myAmount); // Removes the amount of given currencyID. This will auto. convert currencies. For example if you have gold (which is worth 100 silver), and there isn't enough silver available, it will be re-supplied using gold. (This behavior can be defined inside the editors).

```

#### Removing currency from a collection

```csharp
ItemCollectionBase myCollection; // Define collection inside class, and assign it in the inspector.

bool currencyRemoved = myCollection.RemoveCurrency(currencyID, myAmount);

```

### Tips and tricks

A guide on how to [find items in any collection.](FindingItems.md)

#### Get item count in collection

```csharp
    /// Counting
    uint amount = myCollection.GetItemCount(myItem.ID); // Combines all stacks and gets the total count of the given item. Useful when you want to know exactly how many items of the given ID there are in the collection.

```

#### Counting empty slots

```csharp
myCollection.GetEmptySlotsCount(); // Returns the amount of empty slots.

```

#### Get the total weight of all items in a collection

```csharp
float weight = myCollection.GetWeight(); // Get the weight of all items in this collection combined.
```

### Get the total weight of all items in the player's inventory

```csharp
float sumWeight = 0.0f;
foreach (var col in InventoryManager.GetLootToCollections())
    sumWeight += col.GetWeight();
```

### Get the total weight of all items equipped by the player

```csharp
float sumWeight = 0.0f;
foreach (var col in InventoryManager.GetEquipToCollections())
    sumWeight += col.GetWeight();
```

The total weight that the player carries is the sum of the weight of `GetLootToCollections` and `GetEquipToCollections`

#### Get the item in a specific slot

```csharp
var slot = myCollection[index];

if(slot != null) //the slot is not empty
{
   var item = slot.item;
}
```
