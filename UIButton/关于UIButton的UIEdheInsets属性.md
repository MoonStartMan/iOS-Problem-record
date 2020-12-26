# 关于UIButton的UIEdheInsets属性

UIButton共有三个相关属性： 
1. contentEdgeInsets
2. titleEdgeInsets
3. imageEdgeInsets

## UIEdgeInsets

``` Objective-C
typedef struct UIEdgeInsets 
{
	CGFloat top,left,bottom,right;
} UIEdgeInsets
```

它的四个参数：top, left, bottom, right, 分别表示距离上边界，左边界，下边界，右边界的位移，默认值均为0。

## contentEdgeInsets

我们都知道，UIButton按钮可以只设置一个UILabel或者一个UIImageView，还可以同时具有UILabel和UIImageView；如果按钮设置contentEdgeInsets，就是按钮的内容整体(包含UILabel和imageView)进行偏移。

按钮内容整体向右下分别移动10像素：

``` Objective-C

Button.contentEdgeInsets = UIEdgeInsetsMake(10, 10, -10, -10);

```

## titleEdgeInsets & imageEdgeInsets

这两个属性的效果是相辅相成的。如果给一个按钮同事设置了title和image，他们默认的状态是图片在左，标题在右，而且image和title之间没有空隙；那就这就引出一个问题，title和image的UIEdgeInsets属性分别的相对于谁而言的？

真相只有一个：
image的UIEdgeInsets属性的top，left，bottom都是相对于按钮的，right是相对于title；
title的UIEdgeInsets属性的top，bottom，right都是相对于按钮的，left是相对于image；

知道真相的你不知道有没有眼泪流下来，怪不得之前怎么设置都不是想要的结果，原来相对于谁的位移压根没有搞清楚。现在既然搞清楚了，我们来试一下：

### title在左，image在右

``` Objective-C

//拿到title和image的大小：
CGSize titleSize = self.pureButton.titleLabel.bounds.size;
CGSize imageSize = self.pureButton.imageView.bounds.size;
//分别设置偏移量:记住偏移量是位移
self.pureButton.titleEdgeInsets = UIEdgeInsetsMake(0, -imageSize.width, 0, imageSize.width);
self.pureButton.imageEdgeInsets = UIEdgeInsetsMake(0, titleSize.width, 0, -titleSize.width);

```

### image在上，title在下

``` Objective-C

//图片 向右移动的距离是标题宽度的一半,向上移动的距离是图片高度的一半
//标题 向左移动的距离是图片宽度的一半,向下移动的距离是标题高度的一半

self.pureButton.imageEdgeInsets = UIEdgeInsetsMake(-imageSize.height/2, titleSize.width/2, imageSize.height/2, -titleSize.width/2);
self.pureButton.titleEdgeInsets = UIEdgeInsetsMake(titleSize.height/2, -imageSize.width/2, -titleSize.height/2, imageSize.width/2);

```