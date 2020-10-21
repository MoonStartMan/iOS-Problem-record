# for循环动态创建UIButton并赋予点击事件

## 创建代码部分

``` objective-c
- (void) createLabelArray {
	- (void) createLabelArray {
    NSArray *arr = @[@"左上",@"上",@"右上",@"左",@"中",@"右",@"左下",@"下",@"右下"];

    NSInteger centerPointX = (_scrollView.frame.size.width - _scrollView.frame.origin.x)/2 ;
    NSInteger centerPointY = (_scrollView.frame.origin.y + _scrollView.bounds.size.height)/2;
    
    NSMutableArray *labelArr = [[NSMutableArray alloc]init];

    for(int i = 0; i < [arr count]; i++) {
        UIButton *btn = [[UIButton alloc]init];
        if(i <3) {
            btn.frame = CGRectMake(centerPointX*i+40, 40, 40, 40);
        } else if (i>=3 && i<6) {
            switch (i-3) {
                case 0:
                    btn.frame = CGRectMake(0, centerPointY+40, 40, 40);
                break;
                case 2:
                    btn.frame = CGRectMake((centerPointX+40)*2, centerPointY+40, 40, 40);
                break;
                default:
                    break;
            }
        } else {
            btn.frame = CGRectMake(centerPointX*(i-6)+40, centerPointY*2+40, 40, 40);
        }
        [btn setTitle:arr[i] forState:UIControlStateNormal];
        btn.titleLabel.font = [UIFont systemFontOfSize:14 weight:10];
        [btn setBackgroundColor:[UIColor blackColor]];
        [btn setTitleColor:[UIColor whiteColor] forState:UIControlStateNormal];
        btn.contentHorizontalAlignment = UIControlContentHorizontalAlignmentCenter;
        [btn.layer setCornerRadius:10];
        btn.layer.masksToBounds = YES;
        [labelArr addObject:btn];
        if(i == 5) {
            [labelArr removeObjectAtIndex:4];
        }
    }
    
    for(int i=0; i<labelArr.count; i++) {
        [self.view addSubview:labelArr[i]];
        switch (i) {
            case 0:
                [labelArr[i] addTarget:self action:@selector(leftTop:) forControlEvents:UIControlEventTouchUpInside];
            break;
            case 1:
                [labelArr[i] addTarget:self action:@selector(top:) forControlEvents:UIControlEventTouchUpInside];
            break;
            case 2:
                [labelArr[i] addTarget:self action:@selector(rightTop:) forControlEvents:UIControlEventTouchUpInside];
            break;
            case 3:
                [labelArr[i] addTarget:self action:@selector(left:) forControlEvents:UIControlEventTouchUpInside];
            break;
            case 4:
                [labelArr[i] addTarget:self action:@selector(right:) forControlEvents:UIControlEventTouchUpInside];
            break;
            case 5:
                [labelArr[i] addTarget:self action:@selector(leftBottom:) forControlEvents:UIControlEventTouchUpInside];
            break;
            case 6:
                [labelArr[i] addTarget:self action:@selector(bottom:) forControlEvents:UIControlEventTouchUpInside];
            break;
            case 7:
                [labelArr[i] addTarget:self action:@selector(rightBottom:) forControlEvents:UIControlEventTouchUpInside];
            break;
            default:
                break;
        }
    }
    
}

-(void) top:(UIButton *)sender{
    [UIView animateWithDuration:2.0 animations:^{
        CGPoint offset = self.scrollView.contentOffset;
        offset.y = 0;
        self.scrollView.contentOffset = offset;
    }];
}

-(void) leftTop:(UIButton *)send {
    [UIView animateWithDuration:2.0 animations:^{
        CGPoint offset = self.scrollView.contentOffset;
        offset.y = 0;
        offset.x = 0;
        self.scrollView.contentOffset = offset;
    }];
}

-(void) rightTop:(UIButton *)send {
    [UIView animateWithDuration:2.0 animations:^{
        CGPoint offset = self.scrollView.contentOffset;
        offset.y = 0;
        offset.x = self.scrollView.contentSize.width - self.scrollView.frame.size.width;
        self.scrollView.contentOffset = offset;
    }];
}

-(void) left:(UIButton *)send {
    [UIView animateWithDuration:2.0 animations:^{
        CGPoint offset = self.scrollView.contentOffset;
        self.scrollView.contentOffset = offset;
    }];
}

-(void) right:(UIButton *)send {
    [UIView animateWithDuration:2.0 animations:^{
        CGPoint offset = self.scrollView.contentOffset;
        offset.x = self.scrollView.contentSize.width - self.scrollView.frame.size.width;
        self.scrollView.contentOffset = offset;
    }];
}

-(void) leftBottom:(UIButton *)send {
    [UIView animateWithDuration:2.0 animations:^{
        CGPoint offset = self.scrollView.contentOffset;
        offset.x = 0;
        offset.y = self.scrollView.contentSize.height - self.scrollView.frame.size.height;
        self.scrollView.contentOffset = offset;
    }];
}

-(void) bottom:(UIButton *)send {
    [UIView animateWithDuration:2.0 animations:^{
        CGPoint offset = self.scrollView.contentOffset;
        offset.y = self.scrollView.contentSize.height - self.scrollView.frame.size.height;
        self.scrollView.contentOffset = offset;
    }];
}

-(void) rightBottom:(UIButton *)send {
    [UIView animateWithDuration:2.0 animations:^{
        CGPoint offset = self.scrollView.contentOffset;
        offset.x = self.scrollView.contentSize.width - self.scrollView.frame.size.width;
        offset.y = self.scrollView.contentSize.height - self.scrollView.frame.size.height;
        self.scrollView.contentOffset = offset;
    }];
}

- (void)viewDidLoad {
    [super viewDidLoad];
    // Do any additional setup after loading the view.
    [self.scrollView addSubview:self.image];
    [self.view addSubview: _scrollView];
    [self createLabelArray];
    //  2.设置内容的尺寸
}
}
```

## 相关知识点部分

### UIButton相关设置

#### UIButton设置文字

``` objective-c
[btn setTitle: arr[i] forState: UIControlStateNormal];
```

#### UIButton设置文字大小

``` objective-c
btn.titleLabel.font = [UIFont systemFontOfSize:14 weight:10];
```

#### UIButton设置按钮背景色和按钮文字颜色

``` objective-c
[btn setBackgroundColor:[UIColor blackColor]];
[btn setTitleColor:[UIColor whiteColor] forState:UIControlStateNormal];
```

#### UIButton设置按钮文字居中

``` objective-c
btn.contentHorizontalAlignment = UIControlContentHorizontalAlignmentCenter;
```