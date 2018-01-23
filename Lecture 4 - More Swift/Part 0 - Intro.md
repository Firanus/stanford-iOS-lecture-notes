# Lecture 4: More Swift

The main focus of this lecture will be Protocols and Closures. As both these topics are covered at length in Reading 2 (see [this repo](https://github.com/Firanus/swift-language-guide-notes) for more info), we won't aim to duplicate content in these lecture notes. Rather, we'll try to add additional detail when its available.

## `mutating` Demo

At the start of the lecture, Paul turns the `Concentration` class into a `struct`. This necessitates changing the `chooseCard` method to be `mutating`. I have not replicated this in our own code because I do not believe it actually improves the codebase, it merely serves to demonstrate a function.

## Strings

After covering protocols (see next note), Paul gives an explanation of the way Swift represents strings. The intricacies of this (unicodes etc.) is covered by notes [3.1](https://github.com/Firanus/swift-language-guide-notes/blob/master/3%20-%20Strings%20and%20Characters/3.1%20-%20Unicode.md), [3.2](https://github.com/Firanus/swift-language-guide-notes/blob/master/3%20-%20Strings%20and%20Characters/3.2%20-%20Counting%20Characters.md), [3.3](https://github.com/Firanus/swift-language-guide-notes/blob/master/3%20-%20Strings%20and%20Characters/3.3%20-%20Accessing%20and%20Modifying%20a%20String.md) and [3.6](https://github.com/Firanus/swift-language-guide-notes/blob/master/3%20-%20Strings%20and%20Characters/3.6%20-%20Unicode%20Representations%20of%20Strings.md) of the reading exercise notes.

For even more info, see the [Swift Language Guide entry](https://developer.apple.com/library/content/documentation/Swift/Conceptual/Swift_Programming_Language/StringsAndCharacters.html#//apple_ref/doc/uid/TP40014097-CH7-ID293)

We demonstrate this by making the `emojiChoices` array in our Concentration game into a `String`.

## Closures

Finally, in the lecture, Paul tackles closures. The information he covers is also covered in our [reading exercise notes](https://github.com/Firanus/swift-language-guide-notes/tree/master/12%20-%20Closures), so we won't duplicate that content.

We demonstrate the content by improving our implementation of `indexOfTheOneAndOnlyFaceUpCard` in Concentration.

[Previous Lecture](../Lecture%203%20-%20The%20Swift%20Programming%20Language/Part%209%20-%20Data%20Structures.md) | [Back To Contents](https://github.com/Firanus/stanford-iOS-lecture-notes) |  [Next Note](../Lecture%204%20-%20More%20Swift/Part%201%20-%20Protocols.md)