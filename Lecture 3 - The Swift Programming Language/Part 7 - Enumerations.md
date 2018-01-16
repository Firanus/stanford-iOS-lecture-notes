# Lecture 3, Part 7: Enumerations

Enums are an additional type of state, in addition to classes and structs. They are **value types** that can only take discrete values, e.g.

```Swift
enum FastFoodMenuItem {
    case hamburger
    case fries
    case drink
    case cookie
}
```

## Associated Data

In Swift, each case can (but does not have to) have its own associated data. e.g.

```Swift
enum FastFoodMenuItem {
    case hamburger(numberOfPatties: Int)
    case fries(size: FryOrderSize)
    case drink(String, ounces: Int) //Unnamed string is the brand, e.g. "Coke"
    case cookie
}
```

Note that the drink case has two pieces of associated data. FryOrderSize could also be an enum, e.g.:
```Swift
enum FryOrderSize {
    case large
    case small
}
```

## Setting the Value

When you set the value of an enum you must provide the associated data (if any):
```Swift
let menuItem: FastFoodMenuItem = FastFoodMenuItem.hamburger(patties: 2)
let otherItem: FastFoodMenuItem = FastFoodMenuItem.cookie
```
The **only** time you can set the associated data of an enum is when you initialise it.

Swift can also infer type on one or the other side of the assignment operator (but not both)

```Swift
let menuItem = FastFoodMenuItem.hamburger(patties: 2)
let otherItem: FastFoodMenuItem = .cookie
```

## Checking an enum's State

This is **not** done using an `==` operator. Instead, you use `switch`:
```Swift
var menuItem = FastFoodMenuItem.hamburger(patties: 2)
switch menuItem {
    case .hamburger: print("burger")
    case .fries: break
    default: print ("other")
}
```

Note that:
* At the moment, we are ignoring the associated data. 
* We've omitted FastFoodMenuItem, as Swift can infer it.
* We've used `break` to tell Swift that we don't want to do anything with the fries type
* We've used `default`  to wrap up a few cases. This is important, as `switch` statements must handle every possible case.

## Accessing associated data

This is done using the `let` syntax as shown below:

```Swift
var menuItem = FastFoodMenuItem.hamburger(patties: 2)
switch menuItem {
    case .hamburger(let pattyCount): print("a burger with \(pattyCount) patties!")
    default: break
}
```

The name we give to the parameter does not have to be the same as the associated type's internal name.

## Methods and Computed Properties

Enums are allowed to have both methods and computed properties. However, they are not allowed stored properties; the only state an enum can have is its case and any associated data. 

```Swift
enum FastFoodMenuItem {
    case hamburger
    case fries
    case drink
    case cookie
    
    func isIncludedInSpecialOrder(number: Int) -> Bool { /*...*/ }
    var calories: Int { /*...*/ }
}
```

Such an enum can access its own associated data using `switch self`.

An enum can also modify its own state. However, you have to put the `mutating` keyword in front of the function. This is also required in `struct`s. It is necessary because Swift uses copy-on-write when passing on value types. To do so, it needs to know which methods might write. `mutating` tells it.

[Previous Note](../Lecture%203%20-%20The%20Swift%20Programming%20Language/Part%206%20-%20Extensions.md) | [Back To Contents](https://github.com/Firanus/stanford-iOS-lecture-notes) |  [Next Note](../Lecture%203%20-%20The%20Swift%20Programming%20Language/Part%208%20-%20Optionals.md)