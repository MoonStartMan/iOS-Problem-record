# UICollectionViewCell点击事件

## UICollectionViewCell中重写setSelected方法

``` objective-c
-(void)setSelected:(BOOL)selected {
	[super setSelected: selected];
	if(selected) {
        self.backgroundColor = [UIColor colorWithRed:82/255.0 green:94/255.0 blue:255/255.0 alpha:1.0];
        self.smTitleText.textColor = [UIColor colorWithRed:255/255.0 green:255/255.0 blue:255/255.0 alpha:1.0];
    } else {
        self.backgroundColor = [UIColor colorWithRed:19/255.0 green:20/255.0 blue:20/255.0 alpha:1.0];
        self.smTitleText.textColor = [UIColor colorWithRed:144/255.0 green:147/255.0 blue:153/255.0 alpha:1.0];
    }
}
```

## 在UICollectionViewController中定义点击的NSIndexPath

``` objective-c
@property(nonatomic,strong) NSIndexPath* selectIndexPath;
```

## 在UICollectionViewController中

``` objective-c
-(UICollectionViewCell *) collectionView :(UICollectionView *) collectionView cellForItemAtIndexPath:(NSIndexPath *)indexPath{
    MIXMiddleViewCollectionViewCell *cell = [collectionView dequeueReusableCellWithReuseIdentifier:cellIdefdfd_ forIndexPath:indexPath];
    cell.layer.cornerRadius = 4;
    cell.smTitleText.text = self.menuTextArray[indexPath.row][@"menuText"];
    if(indexPath == self.selectIndexPath) {
        cell.backgroundColor = [UIColor colorWithRed:82/255.0 green:94/255.0 blue:255/255.0 alpha:1.0];
        cell.smTitleText.textColor = [UIColor colorWithRed:255/255.0 green:255/255.0 blue:255/255.0 alpha:1.0];
    } else {
        cell.backgroundColor = [UIColor colorWithRed:19/255.0 green:20/255.0 blue:20/255.0 alpha:1.0];
        cell.smTitleText.textColor = [UIColor colorWithRed:144/255.0 green:147/255.0 blue:153/255.0 alpha:1.0];
    }
    return cell;
}

-(void)collectionView:(UICollectionView *)collectionView didSelectItemAtIndexPath:(NSIndexPath *)indexPath {
    MIXMiddleViewCollectionViewCell *cell = [collectionView dequeueReusableCellWithReuseIdentifier:cellIdefdfd_ forIndexPath:indexPath];
    self.selectIndexPath = indexPath;
    [cell setSelected:YES];
    [collectionView reloadData];
}
```