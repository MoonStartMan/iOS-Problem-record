

# iOS设置字体

``` objective-c
-(void)createText {
    UILabel * text = [[UILabel alloc]init];
    text.frame = CGRectMake(32, 453, 311.5, 50);
    text.numberOfLines = 0;
    NSMutableParagraphStyle *paragraphStyle = [[NSMutableParagraphStyle alloc]init];
    [paragraphStyle setLineSpacing:11];
    NSMutableAttributedString *string = [[NSMutableAttributedString alloc] initWithString:@"文字、贴纸、边框、背景、图形一键应用\n用照片讲述生动故事"attributes: @{NSFontAttributeName: [UIFont systemFontOfSize:14],NSParagraphStyleAttributeName:paragraphStyle,NSForegroundColorAttributeName: [UIColor colorWithRed: 191/255.0 green:194/255.0 blue:204/255.0 alpha:1.0]}];
    text.attributedText = string;
    text.textAlignment = NSTextAlignmentCenter;
    [self.view addSubview:text];
}
```

## numberOfLines

该属性设置字体的展示多少行，如果设置为0，则表示有多少行展示多少行。

## 设置字体行高

``` objective-c
NSMutableParagraphStyle *paragraphStyle = [[NSMutableParagraphStyle alloc] init];
[paragraphStyle setLineSpacing: 11];
NSParagraphStyleAttributeName: paragraphStyle
```