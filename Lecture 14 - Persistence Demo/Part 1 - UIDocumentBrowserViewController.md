# Lecture 14, Part 1: UIDocumentBrowserViewController

If you're writing a document-based app, you probably want to make it easy for users to manage their documents (Renaming, moving, accessing them, etc.).

The `UIDocumentBrowserViewController` (henceforth UIDBVC) does this all for you, and is wasy to leverage if you've been storing your documents using `UIDocument`.

(Incidentally, the UI for this controller is very similar to that of the files app for iOS 11. Indeed, that app is likely just a very thin layer on top of this controller.)

## Using UIDocumentBrowserViewController

To use UIDBVC in your app, you first have to make it the root view controller of your storyboard (arrow in storyboard points to it). Your document-editing MVC will then be presented modally on top.

In addition, you have to register the types your application uses. This is done in the Project Settings in the Info tab with your Target selected. In the Document Types area, you can add your document types.

You can also declare your own custom document types and then register them.

Finally, Xcode gives you an option when you start a new project to create a "document-based app". This is probably worth doing, though it doesn't add a lot. What it does add is:
* A stub for Document Types in Project Settings (supporting public.image files)
* An `Info.plist` entry: `Support Document Browser = YES`
* A bit of code in AppDelegate to allow other apps (e.g. Files) to get your app to open a file
* A stubbed out UIDocument subclass with empty `contents` and `load(fromContents)` methods
* A stubbed out MVC to display a document (by calling UIDocument's `open` and `close` methods)
* A subclass of `UIDocumentBrowserViewController` with almost everything implemented

To personalise it, we can fill in or replace the UIDocument and MVC classes. We also need to configure Project Settings to use our own document types rather than the default public.image. Finally, in UIDBVC, we need to:
1. Configure various UIDBVC parameters, e.g.:
   ```Swift
    override func viewDidLoad() {
      super.viewDidLoad()
      delegate = self // the guts of making UIDBVC work are in its delegate methods 
      allowsDocumentCreation = true
      allowsPickingMultipleItems = true
      browserUserInterfaceStyle = .dark
      view.tintColor = .white
    }
    ```
2. Provide a url to a template document to be copied when creating a new document. This happens in a delegate method:
    ```Swift
    func documentBrowser(
      _ controller: UIDBVC,
      didRequestDocumentCreationWithHandler handler: @escaping (URL?, UIDBVC.ImportMode) -> Void
    ){
      let url: URL? = ... // where your blank, template document can be found
      importHandler(url, .copy or .move) 
    }
    ```
3. Present your document-viewing MVC *modally*. We do this using the presentation logic discussed in the aside below. It might end up looking like:

    ```Swift
    func presentDocument(at url: URL) {
      let story = UIStoryboard(name: “Main”, bundle: nil)
      if let docvc = story.instantiateViewController(withIdentifier: “DocVC”) as? DocVC {
        docvc.document = MyDocument(fileURL: url)
        present(docvc, animated: true)
      }
    }
    ```

### ASIDE - Presenting an MVC without segueing

Presenting a new MVC from an existing MVC is as simple as calling `present(animated:)`:

```Swift
let newVC: UIViewController = ...
existingVC.present(newVC, animated: true) {
  // completion handler called when the presentation completes animating
  // (can be left out entirely if you don’t need to do anything upon completion)
}
```

The trick here is getting newVC. We can do this by giving it an identifier and then accessing it from the storyboard using this identifier:

```Swift
let storyboard = UIStoryboard(name: “Main”, bundle: nil) // Main.storyboard
if let newVC = storyboard.instantiateViewController(withIdentifier: “foo”) as? MyDocVC {
  // “prepare” newMVC and then present(animated:) it 
}
```

[Previous Note](../Lecture%2014%20-%20Persistance%20Demo/Part%200%20-%20Intro.md) | [Back To Contents](https://github.com/Firanus/stanford-iOS-lecture-notes)