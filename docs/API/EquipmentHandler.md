# Equipment handler

A custom item equipment handler can be implemented to handle the equipments yourself. This can useful when integrating a 3rd party asset or your own system.

The custom equipment handler HAS to inherit from ItemEquipmentHandlerBase. ItemEquipmentHandlerBase is a scriptable object, so we'll have to add the "CreateAssetMenu" attribute to allow creating a new asset of it, this is great for version control systems, as the data will be stored inside the asset, making it easy to share with team members.

The example below enables the binder's transform and disables it when un-equipped. This is useful for when you already have the models inside your object and only want to enable/disable them at run-time, rather than dynamically instantiate the item's visuals.

```csharp
    [CreateAssetMenu(menuName = InventoryPro.CreateAssetMenuPath + "Enabler equipment handler")]
    public class EnablerChildEquipmentHandler : ItemEquipmentHandlerBase
    {
        public override EquippableInventoryItem Equip(EquippableInventoryItem item, CharacterEquipmentTypeBinder binder, bool createCopy)
        {
            binder.equipTransform.gameObject.SetActive(true);
            return item;
        }

        public override void UnEquip(CharacterEquipmentTypeBinder binder, bool deleteItem)
        {
             binder.equipTransform.gameObject.SetActive(false);
        }
    }
```