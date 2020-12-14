# UICollectionView-自定义UICollectionViewFlowLayout

## 自定义布局需要重写以下四个方法

- 作用：在这个方法中做一些初始化操作
- 注意：子类重写prepareLayout,一定要调用[super prepareLayout]

``` Objective-C

- (void) prepareLayout;

```

- 作用：
- 这个方法的返回值是个数组
- 这个数组中存放的都是UICollectionViewLayoutAttributes对象
- UICollectionViewLayoutAttributes对象决定了cell的排布方式(frame等)

``` Objective-C

- (nullable NSArray<__kindof UICollectionViewLayoutAttributes *> *)layoutAttributesForElementsInRect: (CGRect)rect;

```

- 作用：如果返回YES，那么collectionView显示的范围发生改变时，就会重新刷新布局
- 一旦重新刷新布局，就会按顺序调用下面的方法：
- prepareLayout
- layoutAttributesForElementsInRect:

``` Objective-C

- (BOOL)shouldInvalidateLayoutForBoundsChange:(CGRect)newBounds;

```

- 作用：返回值决定了collectionView停止滚动时最终的偏移量(contentOffset)
- 参数：
- proposedContentOffset：原本情况下,collectionView停止滚动时最终的偏移量
- velocity：滚动速率，通过这个参数可以了解滚动的方向

``` Objective-C

- (CGPoint) targetContentOffsetForProposedContentOffset: (CGPoint)proposedContentOffset withScrollingVelocity:(CGPoint)velocity;

```

