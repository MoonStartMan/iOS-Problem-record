# UILabel相关知识

## 创建

``` Objective-C
CGRect rect = CGRectMake(100, 200, 50, 50);
UILabel *label = [[UILabel alloc] initWithFrame: rect];
```

## text

设置和读取文本内容，默认为nil

``` Objective-C
label.text = @"文本信息";	//	设置内容
NSLog(@"%@", label.text);	//	读取内容
```

## textColor

设置文字颜色，默认为黑色

``` Objective-C
label.textColor = [UIColor redColor];
```

## font 

设置字体大小，默认17

``` Objective-C
label.font = [UIFont systemFontOfSize: 20];	//	一般方法
label.font = [UIFont boldSystemFontSize: 20];	//	加粗方法
label.font = [UIFont fontWithName: @"Arial" size: 16];	//指定字体的方法
```

## textAlignment

设置文本对齐方式。

``` Objective-C
label.textAlignment = NSTextAlignmentCenter;	//	还有NSTextAlignmentRight、NSTextAlignmentLeft
```

## numberOfLines

标签最多显示行数，如果为0则表示多行。

``` Objective-C
label.numberOfLines = 2;
```

## enabled

只是决定了Label的绘制方式，将它设置为NO将会使文本变暗，表示它没有激活，这时向它设置颜色值是无效的。

``` Objective-C
label.enable = NO;
```

## highlighted

是否高亮显示

```Objective-C
label.highlighted = YES;
label.highlightedTextColor = [UIColor orangeColor];	//高亮
```

## ShadowColor

设置阴影颜色
``` Objective-C
[label setShadowColor: [UIColor blackColor]];
```

## ShadowOffset

设置阴影偏移量
``` Objective-C
[label setShadowOffset: CGSizeMake(-1, -1)];
```

## baselineAdjustment

如果adjustsFontSizeToFitWidth属性设置为YES，这个属性就来控制文本基线的行为。

``` Objective-C
label.baselineAdujustment = UIBaselineAdjustmentNone;

UIBaselineAdjustmentAlignBaselines = 0,	默认，文本最上端与中线对齐。

UIBaselineAdjustmentAlignCenters, 文本中线与label中线对齐

UIBaselineAdjustmentNone, 文本最低端与label中线对齐。
```

## Autoshrink

是否自动收缩

``` Objective-C

Fixed Font Size 默认,如果Label宽度小于文字长度时，文字大小不自动缩放

minimumScaleFactor //	设置最小收缩比例, 如果Label宽度小于文字长度时,文字进行收缩,收缩超过正比例后,停止收缩

minimumFontSize 设置最小收缩字号，如果Label宽度小于文字长度时,文字字号减小，低于设定字号后，不再减小。

label.minimumScaleFactor = 0.5;

```

## adjustsLetterSpacingToFitWidth

改变字母之间的间距来适应Label大小

``` Objective-C

myLabel.adjustsLetterSpacingToFitWidth = NO;

```

## lineBreakMode

设置文字过长时的显示格式

``` Objective-C

label.lineBreakMode = NSLineBreakByCharWrapping;	//	以字符为显示单位显示,后面部分省略不显示。

label.lineBreakMode = NSLineBreakByClipping;	//	剪切与文本宽度相同的内容长度，后半部分被删除

label.lineBreakMode = NSLineByTruncatingHead;	//	前面部分文字以...方式省略，显示尾部文字内容

label.lineBreakMode = NSLineBreakByTruncatingMiddle;//	中间的内容以……方式省略，显示头尾的文字内容。

label.lineBreakMode = NSLineBreakByTruncatingTail;//	结尾部分的内容以……方式省略，显示头的文字内容。

label.lineBreakMode = NSLineBreakByWordWrapping;//	以单词为显示单位显示，后面部分省略不显示。

```

## adjustsFontSizeToFitWidth

设置字体大小适应label宽度

``` Objective-C

label.adjustFontSizeToFitWidth = YES;

```

## attributedText

设置标签属性文本

``` Objective-C

NSString *text = @"first";

NSMutableAttributedString *textLabelStr = [[NSMutableAttributedString alloc] initWithString: text];

[textLabelStr setAttributes:@{NSForegroundColorAttributeName: [UIColor lightGrayColor],NSFontAttributeName:[UIFont systemFontOfSize: 17]} range: NSMakeRange(11, 10)];

```

## 竖排文字每个文字加一个换行符，这是最方便和简单的实现方式。

``` Objective-C

label.text = @"请n竖n直n方n向n排n列";
label.numberOfLines = [label.text length];

```

## 计算UIlabel 随字体多行后的高度

``` Objective-C

UILabel *msgLabel = [[UILabel alloc] initWithFrame: CGRectMake(15, 45, 0 ,0)];

msgLabel.backgroundColor = [UIColor lightTextColor];

[msgLabel setNumberOfLines: 0];

msgLabel.font = [UIFont fontWithName: @"Arial" size: 12];

CGSize size = CGSizeMake(290, 1000);

msgLabel.text = @"获取到的deviceToken,我们可以通过webservice服务交给.net应用程序，这里我简单处理，直接打印出来，拷贝到.net应用环境中使用。"

CGSize msgSie = [msgLabel.text sizeWithFont:fontsconstrainedToSize: size];

[msgLabel setFrame: CGRectMake(15, 45, 290, msgSiz.height)];

```

## 渐变字体Label

``` Objective-C

UIColor *titleColor = [UIColor colorWithPatternImage: [UIImage imageNamed:@"btn.png"]];

NSString *title = @"Setting";

UILabel *titleLabel = [[UILabel alloc] initWithFrame: CGRectMake(0, 0, 80 44)];

titleLabel.textColor = titleColor;

titleLabel.text = title;

titleLabel.font = [UIFont boldSystemFontOfSize: 20];

titleLabel.backgroundColor = [UIColor clearColor];

[self.view addSubView: titleLabel];

[titleLabel release];

```

## Label添加边框

``` Objective-C

titleLabel.layer.borderColor = [[UIColor grayColor] CGColor];

titleLabel.layer.borderWidth = 2;

```

## Label自适应宽度

``` Objective-C

+ (float)widthAuto:(NSString *)content fontSize:(CGFloat)fontSize contentheight: (CGFloat)height {
	//	列宽
	
	//	CGFloat contentHeight = height;
	
	//	用何种字体进行展示
	
	UIFont *font = [UIFont systemFontOfSize: fontSize];
	
	//	计算出显示内容需要的最小尺寸
	
	CGSize size = CGSizeMake(100, 100);
	[NSDictionaryWithObjectsAndKeys: font, NSFontAttributeName, nil];
	
	//	ios7方法，获取文本需要的size,限制宽度
	
	CGSize actualsize = [content boundingRectWithSize: size options:NSStringDrawingUsesLineFragmentOrigin | NSStringDrawingUsesFontLeading attributes: tdic context: nil].size;
	
	return	actualsize.width;
}

```