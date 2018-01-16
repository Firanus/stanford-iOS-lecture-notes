# Lecture 3, Part 1: Autolayout, Briefly

There are two things we need to do to make the cards of our concentration game stack automatically:
* We need to make our buttons *stick to the edges*, rather than stick to the upper left corner (the origin of drawing in iOS) as they do at the moment.
* We also need to *group them together* so they can share the space.

Two different features in iOS allow us to accomplish this:
* To group, we will us `UIStackView`. It takes other views and stacks them together either horizontally or vertically.
    * For our Concentration game, we'll need to stack each row horizontally, and then stack the collection of rows vertically
    * There is a button in Xcode which does this automatically. Inspecting the element in the Utilities panel then allows you to adjust the card spacing, axis and distribution.
* To pin items, we need to create relationships between views, which we do by Ctrl+Dragging the Grouped elements to the edges of the view and selecting the 'to Safe Space' options.

[Previous Note](../Lecture%203%20-%20The%20Swift%20Programming%20Language/Part%200%20-%20Intro.md) | [Back To Contents](https://github.com/Firanus/stanford-iOS-lecture-notes) |  [Next Note](../Lecture%203%20-%20The%20Swift%20Programming%20Language/Part%202%20-%20Ranges.md)