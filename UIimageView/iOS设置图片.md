# iOS设置图片及居中

## 设置图片代码

``` objective-c
UIImageView * imageView = [[UIImageView alloc]init];
imageView.image = [UIImage imageNamed:@"bg.png"];
imageView.frame = CGRectMake(0, 0, [UIScreen mainScreen].bounds.size.width,[UIScreen mainScreen].bounds.size.height);
[self.view addSubview:imageView];
```

## 图片居中核心代码

``` objective-c
imageView.frame = CGRectMake(0, 0, [UIScreen mainScreen].bounds.size.width, [UIScreen mainScreen].bounds.size.height);
```