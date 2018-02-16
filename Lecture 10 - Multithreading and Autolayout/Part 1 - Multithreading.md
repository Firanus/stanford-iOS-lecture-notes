# Lecture 10, Part 1: Multithreading

Multithreading, in the course of this lecture, is largely about keeping expensive tasks from blocking the UI of your app, so that it can stay responsive at all times.

## Queues

Multithreading in iOS works largely through queues. Functions, as closures, are lined up in a queue. The system then pulls those closures off the queues and executes them on an associated thread.

Queues can be serial (one closure at a time) or concurrent (multiple threads servicing it)

### Main Queue

The most important serial queue is the main queue, on which all UI activity **MUST** occur.

Conversely, we really don't want time-consuming non-UI activity to happen on this queue, as we want our UI to be responsive and (serially) predicatable.

Functions are pulled off of the main queue only when it is in the "quiet" state.

### Global Queue

For non-main-queue work, you should use a shared, global, concurrent queue.

### Getting a queue

To get the main queue, we can simply use the following command:

```Swift
let mainQueue = DispatchQueue.main
```

When getting a global queue, we have more options. In particular, we have the 4 following options:

```Swift
let backgroundQueue = DispatchQueue.global(qos: DispatchQoS)
DispatchQoS.userInteractive //high priority - for short quick tasks
DispatchQoS.userInitiated //high priority - might take a little longer
DispatchQoS.background //not directly initiated by user, so as slow as needed
DispatchQoS.utility //long-running background process, low priority
```

`userInteractive` is rarely used, and is intended for such quick things they can happen in between the beginning of, say, a drag and a drop. Part of the reason its so rarely used is that if you need something that fast, you can probably do it on the main thread.

`userInitiated` is the most commonly used thread. The idea is that the user has asked for something to happen. They want it to be done ASAP, though it can take a little more time.

`background` is the tasks the user hasn't asked for directly, but still expect to get done fairly soon.

`utility` is for tasks your app wants to do as part of its architecture. E.g. cleaning out your database now and again.

### Putting code on the queue

Once you've selected a queue, you put a closure onto it by using either of the following commands:

* `queue.async { ... }` - which adds your closure to the target queue and continues running on the current queue
* `queue.sync { ... }` - which blocks the current queue until the closure finishes on your selected queue.

We almost always choose `async`. Never do `sync` on the main queue, as you'd block it.

### Other queues, topics and APIs

You might, rarely, need a queue other than main or global. Dispatch queue allows the creation of queues by the user.

There is also a lot more to Grand Central Dispatch, including locking, protecting critical sessions, readers and writers and synchronous dispatch. The documentation has more information.

There is also a second API with classes `Operation` and `OperationQueue` which can be used. They're useful for more complicated multithreading when you have dependencies between closures. However, we use it quite rarely.

## Multithreaded iOS APIs

Various APIs in iOS work off the main thread, and take blocks as arguments to execute them off the main thread.

Remember that if you want to do UI work, you **have to dispatch back to the mai queue**

## Example

For example, to fetch the contents of a URL:

```Swift
let session = URLSession(configuration: .default)
if let url = URL(string: "http://cam.ac.uk/...") {
    let task = session.dataTask(with: url) { (data: Data?, response, error) in
        //you can't do UI work at this level as we're off the main queue
        DispatchQueue.main.async {
            //UI work goes here instead
        }
    }
    task.resume()
}
```

[Previous Note](../Lecture%2010%20-%20Multithreading%20and%20Autolayout/Part%200%20-%20Intro.md) | [Back To Contents](https://github.com/Firanus/stanford-iOS-lecture-notes) |  [Next Note](../Lecture%2010%20-%20Multithreading%20and%20Autolayout/Part%202%20-%20Autolayout.md)