# UICollectionView重用时的视图重叠

## 方法一：移除contentView上的视图再添加视图

``` Objective-C

- (UICollectionViewCell *)collectionView: (UICollectionView *)collectionView cellForItemAtIndexPath:(nonnull NSIndexPath *)indexPath {
    UICollectionViewCell *cell = [self.lineCollectionView dequeueReusableCellWithReuseIdentifier:@"CellId" forIndexPath:indexPath];
    //	移除contentView上的视图,不然会重叠
    for (UIView *view in [cell.contentView subviews]) {
        [view removeFromSuperview];
    }
    //	cell上的视图配置
    cell.backgroundColor = [UIColor colorWithRed:arc4random()%255/255.0 green:arc4random()%255/255.0 blue:arc4random()%255/255.0 alpha:1];
    UILabel* cellLabel = [[UILabel alloc] init];
    [cell.contentView addSubview: cellLabel];
    [cellLabel mas_makeConstraints:^(MASConstraintMaker *make) {
        make.centerX.equalTo(cell.mas_centerX).with.offset(0);
        make.centerY.equalTo(cell.mas_centerY).with.offset(0);
    }];
    
    cellLabel.font = [UIFont systemFontOfSize:20.0f];
    cellLabel.textColor = [UIColor whiteColor];
    cellLabel.text = [NSString stringWithFormat:@"%ld",1 + indexPath.row];
    return cell;
}

```

## 方法二：新建UICollectionViewCell的类,在类中重写init方法初始化想要的视图

1： 首先创建一个类，集成 UICollectionViewCell，将你这个UIImageView加到这个类的init方法里面去
2： 在viewDidLoad的时候，注册重用     [self.collectionView registerClass:[MyCollectionViewCell class] forCellWithReuseIdentifier:@"CELL"];
3： 使用 MyCommentsCell *cell = [collectionView dequeueReusableCellWithReuseIdentifier:@"CELL" forIndexPath:indexPath];