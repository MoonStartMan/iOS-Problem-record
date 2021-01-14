# iOS断言

## 断言推荐使用的场景

1. 用错误处理代码来处理预期会发生的情况,用断言来处理绝不该发生的状况。
2. 避免把需要执行的代码放到断言中,因为断言在Debug模式下是生效的,但是在Release模式无效，这样就会丢失执行代码。
3. 用断言来注释并验证前条件和后条件。
4. 对于高建壮的代码，应该先使用断言，再处理错误。

## Xcode上断言生效的设置

1. Debug默认生效，Release模式下默认失效。

## 断言常用宏：

1. NSAssert(condition, description, ...__vars__...):断言条件不成立时,打印信息并抛出异常[异常无人处理时将退出程序]。只适用于OC函数内部断言。
	
	+ decription是输出表达式,__vars__是表达式中用到的变量参数。
	+ 有多参数版本,其实就是根据有多少个__vars__然后取不同名字的Assert版本,比如NSAssert1,NSAssert2,NSAssert3,NSAssert4和NSAssert5.[但其实直接用原版本即可]

2. NSCAssert(condition, description, ...__vars__...):C断言宏,使用于C函数和OC函数内部只能使用此断言。[在C函数中只能使用NSAssert]

	+ 它与NSAssert的代码区别在于，取函数名时，NSAssert用的是__cmd,而NSCAssert用的是__PRETTY_FUNCTION__。然后NSAssertionHandler调用的抛出函数也不同。
	+ 也有多参数版本。

3. NSParameterAssert( condition )

	+ 定义: #define NSParameterAssert(condition) NSAssert((condition), @"Invalid parameter not satisfying: %@", @#condition)
	+ 作用: 失败时自动输出条件判断语句，相当于NSAssert的一层格式化封装。

4. NSCParameterAssert(condition)

	+ 定义：#define NSCParameterAssert(condition) NSCAssert((condition), @"Invalid parameter not satisfying: %@", @#condition)
	+ 作用: 失败时自动输出条件判断语句，相当于NSCAssert的一层格式化封装。

## AssertHandler断言处理回调：

+ 默认的断言处理回调：当断言不成立时，会向 NSAssertionHandler实例发送一个表示错误的字符串。每个线程都有它自己的NSAssertionHandler实例。【断点无法停留在准确的代码行】
	
	+ NSAeert调用：[[NSAssertionHandler currentHandler] handleFailureInMethod:_cmd object:self file:__assert_file__  lineNumber:__LINE__ description:(desc), ##__VA_ARGS__];告知断言失败。
	
	+ NSCAeert调用：[[NSAssertionHandler currentHandler] handleFailureInFunction:__assert_fn__ object:self file:__assert_file__  lineNumber:__LINE__ description:(desc), ##__VA_ARGS__];告知断言失败。

+ 注册自定义的断言处理回调：

	+ 继承NSAssertionHandler实现自己的断言处理类。
	+ 在继承类中重载上面提到的两个方法。
	+ 在需要使用自定义断言处理的线程上注册。

+ 自定义断言处理类实例:

``` Objective-C

@implementation CJFAssertionHandler

//处理Objective-C的断言
- (void)handleFailureInMethod:(SEL)selector object:(id)object file:(NSString *)fileName lineNumber:(NSInteger)line description:(NSString *)format,...
{
    NSLog(@"NSAssert Failure: Method %@ for object %@ in %@ ,line: %li", NSStringFromSelector(selector), object, fileName, (long)line);
    //建议加上abort(),方便及时发现问题，且调用栈可观察。
    abort();
}
//处理C的断言
- (void)handleFailureInFunction:(NSString *)functionName file:(NSString *)fileName lineNumber:(NSInteger)line description:(NSString *)format,...
{
    NSLog(@"NSCAssert Failure: Function (%@) in %@ ,line: %li", functionName, fileName, (long)line);
    //建议加上abort(),方便及时发现问题，且调用栈可观察。
    abort();
}

@end

```

+ 自定义断言处理类注册:

``` Objective-C

CJFAssertionHandler *myHandler = [[CJFAssertionHandler alloc] init];
//给当前的线程
[[[NSThread currentThread] threadDictionary] setValue:myHandler forKey:NSAssertionHandlerKey];


```