# Lecture 9, Part 2: UIScrollView

This is a very powerful UIView. You can nest horizontal (think iPhone home menu) and vertical scrollviews (think a web page) within each other. Indeed, this feature has been around since iPhone 1.

## Basic Positioning

ScrollView's most important property is `contentSize`, which tells the view how big the space its scrolling around is. Once you've done this however, adding a subview is just the same as adding it to a UIView. So the whole process is:

```Swift
scrollView.contentSize = CGSize(width: 3000, height: 2700)
logo.frame = CGRect(x: 2700, y: 50, width: 120, height: 180)
scrollView.addSubview(logo)
```

## Other Properties

Some other good-to-know properties:
* `contentOffset: CGPoint` - A variable detailing the upper left corner of what the scroll view is currently showing in the content area's coordinate system.
* To obtain the visible rectangle (not necessarily intuitive as the user might have zoomed in on some content), you can use the `convert(_:CGRect, from: UIView)` methods.
* `scrolLRectToVisible(CGRect, animated: Bool)` allows you to scroll programmatically.
* You can also disable scrolling, lock scroll direction, style the scroll indicators, and inset content from the content area.

## Zooming

All UIViews have a property called transform which is an affine transformation (translation, rotation and scaling). All that happens when you zoom in a scroll view is that this property gets modified.

One thing to be careful of, however, is that the `contentSize` and `contentOffset` properties will change when you're zooming.

To enable zoom, you **have to** set the following two properties:
* `scrolLView.maximumZoomScale` e.g. 2.0 would allow scaling to twice its normal size
* `scrollView.minimumZoomScale` e.g. 0.5 would allow scaling to half its normal size

By default, both of these properties are set to 1.0, i.e. no zooming.

You also **have to** implement a `delegate` method called `func viewForZooming(in scrollView: UIScrollView) -> UIView`. This method tells the scroll view which of its subviews to scroll. If you have multiple subviews, often what you would do is put all of them into a single view, and then do your zooming on that view.

There are programmatic methods to zoom, including setting the `zoomScale` property and using the `zoom(to: CGRect)` method, which zooms until the target rect just barely fits into the view.

 ## Delegate Methods
 
ScrollView has a wide variety of delegate methods which you can use yo keep up to date with what's going on in the view. We won't go into great detail on them, but the documentation contains the necessary information.

[Previous Note](../Lecture%209%20-%20View%20Controller%20Lifecycle%20and%20Scroll%20Views/Part%201%20-%20View%20Controller%20Lifecycle.md) | [Back To Contents](https://github.com/Firanus/stanford-iOS-lecture-notes) | [Next Lecture](/Lecture%2010%20-%20Multithreading%20and%20Autolayout/Part%200%20-%20Intro.md)