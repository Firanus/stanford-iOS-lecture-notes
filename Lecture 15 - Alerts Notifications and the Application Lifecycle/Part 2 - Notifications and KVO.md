# Lecture 15, Part 2: Notifications and KVO

Notifications and KVO (Key Value Observing) are mechanism by which the Model (and the View) can send messages which the Controller can receive. The Controller can then assign specific closures to be executed when those messages are received.

## Notifications

With notifications, one uses the `NotificationCenter` class to both post and receive messages. Normally, we use the default instance, available at `NotificationCenter.default`.

### Assigning an Observer

To assign a closure to be run when a specific notification is received, we use the `.addObserver(...)` method:

```Swift
var observer: NSObjectProtocol? // a cookie to later “stop listening” with 

observer = NotificationCenter.default.addObserver(
    forName: Notification.Name, // the name of the radio station 
    object: Any?, // the broadcaster (or nil for “anyone”)
    queue: OperationQueue? // the queue on which to dispatch the closure below
) { (notification: Notification) -> Void in // closure executed when broadcasts occur
    let info: Any? = notification.userInfo
    // info is usually a dictionary of notification-specific information 
}
```

Notice that the type of forName is not a String, but instead a `Notification.Name`. iOS provides dozens of options here, though you can add your own if you want. A good way is by adding an `extension` with a `static let` property, as this is how the iOS standard options were implemented.

In addition, the `NSObjectProtocol` type of the observer is a bit odd. However, we basically don't need to worry about this. Apart from removing an abserver, you'll almost never need to mess with it.

A good time to add/remove observers is viewDidAppear/viewDidDisappear, as this indicates when you're on screen, which is when you actually want to do something.

### Posting a Notification

This is as simple as calling `NotificationCenter.default.post(...)`:

```Swift
NotificationCenter.default.post(
      name: Notification.Name, // name of the “radio station”
    object: Any?, // who is sending this notification (usually self)
  userInfo: [AnyHashable:Any]? = nil // any info you want to pass to station listeners
)
```

When this is called, it will call closures that are observing. However, if they are on a different queue to the queue that sent the notification, they will be executed asynchronously

## KVO

The basic idea behind a KVO is that a closure should be triggered whenever a property value changes. However, the caveat here is that there is a specific mechanism that needs to be implemented for this to work. We're not going to spend any time on that (KVOs are a little niche), but `NSObject` implements it, so you can use KVOs on an class that subclasses NSObject.

NSObject is the root class of all iOS classes (e.g. ViewController etc.). If you want to use it in a class of your own, the easiest way to enable it is just to subclass NSObject

Usually we use KVOs in Controllers to observe either its model or its view.


[Previous Note](../Lecture%2015%20-%20Alerts%20Notifications%20and%20the%20Application%20Lifecycle/Part%201%20-%20Alerts%20and%20Action%20Sheets.md) | [Back To Contents](https://github.com/Firanus/stanford-iOS-lecture-notes)