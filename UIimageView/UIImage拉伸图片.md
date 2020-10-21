# UIImage拉伸图片

## resizableImageWithCapInsets 

设置拉伸保护区域

``` objective-c
resizableImageWithCapInsets:UIEdgeInsetsMake(19, 24, 0, 5)

//  顺序为 上 左 下 右
```

## resizingMode

设置模式

+ UIImageResizingModeStretch: 拉伸模式
+ UIImageResizingModeTile: 平铺模式

``` objective-c
resizingMode:UIImageResizingModeStretch
```
