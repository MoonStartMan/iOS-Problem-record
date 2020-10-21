# iOS13移除 StoryBoard

1. 删除Main.storyboard文件(SceneDelegate.h和SceneDelegate.m文件可删可不删)
2. 删除Info.plist文件Main storyboard file base name项和Application Scene Manifest项
3. 在AppDetegate.h添加以下代码

``` objective-c
//	AppDelegate.h
#import <UIKit/UIKit.h>
@interface AppDelegate : UIResponder <UIApplicationDelegate>
@property (strong, nonatomic) UIWindow *window;
@end
```

4. 在AppDelegate.m添加如下代码

``` objective-c
#import "AppDelegate.h"
#import "ViewController.h"

@interface AppDelegate ()
@end
@implementation AppDelegate
- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
    // Override point for customization after application launch.
    self.window = [[UIWindow alloc] initWithFrame:[[UIScreen mainScreen] bounds]];
    self.window.rootViewController = [[ViewController alloc] init];
    [self.window makeKeyAndVisible];
    return YES;
}
@end
```