# UIViewController Life Cycle

When subclassing UIViewController, all of the life cycle methods are inherited. Each of the life cycle methods below are called automatically by the system. 
When overriding a life cycle method, calling `super.` will allow the original version of the method to be called and do its setup prior to the overridden method's call. While it may not always be necessary, not calling '`super.` may cause unwanted bugs.

```swift
func viewDidLoad()
```
`viewDidLoad()` is called once the view controller has loaded it's view hierarchy is loaded into memory. 


```swift
func viewWillAppear(_ animated: Bool)
```

```swift
func viewDidAppear(_ animated: Bool)
```

```swift
func viewWillDisappear(_ animated: Bool)
```

```swift
func viewDidDisappear(_ animated: Bool)
```

```swift
func viewWillLayoutSubviews()
```

```swift
func viewDidLayoutSubviews()
```

`viewDidLayoutSubviews()` is the method to use for any and all geometry dependent changes.











For more information: https://developer.apple.com/documentation/uikit/uiviewcontroller
