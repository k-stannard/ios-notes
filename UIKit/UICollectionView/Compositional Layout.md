# Compositional Layout

Compositional layout sits right along side UICompositionalFlowLayout as a peer.  
Compositional layouts are:
- composable
- flexible
- fast

You use compositional layouts by:
- composing small layout groups together
- layout groups are line-based
- composition instead of subclassing

### Core components to composing layouts 

The core components to composing a compositional layout include:
1. size
2. item
3. group
4. section
5. layout

The 4 main components, (item, group, section, layout), progress into each other.  
<img width="437.5" alt="Screenshot 2023-03-27 at 4 51 59 PM" src="https://user-images.githubusercontent.com/21287326/228075336-26194577-ac0c-4f0d-94ec-e80f1c71b750.png">

### NSCollectionLayoutSize

Everything has an explicit size.  
Size = width + height

Takes width and height as an NSCollectionLayoutDimension.  

### NSCollectionLayoutDimension 

Axis independent, and there are 4 ways to define
1. fractionalWidth
2. fractionalHeight
3. absolute
4. estimated

The first two are based on the percentage of the container, and the other two are point-based.  
If you don't know how big an item is going to be, you can use estimated. Estimated will grow over time based on the content of the item.  

### NSCollectionLayoutItem

An item is a cell or a supplementary view on the screen.  

### NSCollectionLayoutGroup

The group is the basic unit of layout. There are 3 forms of group:
1. horizontal
2. vertical
3. custom

Can think of groups as mini flow layouts.  
You can compose custom right along side horizontal and vertical layouts.

### NSCollectionLayoutSection

Defines the sections layout.

### UICollectionViewCompositionalLayout

2 ways to construct a compositional layout:
1. specify layout sections definition, similar to flow layout.
2. can specify a closure that will ask for definitions of a section on a per-section basis, allowing layouts to be completely distinct between sections.  

Group size ultimately determines the size of the items. Item size can use fractional width and height to determine what its size will be using a percentage of its container. If you were to give its group an absolute height, that effectively determines the size of the item by taking its fractional height percentage of the absolute height.  

For example:
```swift
let itemSize = NSCollectionLayoutSize(widthDimension: .fractionalWidth(1.0), heightDimension: .fractionalHeight(1.0))
let groupSize = NSCollectionLayoutSize(widthDimension: .fractionalWidth(1.0), heightDimension: .absolute(44))
```

The above says that the item size will be 100% of the width and height of its container. Since the group size is using an absolute value of 44 points, the item size will take 100% of those 44 points for its height. The group is also using 100% of the width of its container as well.

