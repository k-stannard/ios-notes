# Unit Testing in iOS

## How to add unit tests to a project

Add a new Target to the project.
  - Go to the project target list & add a new target by hitting the + sign.
  - Search 'unit' in the search bar to find `Unit Testing Bundle`.
  - Click next, give it a name, then finish.

## How to run unit tests

- To run unit tests, use the shortcut key `cmd+u`.
- To run a single test, click on the green diamond next to the test you want to run.
- To run all tests for a given class, click on the green diamond next to the class name.

## Writing unit tests

Several things are needed to write unit tests
1. Import XCTest
2. Add the keyword `@testable import 'project name'` 
  - This will allow the testing file to access the modules and files in the app.
3. Inherit the `XCTestCase` class to your testing class
4. Add a class to test, force unwrapping said class.
  - For example, if testing a view controller class, you would write `var viewController: ViewController!`
5. Instantiate the class in setUp()
  - `viewController = ViewController()`
  - setUp() is ran once per test. Allows you to not have to remember the state of your app between tests. Fresh start each time.
6. Write your unit test!

## Testing methods

XCTAssertEqual()
- Assert Equal uses a boolean check to see if the result on the left hand side is equal to the value on the right hand side
- Example: 
```swift
var result = "ThisIsTheCorrectAnswer"
XCTAssertEqual(result, "ThisIsTheCorrectAnswer") // returns true, test passes.
```

## Notes

Unit testing will affect the design of your app. Extracting classes, functions, etc. into smaller components will make it easier to write and perform tests.
Unit tests are also a good form of documentation. They will essentially tell the developer how they expect a function to work. If you're trying to learn how a function works, looking for unit tests will give you a good idea.
Unit tests are a core part of the continuous integration process, aka CI. 
- If a CI is implemented on a project, when code is commited to the codebase, all of the unit tests will be ran. You will know about bugs instantaneously. Adding tests will allow you to be confident in the code you are committing.
