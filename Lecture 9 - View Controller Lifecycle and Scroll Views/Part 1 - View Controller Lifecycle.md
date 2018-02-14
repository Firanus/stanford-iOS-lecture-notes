# Lecture 9, Part 1: View Controller Lifecycle

As a view controller progresses through its "lifetime", it emits various messages a user can use to hook into its behaviour. These messages trigger a variety of methods, which we can override to provide specific behaviour at certain points in that cycle.

The basic phases at the beginning of a lifecycle are:
1. **Creation** - MVCs are usually instantiated from a storyboard, though we will see some ways to trigger them using code.
2. **Preperation if being segued too**
3. **Outlet setting**
4. **Appearing and (potentially) disappearing** - an example of disappearing is if you have a split view in portait mode.
5. **Geometry changes** - E.g. rotating your phone will cause these
6. **Low-memory situations** - Least importantly, if you're in a low memory situation, you View Controller might get asked to free some up.

The complete lifecycle is:

#### Initial Load
* **Instantiated** (from a storyboard, usually)
* `awakeFromNib` (if instantiated from a storyboard)
* **Segue Preperation**
* **Outlets set**
* `viewDidLoad`

#### During Lifetime (i.e. after `viewDidLoad`)
* Every time your view goes on/off screen these methods will be called:
  * `viewWillAppear` and `viewDidAppear`
  * `viewWillDisappear` and `viewDidDisappear`
* At any point the layout *might* be affected, the following will be called:
  *  `viewWillLayoutSubviews` and `viewDidLayoutSubviews`
  *  Additionally, if the phone is rotated, `viewWillTransition` is also called (before viewWillLayoutSubviews).
*  If memory gets low, you might get:
   * `didRecieveMemoryWarning`

## Lifecycle Methods - Appearing and Disappearing

As previously mentioned, we can override a variety of method to execute our own code at specific points in the lifecycle. The methods we need to override are:

#### `viewDidLoad`

This function gets called after the outlets have been set (i.e. after step 3 above). It is an excellent place to update your view using your model.

```Swift
override func viewDidLoad() {
  super.viewDidLoad() //make sure to call super.
  //execute custom code here  
}
```

However, you must remember **not to do geometry-related setup here. Your bounds have not been set**

#### `viewWillAppear`

This method gets called just before your MVC appears on screen. Note that unlike `viewDidLoad`, this method can fire multiple times.

This is an excellent place to provide updates to your app based on changes that may have happened since your view last appeared.

```Swift
override func viewWillAppear(_ animated: Bool) {
  super.viewWillAppear(animated) //always call super
  // tell my view what happened while I was gone.
}
```

#### `viewDidAppear`

This one calls immediately *after* the view appeared on screen.

This is a good place to do things like start animations, timers, and observing external items. 

You can also kick off a very expensive task here (say, a network fetch), to avoid making it block the view appearing. You typically also want to ensure such tasks happen in the background, which we'll look at in the next lecture.

These points highlight an important UX principal: **you should never block the user interface experience**. If nothing happens when they try to interact with your app, they will stop using it.

A consequence of this is that you have to make your UI work without these expensive resources.

```Swift
override func viewDidAppear(_ animated: Bool) {
  super.viewDidAppear(animated) //always call super
  // tell my view what happened while I was gone.
}
```

#### `viewWillDisappear`

Analogous to viewWillAppear. This is a great place to undo whatever it was you did in viewWillAppear.

```Swift
override func viewWillDisappear(_ animated: Bool) {
  super.viewWillDisappear(animated)
  //code, e.g. undo what you did in viewWillAppear
} 
```

#### `viewDidDisappear`

Analogous to viewDidAppear. This one is rarely used, but could be useful for clearing up state.

```Swift
override func viewDidDisappear(_ animated: Bool) {
  super.viewDidDisappear(animated)
  //code, e.g. clean up MVC
}
```

## Lifecycle Methods - Geometry

As previously mentioned, you can't do geometry in `viewDidLoad`, as the bounds haven't been set. You also can't do it in `viewWillAppear`, or `viewDidAppear`. Instead, we have two seperate lifecycle methods for this:

* `viewWillLayoutSubviews()`
* `viewDidLayoutSubviews()`

These methods get called just before and just after your view has been set. I.e. just before and after it receives layoutSubviews.

Usually you don't have to do anything in here because of autolayout. Be aware that this method can be called quite frequently, so you need to ensure that whatever is calling it does so in an efficient fashion.

## Lifecycle Methods - Autorotation

Autorotation is what we call the process the iPhone goes through when it rotates from landscape to portrait mode. Of course, this triggers a change to the view's bounds, and hence triggers the will/did layout subviews methods above. In addition, it also triggers an animation of all the app's contents as they are rearranged.

You can inject code into this process using the method:

```Swift
override func viewWillTransition(to size: CGSize, with coordinator: UIViewControllerTransitionCoordinator) {
  super.viewWillTransition(to: size, with: coordinator)
  //code
}
```

In addition, you can even participate in the animation that occurs using the coordinator's `animate(alongsideTransition:)` method. More details about this are in the documentation.

## Lifecycle Methods - Low Memory

Rarely, your device can run low on memory, say if you have built up a lot of large videos, images or sounds. If your app is keeping strong pointers to items in the heap, you can help resolve this situation.

When a low memory warning occurs, the following method gets called in your controller:

```Swift
override func didReceiveMemoryWarning() {
  super.didReceiveMemoryWarning()
  // stop pointing to large memory items on the heap
  // that I'm not using and can recreate as needed
}
```

If your app persists in using an unfair amount of memory, iOS can kill it.

## `awakeFromNib`

This method is not technically a ViewController lifecycle method. However, it is sent to all methods that come out of a storyboard, including a ViewController.

```Swift
override func awakeFromNib() {
  super.awakeFromNib()
  //initialization code
}
```

This is sent very early in the lifecycle, before outlets are set and before preperation for segues. It's probably best to avoid it where possible. And of course, remember that it is only called for views and ViewControllers that come from storyboards.

[Previous Note](../Lecture%209%20-%20View%20Controller%20Lifecycle%20and%20Scroll%20Views/Part%200%20-%20Intro.md) | [Back To Contents](https://github.com/Firanus/stanford-iOS-lecture-notes) |  [Next Note](../Lecture%209%20-%20View%20Controller%20Lifecycle%20and%20Scroll%20Views/Part%202%20-%20UIScrollView.md)