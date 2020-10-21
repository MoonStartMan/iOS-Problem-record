# iOS UIButton同时设置图片及文字

## UIButton同时设置图片和文字

``` objective-c

UIButton* _backButton = [UIButton buttonWithType:UIButton TypeCustom];
[_backButton setFrame: CGRectMake(12, 8, 64, 28)];
//	设置button在没有选中的时候显示的字体
[_backButton setTitle:@"返回" forState: UIControlStateNormal];
//	设置button显示字体的大小
_backButton.titleLabel.font = [UIFont systemFontOfSize: 14.0f];
//	设置button背景显示图片
[_backButton setBackgroundimage:[UIImage imageNamed:@"backButton.png"] forState: UIControlStateNormal];
```

## UIButton的title设置

``` objective-c
[btn setTitle: @"search" forState: UIControlStateNormal];
//	设置按钮的字体大小
btn.titleLabel.font = [UIFont systemFontOfSize: 14.0];
[btn setBackgroundColor: [UIColor blueColor]];

```

## UIButton设置文字位置

文字位置默认是居左，默认的是居中。

``` objective-c
btn.contentHorizontalAlignment = UIControlContentHorizontalAlignmentLeft;
```

