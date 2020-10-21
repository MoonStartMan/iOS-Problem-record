# iOS设置UIButton

## 初始化UIButton

``` objective-c
UIButton *btn = [[UIButton alloc]init];
```

### 设置背景颜色

``` objective-c
btn.backgroundColor = [UIColor redColor];
```

### 给按钮添加文字并添加显示状态

``` objective-c
[btn setTitle:@"立即体验" forState:UIControlStateNormal];
```

#### forState的状态

1. UIControlStateHighlighted
		这种状态下的按钮可以接收点击事件，显示为highlighted状态下的文字颜色和图片。 
2. UIControlStateDisabled
		这种状态下的按钮无法接收点击事件，显示为DIsabled状态下的文字颜色和图片。
3. UIControlStateSelected
		这种状态下的按钮可以接收点击事件，显示为selected状态下的文字颜色和图片。
4. UIControlStateNormal
		这种状态下的按钮可以接收点击事件，但是如果如果是由[button.enabled = NO]状态和其它状态叠加则不可点击。
		
### 设置按钮的颜色并添加显示状态

``` objective-c
[btn setTitleColor:[UIColor redColor]forState: UIControlStateNormal];
```

### 给按钮一个frame 

``` objective-c
btn.frame = CGRectMake(100, 100, 270, 80);
```

### 给按钮添加点击事件

``` objective-c
[btn addTarget:self action:@seletor(handleButton:) forControlEvent: UIControlEventTouchUpInside];
```

### 给按钮添加图片

``` objective-c
[btn setImage: [UIImage ImageNamed@"1.jpg"]forState:UIControlEventTouchUpInside];
```

### 按钮被选中的状态

``` objective-c
button.selected = YES;
```