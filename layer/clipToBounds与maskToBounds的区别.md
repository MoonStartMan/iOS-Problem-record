# clipToBounds与maskToBounds的区别

UIView.clipsToBounds 让子View只显示父 View的Frame部分;
子视图超出frame的部分不显示
默认为NO，设置为YES就会把超出的部分裁掉。
maskToBounds是CALayer的属性，基于View的不少属性其实就是作用于CALayer的。子图层是否剪切图层边界，默认为NO。

``` Objective-C

UIView.layer.maskToBounds = YES
//	效果与下面一样 
UIView.clipToBounds = YES

```