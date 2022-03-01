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

### Creating the Layout

A collection view layout can be made with the `UICollectionViewCompositionalLayout` class.  
The essential components of a compositional layout are:
* item - item determine the size and layout of each individual cell in the collection
* group - group determine the size and layout of each row in the collection
* section - section determine the layout of specific sections in the collection
* layout - layout combines all of the components of the collection into one view

#### Managing the size

The size of the compositional layout can be initalized using the `NSCollectionLayoutSize` method.
```swift 
NSCollectionLayoutSize(widthDimension: CGFloat, heightDimension: CGFloat)
```
There are four methods to set the size for the width and height dimensions:
* .fractionalWidth - using this method will compute the width as a fraction of its ***container***
* .fractionalHeight - same idea as the width for height
* .absolute - this method will compute a dimension with an exact point value
* .estimated - this method will compute a dimension with an estimated point value, and once the content has rendered the actual point value will be determined.

Each of the four components of a compositional layout require their own method for initialization
```swift
NSCollectionLayoutItem(layoutSize: NSCollectionLayoutSize)
NSCollectionLayoutGroup()
NSCollectionLayoutSection(group: NSCollectionLayoutGroup)
UICollectionViewCompositionalLayout(section: NSCollectionLayoutSection)
```
`NSCollectionLayoutGroup` takes an additional method for its layout with:
```swift 
horizontal(layoutSize: NSCollectionLayoutSize, subitems: [NSCollectionLayoutItem])
vertical(layoutSize: NSCollectionLayoutSize, subitems: [NSCollectionLayoutItem])
```
*Notes: these are not the only initializer methods for setting up the layout. Check documentation for other options.*

Combining all of these methods together to create a layout:
```swift 
func createLayout() -> UICollectionViewLayout {
    let itemSize = NSCollectionLayoutSize(widthDimension: .fractionalWidth(0.2), heightDimension: .fractionalHeight(1))
    let item = NSCollectionLayoutItem(layoutSize: itemSize)
        
    let groupSize = NSCollectionLayoutSize(widthDimension: .fractionalWidth(1), heightDimension: .absolute(50))
    let group = NSCollectionLayoutGroup.horizontal(layoutSize: groupSize, subitems: [item])
        
    let section = NSCollectionLayoutSection(group: group)
        
    let layout = UICollectionViewCompositionalLayout(section: section)
    return layout
}
```
will result in a collection view that looks like the following layout:  
<img width="273" alt="Screen Shot 2022-02-09 at 9 23 06 PM" src="https://user-images.githubusercontent.com/21287326/153331161-504e42a8-ea50-45c9-a062-9df6027007b9.png">

#### Content Insets
If you wanted to add spacing around a specific component in a collection view, all you have to do is initialize said component's content insets.  
Content insets will adjust for its final size of the component after the position is computed.  

To add content insets to a component, initialize the contentInsets method on whichever component you want to add spacing to. 
```swift
item.contentInsets = .init(top: CGFloat, leading: CGFloat, bottom: CGFloat, trailing: CGFloat)
```
By initializing a value of 5 to each side of the item, the view adjusts each item to have a spacing of 5 points:    

<img width="273" alt="Screen Shot 2022-02-09 at 9 31 08 PM" src="https://user-images.githubusercontent.com/21287326/153331929-9c1df052-d6e4-4d12-9ec8-da385d9ca02a.png">

## Diffable Datasource Snapshot

What makes the diffable data source is the snapshot. The snapshot is a representation of the state of the data in a view at a specific point in time. 
To use the snapshot, initialize the snapshot, populate it with data, and apply the snapshot to the collection view's data source.

```swift
var snapshot = NSDiffableDataSource<Section, Int>()
snapshot.appendSections([.main])
snapshot.appendItems(Array(0...100))
dataSource.apply(snapshot, animatingDifferences: true)
```

