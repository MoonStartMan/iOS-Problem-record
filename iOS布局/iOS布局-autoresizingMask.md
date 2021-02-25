# iOS布局-autoresizingMask

## AutoresizingMask理解

``` Objective-C

@property(nonatomic) UIViewAutoresizing autoresizingMask;

```

想要让自定义控件在旋转后，同样居中对齐，只需设置该自定义UIView与父视图的左边距和右边距的比例不变，上边距和下边距的比例不变。

### 实例代码

``` Objective-C

UIView *redView = [[UIView alloc] init];
redView.backgroundColor = [UIColor redColor];
CGFloat marginX = self.view.frame.size.width - 100;
CGFloat marginY = self.view.frame.size.height - 100;
redView.frame = CGRectMake(marginX, marginY, 100, 100);
[self.view addSubview:redView];
    
redView.autoresizingMask = UIViewAutoresizingFlexibleLeftMargin | UIViewAutoresizingFlexibleTopMargin | UIViewAutoresizingFlexibleWidth;

```

## UIViewAutoresizing枚举值

| 布局关系 | 视图随父视图等比例变化 |
| ---- | ---- |
| none | 默认值,不会随父视图改变而改变 |
| flexiableLefMargin | 子视图左边距，等比例变化 |
| flexiableWidth | 子视图宽度，等比例变化 |
| flexiableRightMargin | 子视图右边距，等比例变化 |
| flexiableTopMargin | 子视图上边距，等比例变化 |
| flexiableHeight | 子视图高度，等比例变化 |
| flexiableBottomMargin | 子视图底边距离，等比例变化 |

