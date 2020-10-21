# UIButton 设置图片在上文字在下且水平居中

## 使图片和文字水平居中显示

``` objective-c

btn.contentHorizontalAlignment = UIControlContentHorizeontalAlignmentCenter;

```

## 设置文字的位置

文字距离上边框的距离增加imageView的高度,距离左边框减少imageView的宽度，距离下边框和右边框距离不变。

``` objective-c

[btn setTitleEdgeInsets: UIEdgeInsetsMake(btn.imageView.frame.size.height, -btn.imageView.frame.size.width, 0.0, 0.0)];

```

## 设置图片的位置

图片距离右边框距离减少图片的宽度，其它不边

``` objective-c

[btn setImageEdgeInsets:UIEdgeInsetsMake(0.0, 0.0,0.0, -btn.titleLabel.bounds.size.width)];
```