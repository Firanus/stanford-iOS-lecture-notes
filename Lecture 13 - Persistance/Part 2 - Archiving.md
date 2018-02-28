# Lecture 13, Part 2: Archiving

UserDefaults is limited by both the size of items you can store and their type. If you want to store *any* item, you should use archiving. At the moment, there are 2 ways to do this, one that is old (`NSCoder`), and one that is new in iOS 11, which we will go through in depth.

## Old (`NSCoder`)

The old method essentialy required you to implement the following two methods for every object in your object tree:

```Swift
func encode(with aCoder: NSCoder)
init(coder: NSCoder)
```

Essentially, these methods allow you to store and recreate your object from the coder's dictionary. You can then turn an object graph into `Data` using `NSKeyedArchiver`, and back using `NSKeyedUnarchiver`. You can easily write `Data` to a file and the like.

This method is how storyboards are saved.

## New - `Codeable` mechanism

Codeable is also essentially a way to turn objects into dictionaries. To do so, all the objects in your object graph must implement `Codeable`. However, the difference is that, for standard Swift types, *Swift will do this for you*. For non-standard types, you can do something akin to the old method.

Once your object graph is all `Codeable`, you can convert it into either JSON or a property list, e.g.:

```Swift
let object: MyType = //...
let jsonData: Data? = try? JSONEncoder.encode(object) //note that this method throws

//You can also convert your JSON to a string. JSON is always UTF8
let jsonString = String(data: jsonData!, encoding: .utf8)
```
You can configure the names that will be given to your properties by adding a private enum called `CodingKeys` to your code:

```Swift
struct MyType: Codeable {
  var someDate: Date
  var someString: String
  var other: SomeOtherType //which implements Codeable
  
  private enum CodingKeys: String, CodingKey {
    case someDate = "some_date" //will not havew name some_date
    //someString won't be included, as it doesn't have a case
    case other //this key is still called "other"
  }
}
```

Decoding is very similar. Simply use 
```Swift
JSONDecoder().decode(MyType.self, from: jsonData)
```
You can configure your decoder to handle the face that JSON is not strongly typed.

In both of these cases, you can participate directly in the encoding and decoding processes by implementing `encode` and `decode` functions, but this is rare (only required if your type isn't composed of Codeable types), so we won't be focusing on it here.

[Previous Note](../Lecture%2013%20-%20Persistance/Part%201%20-%20UserDefaults.md) | [Back To Contents](https://github.com/Firanus/stanford-iOS-lecture-notes) |  [Next Note](../Lecture%2013%20-%20Persistance/Part%203%20-%20File%20System.md)