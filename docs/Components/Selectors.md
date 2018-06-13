# Selectors

The player components has a field "Trigger Selector" this trigger selector is responsible for choosing whichever trigger should be used when the player clicks a mouse button, or presses a key. By default there are 2 selectors built in:

**Range selector:** Selects a trigger in range based on distance and how much the object is in front of the player. (Useful for 3rd person games)  
**Raycast selector:** Selects the trigger the player is looked at (center of screen) (useful for FPS games)

## Creating the selector objects

It may be required to create a new scriptable object for the range selector or raycast selector if none are found in your project. Not to worry, this is very simple to do. Simply go to your assets pane, click Create > Devdog > Range trigger selector / Raycast trigger selector. This will create a new scriptable object in the set location, and the new scriptable object can be configured to suit your project.

![](Assets/SelectorObject.png)

### Making a custom range selector

```csharp
using System;
using Devdog.General;

[CreateAssetMenu(menuName = "MyScriptableObjects/My trigger selector")]
public class MyTriggerSelector : BestTriggerSelectorBase
{
	public override TriggerBase GetBestTrigger(Player player, List triggersInRange)
	{
		float bestCheck = -999.0f;
		TriggerBase closestTrigger = null;

		foreach (var item in triggersInRange)
		{
			if (item == null || item.enabled == false || item.gameObject.activeSelf == false)
			{
				continue;
			} 

			// Select the object that's furthest away..
			// Set your conditions here, why is the current trigger the 'best' trigger?

			float final = UnityEngine.Vector3.Distance(player.transform.position, item.transform.position);

			if (final > bestCheck)
			{
				closestTrigger = item;
				bestCheck = final;
			}
		}

		return closestTrigger;
	}
}
```