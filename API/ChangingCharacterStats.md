# Changing character stats

Assuming for a moment that we have only one player, we can grab it using the InventoryPlayerManager singleton. All managers use these and allow you to very easily grab an object through a static reference.

```csharp
var myPlayer = PlayerManager.instance.currentPlayer.inventoryPlayer;

```

Alright, that settled, now we can grab the stat from the player's stats collection which contains all the palyer's stats. (player.statsCollection).

Next up we can grab the actual stat and modify it the way we like.

```csharp
var myPlayer = PlayerManager.instance.currentPlayer.inventoryPlayer;
var stat = myPlayer.stats.Get("categoryName", "statName"); // For example categoryName: "Default", and statName: "Health".

// And now we can modify the stat any way we like, events will be auto. fired to update the UI
stat.ChangeCurrentValueRaw(10); // Negative values are also allowed.
stat.ChangeFactor(0.1f); // Add 10% health.

```

## Saving some performance

The UI is repainted whenever a stat changes. This is a heavy operation that takes a lot of time to compute. To avoid wasting any performance we can optimize this a little in certain situations. When you do a lot of modifications on a stat let's say, add some base value, raw value and change the factor you can pass a 2nd argument in the methods to avoid firing events.

```csharp
stat.ChangeCurrentValueRaw(10, false);
stat.ChangeFactor(0.1f, false); // Add 10% health.
stat.ChangeBaseValue(10, true); // Only pass true here, calling the change event

```

This way the stat's event "changed" will only fire once, repainting the UI only 1 time and not 3 times. This is especially useful when updating a stat many times a second ( like Update() ).

### Hunger bar example

When using a huger system you'll likely want to decrease the stamina of the user over time. To do this we'll first have to grab the property, create a loop with an interval and slowly decrease it's value.

```csharp
private WaitForSeconds waitTime;
private InventoryCharacterStat staminaStat; 

public void Awake()
{
    staminaStat = PlayerManager.instance.currentPlayer.inventoryPlayer.stats.Get("Default", "Stamina");

    waitTime = new WaitForSeconds(1f); // Create once to avoid GC
    StartCoroutine(DegradeStaminaOverTime());
}

protected IEnumerator DegradeStaminaOverTime()
{
    yield return waitTime;

    // Decrease stamina by 1 every second. This will auto. repaint any UI that displays this stat.
    staminaStat.ChangeCurrentValueRaw(-1f);
}
```