# Lecture 8, Part 3: Dynamic Animations

This class of animation is a little different. This sets up the physics relating animatable objects and lets the animation run until they're complete.

It's easily possible to set up a system that never reaches stasis, but this can lead to performance problems (and annoying UI).

There are 3 steps to setting up this kind of animation:

## 1) Have an animator:
  
  This is the thing that drives the animation. It has a type `UIDynamicAnimator` You have to provide it with a referenceView, which:
* provides the coordinate system the animations will take place in
* must be a (direct or indirect) superview of all the views that will take part in the animation 

```Swift
var animator = UIDynamicAnimator(referenceView: UIView)
```

## 2) Create and add UIDynamicBehaviour instances

These describe how the items in the view behave.

```Swift
//To add gravity:
let gravity = UIGravityBehaviour()
animator.addBehavior(gravity)

//To add collision
let collider = UICollisionBehaviour()
animator.addBehavior(collider )
```
   
The different types of behaviours can be found in the [UIDynamicBehaviour documentation](https://developer.apple.com/documentation/uikit/uidynamicbehavior)

### UIDynamic Behaviour

UIDynamicBehaviour itself is the parent class of the specific behaviours. While you can subclass it yourself, creating a behaviour can be tricky (very mathematical). More often, you'd use the `addChildBehaviour(UIDynamicBehaviour)` method to create a composite behaviour which encapsualtes the physics of your object.

You can also check the animator of your behaviour by looking at its `dynamicAnimator` property.

Finally, dynamic behaviours have an `action: (() -> Void)?` property. You can assign a closure to this property which will be executed every time the action executes. This can be very useful, but be careful; this closure will get called a lot, so ensure it is efficient. Also, if you reference animator properties, be careful of memory cycles.
   
## 3) Add UIDynamicItems to the behaviours

These are the items that will be effected by the behaviour. Note that they must implement the `UIDynamicItem` protocol. UIViews implement this automatically, and you can implement it yourself in any custom class.

```Swift
let item1: UIDynamicItem = //... usually a UIView
let item2: UIDynamicItem = //... usually a UIView
gravity.add(item1)
collider.add(item1)
gravity.add(item2)
```

As soon as all three of these items are present, they instantly begin enacting the behaviour.

Note also that once you assign an item to an animator, the animator "owns" it. If you want to trigger the animator based off a change you've made, you need to call the `updateItemUsingCurrentState(item: UIDynamicItem)` method.

# UIDynamicItemBehaviour

In addition to dynamic behaviours, we also have dynamic item behaviours, which act like "meta" behaviours that control the behaviour of items that are affected by other behaviours. For example, `allowsRotation: bool` or `friction: CGFloat`. Detail is available in the [documentation](https://developer.apple.com/documentation/uikit/uidynamicitembehavior)

# Stasis

Most of the time, we design our behaviour so that it will reach a point where the animated object eventually comes to a stop. You can find out when an item has reached a stop by setting a delegate `delegate: UIDynamicAnimatorDelegate` and then accessing `dynamicAnimatorDidPause(UIDynamicAnimator)`. For resumption, use `dynamicAnimatorWillResume(UIDynamicAnimator)`

[Previous Note](../Lecture%207%20-%20Multiple%20MVCs%20Timer%20and%20Animation/Part%201%20-%20Multiple%20MVCs.md) | [Back To Contents](https://github.com/Firanus/stanford-iOS-lecture-notes)