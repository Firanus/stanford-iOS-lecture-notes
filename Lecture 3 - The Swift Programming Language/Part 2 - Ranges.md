# Lecture 3, Part 2: Ranges

How would we do the equivalent of `for(i = 0.5; i<15.25; i += 0.3)`? Because Floating Point numbers stride by floating points numbers, and not by Integers, they (e.g. `0.5...15.25`) are `Range`s, not `CountableRange`s, which you need for a `for-in`.

Our solution is to use the `stride` function, which allows you to create Countable ranges where you specify the step. So the equivalent of the above for loop would be:

```Swift
for num in stride(from: 0.5,  through: 15.25, by: 0.3) {
    //...
}
```

[Previous Note](../Lecture%203%20-%20The%20Swift%20Programming%20Language/Part%201%20-%20Autolayout%20Briefly.md) | [Back To Contents](https://github.com/Firanus/stanford-iOS-lecture-notes) |  [Next Note](../Lecture%203%20-%20The%20Swift%20Programming%20Language/Part%203%20-%20Tuples.md)