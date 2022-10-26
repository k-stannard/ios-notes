# Memory Management in Swift

## Value Types

Value types are instances that keep a unique copy of their data.  
  - ie: strings, ints, bools, arrays, dictionaries, structs, enums

Value types are stored as a stack in memory.
  - It works as a Last In First Out (LIFO) basis.
  - When leaving scope, they're removed from the stack.

When a value type is assigned to multiple variables, they all have their own copy of data.
  - When you pass a value type into a function, a copy is made of the value.

## Reference Types

Reference types are instances that share a single copy of data.  
  - ie: classes, UIKit classes such as UILabels, UIViews, UITableViews

Swift has to keep track of how many variables are pointing to a reference type.
All reference types address in memory begin with 0x...

`When will swift remove a reference type from memory?`
  - When there are no more variables pointing to the reference type; ie: pointing an object to nil.

`How does swift know when to remove an object from memory?`
  - Automatic Reference Counting (ARC)
  - Every time an object points to a reference type, the reference count goes up by 1, and it will not remove it from memory until the reference count goes to zero.

## Dependencies

### Removing from memory

```swift
class Child {
}

class Parent {
  var child = Child()
}

var mom: Parent? = Parent()
mom = nil
```

1. Parent is initialized, which automatically initializes a child as well.
2. Both parent & child have their own address in memory, and have their own reference count.
3. When `mom` is set to `nil`, its reference count goes to zero, and the child reference count also goes to zero, because there is no longer a reference pointing to it.

## Orphans

An orphan is an instance where memory has been allocated, but it is stuck in memory and can't be removed.

## Retain Cycles

A retain cycle is an instance where two objects have a strong reference pointer to each other, preventing one another form being deallocated in memory.

`How do you fix a retain cycle?`
  - A class that references another class uses a `strong` reference by default. The child class will exist as long as the parent does.
  - To fix a retain cycle, you must make one of the references `weak`.
    1. Identify who the child is
    2. Make the child have a `weak` or `unowned` reference to the parent.

  - A weak/unowned reference does not increase the reference count.

```swift
// Parent
class Person {
  var job: Job?
}
// Child
class Job {
  weak var person: Person?
}
```

## Strong, Weak, Unowned References

Strong
  - the default reference. Child exists as long as the parent does.

Weak
  - Child may or may not exist.
  - Will not exist if parent is removed form memory.
  - Cannot be a constant.

Unowned
  - Child exists in memory all the time, but is removed when parent is.
  - Does not increase reference count.
  - Cannot be optional, has to have a value.
