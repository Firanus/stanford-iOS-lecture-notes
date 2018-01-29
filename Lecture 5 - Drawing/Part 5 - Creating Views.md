# Lecture 5, Part 5: Creating Views

Normally, you create views using a storyboard. This can be done by adding a generic view from Xcode's Object Palette, and then inspecting it to set its class to your subclass.

You can do it from code as well, by using an initializer:
```Swift
let newView = UIView(frame: myViewFrame)
```
The empty initializer `UIView()` sets frame to `CGRect.zero`, a rectangle with zero origin and zero size.

[Previous Note](../Lecture%205%20-%20Drawing/Part%204%20-%20View%20Coordinate%20System.md) | [Back To Contents](https://github.com/Firanus/stanford-iOS-lecture-notes) |  [Next Note](../Lecture%205%20-%20Drawing/Part%206%20-%20Drawing.md)