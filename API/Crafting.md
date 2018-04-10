# Crafting

Blueprints can also be enabled or disabled through code.

## Enable or disable a blueprint through code:

```csharp
void SetupBluePrints(int maxLevel)
{
    foreach (InventoryCraftingCategory category in ItemManager.database.craftingCategories)
    {
        foreach(InventoryCraftingBlueprint bp in category.blueprints)
        {
             bp.playerLearnedBlueprint = true;
        }
    }
}
```

Blueprints marked with playerLearnedBlueprint = true will show up in the crafting list, the ones marked as false won't.

## Modify standard crafting

The standard crafting system can of course be inherited from and overridden to modify certain aspects of the crafting process. For example, maybe we want to add another collection to scan for potential items the user would require.

```csharp
public override bool CanCraftBlueprint(InventoryCraftingBlueprint blueprint, bool alsoScanBank, int craftCount)
{
    // Add our own conditions here. If our check fails, return false.

    return base.CanCraftBlueprint(blueprint, alsoScanBank, craftCount);
}
```

When a blueprint is crafted the reward is given to the player, of course this behavior can also be modified to your liking. When multiple items are crafted the GiveCraftReward method will be called as many times as you're crafting items.

```csharp
protected virtual bool GiveCraftReward(InventoryCraftingCategory category, InventoryCraftingBlueprint blueprint)
{
    // Add custom reward system.
    // If you're completely replacing the reward system don't call base.GiveCraftReward.   

    return base.GiveCraftReward(category, blueprint);
}
```