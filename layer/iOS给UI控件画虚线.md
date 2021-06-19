# iOS给UI控件画虚线

``` Objective-C

CAShapeLayer *borderLayer = [CAShapeLayer layer];

borderLayer.bounds = CGRectMake(0, 0, self.BottomLineView.frame.size.width, self.BottomLineView.frame.size.height);

borderLayer.position = CGPointMake(CGRectGetWidth(self.BottomLineView.frame)/2, CGRectGetHeight(self.BottomLineView.frame)/2);

borderLayer.path = [UIBezierPath bezierPathWithRoundedRect:borderLayer.bounds cornerRadius:8.0f].CGPath;

borderLayer.lineWidth = 1.5;

//	虚线边框
borderLayer.lineDashPattern = @[@2, @2];
//	实线边框
borderLayer.fillColor = [UIColor clearColor].CGColor;
borderLayer.strokeColor = [UIColor whiteColor].CGColor;
[self.BottomLineView.layer addSublayer:borderLayer];

```

** 如果需要获取相关视图的大小，可以在layoutSubviews中进行实现. **

## 相关参数理解

``` Objective-C

/**

	@param bounds 界限
	@param fillColor 填充色
	@param strokeColor 填充色
	@param lineWidth 虚线宽度
	@param position 位置
	@param path 路径
	@param lineDashPattern 虚线边框
	
*/

```