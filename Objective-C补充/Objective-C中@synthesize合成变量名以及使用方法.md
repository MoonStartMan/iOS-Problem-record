# Objective-C中@synthesize合成变量名以及使用方法

## 代码示例

1. Person.h

``` Objective-C

#import <Foundation/Foundation.h>
 
@interface Person:NSObject
@property (nonatomic, copy) NSString* name;
-(id) initWithName:(NSString*) name;
-(void) info;
@end

```

2. Person.m

``` Objective-C

#import "Person.h"
 
@implementation Person
@synthesize name = _sname; //设置系统合成的属性名为_sname，这个可以是任意合法变量名
-(id) initWithName:(NSString *)name
{
    if(self = [super init])
    {
        self.name = name; //这其实是通过setName方法设置的
        //self->_sname = name; //这是直接设置变量
    }
    return self;
}
-(void) info
{
    NSLog(@"此人名为：%@",self.name);
}
-(void) setName:(NSString *)name
{
    NSLog(@"test");
    self->_sname = name;
}
-(NSString*) description
{
    return [NSString stringWithFormat:@"<Person[_sname=%@]>",self->_sname];
}
@end

```

3. main.m

``` Objective-C

#import "Person.h"
 
int main(int argc, char* argv[])
{
    @autoreleasepool {
        Person* p = [[Person alloc] initWithName:@"a"];
        NSLog(@"%@",[p description]);
    }
}

```

## 使用@synthesize的情形

### 情形1: 不使用@synthesize,可以使用自动生成的带下划线的实例变量名
### 情形2: 使用@synthesize为属性添加带下划线的别名,与不使用@synthesize相同

@synthesize 声明的属性=变量。意思是，将属性的setter,getter方法，作用于这个变量
@synthesize还有一个作用，就是可以指定与属性对应的实例变量，例如我可以这样写@synthesize age = myAge;，那这样子的话我们去调用的时候self.age其实是操作的实例变量myAge,而不是_age了。

### 情形3: 使用@synthesize为属性添加任意别名,此时使用自动生成的实例变量名将报错,只能使用特别的别名。

## 使用@synthesize的注意

1. 属性的setter方法和getter方法是不能同时进行重写的，这是因为，一旦你同时重写了这两个方法，那么系统就不会帮你生成这个成员变量了，所以会报错，如果真的就想非要重写这个属性的setter和getter方法的话，就要手动生成成员变量，然后可以重写了。或是用

``` Objective-C

@synthesize age = myAge;

- (void)setAge:(NSString *)age {
	myAge = age;
}

- (NSString *)age {
	return myAge;
}

```

2. 在getter方法中最后返回return_age;而不是return self.age，这是因为点语法实际上是对setter和getter方法的调用，如果在getter方法中调用return self.age的话，就会循环调用。

3. 在重写属性的setter方法的时候我们一般都是这样写:

``` Objective-C

- (void)setInfoArr: (NSArray *)infoArr {
	_infoArr = infoArr;
	_infoArr = @[@"我是数组"];
}

```

我们需要在setter方法中加上这句_infoArr = infoArr;，我们在重写setter方法的时候将新值infoArr赋值给属性变量_infoArr 以便我们在外面调用。

4. 当.h文件中属性为readonly，.m文件中可以不用@synthesize这个关键字，初始化的方式有下面几种
例如

``` Objective-C

@property(nonatomic, strong, readonly) UILabel *placeHolderLabel;

```

``` Objective-C

- (void)setUpPlaceHoladerLabel {
	_placeHolderLabel = [[UILabel alloc] init];
	_placeHolderLabel.textColor = [self.class defaultPlaceholderColor];
	_placeHolderLabel.numberOfLines = 0;
	_placeHolderLabel.userInteractionEnabled = NO;
	_placeHolderLabel.font = self.font;
}

```

``` Objective-C

- (UILabel *)placeHolderLabel {
	UILabel *label = objc_getAssociatedObject(self, @selector(placeHolderLabel));
	if(!label) {
		label = [[UILabel alloc] init];
		label.textColor = [self.class defaultPlaceholderColor];
		label.numberOfLines = 0;
		label.userInteractionEnabled = NO;
		label.font = self.font;
		objc_setAssociatedObject(self, @selector(placeHolderLabel), label, OBJC_ASSOCIATION_RETAIN_NONATOMIC);
		[self updatePlaceholderLabel];
	}
	return label;
}

```

``` Objective-C

@property(nonatomic, strong, readwrite) UILabel *placeHolderLabel;

```

## 使用@synthesize总结

1. @synthesize 的作用:是为属性添加一个实例变量名，或者说别名。同时会为该属性生成 setter/getter 方法。
2. 禁止@synthesize:如果某属性已经在某处实现了自己的 setter/getter ,可以使用 @dynamic 来阻止 @synthesize 自动生成新的 setter/getter 覆盖。
3. 内存管理：@synthesize 和 ARC 无关。
4. 使用：一般情况下无需对属性添加 @synthesize ，但一些特殊情形仍然需要，例如protocol中声明的属性
