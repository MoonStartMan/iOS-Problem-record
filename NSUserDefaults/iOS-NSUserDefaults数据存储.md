# iOS-NSUserDefaults数据存储

NSUserDefaults适合存储轻量级的本地数据,比如保存一个登陆界面的数据，用户名，密码之类的，个人觉得使用NSUserDefaults是首选。下次再登陆的时候就可以直接从NSUserDefaults里面读取上次登陆的信息。

## 支持的数据格式有

NSUserDefaults支持的数据格式有: NSNumber(Integer、Float、Double),NSString,NSDate,NSArray,NSDictionary,BOOL类型。

## NSUserDefaults常用的方法

NSUserDefaults常用的方法,使用NSMutableDictionary的一些方法类似。

### 设置

``` Objective-C

- (void)setInteger:(NSInteger)value forKey:(NSString *)defaultName;

- (void)setFloat:(float)value forKey:(NSString *)defaultName;

- (void)setDouble:(double)value forKey:(NSString *)defaultName;

- (void)setBool:(BOOL)value forKey:(NSString *)defaultName;

- (void)setURL:(nullable NSURL *)url forKey:(NSString *)defaultName NS_AVAILABLE(10_6, 4_0);

- (void)setObject:(nullable id)value forKey:(NSString *)defaultName;

```

### 获取

``` Objective-C

- (void)setInteger:(NSInteger)value forKey:(NSString *)defaultName;

- (void)setFloat:(float)value forKey:(NSString *)defaultName;

- (void)setDouble:(double)value forKey:(NSString *)defaultName;

- (void)setBool:(BOOL)value forKey:(NSString *)defaultName;

- (void)setURL:(nullable NSURL *)url forKey:(NSString *)defaultName NS_AVAILABLE(10_6, 4_0);

- (void)setObject:(nullable id)value forKey:(NSString *)defaultName;

```

### 同步存储到磁盘中

``` Objective-C

[userDefaults synchronize];

```

**调用set的方法后，如果需要马上同步synchronize方法。注意这个方法不要太频繁调用。如果不调用synchronize，系统会每个一个时间段自动保存。**

### 保存数据到NSUserDefaults

``` Objective-C

-(void)saveNSUserDefaults
{
  NSString *myString = @"enuola";
  int myInteger = 100;
  float myFloat = 50.0f;
  double myDouble = 20.0;
  NSDate *myDate = [NSDate date];
  NSArray *myArray = [NSArray arrayWithObjects:@"hello", @"world", nil];
  NSDictionary *myDictionary = [NSDictionary dictionaryWithObjects:[NSArray arrayWithObjects:@"enuo", @"20", nil] forKeys:[NSArray arrayWithObjects:@"name", @"age", nil]];
  //将上述数据全部存储到NSUserDefaults中
  NSUserDefaults *userDefaults = [NSUserDefaults standardUserDefaults];
  //存储时，除NSNumber类型使用对应的类型意外，其他的都是使用setObject:forKey:
  [userDefaults setInteger:myInteger forKey:@"myInteger"];
  [userDefaults setFloat:myFloat forKey:@"myFloat"];
  [userDefaults setDouble:myDouble forKey:@"myDouble"];
  [userDefaults setObject:myString forKey:@"myString"];
  [userDefaults setObject:myDate forKey:@"myDate"];
  [userDefaults setObject:myArray forKey:@"myArray"];
  [userDefaults setObject:myDictionary forKey:@"myDictionary"];
  //这里建议同步存储到磁盘中，但是不是必须的
  [userDefaults synchronize];
}
```

### 从NSUserDefaults中读取数据

``` Objective-C

-(void)readNSUserDefaults

{

NSUserDefaults *userDefaultes = [NSUserDefaults standardUserDefaults];

//读取整型int类型的数据

NSInteger myInteger = [userDefaultes integerForKey:@"myInteger"];

//读取浮点型float类型的数据

float myFloat = [userDefaultes floatForKey:@"myFloat"];

//读取double类型的数据

double myDouble = [userDefaultes doubleForKey:@"myDouble"];

//读取NSString类型的数据

NSString *myString = [userDefaultes stringForKey:@"myString"];

//读取NSDate日期类型的数据

NSDate *myDate = [userDefaultes valueForKey:@"myDate"];

NSDateFormatter *df = [[NSDateFormatter alloc] init];

[df setDateFormat:@"yyyy-MM-dd HH:mm:ss"];

txtNSDate.text = [NSString stringWithFormat:@"%@",[df stringFromDate:myDate]];

//读取数组NSArray类型的数据

NSArray *myArray = [userDefaultes arrayForKey:@"myArray"];

NSString *myArrayString = [[NSString alloc] init];

for(NSString *str in myArray)

{

NSLog(@"str= %@",str);

myArrayString = [NSString stringWithFormat:@"%@  %@", myArrayString, str];

[myArrayString stringByAppendingString:str];

//        [myArrayString stringByAppendingFormat:@"%@",str];

NSLog(@"myArrayString=%@",myArrayString);

}

//读取字典类型NSDictionary类型的数据

NSDictionary *myDictionary = [userDefaultes dictionaryForKey:@"myDictionary"];

NSString *myDicString = [NSString stringWithFormat:@"name:%@, age:%d",[myDictionary valueForKey:@"name"], [[myDictionary valueForKey:@"age"] integerValue]];

}

```