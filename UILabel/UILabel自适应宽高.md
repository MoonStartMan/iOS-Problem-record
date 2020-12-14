# UILabel自适应宽高

@interface部分

``` Objective-C

@interface UILabel (UILabel_LabelHeighAndWidth)

+ (CGFloat) getHeightByWidth:(CGFloat)width title: (NSString *)title font: (UIFont*)font;

+ (CGFloat) getWidthWithTitle: (NSString *)title font: (UIFont *)font;

@end
```

@implementation 部分

``` Objective-C
#import "UILabel+UILabel_LabelHeightAndWidth.h"

@implementation UILabel (UILabel_LabelHeighAndWidth)

+ (CGFloat)getHeightByWidth: (CGFloat)width title: (NSString *)title font: (UIFont *)font	//	自适应高
{
	UILabel *label = [[UILabel alloc] initWithFrame: CGRectMake(0, 0, width, 0)];
	label.text = title;
	label.font = font;
	label.numberOfLines = 0;
	[label sizeToFit];
	CGFloat height = label.frame.size.height;
	return height;
}

+ (CGFloat)getWidthWithTitle: (NSString *)title font: (UIFont *)font // 自适应高
{
	UILabel *label = [[UILabel alloc] initWithFrame: CGRectMake(0, 0, 1000 ,0)];
	label.text = title;
	label.font = font;
	[label sizeToFit];
	return label.frame.size.width;
}

```