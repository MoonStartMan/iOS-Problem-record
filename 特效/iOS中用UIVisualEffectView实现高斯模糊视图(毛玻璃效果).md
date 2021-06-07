# iOS中用UIVisualEffectView实现高斯模糊视图(毛玻璃效果)

UIVisualEffectView(高斯模糊效果)

``` Objective-C

///	高斯模糊。<br> UIView *tempView= [[UIView alloc] initWithFrame: CGRectMake(100, 100, 100, 100)];
tempView.backgroundColor = [UIColor yellowColor];
[self.view addSubview: tempView];

///	UIBlurEffectStyleExtraLight	聚光灯效果
///	UIBlurEffectStyleLight 效果轻
///	UIBlurEffectStyleDark	效果重

UIBlurEffect *blurEffect = [UIBlurEffect effectWithStyle: UIBlurEffectStyleLight];
UIVisualEffectView *effectView = [[UIVisualEffectView alloc] initWithEffect:blurEffect];
effectView.frame = CGRectMake(100, 100, 100, 100);

//	作用对tempView做高斯模糊效果。
[self.view addSubview: effectView];

```