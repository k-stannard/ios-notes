# Custom UIKit Components

### How to create a custom UIKit component

Start by creating your class and conform to whatever protocol is needed.

```swift
class CustomButton: UIButton { }
```

Next, add the override init method and call its super method.  
By calling the super method, you are initializing all of the normal functionality that a UIButton would have.

```swift
class CustomButton: UIButton {

  override init(frame: CGRect) {
    super.init(frame: frame)
    
  }
}
```

Now, create a configure method and add all of the customization necessary for your component.  
Then call the configure method in the init method.

```swift
class CustomButton: UIButton {
  override init(frame: CGRect) {
    super.init(frame: frame)
    configure()
  }
}

extension CustomButton {
  private func configure() {
    // Example customization
    layer.cornerRadius = 10
    titleLabel?.textColor = .white
    titleLabel?.font = .preferredFont(forTextStyle: .headline)
    translatesAutoresizingMaskIntoConstraints = false
  }
}
```

You can add a custom initializer for even more customization.  
Don't forget to call your configure method at the end of the custom initializer.
```swift
init(backgroundColor: UIColor, title: String) {
    super.init(frame: .zero)
    self.backgroundColor = backgroundColor
    self.setTitle(title, for: .normal)
    configure()
}
```

Now you can call your custom button where ever needed!

```swift
let searchButton = CustomButton(backgroundColor: .systemBlue, title: "Search")
```
<img width="270" alt="Screenshot 2023-03-20 at 12 14 11 PM" src="https://user-images.githubusercontent.com/21287326/226416871-795c1586-529c-4183-bee2-ba641ac1884c.png">
