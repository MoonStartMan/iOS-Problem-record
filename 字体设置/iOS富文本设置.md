# iOS富文本设置

## 富文本设置

``` objective-c

//	封装函数
-(NSMutableAttributedString *)addTextColor:(NSString *)textString indexPath:(NSInteger)index {
    NSMutableAttributedString *font= [[NSMutableAttributedString alloc]initWithString:textString];
    [font addAttribute:NSForegroundColorAttributeName value:[UIColor colorWithRed:207/255.0 green:89/255.0 blue:246/255.0 alpha:1.0] range:NSMakeRange(0, index)];
    return font;
}

// 调用函数
cell.textLabel.attributedText = [self addTextColor:@"300+专业调色滤镜 持续更新" indexPath:4];
```

### UITableView 设置禁止滑动

``` objective-c
tableView.scrollEnabled = NO;
```

### UITableView设置透明背景

``` objective-c
tableView.backgroundColor = [UIColor clearColor];
cell.backgroundColor = [UIColor clearColor];
```