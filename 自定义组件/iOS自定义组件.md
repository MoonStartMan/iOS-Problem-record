# iOS自定义组件

## 自定义控件PageControl

+ 新建PageControl.h和PageControl.m文件

### PageControl.h文件

``` objective-c
#import <UIKit/UIKit.h>

NS_ASSUME_NONNULL_BEGIN

@interface PageControl : UIView

@property(nonatomic,strong) UIView* firstFillter;

@property(nonatomic, strong) UIView* secondFillter;

@property(nonatomic, strong) UIView* thirdFillter;

@property(nonatomic, strong) CAGradientLayer* gl;

@end

NS_ASSUME_NONNULL_END
```

### PageControl.m文件

+ 使用(instancetype) init 初始化

``` objective-c

-(instancetype) init {
	self = [super init];
	if(self) {
		_firstFillter = [[UIView alloc]init];
        _firstFillter.layer.cornerRadius = 4.5;
        _secondFillter = [[UIView alloc]init];
        _secondFillter.layer.cornerRadius = 4.5;
        _thirdFillter = [[UIView alloc]init];
        _thirdFillter.layer.cornerRadius = 4.5;
        [_firstFillter.layer addSublayer:self.gl];
        _secondFillter.backgroundColor=[UIColor colorWithRed:35/255.0 green:38/255.0 blue:63/255.0 alpha:1.0];
        _thirdFillter.backgroundColor =[UIColor colorWithRed:35/255.0 green:38/255.0 blue:63/255.0 alpha:1.0];
        [self addSubview:_firstFillter];
        [self addSubview:_secondFillter];
        [self addSubview:_thirdFillter];
	}
	return self;
}

```

+ 使用(void)layoutSubviews设置子控件的位置和尺寸

``` objective-c
static NSInteger margin = 9;
static NSInteger normalWidth = 9;
static NSInteger activeWidth = 18;
static NSInteger normalHeight = 9;

-(void)layoutSubviews
{
	[super layoutSubviews];
	self.firstFillter.frame = CGRectMake(0, 0, activeWidth, normalHeight);
    self.secondFillter.frame = CGRectMake(activeWidth+margin, 0, normalWidth, normalHeight);
    self.thirdFillter.frame = CGRectMake(activeWidth+margin*2+normalWidth, 0, normalWidth, normalHeight);
}
```

## 在其他页面引用PageControl


### .h文件

``` objective-c
//	引用PageControl
#import "PageControl"

//	声明一个pageCtronl存储
@property(nonatomic, strong) PageControl* pageCtronl;
```

### .m文件

``` objective-c
-(void)initPageCtrol{
//	将PageControl进行初始化并赋值给在.h文件中定义的pageCtronl;
		self.pageCtronl = [[PageControl alloc]init];
    [self.view addSubview: self.pageCtronl];
    [_pageCtronl mas_makeConstraints:^(MASConstraintMaker *make) {
        make.top.equalTo(self.view).with.offset(543);
        make.left.equalTo(self.view).with.offset(160.5);
        make.size.mas_equalTo(CGSizeMake(54, 9));
    }];
}

```

### 在(void)viewDidLoad中执行函数

``` objective-c
[self initPageCtronl];
```

以上就完成了自定义控件的使用。