# Lecture 12, Part 1: UITextField

UITextFields are essentially editable UILabels (though they are slightly more complicated). However, it's important to remember that on iPhones, having text fields isn't actually a great UI experience for the user. Keyboards on the phone aren't a primary input source, and can be a little awkward. (Think how long it can take to write our a detailed text message. Now think how long it would take your mum to do it.)

On the iPad, its not quite so bad, as you can use both hands.

Whenever a UITextField becomes a "first responder", the keyboard will appear. This is set up to happen automatically when one taps the field, or you can do it in code by sending the text field the `becomeFirstResponder` method. (You make the keyboard go away by sending `resignFirstResponder`)

Text fields also have delegates, which are the primary way you interact with it. For instance, there is a method, `textFieldShouldReturn`, that gets called whenever the user hits return. Often, you'll want to close the text field here.

Another, `textFieldDidEndEditing` sends when the text field stops being the first responder.

A UITextField is also a `UIControl`, so you can also set up target actions for certain actions if you want.

## Keyboard

There isn't an official keyboard object in iOS; as previously mentioned, we make it appear and disappear using `become/resignFirstResponder`.

Instead, if we want to control the appearance and behaviour of the keyboard, we do this using properties defined in the `UITextInputTraits` protocol (see [the documentation](https://developer.apple.com/documentation/uikit/uitextinputtraits) for more info)

Finally, its important to remember that when a keyboard comes up, it *covers up* your views, rather than moving them up. There are various ways of dealing with this, but we will leave them for the moment until we're introduced to notifications next week.

[Previous Note](../Lecture%2012%20-%20Drag%20and%20Drop%20UITableView%20UICollectionView%20and%20UITextField/Part%200%20-%20Intro.md) | [Back To Contents](https://github.com/Firanus/stanford-iOS-lecture-notes) | [Next Lecture](../Lecture%2013%20-%20Persistance/Part%200%20-%20Intro.md)