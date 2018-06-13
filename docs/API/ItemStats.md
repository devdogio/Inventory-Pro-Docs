# Item stats

Looping through all stats of an item.

```csharp
using UnityEngine;
using Devdog.InventoryPro;

public class MyClass
{
	public InventoryItemBase item;
	
	public void Awake()
	{
		foreach (var stat in item.stats)
		{
            // stat.stat.name; // Use name (stat name as defined in editor name)
            // stat.value; // Use value
            // stat.floatValue // Value as a float
		}
	}
}
```