# UIImage图片重新绘制背景色

``` objective-c

UIImage *image = [[UIImage imageNamed:@"logo.png"] imageWithRenderingMode:UIImageRenderingModeAlwaysTemplate];
imageView.image = image;
imageView.tintColor = [UIColor purpleColor];
```