# Lecture 3, Part 5, Access Control

Swift supports a number of access control keywords:

* `internal` - The default. It means 'usable by any object in my app or framework.'
* `private` - Only callable from within this object
* `private(set)` - The property is readable outside the object, but not settable.
* `fileprivate` - Accessible by any code within this source file.
* `public` - (Frameworks only) this can be used by objects outside my framework
* `open` - (Frameworks only) public and objects outside my framework can subclass this.

We will be focused on the first 4 in this course, as we are focused on building apps.

A good strategy is to mark everything `private` by default, and only remove the designation when you are sure that the API is ready to be used by other code.

[Previous Note](../Lecture%203%20-%20The%20Swift%20Programming%20Language/Part%204%20-%20Computed%20Values.md) | [Back To Contents](https://github.com/Firanus/stanford-iOS-lecture-notes) |  [Next Note](../Lecture%203%20-%20The%20Swift%20Programming%20Language/Part%206%20-%20Extensions.md)