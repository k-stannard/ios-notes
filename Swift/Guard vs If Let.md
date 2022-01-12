# Guard Statements vs If Let Statements

## What is a guard statement?

The `guard` keyword allows us to check code for certain conditions and exit the current scope if those conditions are not met. Certain required conditions may be checking whether a boolean value is true or whether an optional is not nil. 

A guard statement may be setup as follows:
```swift 
guard <condition> else { return }
```
The `return` exits the scope if the condition is not met. You may also use `break`, `continue`, and `throw` when appropriate to exit scope upon unmet conditions as well.

## What is an if let statement?

If let statements esssentially use the same idea, but are used in the opposite way. For example, you can use an if let statement to check optionals and boolean values as well, but instead of exiting the scope upon failure, you will continue within the current scope when the conditions are met. 

You can see the difference in code as follows:
```swift
guard <condition> else { return }
//continue scope work
```
vs
```swift
if let <variable> = <optionalVariable> { 
  //continue scope work 
}
```

## When should you use guard vs if let?

If you want to ensure certain conditions are met before executing code, use a guard statement.  
If a method is allowed to continue when certain conditions are not met, use an if let statement.

## Further reading / examples

[Guard statements explained with code examples by SwiftLee](https://www.avanderlee.com/swift/guard-statements/)  
[Guard keyword examples by HackingWithSwift](https://www.hackingwithswift.com/new-syntax-swift-2-guard)
