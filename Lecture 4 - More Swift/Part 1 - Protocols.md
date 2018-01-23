# Lecture 4, Part 1: Protocols

We encounter protocols in the reading exercise, but what are they really about? Essentially, protocols let us express a specific API more concisely. By requiring that an implementing type has a particular set of properties and/or methods, we can abstract away details of the underlying implementation. That means that when we're using our API (i.e. a class/struct/enum conforming to the type) we can utterly ignore the specifics of *how* it does what we need it to do.

Protocols are good for:
* Making APIs more flexible and expressive
* Blind, structured communication between View and Controller (delegation)
* Mandating behaviour (e.g. the keys of a dictionary must be hashable)
* Sharing functionality in different types (`String`, `Array`, and `CountableRange` are all `Collections`)
* Multiple inheritance (of functionality, not data remember).

## Optional Protocols

Normally, in Swift, a protocol implementor would be required to implement all the properties and/or methods of the protocol.

However, *in Objective C*, this was *not the case*. You could have optional methods in protocols. To write such protocols, there are a few things you have to do:
1. You must mark your *protocol* `@objc`
2. You must mark the optional *method* with the `optional` keyowrd. This is completely different to an Optional type.
3. Any class that implements an optional protocol must inherit from `NSObject`.

These sorts of protocols are used often in iOS for delegation. Outside of that, they are rarely, if ever used.

As the `@objc` decleration suggests, they're mostly there for backwards compatability. So we encounter them when interacting with parts of the iOS framework that were built back in the Objective C days.

## Delegation

A very important use of protocols is in delegation. It allows us to implement "blind communication" between a View and its Controller. This plays out in the following way (Note the similarity to [the example](https://developer.apple.com/library/content/documentation/Swift/Conceptual/Swift_Programming_Language/Protocols.html#//apple_ref/doc/uid/TP40014097-CH25-ID276) in the Language Guide):

1. A View declares a delegation `protocol` (i.e. what the View want the Controller to do for it. This is the list of `will`s, `did`s and `should`s)
2. The View's API has a `weak` delegate property whose type is that delegation protocol
3. The View uses the delegate property to get/do things it can't own/control on its own.
4. The Controller declares that it implements the protocol
5. The Controller sets the delegate of the View to itself using the property from 2. above
6. The Controller implements the protocol (probably it has a lot of optional methods in it)

At the end of this process, the view is hooked up to the controller, but has no idea what it is, so it remains generic and reusable.

This method was designed pre-closures, which can be a better option.

## Constraining Generic Types

Another use of protocols is to limit the scope of generic types. The most obvious case of this is with Dictionaries, which are declared as:

```Swift
Dictionary<Key: Hashable, Value>
```

Here, `Hashable` is a protocol which requires the type to implement a hashValue property. As a point of interest, `Hashable`, inherits from `Equatable`, which requires the developer to specify the `==` operator for their type. So to make a class hashable, you must satisfy both requirements.

We demonstrate this in action by making the Concentration game's Card's Hashable.

## "Multiple Inheritance"

A good example of a class that conforms to multuple protocols is `CountableRange`, which amongst others implements `Sequence` and `Collection`.

A perk of doing it this way is that if you implement `Sequence`, which requires you to make a `makeIterator` function, you automatically gain automatic implementations of methods like `contains()`, `forEach()`, `min()`, `max()`, `map()`, `filter()` and more. This is because all of these methods were implemented as an extension to the `Sequence` protocol.

[Previous Note](../Lecture%204%20-%20More%20Swift/Part%200%20-%20Intro.md) | [Back To Contents](https://github.com/Firanus/stanford-iOS-lecture-notes) |  [Next Note](../Lecture%204%20-%20More%20Swift/Part%202%20-%20NSAttributedStrings.md)