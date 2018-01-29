# Lecture 5, Part 3: Coordinate System Data Structures

Before we can talk about how we draw, we need to talk about 4 very important data structures. They are all preceded with CG, which stands for *Core Graphics*. iOS has other drawings (e.g. for 3D) that we will not cover here. The structures are:

* `CGFloat` - This is the type you *must* use to talk to the UIView's (floating-point) coordinate system. You can convert to and from `Double` and `Float` using initializers. e.g. 
  ```Swift
  let cgf = CGFloat(aDouble)
  ```
* `CGPoint` - A `struct` with two CGFloats in it, `x` and `y`.
  ```Swift
  var point = CGPoint(x: 37.0, y: 55.2)
  ```
* `CGSize` - Also a `struct` with two CGFloats: `width` and `height`.
  ```Swift
  var size = CGSize(width: 100.0, height: 50.0)
  ```
* `CGRect` - A `struct` with a `CGPoint` and a `CGSize` in it. It represents  rectangle, and has a number of other very useful methods.
  ```Swift
  struct CGRect {
    var origin: CGPoint
    var size: CGSize
    //...
  }
  ```
  
[Previous Note](../Lecture%205%20-%20Drawing/Part%202%20-%20Initializing%20a%20UIView.md) | [Back To Contents](https://github.com/Firanus/stanford-iOS-lecture-notes) |  [Next Note](../Lecture%205%20-%20Drawing/Part%204%20-%20View%20Coordinate%20System.md)