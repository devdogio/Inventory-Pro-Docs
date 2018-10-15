# Character Equipment

In many cases you might want to add custom logic whenever an item is equipped, or to figure out what items are equipped whenever you need it in your code. This can both be done very quickly, and very easily.

## Using events

!!! note
	Remember to add `using Devdog.InventoryPro;` to the top of your script.

```csharp
public CharacterUI characterUI; // Assign in the inspector.

protected virtual void Awake()
{
    characterUI.OnAddedItem += CharacterUI_ItemEquipped;
}

private void CharacterUI_ItemEquipped(IEnumerable items, uint amount, bool cameFromCollection)
{
    var equippable = items.FirstOrDefault() as EquippableInventoryItem;
    if(equippable != null)
    {
        // Item is an equippable, check values.
        // equippable.category.name, etc...
    }
}

```

## Get equipped item directly

!!! note
	Remember to add `using Devdog.InventoryPro;` to the top of your script.

```csharp
public CharacterUI characterUI; // Assign in the inspector.

protected virtual void Awake()
{
    // Get all slots from the character collection that allow an equip type "Head"
    var slots = characterUI.equippableSlots.Where(o => o.equipTypes.Any(e => e.name == "Head")); 

    // OR
    
    // Get the first item from this collection.
    var slot = characterUI[0].item;

    // OR

    // Get all filled slots' items that have the category "Shield"
    var shieldSlots = characterUI.Select(o => o.item != null && o.item.category.name == "Shield");
}

```

## Equipping items

```csharp
var equipSlot = equippableItem.GetBestEquipSlot(characterCollection);
if(equipSlot == null)
	return; // can't equip, no slots found.

characterCollection.EquipItem(equipSlot, equippableItem); // Equip the item to the character collection. 

// OR 
var bestEquipSlot = equippableItem.GetBestEquipSlot(characterCollection);
if(bestEquipSlot == null)
	return;

equippableItem.Equip(bestEquipSlot);
```