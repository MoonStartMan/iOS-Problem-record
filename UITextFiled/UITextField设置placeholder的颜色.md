# UITextField设置placeholder的颜色

## 方法一：通过attributedPlaceholder属性修改占位文字颜色

``` Objective-C

//	初始化UITextField
self.loginTextField = [[UITextField alloc] initWithFrame:CGRectMake(0, 0, 0, 0)];
//	绘制placeholder字体
NSMutableAttributedString *placeholderText = [[NSMutableAttributedString alloc] initWithString:@"请输入手机号" attributes:@{NSFontAttributeName: [UIFont fontWithName:@"PingFang SC" size: 14], NSForegroundColorAttributeName: [UIColor colorWithRed:85/255.0 green:85/255.0 blue:85/255.0 alpha:1.0]}];
//	设置placeholder字体
self.loginTextField.attributedPlaceholder = placeholderText;

```

## 方法二：通过KVC修改占位文字颜色

``` Objective-C

UITextField *textField = [[UITextField alloc] init];
textField.frame = CGRectMake(textFieldX, CGRectGetMaxY(textField.frame) + padding, viewWidth - 2 * textFieldX, textFieldH);
textField.borderStyle = UITextBorderStyleRoundedRect;
textField.placeholder = @"请输入占位文字";
textField.font = [UIFont systemFontOfSize:14];
// "通过KVC修改占位文字的颜色"
[textField setValue:[UIColor greenColor] forKeyPath:@"_placeholderLabel.textColor"];
[self.view addSubview:textField1];

```

## 方法三：通过重写UITextField的drawPlaceholderInRect:方法修改占位文字颜色

``` Objective-C

// 重写此方法
-(void)drawPlaceholderInRect:(CGRect)rect {
// 计算占位文字的 Size
CGSize placeholderSize = [self.placeholder sizeWithAttributes:@{NSFontAttributeName : self.font}];
[self.placeholder drawInRect:CGRectMake(0, (rect.size.height - placeholderSize.height)/2, rect.size.width, rect.size.height) withAttributes:
    @{NSForegroundColorAttributeName : [UIColor blueColor],
                 NSFontAttributeName : self.font}];
}

```