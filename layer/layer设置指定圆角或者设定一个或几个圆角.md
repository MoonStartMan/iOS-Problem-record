# layer设置指定圆角或者设定一个或几个圆角

## 核心代码

``` Objective-C

UIBezierPath *maskPath = [UIBezierPath bezierPathWithRoundedRect:self.statusLabel.bounds byRoundingCorners:UIRectCornerBottomLeft | UIRectCornerTopLeft cornerRadii:4, 4)];

```

## 完整代码

``` Objective-C

UIBezierPath *maskPath = [UIBezierPath bezierPathWithRoundedRect:self.statusLabel.bounds byRoundingCorners:UIRectCornerBottomLeft | UIRectCornerTopLeft cornerRadii:4, 4)];

CAShapeLayer *maskLayer = [[CAShapeLayer alloc] init];
maskLayer.frame = self.statusLabel.bounds;
maskLayer.path = maskPath.CGPath;
self.statusLabel.layer.mask = maskLayer;

```