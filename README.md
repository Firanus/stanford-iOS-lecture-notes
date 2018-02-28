# Developing iOS 11 Apps with Swift - Lecture Notes

This repository compiles notes made on the lectures given as a part of the freely available Stanford course ['Developing iOS 11 apps with Swift'](https://itunes.apple.com/us/course/developing-ios-11-apps-with-swift/id1309275316). They will hopefully serve as an aid to individuals taking the course, but are not intended to replace the lectures themselves. In particular, any instances of live coding in the course have not been replicated here.

## Table of Contents

1. [Lecture 1](/Lecture%201/Lecture%201.md)
1. [Lecture 2: MVC](/Lecture%202%20-%20MVC/Lecture%202%20-%20MVC.md)
1. [Lecture 3: The Swift Programming Language](/Lecture%203%20-%20The%20Swift%20Programming%20Language/Part%200%20-%20Intro.md)
   1. [Autolayout, Briefly](/Lecture%203%20-%20The%20Swift%20Programming%20Language/Part%201%20-%20Autolayout%20Briefly.md)
   2. [Ranges](/Lecture%203%20-%20The%20Swift%20Programming%20Language/Part%202%20-%20Ranges.md)
   2. [Tuples](/Lecture%203%20-%20The%20Swift%20Programming%20Language/Part%203%20-%20Tuples.md)
   2. [Computed Values](/Lecture%203%20-%20The%20Swift%20Programming%20Language/Part%204%20-%20Computed%20Values.md)
   2. [Access Control](/Lecture%203%20-%20The%20Swift%20Programming%20Language/Part%205%20-%20Access%20Control.md)
   2. [Extensions](/Lecture%203%20-%20The%20Swift%20Programming%20Language/Part%206%20-%20Extensions.md)
   2. [Enumerations](/Lecture%203%20-%20The%20Swift%20Programming%20Language/Part%207%20-%20Enumerations.md)
   2. [Optionals](/Lecture%203%20-%20The%20Swift%20Programming%20Language/Part%208%20-%20Optionals.md)
   2. [Data Structures](/Lecture%203%20-%20The%20Swift%20Programming%20Language/Part%209%20-%20Data%20Structures.md)
4. [Lecture 4: More Swift](/Lecture%204%20-%20More%20Swift/Part%200%20-%20Intro.md)
   1. [Protocols](/Lecture%204%20-%20More%20Swift/Part%201%20-%20Protocols.md)
   2. [NSAttributedStrings](/Lecture%204%20-%20More%20Swift/Part%202%20-%20NSAttributedStrings.md)
5. [Lecture 5: Drawing](/Lecture%205%20-%20Drawing/Part%200%20-%20Intro.md)
   1. [Views](/Lecture%205%20-%20Drawing/Part%201%20-%20Views.md)
   2. [Initializing a UIView](/Lecture%205%20-%20Drawing/Part%202%20-%20Initializing%20a%20UIView.md)
   3. [Coordinate System Data Structures](/Lecture%205%20-%20Drawing/Part%203%20-%20Coordinate%20System%20Data%20Structures.md)
   4. [View Coordinate System](/Lecture%205%20-%20Drawing/Part%204%20-%20View%20Coordinate%20System.md)
   5. [Creating Views](/Lecture%205%20-%20Drawing/Part%205%20-%20Creating%20Views.md)
   6. [Drawing](/Lecture%205%20-%20Drawing/Part%206%20-%20Drawing.md)
   7. [Fonts](/Lecture%205%20-%20Drawing/Part%207%20-%20Fonts.md)
6. [Lecture 6: Multitouch](/Lecture%206%20-%20Multitouch/Part%200%20-%20Intro.md)
   1. [Gestures](/Lecture%206%20-%20Multitouch/Part%201%20-%20Gestures.md)
7. [Lecture 7: Multiple MVCs, Timer and Animation ](/Lecture%207%20-%20Multiple%20MVCs%20Timer%20and%20Animation/Part%200%20-%20Intro.md)
   1. [Multiple MVCs](/Lecture%207%20-%20Multiple%20MVCs%20Timer%20and%20Animation/Part%201%20-%20Multiple%20MVCs.md)
   2. [Timer](/Lecture%207%20-%20Multiple%20MVCs%20Timer%20and%20Animation/Part%202%20-%20Timer.md)
   3. [Kinds of Animation](/Lecture%207%20-%20Multiple%20MVCs%20Timer%20and%20Animation/Part%203%20-%20Kinds%20of%20Animation.md)
8. [Lecture 8: Animation](/Lecture%208%20-%20Animation/Part%200%20-%20Intro.md)
   1. [UIViewPropertyAnimator](/Lecture%208%20-%20Animation/Part%201%20-%20UIViewPropertyAnimator.md)
   2. [UIView Transitions](/Lecture%208%20-%20Animation/Part%202%20-%20UIView%20Transitions.md)
   3. [Dynamic Animations](/Lecture%208%20-%20Animation/Part%203%20-%20Dynamic%20Animations.md)
9. [Lecture 9: View Controller Lifecycle and Scroll Views](/Lecture%209%20-%20View%20Controller%20Lifecycle%20and%20Scroll%20Views/Part%200%20-%20Intro.md)
   1. [View Controller Lifecycle](/Lecture%209%20-%20View%20Controller%20Lifecycle%20and%20Scroll%20Views/Part%201%20-%20View%20Controller%20Lifecycle.md)
   2. [UIScrollView](/Lecture%209%20-%20View%20Controller%20Lifecycle%20and%20Scroll%20Views/Part%202%20-%20UIScrollView.md)
10. [Lecture 10: Multithreading and Autolayout](/Lecture%2010%20-%20Multithreading%20and%20Autolayout/Part%200%20-%20Intro.md)
    1. [Multithreading](/Lecture%2010%20-%20Multithreading%20and%20Autolayout/Part%201%20-%20Multithreading.md)
    2. [Autolayout](/Lecture%2010%20-%20Multithreading%20and%20Autolayout/Part%202%20-%20Autolayout.md)
11. [Lecture 11: Drag and Drop, UITableView and UICollectionView](/Lecture%2011%20-%20Drag%20and%20Drop%20UITableView%20and%20UICollectionView/Part%200%20-%20Intro.md)
    1. [Drag and Drop](/Lecture%2011%20-%20Drag%20and%20Drop%20UITableView%20and%20UICollectionView/Part%201%20-%20Drag%20and%20Drop.md)
    2. [UITableView and UICollectionView](/Lecture%2011%20-%20Drag%20and%20Drop%20UITableView%20and%20UICollectionView/Part%202%20-%20UITableView%20and%20UICollectionView.md)
12. [Lecture 12: Drag and Drop, UITableView, UICollectionView and UITextField](/Lecture%2012%20-%20Drag%20and%20Drop%20UITableView%20UICollectionView%20and%20UITextField/Part%200%20-%20Intro.md)
    1. [UITextField](/Lecture%2012%20-%20Drag%20and%20Drop%20UITableView%20UICollectionView%20and%20UITextField/Part%201%20-%20UITextField.md)
13. [Lecture 13: Persistance](/Lecture%2013%20-%20Persistance/Part%200%20-%20Intro.md)
    1. [User Defaults](/Lecture%2013%20-%20Persistance/Part%201%20-%20User%20Defaults.md)
    2. [Archiving](/Lecture%2013%20-%20Persistance/Part%202%20-%20Archiving.md)
    3. [File System](/Lecture%2013%20-%20Persistance/Part%203%20-%20File%20System.md)
    4. [Core Data](/Lecture%2013%20-%20Persistance/Part%204%20-%20Core%20Data.md)
    5. [Cloud Kit](/Lecture%2013%20-%20Persistance/Part%205%20-%20Cloud%20Kit.md)
    6. [UIDocuments](/Lecture%2013%20-%20Persistance/Part%206%20-%20UIDocuments.md)