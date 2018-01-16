# Lecture 3, Part 8: Optionals

Optionals are just enums with two states:
* not set - `nil`
* set - `some(<T>)` with associated data of whatever the object in question is

However, they are very important, and so have a great deal of unique syntax:

* The "not set" case has a special keyword, `nil`
* The `?` is used to declare an optional
* The `!` is used to unwrap an optional if it is in the set case
* The keyword `if` can be used to conditionally access the associated data
* An Optional can be declared with `!` instead of with `?`. This makes it *implicitly unwrap* when accessed
* The nil-coalescing operator, `??` allows us to return a default if trying to access an optional that is not set
* You can also use `?` when *accessing* an optional to bail out of an expression mid-stream. This is called **Optional Chaining**

## Optional Chaining

We have not yet seen Optional Chaining, so an example is shown below. The syntax for it is:
```Swift
let x: String? = ...
let y = x?.foo()?.bar?.z
```
where we assume `x`,`foo()`,`.bar` are/return Optionals. In enums, this would be equivalent to:

```Swift
switch x {
case .none: y = nil
case .some(let data1):
    switch data1.foo() {
        case .none: y = nil
        case .some(let data2):
            switch data2.bar {
                case .none: y = nil
                case .some(let data3): y = data3.z
            }
    }
}
```

[Previous Note](../Lecture%203%20-%20The%20Swift%20Programming%20Language/Part%207%20-%20Enumerations.md) | [Back To Contents](https://github.com/Firanus/stanford-iOS-lecture-notes) |  [Next Note](../Lecture%203%20-%20The%20Swift%20Programming%20Language/Part%209%20-%20Data%20Structures.md)