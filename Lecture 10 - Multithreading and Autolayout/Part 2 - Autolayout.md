# Lecture 10, Part 2: Autolayout

We've seen a fair amount of autolayout already, including:

* Using the dashed blue lines to align your UI elements.
* *Reset to Suggested Constraints* button, which tries to create constraints to reflect what you've set up on the storyboard.
* Ctrl+dragging to the edges and other views to set constraints
* Using the size inspector to set and edit simple constraints.
* Clicking on a constaint directly on the storyboard to get and set detailed information about the constraint.
* The 'pin' menu in the lower right hand corner to add constraints. (There's also an arrange button with more functionality)
* The Document Outline is an excellent place to view and edit constraints, and to solve layout problems.

Mastering Autolayout, however, takes a fair amount of time and experience.

It is possible to do all this autolayout work from code as well. The documentation for `UIView` has more information.

## Size Classes

Sometimes, however, autolayout is just not enough. You actually need to reposition views in their entirety, say, when you rotate the device.

The solution to this is something called size classes, which take a very simple approach to reporting sizes. Each of the width and the height can be only one of two values, either `regular` or `compact`. How do these breakdown? Well...

### iPhones

#### All - Portrait
* height - `regular`
* width - `compact`

#### Non-Plus Phones - Landscape
* height - `compact`
* width - `compact`

#### Plus Phones - Landscape
* height - `compact`
* width - `regular`

### iPads

#### All
* height - `regular`
* width - `regular`

#### However... Split View Master

Depending on the environment an MVC is in, for instance dimensions can be `compact`. For instance, the master view of a split view has a `compact` width.

### Using Size Classes

What can we do with our size classes? Well, as a starting point, you can vary a huge range of `UIView` properties.

But more importantly, you can have your constraints depend on your size classes. What's more, you can do this all graphically using the interface builder.

You can find your size classes by looking in the view controller's trait collection, e.g.
```Swift
let myHorizSizeClass: UIUserInterfaceSizeClass  = traitCollection.horizontalSizeClass
```
but it is rare to do this. We almost always do this using interface builder.

[Previous Note](../Lecture%2010%20-%20Multithreading%20and%20Autolayout/Part%201%20-%20Multithreading.md) | [Back To Contents](https://github.com/Firanus/stanford-iOS-lecture-notes)