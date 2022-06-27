## SwiftUI Basics

### Content View & ContentView_Previews

When creating a new SwiftUI Project, the xcode template will auto generate a ContentView file containing two structs named `ContentView` and `ContentView_Previews`.

The ContentView struct conforms to a `View` protocol, which is generated by SwiftUI. The View protocol consists of anything that can be drawn to the screen, such as buttons, labels, colors, etc.

There is a computed property by default, named `body`, which returns type `some View` - meaning it will return something that conforms to the View protocol.

Inside of body contains a text property containing "Hello, World" text and a method called `.padding()`, otherwise known as a `modifier` in SwiftUI.

The ContentView_Previews struct conforms to a `PreviewProvider` protocol. This struct is used for the purposes of designing, debugging, etc. within xcode and is not required for the final product of an app. 