# UITableView性能优化

每当一个cell进入视野范围就会调用1次这个方法

``` objective-c
- (UITableViewCell *)tableView:(UITableView *)tableView cellForRowAtIndexPath: (NSIndexPath *)indexPath {
	
}
```

## 具体实现方法

``` objective-c
- (UITableViewCell *)tableView:(UITableView *)tableView cellForRowAtIndexPath: (NSIndexPath *)indexPath {
	//	0.定义一个重用标识
	static NSString *ID =@"A";
	//	1.首先去缓存池中找可循环利用的cell
	UITableViewCell *cell = [tableView dequeueReusableCellWithIdentifier:ID];
	//	2.如果缓存池中没有可循环利用的cell,自己创建新的cell
	if(cell == nil) {
		cell = [[UITableViewCell alloc] initWithStyle:UITableViewCellStyleDefault reuseIdentifier:ID];
		
		//	所有cell都一样的设置尽量写在这个大括号中
		//	cell.backgroundColor = [UIColor redColor];
		//	cell不是都一样的设置写在外面
	}
	
	//	3.设置cell显示的数据
	cell.textLabel.text = [NSString stringWithFormat:@"第%zd行数据",indexPath.row];
	if(indexPath.row %2 == 0) {
		cell.accessoryType = UITableViewCellAccessoryDisclosureIndicator;
	} else {
		cell.accessoryType = UITableViewCellAccessoryNone;
	}
	
	//	4.返回cell
	return cell;
}
```