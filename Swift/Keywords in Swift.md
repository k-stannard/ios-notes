# Keywords in Swift

### @escaping

The `@escaping` keyword is used when working with closures. When a closure is marked with `@escaping`, it saying that the closure will exist outside of the scope that it's been passed to. For example, when working with a network call that uses a closure to fetch info from an API. If the user is on a bad connection, the `@escaping` keyword will allow the closure to wait around for the data from the network call before it will execute. Without the `@escaping` keyword, the closure would execute immediately and exit the scope.

### Summary

When should you use `@escaping`?  
When the closure needs to out-live the function it is apart of.

### Notes

[What is @escaping in Swift? | Donny Wals](https://www.donnywals.com/what-is-escaping-in-swift/)  
[Swift Closures: @escaping | Sean Allen](https://www.youtube.com/watch?v=xiS5gJOIQxI)
