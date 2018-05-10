# Lecture 15, Part 1: Alerts and Action Sheets

Alerts and Action sheets are two mechanisms which both "pop up and ask the user something". They have very similar APIs, so we'll be covering the together.

**Alerts** pop up in the middle of the screen. They ususally ask questions with only two answers (Yes/No, OK/Cancel) and can be quite disruptive to the user, so use them carefully. They are often used for asynchronous problems (e.g Connection Reset), and can include a text field to get quick answers, such as a password.

**Action Sheets** usually slide in from the bottom of the screen on iPhones, and in a popover on iPads. Generally, they will ask users questions with more than 2 choices. Think of Action Sheets as presenting branching decisions to the user.

## Example Usage - Action Sheet

To use either an Alert or an Action Sheet, you have to:
1. Initilise the object
2. Add Actions
3. (Optional) Link the popover to a UI Element on iPads
4. Present the Action Sheet

For example:
```Swift
var alert = UIAlertController(
    title: “Redeploy Cassini”,
    message: “Issue commands to Cassini’s guidance system.”,
    preferredStyle: .actionSheet
)

alert.addAction(UIAlertAction(
    title: “Orbit Saturn”, //String
    style: UIAlertActionStyle.default) //UIAlertActionStyle
    { (action: UIAlertAction) -> Void in
        // go into orbit around saturn
    }
)

alert.addAction(UIAlertAction(
    title: “Explore Titan”,
    style: .default)
    { (action: UIAlertAction) -> Void in
        if !self.loggedIn { self.login() }
        // if loggedIn go to titan
    }
)

alert.addAction(UIAlertAction(
    title: “Closeup of Sun”,
    style: .destructive)
    { (action: UIAlertAction) -> Void in
        if !loggedIn { self.login() }
        // if loggedIn destroy Cassini by going to Sun
    }
)

alert.addAction(UIAlertAction(
    title: “Cancel”,
    style: .cancel)
    { (action: UIAlertAction) -> Void in
       // do nothing
    }
)

//Optional
alert.modalPresentationStyle = .popover
let ppc = alert.popoverPresentationController
ppc?.barButtonItem = redeployBarButtonItem

present(alert, animated: true, completion: nil)
```

Notice the differences in the `UIAlertActionStyle`.
* `.default` - created a normal action button
* `.destructive` - creates a button with red text, and is normally used to indicate an action which will have some form of destrucive effect
* `.cancel` - creates a button seperated from the others that is typically used to close the Action Sheet without taking any action. Note that on an iPad, the cancel button will not appear as action sheets on an iPad appear as a popover, and you cancel popovers by clicking somewhere else.

Note as well that if you make the iPad action sheet a popover and you link it to a specific UI element, you don't need to write code specifying this will only happen on iPads. iOS automatically adapts to the device size, so on iPhones it will still slide in from the bottom.

## Example Usage - Alerts

Unlike Action Sheets, Alerts look exactly the same on both iPads on iPhones.

The creation is almost identical. However, you do have the option to put text fields on your alert. For example (see lines 15-28):

```Swift
var alert = UIAlertController(
    title: “Login Required”,
    message: “Please enter your Cassini guidance system...”,
    preferredStyle: .alert
)

alert.addAction(UIAlertAction(
    title: “Cancel”,
    style: .cancel)
    { (action: UIAlertAction) -> Void in
        // do nothing
    }
)

alert.addAction(UIAlertAction(
    title: “Login”,
    style: .default)
    { (action: UIAlertAction) -> Void in
        // get password and log in
        if let tf = self.alert.textFields?.first {
            self.loginWithPassword(tf.text)
        }
} )

alert.addTextField(configurationHandler: { textField in
    textField.placeholder = “Guidance System Password”
    textField.isSecureTextEntry = true
})

present(alert, animated: true, completion: nil)
```

[Previous Note](../Lecture%2015%20-%20Alerts%20Notifications%20and%20the%20Application%20Lifecycle/Part%200%20-%20Intro.md) | [Back To Contents](https://github.com/Firanus/stanford-iOS-lecture-notes) | [Next Note](../Lecture%2015%20-%20Alerts%20Notifications%20and%20the%20Application%20Lifecycle/Part%202%20-%20Notifications%20and%20KVO.md)