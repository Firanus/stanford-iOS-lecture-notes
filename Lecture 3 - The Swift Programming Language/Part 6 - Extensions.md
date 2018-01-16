# Lecture 3 Part 6: Extensions

You can add methods/properties to a class/struct/enum, even if you don't have the source.
There are a few restrictions however:
* You can't re-implement methods or properties that are already there. Only add new ones.
* The properties you add can have no storage associated with them (computed only)

These functions are easily abused, so it is best to be careful with them. Remember, they should improve readability, not to obfuscate. Indeed, when used well, they can be very effective at organising code, though they require a commitment to architecture.

For beginners, it is best to stick to small, well-contained helper functions.

[Previous Note](../Lecture%203%20-%20The%20Swift%20Programming%20Language/Part%205%20-%20Access%20Control.md) | [Back To Contents](https://github.com/Firanus/stanford-iOS-lecture-notes) |  [Next Note](../Lecture%203%20-%20The%20Swift%20Programming%20Language/Part%207%20-%20Enumerations.md)