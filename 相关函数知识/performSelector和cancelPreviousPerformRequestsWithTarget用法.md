# performSelector和cancelPreviousPerformRequestsWithTarget用法

## performSelector

使用方法

``` Objective-C

[self performSelector:@selector(方法名称) withObject:参数 (传递给前面的方法所需要的参数) afterDelay:秒(如果不到1秒则加f，如(0.01)];

```

实际案例

``` Objective-C

CGFloat enterDuration = CGRectGetWidth(self.bounds)/speed;

[self performSelector:@selector(enterScreen) withObject:nil afterDelay:enterDuration];

- (void)enterScreen {
    if(self.moveStatusBlock) {
        self.moveStatusBlock(Enter);
    }
}

```

## cancelPreviousPerformRequestsWithTarget

使用方法

cancelPreviousPerformRequestsWithTarget：取消前面所注册过performSelector方法，就是说当上面这个方法正在运行，比如我们希望10秒钟之后执行某一个方法，但是如何在没到10秒钟的情况下取消performSelector呢？就是用这个方法来实现的

``` Objective-C

[[self class] cancelPreviousPerformRequestsWithTarget:self（请求的目标） selector:@selector(上面的performSelector所注册过的方法名称) object:nil];

[NSObject cancelPreviousPerformRequestsWithTarget:self selector:@selector(scrollDone) object:nil];

```

实际案例

``` Objective-C

[NSObject cancelPreviousPerformRequestsWithTarget:self];

```