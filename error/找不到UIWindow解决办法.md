# 找不到UIWindow解决办法

用Xcode12新建一个工程支持最小iOS版本小于13的话，XCode控制台会爆出[Application] The app delegate must implement the window property if it wants to use的提示。

## 解决办法

1. 在AppDelegate.h添加window属性

``` Objective-C

@property (nonatomic, strong) UIWindow *window;

```

2. 在AppDelegate.m中添加代码

``` Objective-C

@synthesize window = _window;

```