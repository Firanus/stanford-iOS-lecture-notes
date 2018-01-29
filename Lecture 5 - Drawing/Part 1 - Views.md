# Lecture 5, Part 1: Views

## Views

A view (i.e. `UIView` subclass) represents a rectangular area. It defines a coordinate space for drawing and handling touch events.

Views are *heirarchical*. A view can have:
* only one superview... `var superview: UIView?`
* many subviews... `var subviews: [UIView]`

The order of the subview array matters: those later in the array appear above those that are earlier. This has implications if you want to have transparent views.

A view can clip its subviews to its own bounds, but by default it does not.

### `UIWindow`

This is the UIView at the very top of the heirarchy. It includes items like the status bar. Usually, there is only one UIWindow in an iOS application. As such, we usually do not interact with it.

### Coding Views

Most of the time, the heirarchy is constructed graphically using Xcode. Even custom views can be added this way.

However, if you want to, you can also do it in code. You do this by using the functions:
```Swift
func addSubview(_ view: UIView) //this sends the view to its soon-to-be superview
func removeFromSuperview() //you have to send this message to the view you want to remove, NOT its superview.
```
### Where does the view heirarchy start?

The top of the (usable) view heirarchy is the Controller's `var view: UIView`.

This view is automatically wired up for you whe you create an MVC in Xcode. All your MVC's View's UIViews will have it as an ancestor, and it is this class that whose bounds will change when, e.g. the device is rotated.

In addition to accessing your view via this object, you can also access it by using outlets, as we have done thus far.

[Previous Note](../Lecture%205%20-%20Drawing/Part%200%20-%20Intro.md) | [Back To Contents](https://github.com/Firanus/stanford-iOS-lecture-notes) |  [Next Note](../Lecture%205%20-%20Drawing/Part%202%20-%20Initializing%20a%20UIView.md)