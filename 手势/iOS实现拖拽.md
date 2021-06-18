# iOS实现拖拽

## UIView的触摸事件处理

+ 一根或者多根手指开始触摸view，系统会自动调用view的下面方法

``` Objective-C

-(void)touchesBegan:(NSSet *)touches withEvent:(UIEvent *)event;

```

+ 一根或多根手指在view上移动，系统会自动调用view的下面方法(随着手指的移动持续调用该方法)

``` Objective-C

-(void)touchesMoved:(NSSet *)touches withEvent:(UIEvent *)event;

```

+ 一根或者多根手指离开view，系统会自动调用view的下面方法

``` Objective-C

-(void)touchesEnded:(NSSet *)touches withEvent:(UIEvent *)event;

```

+ 触摸结束前，某个系统事件(例如电话呼入)会打断触摸过程，系统会自动调用下面的方法

``` Objective-C

-(void)touchesCancelled:(NSSet *)touches withEvent:(UIEvent *)event;

```

## UITouch

当用户用一根触摸屏幕时,会创建一个与手指相关联的UITouch对象·一根手指对应一个UITouch对象

### UITouch的作用

+ 保存着跟手指相关的信息,比如触摸的位置、时间、阶段
+ 当手指移动时,系统回更新同一个UITouch对象，使之能够一直保存该手指在的触摸位置
+ 当手指离开屏幕时，系统回销毁相应的UITouch对象
+ 提示:iPhone开发中,要避免使用双击事件!

### UITouch的属性

+ 触摸产生时所处的窗口

``` Objective-C

@property(nonatomic,readonly,retain) UIWindow *window;
 
```

触摸产生时所处的视图

``` Objective-C

@property(nonatomic,readonly,retain) UIView *view;

```

短时间内点按屏幕的次数,可以根据tapCount判断单击、双击或更多的点击

``` Objective-C

@property(nonatomic,readonly) NSUInteger tapCount;

```

记录了触摸事件产生或变化时的时间,单位是秒

``` Objective-C

@property(nonatomic,readonly) NSTimeInterval timestamp;

```

当前触摸事件所处的状态

``` Objective-C

@property(nonatomic,readonly) UITouchPhase phase;

```

### UITouch的方法

``` Objective-C

- (CGPoint)locationInView:(UIView *)view;

```

返回值表示触摸在view上的位置
这里返回的位置是针对view的坐标系的(以view的左上角为原点(0, 0))
调用时传入的view参数为nil的话,返回的是触摸点在UIWindow的位置

``` Objective-C

- (CGPoint)previousLocationInView:(UIView *)view;

```

该方法记录了前一个触摸点的位置

## 实际运用部分代码

``` Objective-C

- (void)touchesMoved:(NSSet<UITouch *> *)touches withEvent:(UIEvent *)event {
    NSLog(@"%s", __func__);
    //  做UIView拖拽
    UITouch *touch = [touches anyObject];
    
    //  求偏移量 = 手指当前点的X - 手指上一个点的X
    CGPoint curP = [touch locationInView:self.view];
    
    self.heartView.center = curP;
}

```