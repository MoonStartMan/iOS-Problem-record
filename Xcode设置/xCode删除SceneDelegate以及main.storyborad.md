# xCode删除SceneDelegate以及main.storyborad

## 删除SceneDelegate

1. 直接删除SceneDelegate.h和删除SceneDelegate.m
2. 找到info.list文件中删除Application Scene Manifest
3. 删除SceneDelegate在AppDelegate中的代理

删除以下代码↓

``` Objective-C

#pragma mark - UISceneSession lifecycle
- (UISceneConfiguration *)application:(UIApplication *)application configurationForConnectingSceneSession:(UISceneSession *)connectingSceneSession options:(UISceneConnectionOptions *)options {
    // Called when a new scene session is being created.
    // Use this method to select a configuration to create the new scene with.
    return [[UISceneConfiguration alloc] initWithName:@"Default Configuration" sessionRole:connectingSceneSession.role];
}


- (void)application:(UIApplication *)application didDiscardSceneSessions:(NSSet<UISceneSession *> *)sceneSessions {
    // Called when the user discards a scene session.
    // If any sessions were discarded while the application was not running, this will be called shortly after application:didFinishLaunchingWithOptions.
    // Use this method to release any resources that were specific to the discarded scenes, as they will not return.
}

```

4. 在AppDelegate.h添加window

``` Objective-C
@property(strong, nonatomic) UIWindow *window;
```

## 删除main.storyboard

1. 删除工程包里 Main interface 选项的 Main
2. 找到Appdelegate.m文件中的didFinishLaunchingWithOptions方法加入以下代码

```Objective-C

- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
    self.window = [[UIWindow alloc] initWithFrame:[UIScreen mainScreen].bounds];
    self.window.rootViewController = [[ViewController alloc] init];
    [self.window makeKeyAndVisible];
    [self.window setBackgroundColor: [UIColor whiteColor]];
    return YES;
}

```

3. 找到info.plist里的Application Scene Manifest条目进行删除
