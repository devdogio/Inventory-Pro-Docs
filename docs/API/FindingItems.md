# Finding items

!!! warning
	Find methods are (O(N) performance)

## By ID

Items inside the ItemDatabase are sorted by ID and can be accessed using their ID. Random access is very in-expensive and performs very quickly.

```csharp
var itemWithID = ItemManager.database.items[itemID];
```

## Find by name

ItemManager.instance.items.FirstOrDefault(o => o.name == "Sword 123"); [su_note note_color="#EFEFEF" radius="2"]Items grabbed from the ItemManager.instance.items are prefabs and not instance objects. Before using  [instantiate the object](http://docs.unity3d.com/ScriptReference/Object.Instantiate.html).[/su_note]

## Find in a collection

You can very easily find any item in your collection, either by using the item’s ID, category or even use LINQ (see below).

```csharp
ItemCollectionBase myCollection;
 
public void Start()
{
    /// By ID
    var ofID = myCollection.Find(myItem.ID); // Search for a specific item, returns first object found, or null if none found.
    var allOfID = myCollection.FindAll(myItem.ID); // Returns an array of all items found.
    
    /// By Category
    var ofCategory = myCollection.FindByCategory(myItem.category.ID); // Find first item of a certain category.
    var allOfCategory = myCollection.FindAllByCategory(myItem.category.ID); // Find all items of a certain category.
}
```

## LINQ

Linq is amazing, and I would encourage anyone to use it. Using a very simple expression you can easily grab items in your collection. Note that this returns an array of wrappers, which in turn contain the items. If you'd only like to grab the items you could use another Select() statement.

```csharp
myCollection.FirstOrDefault(o => o.item != null && o.item.name.Contains("sword"));
```