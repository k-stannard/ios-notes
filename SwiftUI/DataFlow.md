# SwiftUI Data Flow

## Property Wrappers

### @State

Views in SwiftUI are value types. Every time a view needs to be updated with new data, a copy of that view is created with the changes and is displayed on screen. What the `@State` wrapper acts as a single local source of truth for a view's property, so that if a `@State` property changes, it allows the property to be redrawn in the updated view.  

A `@State` instance is not the value itself. It is a means of reading and writing the value.  
It is good practice to mark `@State` properties as private, and to place them at the highest point in the view heirarchy in which a view needs access to it. It may then be passed to child views if needed.  

Rule of thumb:  
If you're modifying a view's property in a local UI state, then you want to use a ternary operator on the `@State` variable.  
If you want to switch between two completely different views on the screen, then you'd be better off using a control statement, ie if-statement, switch, optional chaining.

### @Binding

You can think of the `@Binding` wrapper as a link between a parent and a child object, and allows you to read and write to a source of truth that is higher up in the view heirarchy. Updating a property using the `@Binding` wrapper will generate a new view when the updated value is rendered. 

In essence, the main function of `@Binding` is if you want to pass the source of truth from a view's local state into its child view for the purpose of reading and writing to it.

Note: you do not want to mark the `@Binding` property as private so that the parent view can access the property.  

Example:
```swift
struct ParentView: View {
    
    @State private var isRedView: Bool = false
    
    var body: some View {
        VStack {
            ChildView(isRedView: $isRedView)
            Button {
                isRedView.toggle()
            } label: {
                Text("\(isRedView ? "Tap for Blue View" : "Tap for Red View")")
            }
        }
    }
}

struct ChildView: View {
    
    @Binding var isRedView: Bool
    
    var body: some View {
        if isRedView {
            Rectangle()
                .foregroundColor(.red)
                .frame(width: 250, height: 250)
        } else {
            Rectangle()
                .foregroundColor(.blue)
                .frame(width: 250, height: 250)
        }
    }
}
```

### ObservableObject & @Published

The `ObservableObject` protocol allows you to develop your own source of truth within your app that is located outside of your views. The `@Published` wrapper acts a sort of `@State` wrapper inside of an observable object class that keeps track of changes, and publishes them to subscribers when a change has occurred. This pattern is very useful for creating view models in SwiftUI

For example:
```swift
class ViewModel: ObservableObject {
  @Published var users: [String] = []
  @Published var isLoading: Bool = false
  
  func fetchUsers() {
    // Insert fetch code here
  }
}

struct ContentView: View {
  
  @StateObject private var viewModel = ViewModel()
  
  var body: some View {

    if viewModel.isLoading {
      // Do something
    }
    
    Button(action: viewModel.fetchUsers) {
      Text("Tap to fetch users")
    }
  }
}
```

In summary, this pattern allows you to:
1. Create your own custom source of truth outside of your views
2. Easily implement unit testing in the future

### @EnvironmentObject

An environment object is a source of truth that can be used at the root of your app. It is essentially like storing an object in a global state. Any child of a view where that object appears can access it. Good examples are passing authorization status, ie: logged in/out, of an object down through the views from the root entry point of an app.

Example:
```swift
final class PurchaseViewModel: ObservableObject {
  @Published var hasPurchased: Bool = false
  @Published var isLoading: Bool = false
  
  func purchaseFeature() {
    // Implement purchase code
  }
}

@main
struct ExampleApp: App {
  @StateObject private var viewModel = ViewModel()
  
  var body: some View {
    WindowGroup {
      TabView {
        PurchaseView()
          .environmentObject(viewModel) // Injects the view model into the view
        
        NewFeatureView()
      }
    }
  }
}

struct PurchaseView: View {
  @EnvironmentObject var viewModel: PurchaseViewModel
  
  var body: some View {
    Button {
      viewModel.purchaseFeature()
    } label: {
      Text("Tap button to purchase this feature")
    }
  }
}

struct NewFeatureView: View {
  @EnvironmentObject var viewModel: PurchaseViewModel
  
  var body: some View {
    // Insert UI code ...
    viewModel.hasPurchased = true
  }
}

/* 
   You can insert NewFeatureView() into a parent view and 
   you will still be able to access the environment object 
   as long as there is root access from that parent view.
*/
```

Note: you have to inject the environment object into the preview provider to prevent swift previews from crashing.

### @StateObject

`@StateObject` allows you to have a single instance of your source of truth that your views can reference and read from. In order to use the `@StateObject` wrapper, you need to make sure you're using a class that is conforming to `ObservableObject`.

Example:
```swift
struct LoginContentView: View {
    
    @StateObject private var viewModel = LoginViewModel()
    
    var body: some View {
        switch viewModel.currentState {
        case .loading:
            ProgressView()
        case .loggedOut:
            LoginView(user: $viewModel.user) {
                viewModel.login()
            }
        case .loggedIn:
            LoggedInView {
                viewModel.logout()
            }
        }
    }
}

struct User: Equatable {
    
    var username: String = ""
    var password: String = ""
    
    mutating func reset() {
        username = ""
        password = ""
    }
}

final class LoginViewModel: ObservableObject {
    
    enum CurrentState {
        case loading
        case loggedOut
        case loggedIn
    }
    
    @Published var user: User = .init()
    @Published var currentState: CurrentState = .loggedOut
    
    func login() {
        guard !user.username.isEmpty && !user.password.isEmpty else {
            return
        }
        
        currentState = .loading
        
        DispatchQueue.main.asyncAfter(deadline: .now() + 1.5) { [weak self] in
            self?.currentState = .loggedIn
        }
    }
    
    func logout() {
        self.currentState = .loggedOut
        self.user.reset()
    }
}
```

### @StateObject vs @ObservedObject vs @EnvironmentObject

#### @State Object

A `@StateObject` is an object that allows you to create your own custom source of truth that can be observed. When a `@StateObject` is created, only one instance of itself. When a view is revalidated, a state object won't be recreated.  

```swift
// 1. Observable object defined
class PeopleViewModel: ObservableObject {
    @Published var people: [String] = []
}

struct ContentView: View {
    // 2. Source of truth instance created in relevant view
    @StateObject private var viewModel = PeopleViewModel()
    
    var body: some View {
        // 3. Read from source of truth and reflect changes in UI
        Text("Number of people: \(viewModel.people.count)
    }
}
```
When to use a `@StateObject`?  
1. If you're building a source of truth that is only needed for that single view, ie: if you had a view model for executing requests that are only related to that view.
2. If you're building a source of truth that will be used at the root of your application.
3. As a general rule of thumb, if you want to create an instance of your observable object you want wrap it with `@StateObject`.

#### @ObservedObject

The `@ObservedObject` wrapper can be used to create an instance of your observable object. The `@ObservedObject` allows you to pass your observable object between different views, ie: passing an object from a parent view to a child view. It is advised that you do not use this wrapper unless you need to support an app using an iOS version below 14.0. 

```swift
// 1. Observable object defined
class PeopleViewModel: ObservableObject {
    @Published var people: [String] = []
}

struct ContentView: View {
    // 2. Source of truth instance created in relevant view
    @StateObject private var viewModel = PeopleViewModel()
    
    var body: some View {
        // 3. Inject source of truth to a child view
        PeopleView(viewModel: viewModel)
    }
}

struct PeopleView: View {
    
    // 4. Property wrapper to receive & accept source of truth from parent view
    @ObservedObject var viewModel: PeopleViewModel
    
    var body: some View {
        // 5. Read source of truth & update UI
        Text("Number of people: \(viewModel.people.count)")
    }
}
```

When to use `@ObservedObject`?
1. If you have a child view which needs access to a state object that is isolated to that one single view, you can pass it down using an observable object.
2. If you need to create an instance of your observable object on iOS 13 - which is the only time you should use this.

#### @EnvironmentObject 

When to use `@EnvironmentObject`?

Similar to `@ObservedObject`, an `@EnvironmentObject` is used when you need to access a source of truth at the root level of an application, where each screen needs access to the source of truth, and if a child view of a parent view needs access to the root level object.
