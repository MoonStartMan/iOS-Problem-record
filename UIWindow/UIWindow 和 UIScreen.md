# UIWindow 和 UIScreen

通常UIWindow与UIScreen是配合使用的。当我们想自定义window对象或者获取硬件屏幕大小必定会用到UIWindow 和 UIScreen。

## UIWindow

一个APP只有一个UIWindow对象，表示当前窗口对象。UIWindow继承于UIView。通常使用Window自定义根节点的UIViewController。通常在AppDelegate的声明周期didFinishLaunchingWithOptions中声明

``` Objective-C

UIScreen* screen = [UIScreen mainScreen];
NSLog(@"屏幕大小是 %f %f", screen.bounds.size.width, screen.bounds.size.height);
UIWindow* window = [[UIWindow alloc] init];
// 设置窗口大小
window.frame = screen.bounds;
// 设置window根视图控制器
window.rootViewController = [[UIViewController alloc] init];
// 显示到屏幕
[window makeKeyAndVisible];

```

## UIScreen

表示硬件屏幕的类

``` Objective-C

UIScreen* screen = [UIScreen mainScreen];
NSLog(@"屏幕大小是 %f %f", screen.bounds.size.width, screen.bounds.size.height);

```

### 属性

| 名称 | 类型 | 说明 |
|---|---|---|
| bounds | CGSize | 屏幕大小的参数 |
| scale | CGFloat | 屏幕缩放参数 |
| avaliableModes | NSArray<UIScreenMode *> | 屏幕支持的模式列表 |
| currentMode | UIScreenMode | 屏幕当前的模式|
| captured | BOOL | 屏幕是否在投影，录制 |