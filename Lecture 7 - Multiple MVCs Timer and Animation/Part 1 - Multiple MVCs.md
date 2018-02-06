# Lecture 7, Part 1: Multiple MVCs

MVCs can be linking to each other by treating one MVC group as the View in another one. This implies that if an MVC wants to talk to its parent controller, it needs to do so in a blind structured way in the same way that a View does.

To let us do this, iOS provides special controllers whose View is another MVC. (We could also make our own Controller to do this, but it is rarely necessary, so we won't be covering that in this course). The 3 Controller's iOS provides are:

* `UITabBarController` - Creates a tab bar in the UI, each with its own MVC. You can set the tab bar icon, badge and title in either the storyboard or using the `tabBarItem` property. Generally, its recommended not to have more than 5 MVCs in a single tab bar controller, though iOS does provide UI to handle this circumstance.
* `UISplitViewController` - Puts 2 MVCs side-by-side on the screen. The LHS MVC is the 'master', and the RHS is the 'detail'. Split-view is available for tablets and iPhone pluses.
* `UINavigationController` - Acts as a stack onto which you can push and pop MVCs (like a stack of cards). The top area in this view is drawn by the UINavigationController, and it provides a title and back button. This is controlled by the UIViewController's `navigationItem` property. To operate a UINavigationController, you have to set its `rootViewController` property. This sets the view at the bottom of your stack. Note that when you back out of a view, you actually deallocate all the memory is was using from the heap.

Each of these controllers contains a property called `viewControllers: [UIViewController]? {get set}` which allows you to access its sub-MVCs. 

In addition, UIViewController contains three properties, `tabBarController`, `splitViewController` and `navigationController`, which show you which of these controllers, is any, the current View lies under.

## Wiring up a Split View Controller

Wiring up a split view controller is as simple as dragging it onto the storyboard using the interface builder and Ctrl+Dragging the other controllers onto it.

However, because Split View Controllers only work on iPads, we often need to also wrap the master view in a navigation controller so that the app will work correctly on iPhones. This also helpfully provides a title to the view on iPads. iOS is smart enough to automatically adapt to the type of device.

The easiest way to add a Navigation controller is to use the Editor -> Embed in -> Navigation Controller option, though you could also Ctrl+Drag if you wanted.

## Segues

Now that we have our controllers, we need a way to make them appear. This is normally done using segues. The types of segues (all of which can adapt to their environment) are:

* Show Segue - will push in a Navigation Controller, otherwise it will show a modal
* Show Detail Segue - will show detail of a Split View Controller, else will push in a Navigation Controller
* Modal Segue - will take over the entire screen while the MVC is up
* Popover Segue - will make the MVC appear in a little popover window.

Segues always create a **new instance** of an MVC. You never reuse an old instance. (Note that the back button in a Navigation Controller is not a segue, so it does not create a new instance)

The easiest way to introduce a segue is to  Ctrl+Drag from one View to another and then select the appropriate segue. You should then use the attributes view to give your segue a unique identifier, as this will let you reference it in code. Specifically, you can use it too:
* Invoke a segue using the UIViewController method `func performSegue(withIndentifier: string, sender: Any?)`. However, this is quite rare, as we usually set this up using the interface builder
* Preparing for a segue, normally by MVC to-be-segued-to's Model and display charecteristics. Remember that this is always a new MVC instance. The method that does this is `prepare(for segue: UIStoryboardSegue, sender: Any?)`, and we typically `switch` on `segue.identifier`.

  It's very important to remember that preparation happens **BEFORE outlets get set**. This is a common bug.
  
You can also prevent a segue using the method `shouldPerformSegue(withIdentifier identifier: string, sender: Any?) -> Bool`

[Previous Note](../Lecture%207%20-%20Multiple%20MVCs%20Timer%20and%20Animation/Part%200%20-%20Intro.md) | [Back To Contents](https://github.com/Firanus/stanford-iOS-lecture-notes) |  [Next Note](../Lecture%207%20-%20Multiple%20MVCs%20Timer%20and%20Animation/Part%202%20-%20Timer.md)