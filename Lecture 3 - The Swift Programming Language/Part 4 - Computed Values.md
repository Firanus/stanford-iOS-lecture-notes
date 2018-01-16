# Lecture 3, Part 4: Computed Values

The values of properties can be computed rather than stored. These are ideal in circumstances where a property is derived from other state.

A **stored** property looks like:
```Swift
var foo: Double
```

A **computed** property looks like this:
```Swift
var foo: Double {
    get {
        //return the calculated value of foo
    }
    set(newValue) {
        //do something based on the fact foo has changed to newValue
    }
}
```

You don't have to implement `set`. If you don't, the property will become read-only.

Note that if you do implement `set`, you don't explicitly have to name the variable (i.e. you could write `set { //... }` rather than `set(newValue) { //... }`. If you do this, the variable is automatically given the default name, `newValue`.

An example of a good opportunity to implement this in our Concentration app is the `indexOfOneAndOnlyOneFaceUpCard` property. Rather than manually updating that, it would make a lot more sense to compute it by just looking at all the cards to see if there is one face up. If there is, return its index, if not, return nil. The set could then turn all other cards facedown.

[Previous Note](../Lecture%203%20-%20The%20Swift%20Programming%20Language/Part%203%20-%20Tuples.md) | [Back To Contents](https://github.com/Firanus/stanford-iOS-lecture-notes) |  [Next Note](../Lecture%203%20-%20The%20Swift%20Programming%20Language/Part%205%20-%20Access%20Control.md)