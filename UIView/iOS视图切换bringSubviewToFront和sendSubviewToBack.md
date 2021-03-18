# iOS视图切换bringSubviewToFront:和sendSubviewToBack:

## 简介

将一个UIView显示在最前面只需要调用其父视图的bringSubviewToFont()方法。
将一个UIView层推送到背后只需要调用其父视图的sendSubviewToBack()方法。

如:

``` Objective-C

[A bringSubViewToFront:B]; //	B视图在A视图上面
[A sendSubViewToBack:B];	//	B视图在A视图下面

```

## 实战

``` Objective-C

[self.view addSubview: mtestView];
[self.view addSubview:limitCountApplyTableView];

- (void)LimitedCountBtnClicked:(UIButton*)button{
	for (UIView *subviews in self.view.subviews) {
		if ([subviews isKindOfClass:[LimitCountApplyTableView class]]) {
			[self.view bringSubviewToFront:subviews];
			subviews.hidden = NO;
		} else if ([subviews isKindOfClass:[testView class]]) {
			subviews.hidden = YES;
		}
	}
}

- (void)LimitedTimeBtnClicked:(UIButton*)button{
	for (UIView *subviews in self.view.subviews) {
		if ([subviews isKindOfClass: [testView class]]) {
			[self.view bringSubviewToFront: subviews];
			subviews.hidden = NO;
		} else if ([subviews isKindOfClass:[LimitCountApplyTableView class]]) 		{
			subviews.hidden = YES;
		}
	}
}

```