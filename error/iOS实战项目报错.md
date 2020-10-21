# iOS实战项目报错

## 初始化window窗口报错

``` objective-c
self.window = [[UIWindow alloc]initWithFrame:[UIScreen mainScreen].bounds];
```

```
SceneDelegate：[AppDelegate setWindow:]: unrecognized selector sent to instance 0x60000002b440
```

### 解决方法

在AppDelegate.h里加声明window

``` objective-c
@property(nonatomic, strong) UIWindow * window;
```