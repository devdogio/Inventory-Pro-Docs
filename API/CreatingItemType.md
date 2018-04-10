# Creating a custom item type

When creating a new item type, we always start by extending from a base class, when creating a custom consumable I suggest starting from the InventoryItemBase, when creating a custom equippable item I suggest extending from the EquippableInventoryItem, as the Equippable has a lot of basic features for handling the equipment.

## Creating a new type

```csharp
public class MyAwesomeInventoryItemType : InventoryItemBase
{
    public float failFactor = 0.5f; // 0.0f is always success, 1.0f is always failure, 0.5f is 50% chance.

    public override int Use()
    {
        int used = base.Use();
        if (used < 0) // Whoops! Anything below 0 is a failed action.
            return used;

        // Do something specific...

        // 50% chance.
        if (Random.value < failFactor)
        {
            currentStackSize--;
            NotifyItemUsed(1, true);
            return 1; // No need to worry about anything else, the stack will be removed if no objects are left.
        }

        NotifyItemUsed(0, true);
        return 0; // 1, the item was used, but no items were used (stack decrease) in the process
    }
}
```

### How the code works

First we extend from the InventoryItemBase as just explained. This will give us basic functionality and makes it usable in all editors.

Next we’ll override the Use() method. The Use() method is invoked when the user right clicks it in their inventory, uses the context menu -> use or is invoked through code. Here we’ll write the “functionality” of this item, as an example I’ve created an item that has 50% chance of breaking when used.

This little bit of code, triggers the base (InventoryItemBase) code, which handles cooldowns, if base.Use() returns anything lower than 0 the using failed, and the item cannot be used.

```csharp
int used = base.Use();
if (used < 0) // Whoops! Anything below 0 is a failed action.
{
	return used;
}
```

When our item breaks (50% chance) we need to decrease the stack size, after all we lost 1 item. We do this by calling currentStackSize– to reduce the stack by one.

!!! note
	If the stack size becomes less than 1 the system will automatically remove the item from your inventory and cleanup the stack.**

Once the item is used a Notify is required to let the item know we succeeded in using the item. Send the amount of item that we’re used in the process as a first parameter, like below.

```csharp
NotifyItemUsed(1, true); // The 2nd parameter also notifies the collection. You'll almost always want to pass true, unless your object changes collection whenever used, then the collection will have to be notified manually.
```

!!! note
	When creating an equippable item type don't forget to add your type to the CharacterUI's collection filters, to allow it to be equipped.

## InfoBox (Tooltip)

We can also show custom information in the Tooltip / InfoBox (when the user hovers over the item). We can do so by overriding the GetInfo() method.

```csharp
public override LinkedList
```