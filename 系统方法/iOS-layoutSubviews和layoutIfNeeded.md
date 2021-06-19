# iOS-layoutSubviews和layoutIfNeeded

## layoutSubviews

layoutSubviews在以下情况会被调用:

+ init初始化不会触发layoutSubviews但是是用initWithFrame进行初始化时,当rect的值不为CGRectZero时,会触发
+ addSubview会触发layoutSubviews
+ 设置view的Frame会触发layoutSubviews,当然前提是frame的值设置前后发生了变化
+ 滑动ScrollView的时候
+ 旋转Screen会触发父UIView上的layoutSubviews事件

``` Objective-C

layoutSubviews 方法只能被系统触发调用，程序员不能手动直接调用该方法。要引起该方法的调用，可以调用 UIView 的setNeedsLayout方法来标记一个 UIView。这样一来，在 UI 线程的下次绘制循环中，系统便会调用该 UIView 的 layoutSubviews 方法。

```

## layoutIfNeeded

也就是使用约束的时候 调一下可以立即更新效果
setNeedsLayout方法并不会立即刷新，立即刷新需要调用layoutIfNeeded方法！

``` Objective-C

setNeedsDisplay
与setNeedsLayout方法相似的方法是setNeedsDisplay方法。该方法在调用时，会自动调用drawRect方法。drawRect方法主要用来画图。所以，当需要刷新布局时，用setNeedsLayOut方法；当需要重新绘画时，调用setNeedsDisplay方法。

```