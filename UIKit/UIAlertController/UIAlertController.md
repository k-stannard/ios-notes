## UIAlertController 

UIAlertController is the default way to make an alert/pop-up in Swift.  

To create an alert, call the UIAlertController constructor and fill in the parameters.
```swift
let alert = UIAlertController(title: "Alert title", message: "This is the alert message", preferredStyle: .alert)
```

Once the alert is created, add an action to the alert for the user to interact with.
```swift
let alertAction = UIAlertAction(title: "OK", style: .default, handler: nil)
alert.addAction(alertAction)
```

Then once the action is added, simply present the alert:
```swift
present(alert, animated: true, completion: nil)
```

This will create an alert with a title, alert message, and an OK button to dismiss.


