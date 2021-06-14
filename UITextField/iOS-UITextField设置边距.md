# iOS-UITextField设置边距

声明UITextField

``` Objective-C

@property (nonatomic, strong) UITextField *inputTextField;

```

实现UITextField

``` Objective-C

self.inputTextField = [[UITextField alloc] init];
self.inputTextField.font = [UIFont systemFontOfSize:16.0f weight:UIFontWeightMedium];
    self.inputTextField.placeholder = @"请输入需要传入的内容";
    self.inputTextField.textColor = [UIColor blackColor];
    self.inputTextField.layer.masksToBounds = YES;
    self.inputTextField.layer.cornerRadius = 25;
    self.inputTextField.layer.borderWidth = 2;
    self.inputTextField.layer.borderColor = [UIColor blackColor].CGColor;
    [self.inputTextField setValue:[NSNumber numberWithInt:10] forKey:@"paddingLeft"];

```

设置边距关键代码

``` Objective-C

[self.inputTextField setValue:[NSNumber numberWithInt:10] forKey:@"paddingLeft"];

```

forKey:边距

``` Objective-C

forKey:@"paddingLeft"
forKey:@"paddingRight"
forKey:@"paddingTop"
forKey:@"paddingBottom"

```