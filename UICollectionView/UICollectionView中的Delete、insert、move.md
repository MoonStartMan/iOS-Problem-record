# UICollectionView中的Delete、insert、move

UICollectionView的删除和插入(insert,delete),都会自动调用reloadData;因此需要在调用如下方法前先处理一下datasource(数据源)

``` Objective-C

- (void)insertItemsAtIndexPaths:(NSArray<NSIndexPath *> *)indexPaths;
- (void)deleteItemsAtIndexPaths:(NSArray<NSIndexPath *> *)indexPaths;
- (void)reloadItemsAtIndexPaths:(NSArray<NSIndexPath *> *)indexPaths;

```

例子

``` Objective-C

[self.userInfos insertObject:info atIndex:0];
[self.collectionView insertItemsAtIndexPaths: @[[NSIndexPath indexPathForRow:0 insection:0]]];

```

删除或插入尽可能