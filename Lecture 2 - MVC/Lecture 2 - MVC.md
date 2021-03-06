# Lecture 2: MVC

This lecture begins with a description of MVC. His descriptions are:
* **Model** - *What* your application is, but not *how* it's displayed
* **Controller** - *How* your Model is presented to the user. (UI Logic). More properly, Controllers interpret/format the Model's information for the View.
* **View** - The controller's "minions". Typically very generic elements. It is important to note that views **do not own the data they display**.

MVC is about managing the communications between these different types. The keys are:

* The **controller** can talk to both the model and the view directly.
* The **model** and the **view** should *NEVER* talk to each other. They handle entirely different parts of the application
* The **view** can talk to the controller, but the communication needs to be 
    * "Blind" - The View elements are all generic, so they know nothing about how the app is intended to function.
    * Structured - The View needs to think in advance about how its going to communicate with the controller. For example:
      *  The controller to drop a target on itself that the view can call, e.g. when a button is pressed.
      *  The Controller can also set itself as the View's delegate. This is useful when the View needs to synchronise with the Controller, e.g. when scrolling down a page. The delegate is set using *protocals*. More on these later.
      *  Views can also often use Controllers as a data source (remember that they do not own the data they display). This is another form of delegate, which is very similar, but has a slightly different set of methods.
 *  The **model** cannot talk directly to the controller (because it is UI independent). However, it can broadcast messages (e.g. an update has happened on data item X) that he controller can subscribe to.

Interestingly, apps will often use a combination of MVCs, with each individual one responsible for one (or a related set of) UI screens.

When one MVC wants to talk to another, it always treat that MVC as one of its Views. It is important to restrict these connections, or debugging apps become impossible.

[Previous Lecture](../Lecture%201/Lecture%201.md) | [Back To Contents](https://github.com/Firanus/stanford-iOS-lecture-notes) |  [Next Lecture](../Lecture%203%20-%20The%20Swift%20Programming%20Language/Part%200%20-%20Intro.md)
