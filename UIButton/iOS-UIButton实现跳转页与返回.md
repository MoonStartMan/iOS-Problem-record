# iOS-UIButton实现跳转页与返回页

## iOS-UIButton实现跳转

+ 引入需要跳转的页面

``` objective-c
#import "LogViewController.h"
```

+ 为按钮添加点击事件

``` objective-c
[self.homView.goLogin addTarget:self action:@selector(clickRegistGoToLogin:) forControlEvents:UIControlEventTouchUpInside];
```

+ 实例化点击事件的方法

``` objective-c
-(void)clickRegistGoToLogin:(NSInteger)tag
{
    LogViewController *logVC = [[LogViewController alloc] init];
    [self.navigationController pushViewController:logVC animated:YES];
}
```

+ 去掉导航的顶部条状物

``` objective-c
self.navigationController.navigationBar.hidden = YES;
```

## iOS-UIButton实现返回页面

+ 为按钮添加点击事件

``` objective-c
[self.logV.goRegist addTarget:self action:@selector(clickGoRegister:) forControlEvents:UIControlEventTouchUpInside];
```

+ 实例化点击事件方法

``` objective-c
-(void)clickGoRegister:(NSInteger)tag
{
    [self.navigationController popViewControllerAnimated:YES];
}
```