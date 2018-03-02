# Lecture 13, Part 6: UIDocuments

This topic we will be covering in some depth in this course.

`UIDocument` is the type of persistence you should use when the thing that you're persisting is percieved by the user to be a document.

UIDocuments provide a powerful framework for managing your documents, that is extremely simple to use. Its built in features include:
* Managing all interaction with storage devices (including filesystem, iCloud, Box, etc.)
* Providing asynchronous opening, writing, reading and closing of files
* Autosaving your document data
* Making integration with iOS 11's Files app basically free.

What do you need to do to work with UIDocument? Simply: 
1. Subclass UIDocument to add vars to hold the model of your MVC.
2. Implement a method to write your model to a Data
3. Implement a method to read it from a Data

Now all the proviously quoted functionality should work.

As an optional extra, you can also implement a method to inform the document when it has changed, which will give you autosaving functionality.

We'll now go through things in a little more detail.

## Subclassing UIDocument

For simple documents, you only need to add your model as a var (though there are methods you can overwrite if you want to):

```Swift
class EmojiArtDocument: UIDocument {
  var emojiArt: EmojiArt?
}
```

## Creating a UIDocument

As simple as getting the directory URL you want to save the document to and calling an initialiser:

```Swift
var url = FileManager.urls(for: .documentDirectory, in: .userDomainMask).first! 
url = url.appendingPathComponent(“Untitled.foo”)

//use the url in UIDocument's only initialiser
let myDocument = EmojiArtDocument(fileURL: url)

//eventually, set the model in the document
myDocument.emojiArt = ...
```

## Creating a Data for your Model

Overriding the `contents(forType)` method in your UIDocument subclass lets you convert your model into a `Data`:

```Swift
override func contents(forType typeName: String) throws -> Any {
  //return emojiArt converted into a Data, using the archiving info from earlier on
}
```

Note that the return type is `Any`, as you can return either a `Data` or a `FileWrapper`, which is a type that represents a directory full of files that make up your document.

Note also that the `forType` parameter is a UTI (Universal Type Identifier) calculated from your fileURL's file extension. We'll see later how to declare the UTIs your app handles.

## Turning a Data into a Model

There's a method for this too:

```Swift
override func load(fromContents contents: Any, ofType typeName: String?) throws {
  emojiArt = //... contents converted into an EmojiArt
}
```

That's it, now you have access to all the UIDocument methods.

## UIDocument methods

### Opening a Document

```Swift
myDocument.open { success in
  if success {
    // your Model var(s) (e.g. emojiArt) is/are ready to use 
  } else {
    // there was a problem, check documentState 
  }
}
```

This method works asynchronously, and is executed on the same thread you called it in.

### Saving Your Document

You tell your document that something has changed by calling:

```Swift
myDocument.updateChangeCount(.done)
```
or you can use UIDocument's `undoManager`, which we do not have time to cover atm ([see the documentation](https://developer.apple.com/documentation/uikit/uidocument/1619953-undomanager). UIDocument will save your changes at the next available opportunity.

You can also force a save using the method:
```Swift
let url = myDocument.fileURL // or something else if you want “save as” 
myDocument.save(to url: URL, for: UIDocumentSaveOperation) { success in
  if success {
    // your Model has successfully been saved
  } else {
    // there was a problem, check documentState }
  }
```
UIDocumentSaveOperation is either `.forCreating` or `.forOverwriting`

### Closing Your Document

When you're done with a document, you close it:
```Swift
myDocument.close { success in
  if success {
    // your Model has successfully been saved and closed
    // use the open method again if you want to use it 
  } else {
    // there was a problem, check documentState 
  }
}
```

## Document State

As all these processes are going on, your document transitions through various states. The potential values are stored in UIDocumentState, and can be seen [in the documentation](https://developer.apple.com/documentation/uikit/uidocumentstate)

Note also that there is a notification called `UIDocumentStateChanged` that lets you observe document state and be notified of changes.

## Thumbnail

Finally you can also set a thumbnail for your files. You do this by overriding the UIDocument method that sets fileAttributes:

```Swift
override func fileAttributesToWrite(to url: URL, for operation: UIDocumentSaveOperation)
throws -> [AnyHashable : Any] {
  var attributes = try super.fileAttributesToWrite(to: url, for: saveOperation) 
  if let thumbnail: UIImage = ... {
    attributes[URLResourceKey.thumbnailDictionaryKey] = [URLThumbnailDictionaryItem.NSThumbnail1024x1024SizeKey:thumbnail]
  }
  return attributes
}
```

Note that the thumbnail does not have to be 1024x1024

## Other Properties Of Note

```Swift
var localizedName: String
var hasUnsavedChanges: Bool
var fileModificationDate: Date?
var userActivity: NSUserActivity? // iCloud documents only
```

[Previous Note](../Lecture%2013%20-%20Persistance/Part%205%20-%20Cloud%20Kit.md) | [Back To Contents](https://github.com/Firanus/stanford-iOS-lecture-notes) | [Next Lecture](../Lecture%2014%20-%20Persistance%20Demo/Part%200%20-%20Intro.md)