# UITextFiled

创建一个textFiled

``` Objective-C

@interface ViewController()
{
	UITextField* textField;
}

textField = [[UITextField] alloc] initWithFrame: CGRectMake(20, 100, 200, 50)];

```

## 设置初始文字

``` Objective-C

textField.text = @"我是一个输入框";

```

## 设置颜色

``` Objective-C

textField.textColor = [UIColor redColor];

```

## 设置字体

``` Objective-C

textField.font = [UIFont boldSytemFontOfSize: 17];

```

## 设置文字的对齐方式

``` Objective-C

textField.textAlignment = NSTextAlignmentCenter;

```

## 设置输入框的风格

``` Objective-C

textField.borderStyle = UITextBorderStyleLine;

```

## 设置输入框的提示文字

``` Objective-C

textField.placeholder = @"请输入内容：";

```

## 是否开始编辑时清空内容

``` Objective-C

textField.clearsOnBeginEditing = YES;

```

## 设置字体大小是否自适应

``` Objective-C

textField.adjustsFontSizeToFitWidth = YES;
textField.minimumFontSize = 3;	//	自适应最小字体

```

## 设置清除按钮的显示模式

``` Objective-C

textField.clearButtonMode = UITextFieldViewModeWhileEditing;

```

## 设置左视图的显示模式

``` Objective-C

UIView *view = [[UIView alloc] initWithFrame:CGRectMake(0, 0, 30, 30)];
view.backgroundColor = [UIColor greenColor];
textField.leftView = view;
//	设置左视图的显示模式
textField.leftViewMode = UITextFieldViewModeAlways;
//	设置右视图
UIView *view2 = [[UIView alloc] initWithFrame: CGRectMake(0, 0, 30 30)];
view2.backgroundColor = [UIColor greenColor];
textField.rightView = view2;
textField.rightViewMode = UITextFieldViewModeUnlessEditing;

```