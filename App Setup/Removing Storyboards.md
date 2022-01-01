## Removing Storyboards

There are 3 steps needed to remove storyboards from a project.

#### 1. Remove the files
  - Remove SceneDelegate.swift
  - Remove Main.storyboard

#### 2. Update info.plist
  - Need to remove all references of storyboard in the app's info.plist file.
  - Shift+cmd+f and search for `main`.
  - Search main inside of the Target's info.plist file and delete `UIKit Main Storyboard File Base Name`.
  - Go into the Info.plist file and delete the entire section of `Application Scene Manifest`.

#### 3. Update AppDelegate
  - Delete all boiler plate code.
  - Setup the app window:
```swift
    var window: UIWindow?
    
    func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey : Any]? = nil) -> Bool {
        window = UIWindow(frame: UIScreen.main.bounds)
        window?.makeKeyAndVisible()
        window?.backgroundColor = .systemBackground
        window?.rootViewController = ViewController()
        
        return true
    }
```
