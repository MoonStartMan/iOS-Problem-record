# NSIndexSet



NSIndexSet可以用来存储一系列的索引值区间，索引值可以使用单个的NSUInteger或者NSRange来表示。而且和许多其他集合类型一样，它有不可变和可变的执行，分别对应NSIndexSet类型和NSMutableIndexSet类型。NSIndexSet可以通过一个NSUinteger，NSRange或者另一个NSIndexSet来创建。也可以使用NSMutableIndexSet来多次添加NSUinteger或者NSRange对象。

## 例子

比如创建一个NSMutableIndexSet对象,加入数据,然后枚举所有的索引值

### 例子1

``` Objective-C
NSMutableIndexSet *idxSet = [[NSMutableIndexSet alloc] init];
//添加5和2
[idxSet addIndex:5];
[idxSet addIndex:2];
//添加7-10
[idxSet addIndexesInRange:NSMakeRange(7, 4)];
[idxSet enumerateIndexesUsingBlock:^(NSUInteger idx, BOOL *stop)
{
	NSLog(@"%lu", (unsigned long)idx);
}];

```

### 例子1输出

``` vim
2
5
7
8
9
10
```

### 例子2

+ NSIndexSet还支持其他方式的枚举方法,比如可以取一个NSRange范围中的交集,然后还可以以相反的顺序进行枚举。

+ 这个需求需要使用NSIndexSet的enumerateIndexesInRange:options:usingBlock:方法，如下代码：

``` Objective-C
NSMutableIndexSet *idxSet = [[NSMutableIndexSet alloc] init];

//	添加5和2
[idxSet addIndex: 5];
[idxSet addIndex: 2];
//	添加7-10
[idxSet addIndexesInRange: NSMakeRange(7, 4)];
//	idxSet包含的区间: 2, 5, 7 - 10
//	取交集: 3 - 8

[idxSet enumerateIndexesInRange: NSMakeRange(3, 6) options: NSEnumerationReverseusingBlock: ^(NSUInteger idx, BOOL *stop){
	NSLog(@"%lu", (unsigned long)idx);
}];
```

### 例子2输出

``` vim
8 7 5
```

由于NSIndexSet本身的区间是: 2, 5, 7-10。然后取交集的区间是3-8.最后倒序枚举,所以会输出8,7,5。

### 例子3
NSIndexSet同时还包含许多方法判断是否包含某区间或者从一个索引值内获取临近的区间内的索引。如下代码

``` Objective-C
NSMutableIndexSet *idxSet = [[NSMutableIndexSet alloc] init];
//	添加5和2
[idxSet addIndex: 5];
[idxSet addIndex: 2];
//	判断是否包含3 - 5
NSLog(@"%d", [idxSet containsIndexesInRange:NSMakeRange(3, 2)]);
//	从4起找到最近的等于或者大于的索引值
NSLog(@"%lu", (unsigned long)[idxSet indexGreaterThanOrEqualToIndex: 4]);
```

### 例子3输出

``` vim
0
5
```

### 例子4

还可以使用NSIndexSet的indexesInRange:options:passingTest:方法来根据要求返回另一个NSIndexSet。操作过程和上面讲的enumerateIndexesInRange:options:usingBlock:方法类似，只不过Block参数需要返回一个BOOL，通过这个BOOL来决定元素是否被加入到返回的NSIndexSet对象中。

``` Objective-C
NSMutableIndexSet *idxSet = [[NSMutableIndexSet alloc] init];
//添加5和2
[idxSet addIndex:5];
[idxSet addIndex:2];
//添加7-10
[idxSet addIndexesInRange:NSMakeRange(7, 4)];
//从NSRange的交集中倒着枚举
NSIndexSet *subSet = [idxSet indexesInRange:NSMakeRange(3, 6) options:NSEnumerationReverse passingTest
^BOOL(NSUInteger idx, BOOL *stop)
{
     NSLog(@"> %lu", (unsigned long)idx);
     return idx % 2;
}];
//枚举subSet
[subSet enumerateIndexesUsingBlock:^(NSUInteger idx, BOOL *stop)
{
     NSLog(@"%lu", (unsigned long)idx);
}];
```

### 例子4输出

``` vim
> 8
> 7
> 5
5
7
```

### 例子5

最后的方法就是NSArray的objectsAtIndexes，改方法可以根据一个NSIndexSet所在的区间返回数组相应的成员。

``` Objective-C
NSMutableIndexSet *idxSet = [[NSMutableIndexSet alloc] init];
[idxSet addIndex:2];
[idxSet addIndexesInRange:NSMakeRange(5, 3)];
NSArray *arr = @[@0, @1, @2, @3, @4, @5, @6, @7, @8, @9];
NSArray *res = [arr objectsAtIndexes:idxSet];
for(id item in res) {
    NSLog(@"%@", item);
}
```

### 例子5输出

``` vim
2
5
6
7
```