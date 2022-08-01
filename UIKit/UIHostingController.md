# UIHostingController
## How to use SwiftUI code inside of your UIKit applications

You can use SwiftUI views inside of UIKit apps by using `UIHostingController`.

To present a SwiftUI view, configure the controller as follows:

```swift
let view = SwiftUIView()
let hostingController = UIHostingController(rootView: view)

self.present(hostingController, animated: true)
```

UIHostingController works with all of the UIKit view controller APIs.

As of iOS 16, you can provide sizing options for automatic sizing updates to your views using `.sizingOptions` property. To use, configure the sizing option as follows:  

```swift
let view = SwiftUIView()
let hostingController = UIHostingController(rootView: view)

hostingController.sizingOptions = .preferredContentSize

hostingController.modalPresentationStyle = .popover
self.present(hostingController, animated: true)
```

## Bridging Data

There are several different ways to use your data models with SwiftUI views.  
###### Note: since data is owned *outside* of SwiftUI, you will not need to use `@State` and `@StateObject` property wrappers.  

### Passing Data to SwiftUI views with manual updates

```swift
struct SalesView: View {
  var numberOfSales: Int
  
  var body: some View {
      Text("You have made \(numberOfSales) sales")
  }
}

class SalesViewController: UIViewController {

  // The SwiftUI SalesView is a value type, so storing it would create a copy and wouldn't allow updates to the UI
  let hostingController: UIHostingController<SalesView>
  var numberOfSales: Int { 
      didSet { update() }
  }
  
  func update() {
      hostingController.rootView = SalesView(numberOfSales: numberOfSales)
  }
}
```

This pattern requires manual updates every time data is changed.

### Passing Data to SwiftUI views with automatic updates

You can track changes to your data and automatically update your SwiftUI views using the `@ObservedObject` and `@EnvironmentObject` property wrappers.  

#### Creating an @ObservedObject

1. Take an existing model within the app and conform it to the `ObservableObject` protocol.  
2. Add the `@Published` property wrapper to the data property. This wrapper will trigger SwiftUI to update changes on the views.
3. Store the model object using the `@ObservedObject` property wrapper in your SwiftUI view.
4. Initialize the data and UIHostingController in the UIViewController.

```swift
class SalesData: ObservableObject {
  @Published var numberOfSales: Int
  
  init(numberOfSales: Int) {
    self.numberOfSales = numberOfSales
  }
}

struct SalesView: View {
  @ObservedObject var data: SalesData
  
  var body: some View {
    Text("You have made \(data.numberOfSales) sales")
  }
}

class SalesViewController: UIViewController {
  let data: SalesData
  let hostingController: UIHostingController<SalesView>
  
  init(data: SalesData) {
    self.data = data
    let salesView = SalesView(data: data)
    self.hostingController = UIHostingController(rootView: salesView)
  }
}
```

### Resources

[Use SwiftUI with UIKit | WWDC 2022](https://developer.apple.com/videos/play/wwdc2022/10072)  
[UIHostingController | Apple Developer Documentation](https://developer.apple.com/documentation/SwiftUI/UIHostingController)
