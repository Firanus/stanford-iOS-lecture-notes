# Lecture 8, Part 1: UIViewPropertyAnimator

We can animate changes to certain UI properties over time. The properties we can vary are (and this is the complete list):
* `frame` \ `center`
* `bounds` (transient size, which does not conflict with animating center)
* `transform` (translation, rotation, scaling)
* `alpha` (opacity)
* `backgroundColor`

We do this using a class called `UIViewPropertyAnimator`. To use it we pass it some animation parameters and a closure which contains the animation code. This code is executed immediately. You can also pass a second closure to be executed as soon as the animation is complete.

The `UIViewPropertyAnimator` class is extremely powerful, and we do not have the time to cover it in great depth. However, we will cover basic usage, which can be accomplished using the `runningPropertyAnimator` function:

```Swift
class func runningPropertyAnimator (
  withDuration: TimeInterval,
  delay: TimeInterval,
  options: UIViewAnimationOptions,
  animations: () -> Void,
  completion: ((position: UIViewAnimatingPosition) -> Void)? = nil
)
```

An example is shown below, which fades out a view over 3 seconds, beginning 2 seconds after it is called:

```Swift
if myView.alpha == 1.0 {
  UIViewPropertyAnimator.runningPropertyAnimator (
    withDuration: 3.0,
    delay: 2.0,
    options: [.allowUserInteraction],
    animations: { myView.alpha = 0.0 },
    completion: { if $0 == .end { myView.removeFromSuperview() } }
  )
  print("my alpha value is \(myView.alpha)")
}
```

It's important to note that while the change to transparency will not be visible to the user for 5 seconds, in the code, the alpha has immediately been set to 0. i.e. we will see the console output "my alpha value is 0.0" immediately. However, myView will remain a part of the superview until the animation is complete.

There are a wide range of available options you can set when animating UIView properties. The [ documentation for UIViewAnimationOptions](https://developer.apple.com/documentation/uikit/uiviewanimationoptions) lists them all.

[Previous Note](../Lecture%208%20-%20Animation/Part%200%20-%20Intro.md) | [Back To Contents](https://github.com/Firanus/stanford-iOS-lecture-notes) |  [Next Note](../Lecture%208%20-%20Animation/Part%202%20-%20UIView%20Transitions.md)