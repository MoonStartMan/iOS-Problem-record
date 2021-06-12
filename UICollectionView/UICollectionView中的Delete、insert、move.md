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

删除或插入尽可能先判断一下；因为这些插入和删除是线程不安全的

``` Objective-C

//	删除时
[self.infos removeLastObject];
if ([self.collectionView numberOfItemsInSection:0] == self.infos.count) {
      [self.collectionView reloadData];
}else{
      [self.collectionView deleteItemsAtIndexPaths:@[[NSIndexPath indexPathForItem:self.infos.count-1 inSection:0]]];
 }
//	添加时
[self.infos insertObject:info atIndex:0];

if (self.infos.count == 1 || [self.collectionView numberOfItemsInSection:0] == self.infos.count) {
        [self.collectionView reloadData];
}else{
        [self.collectionView insertItemsAtIndexPaths:@[[NSIndexPath indexPathForItem:0 inSection:0]]];
}

```

demo-长按删除cell的方法

``` Objective-C

- (void)deleteAddress:(UILongPressGestureRecognizer*)longPress{
    CGPoint pt = [longPress locationInView:self.collectionView];
  
    //主要是此方法可以根据point拿到当前点击的cell的index；
    NSIndexPath *indexPath = [self.collectionView indexPathForItemAtPoint:pt];
   
    UIAlertController *alertControl = [UIAlertController alertControllerWithTitle:@"删除地址" message:nil preferredStyle:UIAlertControllerStyleAlert];
    
    UIAlertAction *action = [UIAlertAction actionWithTitle:@"确定" style:UIAlertActionStyleDefault handler:^(UIAlertAction * _Nonnull action) {
        LTAddressListModel *model = self.dataArray[indexPath.row];
        [self deletMyAddressWithParmas:@{@"ids":model.ID}];
        [self.dataArray removeObjectAtIndex:indexPath.row];
        [self.collectionView deleteItemsAtIndexPaths:@[indexPath]];
    }];
    
    UIAlertAction *cancelAction = [UIAlertAction actionWithTitle:@"取消" style:UIAlertActionStyleCancel handler:nil];
    
    [alertControl addAction:action];
    [alertControl addAction:cancelAction];

    [self presentViewController:alertControl animated:NO completion:nil];
}

```