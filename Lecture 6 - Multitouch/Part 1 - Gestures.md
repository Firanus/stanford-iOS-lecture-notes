# Lecture 6, Part 1: Gestures

There are two ways to get touches in iOS:
1. Get notified of the raw touch events (don't do this one)
2. React to certain predefined touch events. This is the way to go!

To get the gestures, we use the classes that inherit from an abstract base class called `UIGestureRecogniser`. There is one for each of the main gestures, e.g. `UIPanGestureRecognizer`. There are a [variety of common gesture that iOS supports](https://developer.apple.com/ios/human-interface-guidelines/user-interaction/gestures/)

In more depth, the process is:
1. Add a gesture recogniser to a `UIView`. This is usually done by the controller, though it can be done by the view itself if its integral to its existence.
2. Provide a method to handle the gesture. This can be done be either the View (i.e. if it only affects the way things are viewed) or the Controller (i.e. if it in some way affects the model).

## Setting the Recogniser

The first step, setting the gesture recogniser, is usually done in the `didSet` of an outlet setter, which gets called when iOS sets up the outlet:

```Swift
@IBOutlet weak var pannableView: UIView {
  didSet {
    let panGestureRecognizer = UIPanGestureRecognizer(
      target: self, action: #selector(ViewController.pan(recognizer:))
    )
    pannableView.addGestureRecognizer(panGestureRecognizer)
  }
}
```

In this method, the parameters are:
* `target` - which is what gets notified when the gesture is recognised. Here, it is the controller
* `action` - the method invoked on recognition.  The argument to that method is the recognizer.

You can add as many gesture recognizers as you want.

You can also add the gesture recognizer to the storyboard directly using the interface builder. This can be useful for simple gestures.

## Gesture Methods and States

The handler for a gesture needs gesture-specific information. For example, the UIPanGestureRecognizer provides 3 methods:

* `func translation(in: UIView?) -> CGPoint`
* `func velocity(in: UIView?) -> CGPoint`
* `func setTranslation(CGPoint, in: UIView?)`

The final one is interesting, as it lets you reset the translation so far. This can provide "incremental" translation.

Gestures are also provided (by the abstract superclass) with a property called `state`. This enum has several states. For a pan (an example of a continuous gesture), the ones that are triggered are:
* `.possible` - State before the pan starts
* `.began` - State when the finger goes down and a pan begins
* `.changed` - State that is set repeatedly as the pan goes on
* `.ended` - State that triggers when the finger is lifted

Other gestures are discrete (either on or off). For a swipe, the state changes would go from `.began` straight to `.ended` or `.recognised`. The key is that the gesture recigniser gets called whenever one of these state changes happens, even if a state is changing to itself (i.e. `.changed -> .changed`).

We also have two other important states:
* `.failed` - This one often gets triggered if you have multiple competing gestures (e.g. a tap and a pan), and one 'wins'. The other gets set to .failed.
* `.canceled` - This one happens a lot with drag and drop. For instance, it looks like we're about to start a gesture, but then it becomes a drag and drop. In this case the other state (e.g. a pan) becomes .canceled.

## The Handler

What might a handler look like? For our pan gesture, and many others, it makes sense to `switch` on the recognizer's state. In fact, you should **always** do this:

```Swift
@objc func pan(recognizer: UIPanGestureRecognizer) {
  switch recognizer.state {
    case .changed: fallthrough
    case .ended:
      let translation = recognizer.translation(in: pannableView)
      //update of anything that depends on the pan gesture using translation.x and .y
      recognizer.setTranslation(CGPoint.zero, in: pannableView)
    default: break
  }
}
```

Note the `@objc` annotation on the method. This is necessary because the gesture action recogniser is built on Objective C. As a result, any method that is the action of a gesture recogniser needs this annotation.

[Previous Note](../Lecture%206%20-%20Multitouch/Part%200%20-%20Intro.md) | [Back To Contents](https://github.com/Firanus/stanford-iOS-lecture-notes) | [Next Lecture](../Lecture%207%20-%20Multiple%20MVCs%20Timer%20and%20Animation/Part%200%20-%20Intro.md)