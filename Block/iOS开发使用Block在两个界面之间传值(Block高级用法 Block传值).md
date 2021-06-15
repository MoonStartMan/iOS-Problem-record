# iOS开发使用Block在两个界面之间传值(Block高级用法: Block传值)

## 使用场景

1. A控制器push到B控制器，B控制器pop时需要通知或者传值给A控制器
2. A控制器使用B,C等自定义视图,B/C中的交互事件需要通知或者传值给A控制器

### A控制器点击跳转(push)到B控制器(正向传值)

#### FirstViewController

##### FirstViewController.h

``` Objective-C

@property(nonatomic, strong) UITextField *inputTextField;

```

##### FirstViewController.m

``` Objective-C

- (void)sender:(UIButton *)sender {
	SecondViewController *SVC = [[SecondViewController alloc] init];
	SVC.textField.text = self.inputTextField.text;
	SVC.returnTextBlock = ^(NSString * _Nonnull showText) {
        self.inputTextField.text = showText;
    };
    [self.navigationController pushViewController:SVC animated:YES];
}

```

### B控制器(pop)回到A控制器

#### secondViewController

##### SecondViewControll.h

``` Objective-C

//  给Block重新定义一个名字
typedef void(^ReturnTextBlock)(NSString *text);

@property (nonatomic, strong) UITextField *textField;
@property (nonatomic, strong) UIButton *returnBtn;

@property (nonatomic, copy) ReturnTextBlock returnTextBlock;

```

##### SecondViewController.m

``` Objective-C

[self.returnBtn addTarget:self action:@selector(tap) forControlEvents:UIControlEventTouchUpInside];

- (void)tap {
    if (self.returnTextBlock) {
        self.returnTextBlock(self.textField.text);
    }
    [self.navigationController popViewControllerAnimated:YES];
}

```