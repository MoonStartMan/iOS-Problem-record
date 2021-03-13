# iOS-单例模式

## 定义

一个单例类，在整个程序中只有一个实例，并且提供一个类方法供全局调用，在编译时初始化这个类，然后一直保存在内存中，到程序(APP)退出时由系统自动释放这部分内部。

## 系统提供的单例类

+ UIApplication(应用程序实例类)
+ NSNotificationCenter(消息中心类)
+ NSFileManager(文件管理类)
+ NSUserDefaults(应用程序设置)
+ NSURLCache(请求缓存类)
+ NSHTTPCookieStorage(应用程序cookies池)

## 单例模式的基本实现

``` Objective-C

@interface Tool: NSObject 
    
+(instancetype)sharedInstance;
@end

@implementation Tool

+(instancetype)sharedInstance {

    static Tool *instance = nil;

    static dispatch_once_t onceToken;

    dispatch_once(&onceToken, ^{
        _instance = [[[self class] alloc] init];
    })

    return instance;
}

@end

```

### 注意点：

1. 单例必须是唯一的,所以它才被称为单例。在一个应用程序的生命周期里,有且只有一个实例存在。单例的存在给我们提供了一个唯一的全局状态。比如NSNotificaton,Application,NSuserDefault都是单例。
2. 为了保持一个单例的唯一性，单例的构造器必须是私有的。这防止其他对象也能创建出单例类的实例。
3. 为了确保单例在应用程序的整个生命周期是唯一的，它就必须是线程安全的。简单来说，如果你写单例的方式是错误的，就有可能会有两个线程尝试在同一时间初始化同一个单例，这样就有潜在的风险得到两个不同额单例。这就意味着我们需要用到GCD的dispatch_once来确保初始化单例的代码在运行时只执行一次。