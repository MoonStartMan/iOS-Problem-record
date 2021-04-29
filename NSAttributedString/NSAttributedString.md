# iOS富文本

## 初始化label

``` Objective-C

UILabel *introLabel = [[UILabel alloc] init];
[self.view addSubview:self.introLabel];

```

## 富文本设置颜色

我这里封装了一个方法把需要进行颜色处理和不进行颜色处理的文字设置好。

``` Objective-C

//  给文字添加颜色
- (NSMutableAttributedString *)setNormlVipText:(NSString *)normalText setColorVipText: (NSString *)colorText {
    NSString *strText = [NSString stringWithFormat:normalText,colorText];
    //	字符串合并
    NSMutableAttributedString *str = [[NSMutableAttributedString alloc] initWithString: strText];
    //	富文本设置字体大小和字体样式
    [str addAttribute:NSFontAttributeName value:[UIFont systemFontOfSize:12.0f weight:UIFontWeightRegular] range:NSMakeRange(0, strText.length)];
    //	富文本设置文字颜色
    [str addAttribute:NSForegroundColorAttributeName value:[UIColor colorWithString:@"#7A7A80"] range:NSMakeRange(0, strText.length)];
    if (colorText != nil) {
        NSRange colorRange = [[str string] rangeOfString:colorText];
        //	给颜色处理部分的文字加颜色处理
        [str addAttribute:NSForegroundColorAttributeName value:[UIColor colorWithString:@"#37EFFA"] range:colorRange];
    }
    return str;
}

```