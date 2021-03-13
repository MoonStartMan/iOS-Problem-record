# NSNotificationCenter

NSNotificationCenter通知中心是iOS程序内部的一种消息广播的实现机制，可以在不同对象之间发送通知进而实现通信，通知中心采用的是一对多的方式，一个对象发送的通知可以被多个对象接收。

## NSNotificationCenter属性和方法

### 核心属性

``` Objective-C

//	通知的名称,有时可能会使用一个方法来处理多个通知,可以根据名称区分
@property(readonly, copy) NSNotificationName name;
//	通知的对象,常使用nil,如果设置了值注册的通知监听器的object需要与通知的object匹配,否则接收不到通知
@property(nullable, readonly, retain)id object;
//	字典类型的用户信息,用户可将需要传递的数据放入该字典中
@property(nullable, readonly, copy)NSDictionary *userInfo;

```

NSNotificationCenter通知中心，通知中心采用单例的模式，整个系统只有一个通知中心，通过如下代码获取:

``` Objective-C

[NSNotificationCenter defaultCenter];

```

### 核心方法

``` Objective-C

/*
注册通知监听器，只有这一个方法
observer为监听器
aSelector为接到收通知后的处理函数
aName为监听的通知的名称
object为接收通知的对象，需要与postNotification的object匹配，否则接收不到通知
*/
- (void)addObserver:(id)observer selector:(SEL)aSelector name:(nullable NSNotificationName)aName object:(nullable id)anObject;

/*
发送通知，需要手动构造一个NSNotification对象
*/
- (void)postNotification:(NSNotification *)notification;

/*
发送通知
aName为注册的通知名称
anObject为接受通知的对象，通知不传参时可使用该方法
*/
- (void)postNotificationName:(NSNotificationName)aName object:(nullable id)anObject;

/*
发送通知
aName为注册的通知名称
anObject为接受通知的对象
aUserInfo为字典类型的数据，可以传递相关数据
*/
- (void)postNotificationName:(NSNotificationName)aName object:(nullable id)anObject userInfo:(nullable NSDictionary *)aUserInfo;

/*
删除通知的监听器
*/
- (void)removeObserver:(id)observer;

/*
删除通知的监听器
aName监听的通知的名称
anObject监听的通知的发送对象
*/
- (void)removeObserver:(id)observer name:(nullable NSNotificationName)aName object:(nullable id)anObject;

/*
以block的方式注册通知监听器
*/
- (id <NSObject>)addObserverForName:(nullable NSNotificationName)name object:(nullable id)obj queue:(nullable NSOperationQueue *)queue usingBlock:(void (^)(NSNotification *note))block API_AVAILABLE(macos(10.6), ios(4.0), watchos(2.0), tvos(9.0));

```

## NSNotificationCenter例子

``` Objective-C

- (void)ViewDidLoad {
   //  注册通知----第一部
    [[NSNotificationCenter defaultCenter]addObserver:self selector:@selector(showLabelText:) name:@"labelTextNotification" object: nil];
}

//  实现通知监听----第二部
- (void)showLabelText:(NSNotification *)notification
{
    //  第三,实现通知中心内部的方法,并实现传值
    id text = notification.object;
    //  赋值到文本上面
    self.textString.text = text;
}

//  释放通知----第四部
- (void)dealloc {
    [[NSNotificationCenter defaultCenter] removeObserver:self name:@"labelTextNotification" object:nil];
}

```