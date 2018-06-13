# Collection sorting

By default the “BasicCollectionSorter” is used for sorting a collection. Of course this is customizable. At the bottom of the default sorter you’ll find the actual ordering by type name, then by category name and lastly by item name.

I Advice you not to modify this file, an update will overwrite your changes. Check below on how to create your own sorter.

```csharp
public IList Sort(IList items)
{
    /// ... (removed some code for clarity)

    // Orders by category.ID but can easilly be switched to anything else.
    // Simply change o => o.category.ID to any object variable to sort by.
    // For example: o => o.buyPrice will sort items based on the buying price.
    // Another examlpe: o => o.name will sort items on an alphabetical order.
    // If you want to go wild you can chain OrderBy's this allows you to filter on the first category first (for example category), then rarity. (check uncommented line below)
    return sortedList.OrderBy(o => o.GetType().Name).ThenBy(o => o.category.ID).ThenBy(o => o.name).ToArray(); // Order by and return
    //return sortedList.OrderBy(o => o.category.ID).ThenBy(o => o.rarity.ID).ToArray(); // Order by and return      
}

```

## Creating a new sorting class

Create a new script **outside of the Devdog/InventoryPro folder**, and copy the content of the BasicCollectionSorter. Modify it to your liking (little example below). Example of optional sorting, sorts by category, then rarity:

```csharp
[CreateAssetMenu(menuName = InventoryPro.CreateAssetMenuPath + "Basic Collection Sorter")]
public class MyCollectionSorter : CollectionSorterBase
{
    public IList<InventoryItemBase> Sort(IList items)
    {
        // ... (removed some code for clarity)
        return sortedList.OrderBy(o => o.category.ID).ThenBy(o => o.rarity.ID).ToArray(); // Order by and return        
    }
}
```

Only 1 thing remaining, we need to let the system know which sorter to use. Next, create a new scriptable object asset from your own created type, and assign it in the settings.