# UINavigationController的使用

## 在根控制器中设置UINavigationController

``` Objective-C

self.window = [[UIWindow alloc] initWithFrame:[[UIScreen mainScreen] bounds]];
//	Override point for customization after application launch.

UIViewController *VC = [[UIViewController alloc] init];
VC.title = @"主页";

UINavigationController *nav = [[UINavigationController alloc] initWithRootViewController: VC];
self.window.rootViewController = nav;

VC = nil;
nav = nil;

```

## 从根控制器的ViewController跳转到另一个ViewController

``` Objective-C

UIViewController *VC = [[UIViewController alloc] init];
[self.navigationController pushViewController:VC animated:YES];

```