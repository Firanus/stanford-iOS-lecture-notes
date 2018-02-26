# Lecture 11, Part 2: Table and Collection Views

Table and Collection Views are both subclasses of UIScrollView that are designed to show unbounded amounts of information. TableViews display it as a list, while CollectionViews display it in a configurable 2D format. The default is one called "flow layout", which mimics the way text is laid out on a page (left to right, flowing onto the next row).

The APIs of the two systems are very similar, so we will look at them in tandem.

## Layouts - Basic and Custom

Table Views support many of the standard features you would expect form a list. You can:

* list items (duh)
* have sections
* group your items (typically only used for static views)
* show ancilliary information (e.g. an image) in one of 4 basic styles
  * Basic - text only
  * Subtitle - show your ancilliary info as a subtitle
  * Left Detail - show the info on the left of the row
  * Right Detail - show the info on the right hand side of the list row


In addition, you can also define a custom style of your own. To do this, you have to create a custom table view class which subclasses UITableViewCell, and provide outlets to the view of all the items that it will contain. Later on, we'll be setting these when setting up our views.

Collection Views also support sections, but do not have the default basic styles. For a collection view you must always specify create a custom view with outlets.

## Adding a view to your app

As you would expect, adding a tableview or a collection view to your application is as easy as dragging it in using the interface builder.

It's worth noting that if all your view will contain is a table view or a collection view, then Xcode also comes with prepackaged table and collection view controllers which are quite convenient.

## Data

How does your data get to your view? It's important to remember at this stage that views should not have their own data; you cannot just put a var on your table view and go off to the model.

Instead, table and colelction views have a property called dataSource, the type of which is a protocol that supplies its data. It is exactly like a delegate in how it works.

Similarly, both TableView and CollectionView have a delegate property (called `delegate`) that controls *how* they are displayed,

You set both these vars to your controller 99% of the time. Note that if your drag out a TableViewController or a CollectionViewController from the interface builder, than these properties are setup for you automatically.

### DataSource Protocol Methods

The dataSource of TableViews and Collection Views have many methods (12+), but there are 3 that are important to set whenever your are implementing these view. They are very similar for both sets of views.

#### TableViews

* `func numberOfSections(in tableView: UITV) -> Int` - The number of sections in your table. If you don't implement this, a default value of 1 is returned.
* `func tableView(_ tv: UITV, numberOfRowsInSection section: Int) -> Int` - The number of rows in each section
* `func tableView(_ tv: UITV, cellForRowAt indexPath: IndexPath) -> UITableViewCell` - The cell that you assign to each row. This is the most complicated of the 3 methods, and we'll look at it in a little more depth.

#### CollectionViews

* `func numberOfSections(in collectionView: UICV) -> Int` - Identical to its counterpart for tableViews
* `func collectionView(_ cv: UICV, numberOfItemsInSection section: Int) -> Int` - CollectionViews don't have rows, so you specify the number of items in a section instead.
* `func collectionView(_ cv: UICV, cellForItemAt indexPath: IndexPath) -> UICollectionViewCell` - The same as for tableViews, but of course, returning a UICollectionViewCell instead,

In both of of the 3rd methods, you will notice a parameter of type `IndexPath`. This struct just defines a way of specifying which item we're talking about.

### Defining a UITableViewCell

The `cellForRowAt` method returns the actual view that we'll be displaying in our application. An example implementation might look like:

```Swift
override func tableView(_ tableView: UITableView, cellForRowAt indexPath: IndexPath) -> UITableViewCell {
        let prototype = decision ? "CellIdentifier" : "OtherCellIdentifier"
        let cell = tableView.dequeueReusableCell(withIdentifier: prototype, for: indexPath)
        if let myTVCell = cell as? MyTVC {
            myTVC.name = food(at: indexPath)
            myTVC.emoji = emoji(at: indexPath)
        }
    }
```

There's a lot to unpack here, so let's go through things one at a time.

### Reusability

The most unusual line of the above method is certainly:

```Swift
let cell = tableView.dequeueReusableCell(withIdentifier: prototype, for: indexPath)
```

Because lists can be of a theoretically huge size, iOS doesn't actually render a view for every single item. Instead, it only renders cells for the items that are onscreen, and then reuses them when they go off the screen.

This has serious implications for multithreading which must be remembered. For instance, if you get an image to display in a cell, it's important to check when you get the image back that the cell hasn't been reused in the meantime.

### Prototypes

Of course, before you can reuse a cell, you have to create it. This is done using a prototype cell that has been created on the storyboard. The line:
```Swift
let cell = let prototype = decision ? "CellIdentifier" : "OtherCellIdentifier"
```

demonstrates how we might choose from several prototypes when rendering our cells.

### Configuration

Once we've got our cell, configuring it is just a matter of setting its properties. For basic table cells, properties already exist you can set. If you're creating a custom view (as you have to do for CollectionViews), you provide outlets to its various features that you then set. This is what we do in the lines:
```Swift
if let myTVCell = cell as? MyTVC {
    myTVC.name = food(at: indexPath)
    myTVC.emoji = emoji(at: indexPath)
}
```

after we of course case the cell to the appropriate custom type.

## Static TableViews

Sometimes, we just want a table to have fixed data. Really, we're just using the table view for UI purposes.

If that's the case, we don't need any of the previous methods. Instead, you can create your table manually on the storyboard and provide custom outlets directly to your controller.

Remember to set your table view to have static cells in the interface builder when you do this.

## Segueing from a UITableView

This is as simple as Ctrl+Dragging to a new view and setting the segue as usual.

The difference, however, is in the prepare. If you're segueing from a prototype, you need info about which specific row your segueing from.

The `sender` argument will help you out here. By casting is as a `UITableViewCell` (or your subclass), you'll gain access to the `indexPath(for: cell)` method, which lets you identify the cell.

```Swift
override func prepare(for segue: UIStoryboardSegue, sender: Any?) {
  if let identifier = segue.identifier {
    switch identifier {
    case "XyzSegue": //handle XyzSegue here
    case "AbcSegue":
      if let cell = sender as? UITableViewCell {
        let indexPath = tableView.indexPath(for: cell)
        let seguedToMVC = segue.destination as? MyVC {
            seguedToMVC.publicAPI = data[indexPath?.section][indexPath?.row]
        }
      }
    default:
        break
    }
  }
}
```

## CollectionView Segue

For CollectionViews, it is probably best to segue from code. There's a delegate method called `func collectionView(_ collectionView: UICV, didSelectItemAtIndexPath indexPath: IndexPath)` that gets called every time you select an item. 

In that you can call `performSegue`, though you'll have to explicitly specify the `sender`.

This would also be a valid strategy for tableViews.

## What if your model changes?

There's a method called `reloadData()`, which calls all 3 of the data prototype methods above. This will reload all the data for your table. It's a heavy-handed way of updating your data, but effective when you have large scale changes. 

For smaller changes, there are functions like `func reloadRows(at indexPaths: [IndexPath], with animation: UITableViewRowAnimation)` which can give you finer grained control.

## Row Height

How do we set the row height? There are 3 main ways:

* set a property called `rowHeight`
* Use Autolayout - This requires setting `rowHeight = UITableViewAutomaticDimension`. In addition, because autolayout can be computationally complex, you should also set a property called estimatedRowHeight to help the API handle rows that aren't on the screen.
* Finally, you can use the UITableView delegate's method(s) `func tableView(UITableView, {estimated}heightForRowAt indexPath: IndexPath) -> CGFloat`. Be careful though, the non-estimated version of this could get called a LOT large tables.

For CollectionViews, you have the same 3 options (with minor differences), but are handling cells with CGSizes rather than rows. The method is `func collectionView(_ collectionView: UICollectionView, layout collectionViewLayout: UICollectionViewwLayout, sizeForItemAt indexPath: IndexPath) -> CGSize` Note the `layout` parameter, which is important because you can set custom layouts for your collection views.

## Headers

For tables setting headers is just a matter of implementing the `func tableView(_ tv: UITV, titleForHeaderInSection section: Int) -> String?`  method, though if you want a custom view, that option is also available to you.

For collections, unfortunately you have to setup a custom view. This ends up being very similar to setting up a custom view item, and so we won't cover it in depth here.

There's tons of other stuff as well. See the documentation :).

[Previous Note](../Lecture%2011%20-%20Drag%20and%20Drop%20UITableView%20and%20UICollectionView/Part%201%20-%20Drag%20and%20Drop.md) | [Back To Contents](https://github.com/Firanus/stanford-iOS-lecture-notes) |  [Next Lecture](../Lecture%2012%20-%20Drag%20and%20Drop%20UITableView%20UICollectionView%20and%20UITextField/Part%200%20-%20Intro.md)