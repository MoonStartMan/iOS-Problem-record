# iOS开发 tableView/collectionView获取当前点击的cell

## collectionView

``` Objective-C

- (void)collectionView: (UICollectionViewCell *)collectionView didSelectItemAtIndexPath: (NSIndexPath *) indexPath {
	//	cell不是自定义
	UICollectionViewCell *cell = (UICollectionViewCell *) [collectionView cell cellForItemAtIndexPath: indexPath];	//	即为要得到的cell
	//	自定义的cell
	MyViewCell *cell = (MyViewCell *)[self collectionView:collectionView cellForItemAtIndexPath: indexPath];	//	即为要得到的cell
}

```

## tableView

``` Objective-C

- (void)tableView: (UITableView *)tableView didSelectRowAtIndexPath: (NSIndexPath *)indexPath {
//	非自定义cell
	UITableViewCell *cell = (UITableViewCell *)[tableView cellForRowAtIndexPath: indexPath];
//	自定义cell
	MyViewCell *cell = (MyViewCell *)[self tableView: tableView cellForRowAtIndexPath: indexPath];
}

```