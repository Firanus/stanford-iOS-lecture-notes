# Lecture 8, Part 2: UIView Transitions

Sometimes you want to make modifications to an entire view at once. This can include things like rotating the entire view (say, flipping a card), dissolving between states, and curling up and down.

With these animations, you are not limited to special properties of the view.

To do this, you use the UIView method `transition`:

```Swift
UIView.transition(with: myPlayingCardView,
  duration: 0.75,
  options: [.transitionFlipFromLeft],
  animations: { cardIsFaceUp = !cardIsFaceUp }
  completion: nil
)
```

The above method could, for example, be used to flip over a playing card.

[Previous Note](../Lecture%208%20-%20Animation/Part%201%20-%20UIViewPropertyAnimator.md) | [Back To Contents](https://github.com/Firanus/stanford-iOS-lecture-notes) |  [Next Note](../Lecture%208%20-%20Animation/Part%203%20-%20Dynamic%20Animations.md)