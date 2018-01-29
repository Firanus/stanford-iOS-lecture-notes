# Lecture 5, Part 4: View Coordinate System

There are a number of important detauls to note about the view coordinate system:

* The origin is in the **upper left**. Thus:
  * Increasing x pushes items to the *right*
  * Increasing y pushes items *down*
* Units are *points*, not pixels. Points are the minimum-sized unit of drawing your device is capable of. You can see how many pixels per point there are by checking `UIView.contentScaleFactor: CGFloat`
* The boundaries of where drawing happens are availble in a view's `bounds: CGRect` property. This rectangle contains the drawing space in its own coordinate system. It's up to your view's implementation to interpret where `bounds.origin` means. Often, nothing
* The position of a UIView is determined by the properties (neither of which are needed for drawing):
  * `center: CGPoint` - represents the center of a UIView in its *superview's coordinate system*.
  * `frame: CGRect` - the rect containing a UIView in its *superview's coordinate system*.

One might assume `frame` and `bounds` are always the same, but views can be rotated. As a result, they can be different. So never use frame to draw.

[Previous Note](../Lecture%205%20-%20Drawing/Part%203%20-%20Coordinate%20System%20Data%20Structures.md) | [Back To Contents](https://github.com/Firanus/stanford-iOS-lecture-notes) |  [Next Note](../Lecture%205%20-%20Drawing/Part%205%20-%20Creating%20Views.md)