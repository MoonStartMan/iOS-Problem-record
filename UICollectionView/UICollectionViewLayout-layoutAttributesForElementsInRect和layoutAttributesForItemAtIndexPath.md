# UICollectionViewLayout-layoutAttributesForElementsInRect和layoutAttributesForItemAtIndexPath

## layoutAttributesForItemAtIndexPath

``` Objective-C

- (UICollectionViewLayoutAttributes *)layoutAttributesForItemAtIndexPath: (NSIndexPath *)indexPath

```

作用：返回rect中的所有元素的布局属性。

## layoutAttributesForElementsInRect

``` Objective-C

-(NSArray *)layoutAttributesForElementsInRect:(CGRect)rect

```

作用：返回对应indexPath的位置的cell的布局属性