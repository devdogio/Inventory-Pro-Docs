# Custom notification

First create a  [partial class](http://devdog.nl/documentation/core-concepts/)  **outside of the Devdog/InventoryPro folder**. Make sure the namespace and class name are exactly the same as those of the internal code (see code below):

```csharp
namespace Devdog.InventoryPro
{
    public partial class LangDatabase
    {
        public InventoryNoticeMessage myCustomMessage = new InventoryNoticeMessage("", "Default message name", NoticeDuration.Medium, Color.white);
    }
}
```

This will merge your custom message attributes with the build-in language database. Now we can access the “myCustomMessage” notification from anywhere in our code.

```csharp
InventoryManager.langDatabase.myCustomMessage.Show(item.name, item.description); // Pass in as many parameters as you like
```

The parameters passed in .Show() can be used inside your message as {0}, {1}, etc… By default all messages regarding an inventory item can use {0} for the item name and {1} for the item description.

- {0} = Item name
- {1} = Item description

For example: “You sold item {0}”, will result in “You sold item Apple”.