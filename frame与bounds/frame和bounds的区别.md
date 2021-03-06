# frame和bounds的区别

+ frame: 该View在父View坐标系统中的位置和大小。(参照点是,父亲的坐标系统)
+ bounds: 该view在本地坐标系统中的位置和大小。(参照点是,本地坐标系统,就相当于ViewB自己的坐标系统,以0,0点为起点)。

其实本地坐标系统的关键就是要知道的它的原点(0, 0)在父坐标系统中的位置(这个位置是相对于父view的本地坐标系统而言的，最终的父view就是UIWindow,它的本地坐标系统原点就是屏幕的左上角了)。

通过修改view的bounds属性可以修改本地坐标系统的原点位置。

## bounds到底起什么作用

### 实例代码

``` Objective-C

UIView *view = [[UIView alloc] initWithFrame: CGRectMake(100, 100, 200, 200)];
view1.backgroundColor = [UIColor redColor];
[self.view addSubView: view1];	//	添加到self.view
NSLog(@"view1 frame:%@========view1 bounds:%@");

```

### 输出日志

``` Objective-C

view1 frame:{{100, 100}, {200, 200}}========view1 bounds:{{0, 0}, {200, 200}}
view2 frame:{{0, 0}, {100, 100}}========view2 bounds:{{0, 0}, {100, 100}}

```

改变view1的bounds,代码如下

``` Objective-C

[view1 setBounds: CGRectMake(-20, -20, 200, 200)];

```

此时显示和输出的日志如下:

``` Objective-C
 view1 frame:{{100, 100}, {200, 200}}========view1 bounds:{{-20, -20}, {200, 200}}

view2 frame:{{0, 0}, {100, 100}}========view2 bounds:{{0, 0}, {100, 100}}
```

### 分析

上面设置view1的bounds的代码起到了让view2的位置改变的作用。为何(-20, -20)的偏移量,却可以让view2向右下角移动呢?

这是因为setBounds的作用是:强制将自己(view1)本地坐标的原点改为(-20, -20)。这个(-20, -20)是相对view1的父view(self.view)偏移的。也就是想左上角偏移。

那么view1的坐标系中(0, 0)这个点是需要向右下各偏移20。

因为view1的subview(view2)的frame参照的坐标系是父view(view1)的bounds设置的，而此时view2的frame设置为(0, 0),就会导致view2向下各偏移20.如上图所示。

### 总结

所以,bounds的有这么一个缺点:
它是参考自己坐标系，它可以修改自己坐标系统的原点位置，进而影响到"子view"的显示位置。

## bounds使用场景

其实bounds我们一直在使用，就是我们使用scrollView的时候。
为什么我们滚动scrollView可以看到超出显示屏的内容。就是因为scrollView在不断改变自己的bounds，从而改变scrollView上的子view的frame，让他们的frame始终在最顶级view(window)的frame内部,这样我们就可以始终看到内容了。

## bouns大于frame的情况

假设设置了控件的bounds大于frame,那么此时会导致frame被撑大,frame的x,y,width,height都会改变。

``` Objective-C

UIView *view3 = [[UIView alloc] initWithFrame:CGRectMake(100, 100, 200, 200)];
    view3.backgroundColor = [UIColor redColor];
    [view3 setBounds: CGRectMake(0, 0, 300, 300)];
    [self.view addSubview: view3];
    NSLog(@"view3 frame: %@========view3 bounds: %@", NSStringFromCGRect(view3.frame), NSStringFromCGRect(view3.bounds));
    
    UIView *view4 = [[UIView alloc] initWithFrame:CGRectMake(0, 0, 100, 100)];
    view4.backgroundColor = [UIColor yellowColor];
    [view3 addSubview: view4];  //  添加到view3上
    NSLog(@"view4 frame:%@========view4 bounds%@", NSStringFromCGRect(view4.frame), NSStringFromCGRect(view4.bounds));

```

### 结论

+ 新的frame的size等于bounds的size
+ 新的frame.x = 旧frame.x - (bounds.size.width - 旧frame.size.width) / 2;
+ 新的frame.y = 旧frame.y - (bounds.size.height - 旧frame.size.height) / 2;

## bounds的改变会累加

假设view1上面添加了view2,view2上面添加了view3.三个view的size都是(100, 100)。我们设置如下:

view1.bound = (0, 100, 100, 100)
view2.bound = (0, 100, 100, 100)
那么此时view3.frame = (0, 0, 100, 100),view3会相对于原来没有设置view1、view2的bound时的位置向上偏移200。