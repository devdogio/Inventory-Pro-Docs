# Collection conditions

Collection conditions can be used to implement your own use conditions for collections without overriding methods, avoiding you to wrap each collection in your own code. Custom item use conditions are also available, allowing you to add restrictions on build-in item types.

## Code

```csharp
public class CustomCollectionAddItemConditions : MonoBehaviour
{
    // GetComponent<>() assumes this script is attached to a collection, but you can of course also serialize it.
    public void Start()
    {
        // Register our custom check.
        GetComponent<ItemCollectionBase>().canAddItemToCollectionConditionals.Add(CustomCollectionConditions);
    }

    private bool CustomCollectionConditions(InventoryItemBase item)
    {
        // Only allow items that are less than 20 gold in the collection.
        if (item.buyPrice < 20)
        {
			return true; // The item can be added to the collection.
		}
		
        return false; // The item cannot be  added to the collection.
    }
}
```