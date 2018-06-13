# Creating a new collection slot

When you want to extend the UI features such as showing more information or adding extra input functionality you can create a new slot UI.

When using Unity UI (uGUI) it's easiest to extend from  **ItemCollectionSlotUI** there's also an abstract class  **ItemCollectionSlotUIBase** that has no Unity UI dependencies and can be used to implement other UI systems such as NGUI.

For this example we'll assume you're using Unity UI (uGUI) and inherit from  `ItemCollectionSlotUI`.

## Code

A simple example is shown below where an extra text field is added. This field gets the item's name as long as the slot is not empty.

!!! note
	Repaint is only called after the object changed, not every frame like Update().

```csharp
public partial class ItemCollectionSlotUILoot : ItemCollectionSlotUI
{
    public UnityEngine.UI.Text extraTextField;

    public override void Update()
    {
        base.Update();
    }

    public override void Repaint()
    {
        base.Repaint();

        if (item != null)
        {
            extraTextField.text = item.name;
        }
        else
        {
            extraTextField.text = "";
        }
    }
}
```