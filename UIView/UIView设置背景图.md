# UIView设置背景图


## 实现代码

``` Objective-C

- (void)setUIViewBackground: (UIView *)uiview name:(NSString *)name {
	UIGraphicsBeginImageContext(uiview.frame.size);
	[[UIImage imageNamed:name] drawInRect: uiview.bounds];
	UIImage *image = UIGraphicsGetImageFromCurrentImageContext();
	UIGraphicsEndImageContext();
	
	uiview.backgroundColor = [UIColor colorWithPatternImage: image];
}

```