# UIWindow

<iframe width="560" height="315" src="https://www.youtube.com/embed/sSy7s3cEnBQ" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen></iframe>

UIWindows are used a lot throughout Inventory Pro, this component handles the showing and hiding of any window and fires event when it does so.

## Properties

You can use the `isVisible` property to check whether the window is currently shown.

## Actions

```csharp
using Devdog.General;

public void Awake()
{
    var window = GetComponent<UIWindow>();
    
    // Common UIWindow actions 
    window.Show();
    window.Hide();
    window.Toggle();
}

```

You can add your own actions whenever a window is shown or hidden. For example, whenever the inventory is closed you want to show a message.

## Events

!!! note
​    You can also add handlers to **OnShow** and **OnHide** on the window in the inspector. 

```csharp
public void Awake()
{
    var window = GetComponent<UIWindow>();

    // Register the hide event
    window.OnHide += () =>
    {
        // Window hidden
    };

    // Register the show event
    window.OnShow += () =>
    {
        // Window shown
    };
}
```