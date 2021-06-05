# UICollectionView实现水平滑动pagingEnabled分页偏移问题

1. 创建UICollectionView

设置```flowLayout.minimumLineSpacing = 0.000001f;```

``` Objective-C

UICollectionViewFlowLayout *flowLayout = [[UICollectionViewFlowLayout alloc] init];
flowLayout.minimumLineSpacing = 0.000001f;
flowLayout.scrollDirection = UICollectionViewScrollDirectionHorizontal;

```