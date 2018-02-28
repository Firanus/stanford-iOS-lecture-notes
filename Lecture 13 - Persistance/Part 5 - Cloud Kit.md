# Lecture 13, Part 5: Cloud Kit

Yet another topic we don't have the time to do in depth in this course. However, this one was covered in the Spring 2015-16 semester. So go hunting for that as well!

Cloud Kit is also a database, but it is simpler than a SQL database. What distinguishes it from Core Data is that it is on the network. As a result, accessing the DB could be slow or even impossible. You need to be quite thoughtful to handle this.

## Important Concepts
* **Record Type** - The equivalent of a struct or a class
* **Fields** - The equivalent of variables in a class or a struct
* **Record** - An instance of a Record Type
* **Reference** - A pointer to another Record
* **Database** - a place where Records are stored
* **Zone** - a sub-area of a database
* **Container** - a collection of databases
* **Query** - a Database search
* **Subscription** - a "standing query" which sends push notifications when changes occur

To use Cloud Kit in your app, you need to turn on  iCloud in the Capabilities section of your project settings, and select CloudKit.

From this location, you can also access a web-based UI of your database schema. As an aside, in development mode, you don't have to explicitly define your database schema. CloudKit will create it on the fly as you upload items.

## Creating a Record

Example code to add a tweet to your Cloud Kit DB:

```Swift
let db = CKContainer.default.publicCloudDatabase
let tweet = CKRecord(“Tweet”)
tweet[“text”] = “140 characters of pure joy”
let tweeter = CKRecord(“TwitterUser”)
tweet[“tweeter”] = CKReference(record: tweeter, action: .deleteSelf)

db.save(tweet) { (savedRecord: CKRecord?, error: NSError?) -> Void in
if error == nil {
  // hooray!
} else if error?.errorCode == CKErrorCode.NotAuthenticated.rawValue {
  // tell user he or she has to be logged in to iCloud for this to work!
} else {
  // report other errors (there are 29 different CKErrorCodes!) }
}
```

## Querying for a Record

Like Core Data, we use `NSPredicate`, but they can't be as complicated:

```Swift
let predicate = NSPredicate(format: “text contains %@“, searchString)
let query = CKQuery(recordType: “Tweet”, predicate: predicate)

db.perform(query) { (records: [CKRecord]?, error: NSError?) in
  if error == nil {
    // records will be an array of matching CKRecords
  } else if error?.errorCode == CKErrorCode.NotAuthenticated.rawValue {
    // tell user he or she has to be logged in to iCloud for this to work!
  } else {
    // report other errors (there are 29 different CKErrorCodes!) }
}
```

## Standing Queries

One of CLoud Kit's coolest features is the ability to send push notifications when the DB changes.

Unfortunately, we can't really delve into this here because we haven't yet done push notifications. However, they are quite simple, so look into them. Start with [the documentation](https://developer.apple.com/documentation/usernotifications) for `UserNotifications`

[Previous Note](../Lecture%2013%20-%20Persistance/Part%204%20-%20Core%20Data.md) | [Back To Contents](https://github.com/Firanus/stanford-iOS-lecture-notes) |  [Next Note](../Lecture%2013%20-%20Persistance/Part%206%20-%20UIDocuments.md)