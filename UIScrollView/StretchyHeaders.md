## How to implement stretchy header views
With some complicated math, a stretchy header can be implemented with the following:
```swift        
    func scrollViewDidScroll(_ scrollView: UIScrollView) {
        let changeY = -scrollView.contentOffset.y
        var width = view.frame.width + changeY * 2
        width = max(view.frame.width, width)
        imageView.frame = CGRect(x: min(0, -changeY), y: min(0, -changeY), width: width, height: width)
    }
```

An alternative method using the imageView's center property and less complicated math:

```swift
    func scrollViewDidScroll(_ scrollView: UIScrollView) {
        let scrollViewY = scrollView.contentOffset.y
        let width = max(view.frame.width - scrollViewY, view.frame.width)
        imageView.frame = CGRect(x: 0, y: scrollViewY, width: width, height: width)
        imageView.center.x = scrollView.center.x
    }
```

## Example

![ezgif com-gif-maker(1)](https://user-images.githubusercontent.com/21287326/142337872-6d4353c7-5ca9-4ef6-a8bb-5f1390faa292.gif)
