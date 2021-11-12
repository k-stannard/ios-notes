Reusable View

```swift

extension ReusableView where Self: UIView {
    static var reuseIdentifier: String {
        return String(describing: self)
    }
}

extension UITableViewCell: ReusableView {}
extension UITableViewHeaderFooterView: ReusableView {}

extension UICollectionView: ReusableView {}
extension UICollectionReusableView: ReusableView {}

```

UITableView+Utilities

```swift

extension UITableView {
    func register<T: UITableViewCell>(_: T.Type) {
        register(T.self, forCellReuseIdentifier: T.reuseIdentifier)
    }

    func register<T: UITableViewHeaderFooterView>(_: T.Type) {
        register(T.self, forHeaderFooterViewReuseIdentifier: T.reuseIdentifier)
    }
    
    func dequeueReusableCell<T: UITableViewCell>(forIndexPath indexPath: IndexPath) -> T {
        let cell = dequeueReusableCell(withIdentifier: T.reuseIdentifier, for: indexPath)
        return cell as! T
    }

    func dequeueHeaderFooterView<T: UITableViewHeaderFooterView>() -> T {
        let headerFooterView = dequeueReusableHeaderFooterView(withIdentifier: T.reuseIdentifier) as! T
        return headerFooterView
    }
}

```
