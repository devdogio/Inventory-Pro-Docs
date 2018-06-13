# Trigger callbacks

<iframe width="560" height="315" src="https://www.youtube.com/embed/KJ1nP0Y6wDw" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen></iframe>

When a trigger is used callbacks will be invoked which can be used run your own code. To use these either the manager can be used for global control, or the triggers can be used for individual control.

## Manager

When using the manager you'll be able to hook onto the global event, which gets called whenever ANY trigger in the scene is affected.

```csharp
void Start()
{
    OnCurrentTriggerChanged.OnCurrentTriggerChanged += (oldTrigger, newTrigger) =>
    {
        // New 'best' trigger. The best trigger is chosen based on the settings.
        // This can either be raycast from center, or closest in range.
    };
}
```

## Triggerer callbacks

If you want more fine-grained control you can use the trigger's callbacks. There are trigger's that can be used and un-used, like for example the vendor, and there are triggers that can only be used, like item triggers (pickup only - The drop creates a new trigger object, but doesn't use it - So, use only).

### Trigger callbacks

The callbacks are invoked on the first enabled component that implements the ITriggerCallback interface.

```csharp
using UnityEngine;
using Devdog.General;

public class MyCallbackComponent : MonoBehaviour, ITriggerCallbacks {

	public bool OnTriggerUsed(Player player)
	{
	    // The trigger has been used.

            // Return true to consume the event (other callback listeners won't receive it)
            // Return false to not cosnume the event.
	}

	public bool OnTriggerUnUsed(Player player)
	{
	    // The trigger has een unused
		// Return true to consume the event (other callback listeners won't receive it)
		// Return false to not cosnume the event.
	}	
}

```

Attach this new component to your trigger, and the OnTriggerUsed and UnUsed will be invoked accordingly.