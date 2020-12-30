# iOS使用贝塞尔曲线画圆角及指定位置圆角

``` objective-c
CFFloat radius = 12;	//	圆角大小
UIRectCorner conrer = UIRectCornerAllCorners;	//	圆角位置，全部位置
UIBezierPath *path = [UIBezierPath bezierPathWithRoundedRect:view.bounds byRoundingCorners:corner cornerRadii:CGSizeMake(radius, radius)];
CAShapeLayer *maskLayer = [[CAShapeLayer alloc] init];
maskLayer.frame = view.bounds;
maskLayer.path = path.CGPath;
view.layer.mask = maskLayer;
```