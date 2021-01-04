# UICollectionView设置间距技巧

## 定义每一个cell的大小

``` Objective-C

- (CGSize)collectionView: (UICollectionView *)collectionView layout: (UICollectionViewLayout *)collectionViewLayout sizeForItemAtIndexPath: (NSIndexPath *)indexPath {
	CGSize size = CGSizeMake(80, 80);
	return size;
}

```

## 定义每个Section的四边间距

``` Objective-C

- (UIEdgeInsets)collectionView: (UICollectionView *)collectionView layout: (UICollectionViewLayout *)collectionViewLayout insetForSectionAtIndex: (NSInteger)section {
	return UIEdgeInsetsMake(15, 15, 5, 15);	//	分别为上、左、下、右
}

```

## 这个是两行cell之间的间距(上下行cell的间距)

``` Objective-C

- (CGFloat)collectionView: (UICollectionView *)collectionView layout: (UICollectionViewLayout *)collectionViewLayoutminimumLineSpacingForSectionAtIndex: (NSInteger)section;

```

## 两个cell之间的间距 (同一行的cell间距)

``` Objective-C

- (CGFloat)collectionView: (UICollectionView *)collectionView layout: (UICollectionViewLayout *)collectionViewLayoutminimumInteritemSpacingForSectionAtIndex:(NSInteger)section;

```