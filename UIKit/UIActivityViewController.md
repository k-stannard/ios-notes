# What is UIActivityViewController?

UIActivityViewController is a view controller that is used to offer standard services from your app. These services include things such as: 
1. copying items to the pasteboard
2. posting content to social media
3. sending items via email or text
4. add your own custom services

You are responsible for configuring, presenting, and dismissing the view controller.

## Configuration

```swift
let items = ["I am sharing this string"]
let ac = UIActivityViewController(activityItems: items, applicationActivities: nil)
present(ac, animated: true)
```
