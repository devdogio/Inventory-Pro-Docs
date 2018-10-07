# Character Stats

Stats can be defined using the editor, this tutorial is only about using the stats inside your own code though. First of let’s create a new class **outside the Devdog/InventoryPro folder**  and name it MyStatsReader.cs To retrieve the stats we first need to grab the stats collection from our player. If you only use a single player you can use the following code.

```csharp
var myPlayer = PlayerManager.instance.currentPlayer.inventoryPlayer.stats; // Grab the stats collection from the current player
```

If you have multiple characters in your scene you'll have to grab the player you wish to use manually. Which all depends on your own architecture.

## MyStatsReader example

Of course you can also serialize the category and stat names to strings.

```csharp
public class MyStatsReader : MonoBehaviour
{
    public InventoryPlayer myPlayer; // Reference to the characterUI we wish to get stats from - Assign in the inspector.

    protected void Start()
    {
        var myStat = myPlayer.stats.Get("categoryName", "statName");
        if (myStat == null)
        {
            Debug.LogWarning("No such stat exists");
            return;
        }
        Debug.Log(myStat.currentValue); // final value can be used for calculations
        Debug.Log(myStat.ToString()); // Formatted name of stat

        // Changing stats
        myStat.ChangeCurrentValueRaw(10f); // Add +10 to our stat.
        myStat.ChangeFactor(-0.1f); // Remove 10% of our stat.
        myStat.SetMaxValueRaw(200f, false); // Set the max value (this is the raw value, so max health can still be increased by the factorMax).

        // And read our value
        Debug.Log("Value after transmutations: " + myStat.currentValue);
    }
}

## Tips and tricks
Stats have events that are called when their values change. By subscribing to these events, you can insert your own logic.

```csharp

public class PlayerLogic : MonoBehaviour //On you player object
{
	public void healthStat; //Drag the health definition file in here
	
	public void Start()
	{
		GetComponent<Player>().inventoryPlayer.stats.Get(stat).OnValueChanged += DieWhenNoHealth;
	}
	
	private void DieWhenNoHealth(IStat stat)
	{
		if(stat.currentValue < 0)   
		{
			Die(); 
		}
	}
	
	private void Die()
	{
	    //Logic to make the player die
	}
}
```