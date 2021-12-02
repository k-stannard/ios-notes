# UIViewController Life Cycle

When subclassing UIViewController, all of the life cycle methods are inherited. Each of the life cycle methods below are called automatically by the system. 
Calling `super.` will give access to all of the features that Apple intended for each method. 

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













For more information: https://developer.apple.com/documentation/uikit/uiviewcontroller
