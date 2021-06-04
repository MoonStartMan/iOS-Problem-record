# UICollectionView跳转到指定位置

UICollectionView视图滚动到指定位置的方法

``` Objective-C

-(void)scrollToItemAtIndexPath:(NSIndexPath *)indexPath atScrollPosition:(UICollectionViewScrollPosition)scrollPosition animated:(BOOL)animated;

```

``` Objective-C

[collectionView setContentOffset: offsetPoint animated: NO];

```