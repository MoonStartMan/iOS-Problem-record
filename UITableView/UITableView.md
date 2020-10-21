# UITableView

## UITableView各类设置

### UITableView初始化并设置数据源

``` objective-c
UITableView *tableView = [[UITableView alloc] initWithFrame:CGRectMake(0,0,self.view.bounds.size.width,self.view.bounds.size.height)];
tableView.dataSource = self;	//	设置数据源
```

### 不显示cell的下划线

``` objective-c
tableView.separatorStyle = UITableViewCellSeParatorStyleNone;	//	不显示下划线
```

### 告诉tableView一共有多少组数据

``` objective-c
- (NSInteger)numberOfSectionsInTableView:(UITableView *)tableView
{
    return 5;
}
```

### 告诉tableView每一组有多少行

``` objective-c
- (NSInteger)tableView:(UITableView *)tableView numberOfRowsInSection:(NSInteger)section {
    return 1;
}
```

### 告诉tableView每一行显示的内容一定是UITableCell或者它的子类

``` objective-c
- (UITableViewCell *) tableView:(UITableView *)tableView cellForRowAtIndexPath:(NSIndexPath *)indexPath {
    static NSString *tableIdentifier = @"tableIdentifier";
    UITableViewCell *cell = [tableView dequeueReusableCellWithIdentifier:tableIdentifier];
    if(cell == nil) {
        cell = [[UITableViewCell alloc] initWithFrame:CGRectZero];
    }
    switch (indexPath.section) {
        case 0:
            cell.textLabel.attributedText = [self addTextColor:@"300+专业调色滤镜 持续更新" indexPath:4];
            break;
        case 1:
            cell.textLabel.attributedText = [self addTextColor:@"3000+海报模版 贴纸、字体等资源" indexPath:5];
            break;
        case 2:
            cell.textLabel.attributedText = [self addTextColor:@"40+艺术滤镜 持续更新" indexPath:3];
            break;
        case 3:
            cell.textLabel.text = @"渐变滤镜、照片批处理等高级工具";
            break;
        case 4:
            cell.textLabel.text = @"可跨平台享受会员权益";
            break;
        default:
            break;
    }
    UIImage *img = [UIImage imageNamed:@"close_icon"];
    cell.imageView.image = img;
    return cell;
}
```

