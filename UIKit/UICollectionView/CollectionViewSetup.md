## Setting up UICollectionView with Diffable DataSource

To setup a new UICollectionView, you must first declare a property for both the collection view and its data source.

```swift
var collectionView: UICollectionView! = nil
var dataSource: UICollectionViewDiffableDataSource<Section, Item>! = nil
```
UICollectionViewDiffableDataSource takes a section identifier type and an item identifier type as its parameters. The section identifier type can be defined with an enumeration, a standard type such as Int, or a custom class. Same idea with the item identifier type.

```swift 
enum Section {
  case main
}
```

