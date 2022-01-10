# General Software Principles

## SOLID

S - Single Responsibility Principle
  - A class should have *one and only one* reason to *change*

O - Open/Closed Principle
  - Software entities should be *open for extension* but *closed for modification*

L - Liskov Substitute Principle
  - Subtypes must be *substitutable* for their base types.

I - Interface Segregation Principle
  - The dependency of one class to another should depend on the *smallest* possible interface.
    - Clients should not be forced to implement interfaces they don't use.
    - Many smaller groups of interfaces > one giant interface.

D - Dependency Inversion Principle
  - Depend upon *abstractions (interfaces)* not upon concrete classes.


## DRY - Don't Repeat Yourself

When writing codes, there may be times where several instances of the application may need the same or similar logic. Instead of writing said logic over and over again, abstract it out into a single method and call that method where needed.

## AGILE

Agile is an interative approach to building software. Instead of trying to deliver everything all at once, the developers will break the project down into smaller pieces of functionality, sort by priority, then deliver those features in two week cycles.
