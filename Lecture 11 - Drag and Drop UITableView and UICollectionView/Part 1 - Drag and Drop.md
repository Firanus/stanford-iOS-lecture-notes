# Lecture 11, Part 1: Drag and Drop

Drag and Drop lets us move information around and between apps. From a user perspective, its very simple: just do a long press on any item.

Interestingly, with iOS 11's multitasking UI, you can use another finger to continue operating the UI while you're dragging an item. This makes drag and drop very useful.

To make this work in your code, you have to add an "Interaction" to your view. These are a bit like gestures for dragging and dropping. In doing so, you specify a delegate that will get involved when a drag and/or a drop happens. e.g.

```Swift
let dragInteraction = UIDragInteraction(delegate: theDelegate)
            view.addInteraction(dragInteraction)
```

Once you sign up to participate in the drag and or drop, your delegate will get sent one of 5 messages. You have to implement the corresponding functions to specify how your app will handle the drag and drop behaviour. The functions are:

* **Starting a Drag** - When a user starts a drag, the delegate gets the following function:
  ```Swift
  func dragInteraction(
    _ interaction: UIDragInteraction, 
    itemsForBeginning session: UIDragSession
  ) -> [UIDragItem]
  ```
  In which you return the items you are happy to have dragged. An empty array means nothing can be dragged.
  You create a UIDragItem using its initializer which takes an item provider as a parameter. An item provider is something which provides the data of the item that will be dragged. This is passed rather than the item to drag, because dragging the actual item might be expensive (e.g. an image). Item Providers minimise the amount of work that needs to be done, and only provide the data at the end of the drop. Many common classes have item providers. See the documentation.
  
  You can also provide an object that will be passed to drop target within your app using the `UIDragItem.localObject: Any` property.
* **Adding to a Drag** - If a user drags on something else during a drag, the delegate gets:
  ```Swift
  func dragInteraction(
    _ interaction: UIDragInteraction, 
    itemsForAddingTo session: UIDragSession
  ) -> [UIDragItem]
  ```
  
  Where the `[UIDragItem]` is the array of items to add to the drag. Usually, it has one item, or none (i.e. items cannot be added to the drag)
* **Accepting a Drop - Step 1** - When a drag moves over a view with a `UIDropInteraction`, the delegate gets:
  ```Swift
  func dropInteraction(
    _ interaction: UIDropInteraction, 
    canHandle session: UIDropSession
  ) -> Bool
  ```
  The bool return here determines whether the delegate will accept a drop of that type. To figure that out, the delegate asks what kind of objects can be provided using the method `func canLoadObjects(ofClass aClass: NSItemProviderReading.Type) -> Bool`
  ```Swift
  let stringAvailable = session.canLoadObjects(ofClass: NSAttributedString.self)
  let imageAvailable = session.canLoadObjects(ofClass: UIImage.self)
  ``` 
  and refuses to drop if it isn't to your liking. The list of valid NSItemProviderReading classes can be seen [in the documentation](https://developer.apple.com/documentation/foundation/nsitemproviderreading)
* **Accepting a Drop - Step 2** - If you don't refuse the drop in the `canHandle` step, you'll get the function:
  ```Swift
  func dropInteraction(
    _ interaction: UIDropInteraction, 
    sessionDidUpdate session: UIDropSession
  ) -> UIDropProposal
  ```
  This method allows you to specify as a drop receiver what you want to do with the drop. You have 3 options: `UIDropPropostion(operation: .copy/.move/.cancel)`
  * `.cancel` - refuse the drop
  * `.copy` - accepts the drop and copies the item
  * `.move` - accept the drop and move the item (only for in-app drags)
* **Accepting a Drop - Step 3** - Finally, if you make it through `sessionDidUpdate`, the following function runs:
  ```Swift
  func dropInteraction(
    _ interaction: UIDropInteraction, 
    performDrop session: UIDropSession
  )
  ```
  You implement this method by calling `loadObjects(ofClass:)` on the session. This goes and *asynchronously* fetches the data from the drag source. (Remember the itemProvider?). It then runs the closure you specify on that data *on the main thread* (so you can do UI work):
  
  ```Swift
  session.loadObjects(ofClass: NSAttributedString.self) { theStrings in
    //do something with the strings.
  }
  ```
  
  You can call `loadObjects` multiple times to handle different classes. However, you normally don't do anything else.
  
[Previous Note](../Lecture%2011%20-%20Drag%20and%20Drop%20UITableView%20and%20UICollectionView/Part%200%20-%20Intro.md) | [Back To Contents](https://github.com/Firanus/stanford-iOS-lecture-notes) |  [Next Note](../Lecture%2011%20-%20Drag%20and%20Drop%20UITableView%20and%20UICollectionView/Part%202%20-%20UITableView%20and%20UICollectionView.md)