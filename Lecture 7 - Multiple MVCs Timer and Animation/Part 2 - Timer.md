# Lecture 7, Part 2: Timer

Timer is a class used to execute code in the future, either once or repeatedly. It's functionality is analogous to JavaScript's `setTimeout` and `setInterval` methods.

Importantly, the exact time of execution is not guaranteed, it simply tries to get it to go off near that time. For most UI activities however, it is precise enough. 

If you want to provide some leeway to the timer, you can set a `.tolerance`. Note however, that tolerance is measured in seconds, and so is usually intended for larger intervals, e.g. if your computer has gone to sleep when you wanted the timer to trigger. This can be useful for battery efficiency.

To use it we typically use the function:
```Swift
class func scheduledTimer(
  withTimeInterval: TimeInterval,
  repeats: Bool,
  block: (Timer) -> Void
) -> Timer
```

An example usage which repeats every 2 seconds would be:

```Swift
private weak var timer: Timer?
timer = Timer.scheduledTimer(withTimeInterval: 2.0, repeats: true) {
  // your code here
}
```

Note that the variable here is `weak`. This is fine, as the run loop will keep a strong pointer to the timer as long as its scheduled.

Thus, if the timer finished, e.g. if it is not repeating or if its been manually stopped, its memory will automatically be deallocated. What's more, we can check to see if the timer is still running by just seeing if it's nil or not. Nifty!

 To stop a timer manually, we just call:
 ```Swift
 timer.invalidate()
 ```

[Previous Note](../Lecture%207%20-%20Multiple%20MVCs%20Timer%20and%20Animation/Part%201%20-%20Multiple%20MVCs.md) | [Back To Contents](https://github.com/Firanus/stanford-iOS-lecture-notes) |  [Next Note](../Lecture%207%20-%20Multiple%20MVCs%20Timer%20and%20Animation/Part%203%20-%20Kinds%20of%20Animation.md)