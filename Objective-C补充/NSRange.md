# NSRange

## NSRange的定义

``` Objective-C

typedef struct _NSRange
{
	NSUInteger location;
	NSNInteger length;
}NSRangge;

```

NSRange是一个结构体，其中locacation是一个以0开始的的index，length是表示对象的长度。他们都是NSUInteger类型。而NSUInteger类型的定义如下:

``` Objective-C

NSRange用来表示事物的一个范围，通常是字符串里的字符范围或者数组里面的元素范围。
NSRange有2个成员
NSUInteger location: 表示该范围的起始位置
NSUInteger length: 表示该范围内的长度
```

## NSRange的创建

``` Objective-C

1), NSRange range;
//	通过结构体变量访问成员
range.location = 3;
range.length = 2;

2), //结构体变量整体赋值
range = (NSRange){5, 3};
NSRange r2 = {4, 5};	//	最简单的

3),
NSRange r3 = {.location = 3, .length = 5};

4),	//	OC中新增的(OC中建议使用这种)
//	NSMakeRange函数的作用给NSRange结构体变量赋值
NSRange r4 = NSMakeRange(3, 3);
NSString *str = NSStringFromRange(r4);	//	将一个结构体转化成字符串
```

## 字符串的截取和替换

``` Objective-C

//1. 从指定位置from开始(包含起始位置)到尾部

	- (NSString *)substringFromIndex: (NSUInteger)from;

//2. 从字符串的开头一直截取到指定的位置to,不包含结束位置
	- (NSString *)substringToIndex: (NSInteger)to;

//3. 按照所给出的NSRange从字符串中截取子串
	- (NSString *)substringWithRange: (NSRange)range;

//4. 字符串截取练习(获取itcast标签中的内容)
	NSString *str = @"<hello>tangFeng</hello>"
//	@">/" loc+1
	NSUInteger loc = [str rangeOfString:@">"].location + 1;	//	"t"得位置
//	@"</" loc
	NSUInteger len = [str rangeOfString:@"</"].location - loc	//	要截取的字符的长度
//	构建 range
NSRange r2 = NSMakeRange(loc, len);
//	截取
NSString *subStr = [str substringWithRange: r2];

//	5.字符串替换
- (NSString *)stringByReplacingOccurrencesOfString: (NSString *)target withString: (NSString *)replacement;
//	用replacement替换target
```

## 字符串和其他数据类型转换

``` Objective-C
//	1. 和基本数据类型的转换
	- (double)doubleValue;
	- (float)floatValue;
	- (int)intValue;
	- (BOOL)boolValue;

//	2. C字符串转OC 字符串
		char *s = "zhangsanfeng";
		NSString *str = [NSString stringWithUTF8String:s];
		
//	3.OC字符串转C字符串
		NSString *str2 = @"zbz";
		const char *s1 = [str2 UTF8String];
		
//	4.去除字符串首尾的空格
		NSString *str = @"test at";
		NSCharacterSet *set = [NSCharacterSet whitespaceCharacterSet];
		NSString *newStr = [str stringByTrimmingCharactersInset: set];
```

## NSURL读写字符串

``` Objective-C
//	1,URL介绍
//	URL的全称是Uniform Resource Locator(统一资源定位符).
//	URL是互联网上标准资源的地址

//	2,URL格式
//	基本URL包含:协议、主机域名(服务器名称\IP地址)、路径
//	举例：http://www.baidu.com/12121.png
//	可以简单认为： URL == 协议头;	//	主机域名/路径

//	3，通过URL读写字符串
//	构建URL
NSURL *url = [NSURL URLWithString:@"file://Users/apple/Desktop/str.txt"];	//	需要手动加file://协议头
//	通过文件路径创建(默认就是file协议的)
NSURL *url = [NSURL fileURLWithPath: @"/Users/apple/Desktop/str.txt"];	//	自动会将file://协议头加上

NSString *str = @"$10000000";
//	1) ,写入字符串
	[str writeToURL: url atomically: YES encoding: NSUTF8StringEncoding error: nil];
//	2), 读取字符串
	NSString *str2 = [NSString stringWithContentsOfURL:url encoding: NSUTF8StringEncoding error: nil];
```

## NSMutableString的介绍和补充

``` Objective-C
//	1, NSMutableString类继承NSString类
//	2, NSMutableString和NSString的区别:
//	NSString是不可变的，里面的文字内容是不能进行修改的;
//	NSMutableString是可变的,里面的文字内容可以随时更改
//	NSMutableString能使用NSString的所有方法.(继承);

//	3,可变和不可变的概念
//	不可变:	指的是字符串在内存中占用的存储空间固定,并且存储的内容不能发生变化;
//	可变:	指的字符串在内存中占用的存储空间可以不固定,并且存储的内容可以被修改;
//	4,使用:
		NSMutableString *str2 = [NSMutableString stringWithFormat:@"Jack"];
		//	1), 添加:
		[str2 appendString:@"&Rose"];
		[str appendFormat: @"http://www.baidu.com/%d", 100];	//	格式化的添加字符串
		//	2), 在指定的位置插入一个字符串:
		[str insertString: @"p://" atIndex: 3];
		//	3),	删除一部分字符串:
		[str deleteCharactersInRange: NSMakeRange(3, 4)];
		//	4),	替换字符串的一部分内容
		[str replaceCharactersInRange: NSMakeRange(11, 5) withString:@"itnnnn"];
		//	使用注意:
		//	1),不能将不可变的字符串赋值给可变的字符串;
			NSMutableString *str = [NSString stringWithFormat: @"abc"];
		//	2), NSMutaleString的string属性:会将源对象的所有字符串都覆盖掉。.string属性可以修改字符串的内容
		//	3),	开发中到底使用NSString还是NSMutableString?开发中绝大多数用到的都是NSString只是如果需要做特殊处理的时候(截取、拼接、替换)等操作，才考虑使用NSMutableString
```

## 改变字符串其中一段字体和颜色

``` Objective-C
NSMutableAttributedString *textColor = [[NSMutableAttributedString alloc]initWithString:_bookPrice.text];
    NSRange rangel = [[textColor string] rangeOfString:[_bookPrice.text substringFromIndex:6]];
    [textColor addAttribute:NSForegroundColorAttributeName value:[UIColor redColor] range:rangel];
    [textColor addAttribute:NSFontAttributeName value:[UIFont systemFontOfSize:17] range:rangel];
		[_lable setAttributedText:textColor];
```

## 判断字符串的各种操作

``` Objective-C
//抽取指定范围的字符串
    NSString *string1 = @"0123456789";
    NSRange range1 = NSMakeRange(0, 4);//NSMakeRange这个函数的作用是从第0位开始计算，长度为4
    NSLog(@"从第0个字符开始，长度为4的字符串是：%@",[string1 substringWithRange:range1]);
    NSLog(@"抽取从头开始到第4个字符：%@",[string1 substringToIndex:4]);
    NSLog(@"抽取从第6个字符开始到末尾：%@",[string1 substringFromIndex:6]);
    
    NSString *string2 = @"wo shi xiao bai zhu";
    NSRange range2 = [string2 rangeOfString:@"bai"];
    if (range2.length > 0) {
        NSLog(@"{字符串中“bai”的位置,长度}==%@",NSStringFromRange(range2));
    }
    //判断在一串字符串中是否找到某个字符串
    NSRange range3 = [string2 rangeOfString:@"zhu"];
    if (range3.location != NSNotFound) {
        NSLog(@"找到了@“zhu”这个字符串！");
    }
    else
        NSLog(@"没找到！");
```