# iOS-MAXFLOAT常量的使用

``` Objective-C

+ (CGSize)labelheight:(UILabel *)detlabel
{
    CGSize size = CGSizeMake(SCREENWIDTH - 16, 1000);

    CGSize contentactually = [detlabel.text boundingRectWithSize:size options:(NSStringDrawingUsesLineFragmentOrigin|NSStringDrawingUsesFontLeading) attributes:[NSDictionary dictionaryWithObjectsAndKeys:detlabel.font,NSFontAttributeName,nil] context:nil].size;
    return contentactually;
}

```

这里的label需要根据屏幕的尺寸来进行调节所以设置成了屏幕宽度减去16。
第二个是这个label最大能达到的高度，所以你要尽量的设置大一些。

CGSizeMake(300,MAXFLOAT),是计算宽和高的,里面的MAXFLOAT通俗点说就是最大的数值,代表你的label的宽和高是随着你label内容变化而变化,不用担心因为label内容过场而现实不全。