## Equality Operators

There are two equality operators in Swift.
1. ==
2. ===

### What is the difference?

1. ==  
This equality operator tests that two things are equal for whatever definition of `equal` those things use.  

Example:  
```
5 == 5 equals true because the == uses integer comparison.  
The same is true for other built-in types in Swift, such as strings, booleans, and doubles.  
```
2. ===  
This is the `identity operator`, which checks whether two instances of a class point to the same memory.  
This operator is only available to use for classes due to classes being reference types. Struct objects will always point to different memory.  

## Notes

[What’s the difference between == and ===? @ HackingWithSwift](https://www.hackingwithswift.com/example-code/language/whats-the-difference-between-equalsequals-and-equalsequalsequals)
