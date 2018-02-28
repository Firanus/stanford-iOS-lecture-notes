# Lecture 13, Part 4: Core Data

Sometimes you need to store large amounts of data locally in a data base. You also need to be able to search through it in an efficient, sophisticated manner.

Core Data provides this functionality. It is essentially a SQL database that you can interact with using an object-oriented API. Note that you can actually customise it to have non-SQL backends.

While a very powerful feature, there isn't actually time to give it the love it deserves in this series. We'll *very briefly* look at it here. However, there are 2 lectures from the Winter 2016-17 semester of this course which cover it in great depth. Would be excellent as an extension.

In actual point of fact, what Core Data does is create an object graph that has a (usually SQL) database backing it up.

You can do this using Xcode's built in mapper tool. This provides you a GUI which you can manipulate, which is similar in appearance to e.g. the schema editors in ASP.NET.

## Creating and Accessing Data

Core Data is managed using an `NSManagedObjectContext` (there is also a second option we'll look at later, `UIDocument`). The option **Use Core Data** you get when starting an Xcode project creates one for you in your AppDelegate.

Creating and Updating objects looks a lot like standard Swift:

```Swift
let context: NSManagedObjectContext = ...
if let tweet = Tweet(context: context) {
  tweet.text = “140 characters of pure joy”
  tweet.created = Date()
  let joe = TwitterUser(context: tweet.managedObjectContext)
  tweet.tweeter = joe
  tweet.tweeter.name = “Joe Schmo” 
}
```

Deleting is just a matter of calling:
```Swift
context.delete(tweet)
```

When using `NSManagedObjectContext`, we have to explicitly save our context, and also handle errors, as saving `throws` (`UIDocument` autosaves):

```Swift
do {
  try context.save()
} catch {
  // deal with error
}
```

Finally, if we want to query our DB, we'd do this using an `NSFetchRequest`. We build this up using predicates. The example below looks for tweets that have been made in the last 24 hours, sorted by the TwitterUser's name:

```Swift
//create a request
let request: NSFetchRequest<TwitterUser> = TwitterUser.fetchRequest()

//set it to look for tweets from the last 24 hours
let yesterday = Date(timeIntervalSinceNow:-24*60*60) as NSDate
request.predicate = NSPredicate(format: “any tweets.created > %@”, yesterday)

//define sorting behaviour
request.sortDescriptors = [NSSortDescriptor(key: “name”, ascending: true)]

//get context and fetch result
let context: NSManagedObjectContext = ...
let recentTweeters = try? context.fetch(request)
```

If there are no matches in the DB, we will get an empty array (`[]`) back. If there is an error in the predicate, this method will throw.

## And More...

There is a vast amount more that Core Data can do. This includes:

* support for multithreading
* Close integration with UITableView
* Optimistic Locking (`deleteConflictsForObject`)
* Rolling back unsaved changes
* Undo/Redo
* Staleness (how frequently should we refetch objects?)
* etc...

[Previous Note](../Lecture%2013%20-%20Persistance/Part%203%20-%20File%20System.md) | [Back To Contents](https://github.com/Firanus/stanford-iOS-lecture-notes) |  [Next Note](../Lecture%2013%20-%20Persistance/Part%205%20-%20Cloud%20Kit.md)