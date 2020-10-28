# UITableView的代理方法

## 设置分区

``` objective-c
- (NSInteger)numberOfSectionsInTableView:(UITableView *)tableView {
	return 1;
}
```

## 设置行

``` objective-c
- (NSInteger)tableView:(UITableView *)tableView numberOfRowsInSection: (NSInteger)section {
	return 4;
}
```

## 当用户点击(选中)某一行cell的时候就会自动调用这个方法

``` objective-c

- (void)tableView: (UITableView *)tableView didSelectRowAtIndexPath:(nonnull NSIndexPath *)indexPath {
	NSLog(@"选中-%zd", indexPath.row);
}

```

## 当用户取消点击(选中)某一行cell的时候就会自动调用这个方法

``` objective-c
- (void)tableView: (UITableView *)tableView didDeselectRowAtIndexPath:(nonnull NSIndexPath *) indexPath {
	NSLog(@"取消选中-%zd",indexPath.row);
}
```

## 返回每一组的头部控件

``` objective-c
- (UIView *)tableView:(UITableView *)tableView viewForHeaderInSection:(NSInteger)section {
    return [UIButton buttonWithType:UIButtonTypeContactAdd];
}
```

## 返回每一组的尾部控件

``` objective-c
- (UIView *)tableView:(UITableView *)tableView viewForFooterInSection:(NSInteger)section {
    return [UIButton buttonWithType:UIButtonTypeSystem];
}
```

## 返回每一组的尾部高度

``` objective-c
- (CGFloat)tableView: (UITableView *)tableView heightForFooterInSection:(NSInteger)section {
    if(section == 0) {
        return 50;
    } else {
        return 100;
    }
}
```

## 返回每一行cell的高度

``` objective-c
- (CGFloat)tableView: (UITableView *)tableView heightForRowAtIndexPath:(nonnull NSIndexPath *)indexPath {
    if (indexPath.row %2 == 0) {
        return 70;
    } else {
        return 100;
    }
}
```
