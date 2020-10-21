# iOS跳转到指定页面

## 第一步：引入指定的页面控制器ViewController

``` objective-c
#import "MIXIAPProductViewController";
```

## 通过pushViewController跳转到指定页面

``` objective-c
MIXIAPProductViewController *iap = [[MIXIAPProductViewController alloc] init];
[self.navigationController pushViewController:iap animated:YES];
```