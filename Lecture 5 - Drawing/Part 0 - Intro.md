# Lecture 5: Drawing

Lecture 5 starts by covering a last few items of Swift, and then moves on to Custom Drawing, which is done largely through a demo.

W.r.t the Swift content, most of it is covered by Reading Exercise 3. To avoid duplicating content, we will only cover new content here.

## 4 Interesting Classes

* `NSObject` - Base class for all Objective-C classes. Some advanced features will require you to subclass from NSObject (and it can't hurt to do so)
* `NSNumber` - In Objective C, when you pass numbers around, you pass them as NSNumbers. It is a generic reference type (i.e. class) that can represent all kinds of numbers. All Objective C methods that took NSNumber have automatically been bridged to take Swift number types.
* `Date` - Value type used to find out the date and time right now or to store past and future dates. If you are displaying a date in your UI, there are localization ramifications, so be careful. See also `Calendar`, `DateFormatter`, `DateComponents`
* `Data` - A value type bag of bits". Used to save/restore/transmit raw data throughout the iOS SDK.

## Drawing Hints and Tricks

In the second half of the lecture, Paul covers a number of tips and tricks regarding drawing and using views. These are largely things better learnt by doing, rather than making notes. I will note the topics, but leave the rest for the programming exercises. The topics include:

* An example of drawing a triangle
* A few methods for drawing shapes and rounding corners
* How to clip an image to a subview
* How to set colors
* How to make views transparent
* How to hide a view without taking it from the view heirarchy (`isHidden`)
* Drawing text manually, rather than with UILabel
* Accessing a range of characters in an `NSString` string using `NSRange` for adding attributes to parts of an NSAttributed String:

  ```Swift
  let pizzaJoint = "café pesto"
  var attrString = NSMutableAttributedString(string: pizzaJoint)
  let firstWordRange = pizzaJoint.startIndex..<pizzaJoint.indexOf(" ")
  let nsrange = NSRange(firstWordRange, in: pizzaJoint)
  attrString.addAttribute(.strokeColor, value: UIColor.orange, range: nsrange)
  ```
* Drawing images, whether by using a `UIImageView`, or by creating a `UIImage` object, and linking it to a file in Assets.xcassets (or a file in the filesystem, or from a bag of bits).
* Redrawing on bounds changing with `UIViewContentMode` and the func `layoutSubviews()`

[Previous Lecture](../Lecture%204%20-%20More%20Swift/Part%202%20-%20NSAttributedStrings.md) | [Back To Contents](https://github.com/Firanus/stanford-iOS-lecture-notes) |  [Next Note](../Lecture%205%20-%20Drawing/Part%201%20-%20Views.md)