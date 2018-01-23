# Lecture 3, Part 9: Data Structures

Swift has 4 essential data structure-building concepts:
* `class`
* `struct`
* `enum`
* `protocol`

## `class`

Classes support OOP, and have **single** inheritance of both functionality and data. (i.e. instance variables)

Classes are reference types stored in the heap and passed around using references.

The Heap is automatically kept clean by Swift, using *reference counting*, rather than garbage collection.

### [Automatic Reference Counting](https://developer.apple.com/library/content/documentation/Swift/Conceptual/Swift_Programming_Language/AutomaticReferenceCounting.html)

In order to know when to reclaim memory from the objects stored in the heap, Swift (automatically) "counts references" to them. As soon as there are zero references to the object, it is immediately deallocated. This makes the process deterministic and preictable.

In contrast, Garbage Collection is a typically two step process that runs in the background of your project. The steps are:
1. Going through the object graph and mark the objects which are safe to remove.
2. At some indeterminate time later, deallocate the marked objects.

This is less predictable and immediate than ARC. However, it has advantages of its own. See [this article](https://www.jbssolutions.com/garbage-collection-net-vs-arc-swift/) for more information.

#### Influencing ARC

You can influence ARC using the following keywords:

* `strong` - This is normal reference counting. As long as anyone has a strong reference to the object, it will remain in the heap.
* `weak` - Weak means "If nobody else is interested in this, then neither am I. In that case set me to `nil`". As a result, they will *never* keep an object in the heap. Because weak pointers have to be nil-able, they apply only to Optional pointers to reference types. Good examples include outlets (which are strongly held by the View heirarchy, so they can be weakly held by the outlet).
* `unowned` -  Unowned means "don't reference count this, and crash if I'm wrong". Very rarely used. Usually only to break the memory cycles between objects. This is when to objects in the heap reference each other, but nothing else. Thus, they keep each other in the heap, but are of no use to anyone else. They are quite hard to make in Swift, except when closures are concerned. We'll get back  to them on Wednesday

## `struct`

Structures in Swift are all value types that use-copy-on-write. That behaviour requires you to mark methods as `mutating` if they alter internal state.

Structures don't support inheritance (of data), and can have their mutability controlled using the `let` keyword. They also support functional programming design.

## `enum`

Used for variables that have one of a discrete set of values, each of which can, in principle, have associated data with it. They are value types that can have methods and computed properties (i.e. not stored properties).

## `protocol`

Protocal are a type which is a declaration of **functionality only**. They have **no data storage of any kind**, so it doesn't really make sense to call them value or reference types. They essentially provide multiple inheritance of functionality to Swift.

We'll take a deeper look at them in Lecture 4.

[Previous Note](../Lecture%203%20-%20The%20Swift%20Programming%20Language/Part%208%20-%20Optionals.md) | [Back To Contents](https://github.com/Firanus/stanford-iOS-lecture-notes) |  [Next Lecture](../Lecture%204%20-%20More%20Swift/Part%200%20-%20Intro.md)