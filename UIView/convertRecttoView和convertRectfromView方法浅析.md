# convertRect:toView和convertRect:fromView:方法浅析

## -(CGRect)convertRect:(CGRect)rect fromView:(nullable UIView*)view;

``` Objective-C
CGRect = newRect = [someView converRect:rect fromView:fromView];
```

将在fromView为参照系的一个位置为rect.origin、大小为rect.size的一块矩形转换成在someView为参照系的矩形

+ 也就是计算以fromView.origin为原点的坐标系下的一块rect矩形,在以someView.origin为原点的坐标系下 这块rect的位置是多少
+ 因为只转换位置(origin)，所以size是不会变的，也就是newRect.size == rect.size

``` Objective-C

UIView *greenView = [[UIView alloc] initWithFrame:CGRectMake(10, 90, 100, 100)];
    greenView.backgroundColor = [UIColor greenColor];
    UIView *redView = [[UIView alloc] initWithFrame:CGRectMake(110, 190, 300, 300)];
    redView.backgroundColor = [UIColor redColor];
    UIView *purpleView = [[UIView alloc] initWithFrame:CGRectMake(50, 50, 180, 180)];
    purpleView.backgroundColor = [UIColor purpleColor];
    
    [self.view addSubview:greenView];
    [self.view addSubview:redView];
    [redView addSubview:purpleView];
    
    CGRect newRect = [self.view convertRect:purpleView.frame fromView:redView];
    NSLog(@"%@",NSStringFromCGRect(newRect));

```

## 跟父视图同一级的其他view

上面我们测试了purpleView在其父视图(redView)的父视图(self.view)转换情况,现在我们测试purple在其父视图平级的view上转换情况。

``` Objective-C

CGRect newRect = [greenView converRect:purpleView.frame fromView: redView;]

```

分析:

根据我们的结论,newRect的size等于purple的size,也就是{180,180};purple的origin为{50,50},是相对于redView来说的,现在要计算相对于greenView的位置;也就是下图中(x,y)的值

我们可以分两步计算,第一步,计算redView.origin相对于greenView.origin位置:redView的origin为{110, 190},greenView的origin为{10, 90},现在我们要把greenView的origin作为原点,也就是greenView的origin为{0,0},那么redView的origin为{110-10,190-90},也就是{100,100},而purple相对于redView的位置为{50,50},也就是purple相对于greenView的位置{100 + 50, 100 + 50},也就是{150, 150},所以newRect应该等于{{150, 150}, {180, 180}};

我们打印下rect值为

``` Objective-C
newRect is ---- {{150, 150}, {180, 180}}
```

跟我们的猜想是一致;

## 结论

| 方法 | 相同点 | 不同点 |
| ---- | ---- | ----- |
| newRect = [someView convertRect:rect toView:toView]; | 只改变rect的origin,size不变 | rect是相对于someView的,以toView为坐标系重新计算rect的值 |
| newRect = [someView convertRect:rect fromView: fromview] | 只改变rect的origin,size不变 | rect是fromView为坐标系下的值, 将rect转为以someView为坐标系的值 |