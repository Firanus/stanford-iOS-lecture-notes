# Lecture 12: Drag And Drop, UITableView, UICollectionView and UITextView

In this lecture, we continue the demo started at the end of lecture 11 by implementing a UICollectionView with drag and drop. We end the lecture by looking at UITextFields.

Implementing drag and drop in a UICollectionView is very similar to implementing it in a normal view. However, iOS helps out by giving direct access to the `indexPath` of the items being dragged. See [the documentation](https://developer.apple.com/documentation/uikit/views_and_controls/collection_views/supporting_drag_and_drop_in_collection_views) for more information.

Particularly interesting in the lecture is the use of placeholders to handle asynchronous adding of items to collectionViews.

[Previous Lecture](../Lecture%2011%20-%20Drag%20and%20Drop%20UITableView%20and%20UICollectionView/Part%202%20-%20UITableView%20and%20UICollectionView.md) | [Back To Contents](https://github.com/Firanus/stanford-iOS-lecture-notes) |  [Next Note](../Lecture%2012%20-%20Drag%20and%20Drop%20UITableView%20UICollectionView%20and%20UITextField/Part%201%20-%20UITextField.md)