# Skillbar

The skillbar, like any other window containing items, is a collection.

Key combinations can be set up using the keys field. Any number of fields can be used, and the skillbar's slot will auto. be generated based on the amount of keys you have defined. When using references multiple wrappers can be used to define it's behavior.

For example, when using the `UI_Item_KeyTriggerer_PFB` (as shown in the picture) stacks will behave as normal and will deplete as the item referenced is depleted. The `UI_Item_reference_Sum_PFB` wrapper creates a sum (total amount of set item in the player's inventories) and shows this as the actual value.

!!! note
	Using a wrapper that implements the `IInventoryItemWrapperKeyTriggerer` interface is required.

![](Assets/SkillbarUI.png)