# UICollectionView-scrollToItemAtIndexPath没有作用解决方法

## 解决方法1: 前面加上layoutIfNeeded

``` Objective-C

[self loadViewIfNeeded];

[self.collectionView scrollToItemAtIndexPath:[NSIndexPath indexPathForRow:self.currentIndex inSection:0] atScrollPosition:UICollectionViewScrollPositionCenteredHorizontally animated:NO];


```

## 解决方法2: viewDidLayoutSubviews

``` Objective-C

- (void)viewDidLayoutSubviews {

[super viewDidLayoutSubviews];

[self.collectionView scrollToItemAtIndexPath:[NSIndexPath indexPathForRow:self.currentIndex inSection:0] atScrollPosition:UICollectionViewScrollPositionCenteredHorizontally animated:NO];

}

```