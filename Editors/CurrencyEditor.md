# Currency Editor

The currency editor allows you to define the currencies that can be used inside your items, crafting blueprints, vendors, etc.

Each currency can contain a set of conversions. These conversions allow you to convert something such as a dollar to an euro. Auto conversion defines if it can be used when auto. converting between currencies.

For example many games use a system of Gold, Silver and copper.

When running out of copper the system can convert the silver currency down to copper. Essentially re-filling it from a higher currency that can be converted down.

The automatic conversion can be defined at the bottom of the editor.

**Auto convert on max:**  allows you to convert to a more valuable currency once you hit a defined maximum. For example you can’t have more than 100 copper, so once the system notices that you have more than a 100 copper it will be converted to 1 silver.

**Auto convert fractions:** When “Allow fractions” (at the top) isn’t enabled fractions either have to be converted, or discarded. For example, when you have 1.1 silver (which isn’t allowed) the system will convert it down to 1 silver and 10 copper.

![](Assets/CurrencyEditor.png)