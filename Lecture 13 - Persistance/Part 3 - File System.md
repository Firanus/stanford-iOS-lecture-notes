# Lecture 13, Part 3: File System

Once you have some data, you'll want to store it in the file system. Your app sees the file system as a normal Unix file system that starts at `/`.

However, there are file protections in place. In fact, you can only read and write to your own app's "sandbox". There are 3 main reasons for this:

* **Security** - so that nobody else can damage your application.
* **Privacy** - so that no other apps can view your app's data.
* **Cleanup** - so that when you delete your app, all the data its written  can neatly go with it

## Sandbox Contents

The sandbox has various different directories in it. These include:

* The **Application** directory - which contains your executable, storyboards, assets and the like. It is, however, not writeable
* The **Documents** directory - permanent storage that is directly visible to the user. This is readable, writeable, and visible on iOS 11's Files app
* The **Application Support** directory - which is permanent storage not directly visible to the user. Also writeable
* The **Caches** directory - which lets you store temporary information. This is not backed up by iTunes.

There are many more. See, for example [the documentation for SearchPathDirectory](https://developer.apple.com/documentation/foundation/filemanager.searchpathdirectory).

## Accessing the File System

You'll use 2 classes to get access to the file system: `FileSystem` and `URL`.

There are a couple of ways to get paths to the filesystem using these classes. The first is to use the `FileManager.default.url(//...)`:

```Swift
let url: URL = FileManager.default.url(
  for directory: FileManager.SearchPathDirectory.documentDirectory, // for example 
  in domainMask: .userDomainMask // always .userDomainMask on iOS
  appropriateFor: nil, // only meaningful for “replace” file operations
  create: true // whether to create the system directory if it doesn’t already exist
)
```

`SearchPathDirectory` is the enum with the list of directories.

Once you have a base path, you can begin to append to it using the methods:

```Swift
func appendingPathComponent(String) -> URL
func appendingPathExtension(String) -> URL //e.g. .jpg
```

You can also determine if a file exists at a particular URL by checking `var isFileURL: Bool`, and various properties of the file using 
```Swift
func resourceValues(for keys: [URLResourceKeys]) throws -> [URLResourceKey: Any?]
```
where URLResourceKeys is an enum of values you can investigate. The full list is in [the documentation](https://developer.apple.com/documentation/foundation/urlresourcekey)

## Reading and Writing

This is done using the `Data` type. To read we use the initializer:

```Swift
init(contentsOf: URL, options: Data.ReadingOptions) throws
```

and to write we use the method:

```Swift
func write(to url: URL, options: Data.WritingOptions) throws -> Bool
```

## FileManager

FileManager is a very versatile class that lets you do a wide variety of file operations. It also has a delegate that lets you, amongst other things, restrict functionality with lots of `should...` methods. Finally, it is also thread-safe, as long as a given instance is used in only one thread. See [the documentation](https://developer.apple.com/documentation/foundation/filemanager) for more info.

[Previous Note](../Lecture%2013%20-%20Persistance/Part%202%20-%20Archiving.md) | [Back To Contents](https://github.com/Firanus/stanford-iOS-lecture-notes) |  [Next Note](../Lecture%2013%20-%20Persistance/Part%204%20-%20Core%20Data.md)