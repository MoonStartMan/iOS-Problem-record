# iOS设置UIImageView背景图片以及大小自适应


``` objective-c
UIImageView *imageView = [[UIImageView alloc] init];

imageView.image = [UIImage imageNamed:@"bg.png"];
imageView.frame = CGRectMake(0, 0, [UIScreen mainScreen].bounds.size.width, [UIScreen mainScreen].bounds.size.height);
imageView.contentMode = UIViewContentModeScaleAspectFit;

[self.view addSubview:imageView];
```


## contentMode 

设置图片方式

UIViewContentModeScaleAspectFit：不会填满整个区域，在不变形的情况下最大填满区域。