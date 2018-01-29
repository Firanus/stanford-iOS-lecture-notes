# Lecture 4, Part 2: NSAttributedStrings

Conceptually, an `NSAttributedString` is a an object that pairs a String with a Dictionary of attributes for each character. These attributes comprise things like the cards' font and color. In addition, you can put these strings on `UILabel` and `UIButton` classes, or even on the screen directly.

The syntax for creating an attributed string is:

```Swift
let attributes: [NSAttributedStringKey : Any] = [ //note: type cannot be inferred here
  .strokeColor : UIColor.orange
  .strokeWidth : 5.0 //negative number would mean fill. Positive means outline.
]

let attribtext = NSAttributedString(string: "Flips: 0", attributes: attributes)
flipCountLabel.attributedText = attribtext
```

The syntax here is a little unusual, because this is an Objective C API (the "NS" is your clue) trying to live in the Swift world. We need to explicitly type the Dictionary value as `Any`, because the attributes can have various different types. This is normally very bad practice in Swift. Instead, it'd be much more normal to have an enum of some kind. While this is not an option here, you should NEVER design your own APIs to use the `Any` keyword.

NSAttributedStrings are entirely different to strings. They are classes, not structs. And to make mutable strings, you need to use another class; `NSMutableAttributedString`.

In addition, NSAttributedStrings were designed to work with NSStrings (Objective C's old string type), and as such have slightly different encoding to Swift strings. This means that you need to be careful of "wacky" Characters when converting from one to t'other.

[Previous Note](../Lecture%204%20-%20More%20Swift/Part%200%20-%20Intro.md) | [Back To Contents](https://github.com/Firanus/stanford-iOS-lecture-notes) |  [Next Lecture](../Lecture%205%20-%20Drawing/Part%200%20-%20Intro.md)