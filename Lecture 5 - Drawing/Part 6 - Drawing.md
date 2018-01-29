# Lecture 5, Part 6: Drawing

The *only* way to draw is to create a UIView subclass and `override draw(CGRect)`. You can draw outside the rectangle if you want, as it is `bounds` that determines the drawing area. `rect` is there just as an optimization.

## NEVER, EVER call `draw(CGRect)`

Instead, if you need to redraw your view, call either:
```Swift
setNeedsDisplay()
``` 
or 
```Swift
setNeedsDisplay(_ rect: CGRect) //rect is the area to redraw
```

iOS will then redraw at the appropriate time. In the second case, you can select a smaller rect to redraw as an optimisation.

## How do we implement `draw(CGRect)`?

There are two main ways. You can either: 
* Get a drawing context and tell it what 
* Create a path of drawing using UIBezierPath

### Core Graphics Context

To use the core graphics context (option 1 above):
1. You get a context to draw into, e.g. by using `UIGraphicsCurrentContext()`
2. Create paths out of lines, arcs, etc.
3. Set drawing attributes like colors, fonts, textures, linewidths etc.
4. Stroke or fill (these are the only two options) the above created paths with the given attributes.

### `UIBezierPath`

Same as above, but it captures all the drawing in a `UIBezierPath` instance. For instance, it automatically draws into the current context, and has methods to draw, set attributes, colors, and to stroke and/or fill.

[Previous Note](../Lecture%205%20-%20Drawing/Part%205%20-%20Creating%20Views.md) | [Back To Contents](https://github.com/Firanus/stanford-iOS-lecture-notes) |  [Next Note](../Lecture%205%20-%20Drawing/Part%207%20-%20Fonts.md)