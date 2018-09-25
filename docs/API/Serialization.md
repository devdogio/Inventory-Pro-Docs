# Serialization

Serialization in Inventory Pro is handled by a set of interfaces that can easily be extended to allow extra functionality or to replace the build-in functionality entirely.

## JsonItemsSerializer

JsonItemsSerializer is the default serializer used for Inventory Pro. Alternatively you can use Easy Save 2 or write your own implementation (see IItemsSerializer below).

### Extending the JsonItemsSerializer

Assume you'd like to save additional information about a collection you can of course do so. This can be done by creating a new class and inheriting the JsonItemsSerializer class; and lastly by overriding the Serialize and Deserialize methods.  **Some example code:**

```csharp
    public class MyJsonCollectionSerializer : JsonItemsSerializer
    {
        
        public override object SerializeCollection(ItemCollectionBase collection)
        {
            var myObjectToSerialize = new << Add type here >>();            

            return Integration.SimpleJson.SimpleJson.SerializeObject(myObjectToSerialize);
        }

        public override ItemCollectionSerializationModel DeserializeCollection(object serializedData)
        {
            Assert.IsTrue(serializedData is string, "Serialized data is not string, json collection serializer can only use a JSON string.");

            var model = new << Deserialize object here >> ();
            return model;
        }
    }

```

As you might have noticed the ItemCollectionSerializationModel is used as a data carrier to store the deserialized data into. All methods on this class are marked virtual, so you can easily create an object that extends the ItemCollectionSerializationModel and add your own fields, collection filling, etc. (See below for example).

## ItemCollectionSerializationModel

The serialization model represents a single collection and only stores the information you want to be serialized.

The ItemCollectionSerializationModel can be extended easily by creating a new class, implementing ItemCollectionSerializationModel and adding / overriding the methods you'd like to change.  **Some example code:**

```csharp
public class MyItemCollectionSerializationModel : ItemCollectionSerializationModel
{
    public override void FromCollection(ItemCollectionBase collection)
    {
        base.FromCollection(collection);
    
        // Do extra work here
    }
    
    public virtual void ToCollection(ItemCollectionBase collection)
    {
        base.ToCollection(collection);
        
        // Do extra work here
    }
}
```

## IItemsSerializer

The IItemsSerializer can be implemented to write your own serialization system. By default a JSON serializer is added, as JSON is currently the most popular data interchangeable format.

## CollectionSaverLoaderBase

The collection saver loader instigates the saving and loading and is responsible for saving the serialized data 'somewhere'. The default uses the Unity PlayerPrefs.

The abstract class CollectionSaverLoaderBase can be implemented into your own class to create a custom saving / loading system, such as for example, saving & loading to a web API. The nice thing about this system is that, if you were to choose to implement your own saving / loading and still wish to use JSON no changes to the serialization have to be made.
