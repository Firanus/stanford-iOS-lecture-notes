# Lecture 13, Part 1: UserDefaults

The first persistance method we'll be looking at is called `UserDefaults`. It is essentially a very small database that persists between launchings of your app. It is ideal for settings and the like, but beware trying to store anything too large.

## What can you store?

UserDefaults can only store *Property List* data. A Property List is an old Objective-C API that represents any combination of the following data types:
* Array
* Dictionary
* String
* Date
* Data
* Number (i.e. Int, Double, etc.)

Swift doesn't have an enum to represent this sadly, so its represented as an `Any`, but will fail if you try to put other kinds of data in.

## Reading and Writing

While you can create a database with `UserDefaults()`, this is unusual. Normally, we just access `UserDefaults.standard` and use that.

To set a value, we just use the `.set(Any?, forKey: String)` command. For example:

```Swift
let defaults = UserDefaults.standard

defaults.set(3.1415, forKey: "pi")
defaults.set(nil, forKey: "Setting to remove")
```

Similarly, to get a value, we can use the `object(forKey: String) -> Any?`. There are also convenience methods to access objects of specific types, as with the `object` method, you would have to cast the result to your desired type. Some of them will return nil if the selected object is of the wrong type, while others will not:

```Swift
func double(forKey: String) -> Double
func array(forKey: String) -> [Any]?
func dictionary(forKey: String) -> [String: Any]?
```

## Saving (Optional)

The User Defaults DB saves automatically. However if you want to force a save (most often, for debugging purposes), you can call the `synchronise()` method. This is not "free", but it is relatively lightweight, so use it when you need to.

[Previous Note](../Lecture%2013%20-%20Persistance/Part%200%20-%20Intro.md) | [Back To Contents](https://github.com/Firanus/stanford-iOS-lecture-notes) |  [Next Note](../Lecture%2013%20-%20Persistance/Part%202%20-%20Archiving.md)