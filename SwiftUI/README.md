# Creating and Combining Views
### LandmarksApp.swift
SwiftUI uses a structure that conforms to the App Protocol. The structure's body property returns one or more scenes, which in turn provide content for display. The @main attribute identifies the app's entry point.

```swift
@main
struct LandmarksApp: App {
    var body: some Scene {
        WindowGroup {
            ContentView()
        }
    }
}
```

### ContentView.swift
SwiftUI view files declare two structures. The first conforms to the view protocol and describes the view's content and layout. The second declares a preview for that view.

```swift
struct ContentView: View {
    var body: some View {
        Text("Hello, World!")
        .padding()
    }
}

struct ContentView_Previews: PreviewProvider {
    static var previews: some View {
        ContentView()
    }
}
```

As you change the code in a view's body property, the preview updates to reflect your changes.

## Customize the Text View
There are three ways you can edit text on a view: 1) the source editor, 2) the canvas, and 3) the inspectors.

To use the SwiftUI Inspector, command-click the text to bring up the editing popover and select the corresponding option. The editing popover also shows different attributes that you can customize, depending on the type of view that is inspected.

To customize a view, you can call modifier methods. Modifiers wrap a vie to change its display or other properties. Each modifier returns a new view, so it's common to chain multiple modifiers, stacked vertically.

```swift
    Text("Turtle Rock")
        .font(.title)
        .foregroundColor(.green)
```

You may also command-click a property in the source code to access the Inspector tool.

## Combining Views Using Stacks
When creating a view, you can describe its content layout, and the behavior in the view's body property; however the body property only returns a single view. You can combine and embed multiple views in a stack view.

To embed a stack view, wrap the appropriate containt with the VStack property.
```swift
VStack {
    Text("Turtle Rock")
        .font(.title)
        .foregroundColor(.green)
}
```

To add another text label in the stack, simply insert Text() where desired.
```swift
Text("Turtle Rock")
    .font(.title)
Text("Joshua Tree National Park")
    .font(.subheadline)
```

To set the alignment view of of the Stack view, add the alignment property to the VStack.
```swift
VStack(alignment: .leading) {
    //text labels, etc
}
```

You may embed a stack within a stack with ease. Simply wrap the second preferred stack inside/outside of the original stack.
```swift
VStack {
    //Text label
    HStack {
        //More text labels
    }
}
```

You can add spacers between labels. A spacer expands to make its containing view use all of the space of its parent view, instead of having its size defined only by its contents.
```swift
VStack {
    Text("Some text")
    Spacer()
    Text("More text")
}
```

You can use the .padding() modifier to give the view's content a little more space.

## Create a Custom Image View
To create an image view, you will need a new SwiftUI view for the custom image.
File > New > File > SwiftUI View

To add an image to the view, replace the default Text() init with Image() init and pass the image name to display.
```swift
struct CircleImage: View {
    var body: some View {
        Image("turtlerock")
    }
}
```

To apply a circular clipping shape, simply call the clipShape() method to apply the clipping.
The Circle type is a shape that you can use as a mask, or as a view by giving thecircle a stroke or fill.
```swift
Image("turtlerock")
    .clipShape(Circile())
```

You can add strokes and shadows and add them as an overlay to give an image a border.
```swift
.overlay(Circle().stroke(Color.gray, lineWidth: 4))
.shadow(radius: 7)
```

## Use SwiftUI Views From Other Frameworks
You can use the Map view from MapKit to render a map in SwiftUI. 

First, import MapKit

Use the @State attribute to establish a source of truth for data in your app that you can modify from more than one view. SwiftUI manages the underlying storage and automatically updates views that depend on the value.

```swift
@State private var region = MKCoordinateRegion(
    center: CLLocationCoordinate2D(latitude: 34.001_286, longitude: -116.166_868),
    span: MKCoordinateSpan(latitudeDelta: 0.2, longitudeDelta: 0.2)
)
```

Next, add the map view to the body that takes a binding to the region.
By prefixing a state variable with $, you pass a binding, which is like a reference to the underlying value. When the user interacts with the map, the map updates the region value to match the part of the map that's currently visible in the user interface.
```swift
Map(coordinateRegion: $region)
```

When previews are in static mode, they only fully render native SwiftUI views. For the Map view, you'll need to switch to a live preview to see it render.

## Compose the Detail View
You may specify the MapView's properties without having to provide a value for each.

```swift
MapView()
    .frame(height: 300)
```
When you specify only the height parameter, the view automatically sizes to the width of its content. In this case, MapView expands to fill the available space.

To layer views ontop of other views, you may specify offset and padding values.
```swift
CircleImage()
    .offset(y: -130)
    .padding(.bottom, -130)
```

To allow the map content to extend to the top edge of the screen, add the ignoreSafeArea(edges:) modifier to the map view.

You can add a divider to the screen with a call to Divider()

When you apply a modifier to a layout view like a stack, SwiftUI applies the modifier to all the elements contained in the group. To apply a modifier to a stack, add the notation outside of the end of the stack.
```swift
HStack {
    //Text etc..
}
.font(.subheadline)
.foregroundColor(.secondary)
```