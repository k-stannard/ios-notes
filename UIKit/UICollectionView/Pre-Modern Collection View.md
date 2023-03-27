# Pre-Modern Collection Views

## Key Concepts

- Layout
- Data source
- Delegate

UICollectionView is not meant to be used directly, instead concrete subclasses of UICollectionView are given.

### UICollectionViewFlowLayout

- Subclass of UICollectionViewLayout
- UICollectionViewDelegateFlowLayout extends UICollectionViewDelegate
- Line-based layout system that covers a wide range of designs
  1. Orthogonal layout system, line by line

#### Ways to customize flow layouts
1. line spacing - the space between the items on the horizontal axis
2. inter-item spacing - the space between each item on each line
3. line orientation - the space between the items on the vertical axis

### UICollectionViewDataSource

- provides content
- section and item counts

#### 3 Core methods of UICollectionViewDataSource

```swift
optional func numberOfSections(in collectionView: UICollectionView) -> Int { }
func collectionView(_ collectionView: UICollectionView, numberOfItemsInSection section: Int) -> Int { }
func collectionView(_ collectionView: UICollectionView, cellForItemAt indexPath: IndexPath) -> UICollectionViewCell { }
```

### UICollectionViewDelegate

- Use of the collection view delegate is optional
- Extends UIScrollViewDelegate
- Fine-grained control
  1. highlighting
  2. selection
- View appearance events
  1. willDisplayItem
  2. didEndDisplayingItem

### When should you use custom layout?

If your design is more complex than a line-by-line based layout, then custom is the way to go.

### 4 basic methods of custom layouts

#### 1. Providing Content Size
```swift
open var collectionViewContentSize: CGSize { get }
```

- Size of bounds which contains all items
- Needed for UIScrollView.contentSize

#### 2. & 3. Providing Layout Attributes
```swift
func layoutAttributesForElements(in rect: CGRect) -> [UICollectionViewLayoutAttributes]?
func layoutAttributesForItem(at indexPath: IndexPath) -> UICollectionViewLayoutAttributes?
```
- query by geometric region
- query by index path
- performance matters

#### 4. Preparing the Layout
```swift
func prepare()
```
- called for every `invalidateLayout`
- cache `UICollectionViewLayoutAttributes`
- compute `collectionViewContentSize`

#### 5. Handling Bounds Changes in Your Custom Layout
```swift
func shouldInvalidateLayout(forBoundsChange newBounds: CGRect) -> Bool
```
- called for every bounds change (size, origin)
- called during scrolling
- default implementation returns `false`
