# iOS-给视图添加手势

## 轻拍手势

### 创建一个轻拍手势 同时绑定了一个事件

``` objective-c
UITagpGestureRecognizer *aTapGR = [[UITapGestureRecognizer alloc] initWithTarget: self action:@selector(tapGRAction:)];
```

### 设置轻拍次数

``` objective-c
aTapGR.numberOfTapsRequired = 1;
```

### 设置手指触摸的个数

``` objective-c
aTapGR.numberOfTouchesRequired = 2;
```

### 添加手势

``` objective-c
[self.rootView addGestureRecognizer:aTapGR];
[aTapGR release];
```

## 长按手势

``` objective-c
UILongPressGestureRecognizer *longPressGR = [[UILongPressGestureRecognizer alloc] initWithTarget: self action:@selector(longPressAction:)];

[self.rootView addGestureRecognizer:longPressGR];
[longPressGR release];
```

## 旋转手势

``` objective-c
UIRotationGestureRecognizer *rotationGR = [[UIRotationGestureRecognizer alloc] initWithTarget:self action:@selector(rotationAction:)];
[self.rootView.testImageView addGestureRecognizer:rotationGR];
[rotationGR release];
```

## 捏合手势

``` objective-c
UIPinchGestureRecognizer *pinchRG = [[UIPinchGestureRecognizer alloc] initWithTarget: self.action:@selector(pinchAction:)];
[self.rootView addGestureRecognizer:pinchRG];
[rotationGR release];
```

## 平移手势

``` objective-c
UIPanGestureRecognizer *panGR = [[UIPanGestureRecognizer alloc] initWithTarget:self action:@selector(panGRAction:)];
[self.rootView.testImageView addGestureRecognizer:panGR];
[panGR release];
```

## 轻扫手势

``` objective-c
UISwipeGestureRecognizer *swipeGR = [[UISwipeGestureRecognizer alloc] initWithTarget:self action:@selector(swipeGRAction:)];
```

## 设置滑动方向

``` objective-c

swipeGR.direction = UISwipeGestureRecognizerDirectionLeft; // 设置向左滑动 
[self.rootView.testImageView addGestureRecognizer:swipeGR];
[swipeGR release];

```