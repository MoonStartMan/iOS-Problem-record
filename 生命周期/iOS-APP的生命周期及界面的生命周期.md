# iOS-APP的生命周期及界面的生命周期

## 应用的生命周期

应用的生命周期方法一般写在AppDelegate中

### 各个程序运行状态时代理的回调:

``` Objective-C

- (BOOL)application:(UIApplication *)application willFinishLaunchingWithOptions:(NSDictionary)launchOptions

```

### 进程即将启动的时候代理会执行该方法

``` Objective-C

- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions

```

### 进程启动完成程序准备开始运行的时候执行该方法

``` Objective-C

- (void)applicationDidFinishLaunching:(UIApplication *)

```

### 当程序载入后执行

``` Objective-C

- (void)applicationDidBecomeActive:(UIApplication *)application 

```

### 当应用程序入活动状态执行

``` Objective-C

- (void)applicationWillResignActive:(UIApplication *)application

```

### 当应用程序将要入非活动状态执行，在此期间，应用程序不接收消息或事件，比如来电话了

``` Objective-C

- (void)applicationDidEnterBackground:(UIApplication *)application

```

### 当程序被推送到后台的时候调用。所以要设置后台继续运行，则在这个函数里面设置即可。

``` Objective-C

- (void)applicationWillEnterForeground:(UIApplication *)application

```

### 当程序从后台将要重新回到前台的时候调用

``` Objective-C

- (void)applicationWillTerminate:(UIApplication *)application

```

### 当程序将要退出是被调用，通常是用来保存数据和一些退出前的清理工作。这个需要要设置UIApplicationExitsOnSuspend的键值。

## 界面之间的生命周期

### -(void) viewDidLoad;

第一次打开该界面的时候会调用,在这里一般用来做各种数据的初始化。(注意返回到该页面不会执行该方法,除非关闭该页面,重新打开才会执行该方法)

### -(void) viewWillAppear:(BOOL)animated;

在上面的didload方法执行完毕之后,页面即将将要显示的时候会执行该方法,该方法也可以对数据来进行初始化。(即使是返回到该页面,也会执行该方法)

### -(void) viewDidAppear:(BOOL)animated;

等页面加载完之后就执行的方法。

### -(void) viewWillDisappear: (BOOL)animated;

页面将要消失执行的方法

### -(void) viewDidDisappear: (BOOL)animated;

界面已经消失的时候执行的方法