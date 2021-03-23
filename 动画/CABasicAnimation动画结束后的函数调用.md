# CABasicAnimation动画结束后的函数调用

## 添加代理

``` Objective-C

@interface LoadingView()<CAAnimationDelegate>

@end

```

## 动画结束后的函数调用

``` Objective-C

- (void)animationDidStop:(CAAnimation *)anim finished:(BOOL)flag {
    if (self.progess == 1) {
        self.hidden = YES;
    } else {
        self.hidden = NO;
    }
}

```