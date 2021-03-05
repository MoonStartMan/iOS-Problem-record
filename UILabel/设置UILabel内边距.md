# 设置UILabel内边距

自定义UILabel，然后重写drawTextInR

## CustomLabel.h

``` Objective-C

@interface CustomLabel : UILabel;

@property (nonatomic, assign) UIEdgeInsets textInsets;	//	控制字体与控件边界的间隙

@end

```

## CustomLabel.m

``` Objective-C

#import "CustomLabel.h"

@implementation CustomLabel

- (instancetype)initWithFrame: (CGRect)frame {
	if (self = [super initWithFrame: frame]) {
		_textInsets = UIEdgeInsetsZero;
	}
}

- (void)drawTextInRect: (CGRect)rect {
	[super drawTextInRect: UIEdgeInsetsInsetRect(rect, _textInsets)];
}

@end

```

## 使用方法

``` Objective-C

CustomLabel *titleLabel = [[CustomLabel alloc] 
titleLabel.textInsets = UIEdgeInsetsMake(0.f, 15.f, 0.f, 0.f); // 设置左内边距，只要设置该属性就可以设置内边距了，.m中的 - (void)drawTextInRect:(CGRect)rect 方法就是实现过程

```