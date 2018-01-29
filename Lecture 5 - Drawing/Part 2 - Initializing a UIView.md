# Lecture 5, Part 2: Initializing a UIView

## Using an initializer (AVOID)

As always, try to avoid doing this using an initializer. If you have to, it is slightly more common to have a `UIView` initialiser than a `UIViewController` initialiser.

If you do have to, UIView has two initializers, and you **must implement both**:
* `init(frame: CGRect)` - This is the initializer if the UIView is created in code.
* `init(coder: NSCoder)` - This is the initializer used if the UIView comes out of a storyboard. (`NSCoder` is a protocol which handles "freeze-drying" the storyboard content and generating it in the app when you run it.)

The reason that you have to implement both is that:
1. `init(frame: CGRect)` is a designated initializer
2. `init(coder: NSCoder)` is a `required` (failable) initialiser required by a protocol that UIView implements.

## Using `awakeFromNib()`

This is a function that's sent to every single object that comes out of an interface builder (storyboard). As a result, it will only work for UIViews that come from storyboards.

It is called immediately after initialization is complete.Order is not guaranteed, so you can't message other objects in the storyboard here.

[Previous Note](../Lecture%205%20-%20Drawing/Part%201%20-%20Views.md) | [Back To Contents](https://github.com/Firanus/stanford-iOS-lecture-notes) |  [Next Note](../Lecture%205%20-%20Drawing/Part%203%20-%20Coordinate%20System%20Data%20Structures.md)