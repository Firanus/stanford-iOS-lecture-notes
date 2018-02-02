# Lecture 6: Multitouch

Lecture 6 begins with an extensive deme of drawing, which was introduced in the last lecture. It then introduces the concept of multitouch, and goes on to implement it in another demo.

Topics introduced during the demo:

* implementing the `CustomStringConvertible` protocol to make your classes `print` more readably.

* Drawing using `draw(_ rect:CGRect)`
  * Using Core Graphics
  * Using UIBezierPath
  * Changing the View Content Mode to 'redraw' to handle changing bounds.
  * Introducing clipping to views
  * Removing the `Opaque` setting on views for transparency
* Drawing using subviews
  * Creating a UILabel to show text
  * Fonts (`UIFont.preferredFont(forTextStyle:String)`) and centering (`NSMutableParagraphStyle.alignment`) in NSAttributedStrings
  * Introducing UIFontMetrics to scale fonts of custom sizes for accessibility purposes
  * Translating and Rotating subviews
* Using property observers in custom views to trigger redraws (call `setNeedsDisplay()`) and the laying out of subviews (call `setNeedsLayout()`)
* Overriding `traitCollectionDidChange(_ previousTraitCollection) to also layout subviews and scale text.
* Creating private structs to hold view-related magic numbers
* Using the size inspector to edit constraints.
* Fixing the aspect ratio of cards using constraints
* Ordering constraints.
* Adding and retrieving images using `UIImage(named:String)`
* Making your view visible in the interface builder using the `@IBDesignable` class attribute. (This doesn't work with images unless you add the `in` and `compatableWith` properties  to the UIImage constructor)
* Adding your custom view properties to the inspector using the `@IBInspectable` property attribute

[Previous Lecture](../Lecture%205%20-%20Drawing/Part%207%20-%20Fonts.md) | [Back To Contents](https://github.com/Firanus/stanford-iOS-lecture-notes) |  [Next Note](../Lecture%206%20-%20Multitouch/Part%201%20-%20Gestures.md)