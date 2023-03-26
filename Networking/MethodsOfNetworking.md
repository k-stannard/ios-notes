# Methods of Networking

## Escaping Closures

You can create network requests using basic escaping closures:

```swift
func getUserData(for username: String, completion: @escaping (User?, String?) -> Void) { }
```

In this example, the getUserData function has an escaping closure that takes an optional user or string if there's an error.
You'd then call the closure and pass the appropriate data:

```swift
 URLSession.shared.dataTask(with: request) { data, response, error in 
  if let _ = error {
    completion(nil, "Error message goes here")
  }
  
  /* ... remaining networking code ... */
 }
```

You can refactor the error message into an enum to improve code readability:
```swift
enum ErrorMessage: String {
  case invalidUsername = "Invalid username. Please try again."
  case unableToComplete = "Unable to complete your request. Please check your internet connection."
  // ...
}

// modified completion handler
if let _ = error {
  completion(nil, .unableToComplete)
}
```

This way of networking works fine, but you constantly have to swap values back and forth in the completion handler.  There's also a risk of both optional values of User and Error being nil and cause your app to crash. You can remove the risk by refactoring your closure to use the `Result` type.

## Conforming to Result Type

To refactor to use the `Result` type:
```swift
// network call
func getUserData(for username: String, completion: @escaping (Result<User, ErrorMessage>) -> Void) { }

// refactor error message to conform to the Error protocol
enum ErrorMessage: String, Error { }

// error
if let _ = error {
  completion(.failure(.unableToComplete))
}

// call site
getUserData(for: username) { result in
  switch result {
    case .success(let data):
      // do something with data
    case .failure(let error):
      // do something with error
  }
}
```
