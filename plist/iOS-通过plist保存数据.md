# iOS-通过plist保存数据

## 将数据写入plist文件中

``` objective-c
NSArray *shops = @[
        @{
            @"image":@"commodity1",
            @"name":@"鞋子"
        },
        @{
            @"image":@"commodity2",
            @"name":@"遮光镜"
        },
        @{
            @"image":@"commodity3",
            @"name":@"玉坠"
        },
        @{
            @"image":@"commodity4",
            @"name":@"菜板"
        },
        @{
            @"image":@"commodity5",
            @"name":@"指甲刀"
        },
        @{
            @"image":@"commodity6",
            @"name":@"装饰品"
        },
    ];
    
BOOL flag = [shops writeToFile: @"/Users/wangxiao/Desktop/shops.plist" atomically: YES];

if(flag) {
	NSLog(@"注入成功");
}
```

## 从plist文件中读取数据

``` objective-c
[NSArray arrayWithContentOfFile: @"/Users/wangxiao/Desktop/shop.plist"];
NSlog(@"%@", shops);
```

## plist使用注意点

+ plist的文件名不能叫做"info"、"Info"之类的
+ 添加plist等文件资源的时候，一定要勾选下面的选项  *Add to targets*