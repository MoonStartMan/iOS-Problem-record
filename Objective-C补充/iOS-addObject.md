# iOS-addObject

添加对象

``` Objective-C

// 创建一个临时的可变数组

      NSMutableArray * array = [NSMutableArray array];

       // 将字典转换成模型

       for(NSDictionary * dict in dictArray)

       {

          HQQuestion * question = [[HQQuestion alloc] init];

          question.icon = dict[@"icon"];

          question.title = dict[@"title"];

          question.answer = dict[@"answer"];

          question.options = dict[@"options"];

           [array addObject:question]; // 将对象元素添加到数组中

       }
       // 赋值
       _questions = array;
```