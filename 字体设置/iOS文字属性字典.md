# iOS文字属性字典

iOS开发过程中当需要给字体，颜色，下划线等属性的时候参数是一个NSDictionary字典。

## 在词典中加入文本的字体 大小

``` Objective-C

NSDictionary *attrs = @{NSFontAttributeName:[UIFont fontWithName:@"ChineseTypewriter" size:30]};

```

## 设置字体颜色

``` Objective-C

NSDictionary *attrs = @{NSFontAttributeName:[UIFont fontWithName:@"ChineseTypewriter" size:30],NSForegroundColorAttributeName:[UIColor redColor]};

```

## 段落格式

``` Objective-C

- (void)drawRect: (CGRect)rect 
{
	NSString *attrString = @"hello word";
	
	NSMutableParagraphStyle *paragraph = [[NSMutableParagraphStyle alloc]init];
	paragraph.alignment=NSTextAlignmentCenter;	//居中
	
	NSDictionary *attrs = @{NSFontAttributeName: [UIFont fontWithName:@"ChineseTypewriter" size:30],//文本的颜色 字体大小
	NSForegroundColorAttributeName:[UIColor redColor],	//	文字颜色
	NSParagraphStyleAttributeName:paragraph,//段落格式
	};
	[attrString drawInRect:CGRectMake(20, 120, 320, 200) withAttributes:attrs];
}

```