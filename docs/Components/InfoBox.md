# Info Box (tooltip)

The `InfoBoxUI` can be used as a tooltip, but is certainly not limited to just being a tooltip.

![](Assets/InfoBox.png)

The InfoBoxUI works as a seperate module and can be removed without affecting other parts of the system. If you prefer not to use it, simply remove it from your scene.

![](Assets/InfoBoxUI.png)

### Coding

!!! note
​	Custom item types supply the InfoBoxUI with information by overriding the GetInfo() method.

```csharp
public UnityEngine.UI.Text myTextField;

// Override the repaint method. This will be called by Inventory Pro.
protected override void Repaint(InventoryItemBase item, LinkedList rows)
{
	base.Repaint(item, rows); // Call the default repainting method.

	myTextField.text = "ABC"; // Add our own repainting
}
```

The `InfoBoxUI` has various behaviors for various input scenarios. In some cases, you may not want any behaviors and simply control display of the box yourself. In this case, you can define your own class that extends from `InforBoxUI` and defines an empty Update method, like this:

```csharp
public class MyInfoBoxUI : InfoBoxUI
{
   public void Update()
   {} //Do nothing
}
```

You can feed an item to an info box using the `HandleInfoBox`method.