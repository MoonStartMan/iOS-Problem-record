# OC里.和->的用法区别

## 例子

``` Objective-C

#import <Foundation/Foundation.h>

@interface Test: NSObject
{
	int temp;	//	成员变量
}
@end

@implementation Test

@end

int main()
{
	Test *t = [[Test alloc] init];
	t->temp = 100;
	NSLog(@"%d", t->temp);
	return 0;
}

```
这里

``` Objective-C

t->temp = 100;
NSLog(@"%d", t->temp);

```

这两行中的t->temp会提示错误,错误说明为instance varviable "temp" is protected。说明是可以访问的,但是因为受保护所以报错,那我们把权限改成public试试。

``` Objective-C

@public
int temp;

```

结果显示通过，没有错误，说明想法是对的。
接下来看看.点语法

``` Objective-C

#import <Foundation/Foundation.h>

@interface Test : NSObject
{
    int temp;    //成员变量
}
@end
@implementation Test
@end

int main()
{

    Test *t = [[Test alloc] init];
    t.temp = 100;
    NSLog(@"%d",t.temp);
    return 0;
}

```

把代码中的t->temp改成t.temp,发现又会报错,错误说明为Propetery temp not found,也即是说没有找到temp这个属性,当然找不到,因为我们没有定义这个属性。
这时再在成员变量的声明后加一行代码

``` Objective-C

@property int temp;

```

代码通过,没有错误,说明.语法是用来访问属性的。再进一步猜想@property是声明set、get方法，要是我有set、get方法没有声明@property可不可以呢，试试就知道

``` Objective-C

 #import <Foundation/Foundation.h>

@interface Test : NSObject
{
    int temp;    //成员变量
}
-（void)setTemp:(int)temp;
-(int)Temp;
@end
@implementation Test

-（void)setTemp:(int)temp
{
}
-(int)Temp
{
}
@end

int main()
{

    Test *t = [[Test alloc] init];
    t.temp = 100;
    NSLog(@"%d",t.temp);
    return 0;
}

```

偷懒没有实现方法,但是同样没有报错，也就说明证实了猜想。

## .(点)和->(箭头)的区别

.(点语法)是访问类的属性,本质是调用set、get方法。
->(箭头)是访问成员变量，但成员变量默认受保护，所以常常报错，手动设为public即可解决。