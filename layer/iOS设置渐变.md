# iOS设置渐变

## CAGradientLayer实现渐变

``` objective-c
//	渐变器
CAGradientLayer *gradient = [CAGradientLayer layer];
gradient.frame = self.view.bounds;
gradient.colors = [NSMutableArray arrayWithObjects:(id)[UIColor colorWithRed:250/255.0 green:94/255.0 blue:99/255.0 alpha:1].CGColor,(id)[UIColor colorWithRed:227/255.0 green:40/255.0 blue:117/255.0 alpha:1].CGColor,nil];

//	渐变
gradient.startPoint = CGPointMake(0, 0);
gradient.endPoint = CGPointMake(0, 1);
[self.view.layer insertSublayer: gradient atIndex:0];
```

### 相关属性

1. colors： 渐变的颜色。
2. locations： 渐变颜色的分割点。
3. startPoint&endPoint：颜色渐变的方向，范围在(0, 0)与(1.0, 1.0)之间，如(0, 0)(1.0, 0)代表水平方向渐变，(0, 0)(0, 1.0)代表竖直方向渐变。

## Core Graphics相关方法实现渐变

### CGContextDrawLinearGradient(线性渐变)

``` objective-c
#import "ViewController.h"

@interface ViewController ()

@end

@implementation ViewController

-(void)drawLinearGradient:(CGContextRef)context path:(CGPathRef)path startColor:(CGColorRef)startColor endColor:(CGColorRef)endColor
{
    CGColorSpaceRef colorSpace = CGColorSpaceCreateDeviceRGB();
    CGFloat locations[] = {0.0, 1.0};
    
    NSArray *colors = @[(__bridge id)startColor, (__bridge id)endColor];
    CGGradientRef gradient = CGGradientCreateWithColors(colorSpace, (__bridge CFArrayRef)colors, locations);
    CGRect pathRect = CGPathGetBoundingBox(path);
    
    //具体方向可根据需求修改
    CGPoint startPoint = CGPointMake(CGRectGetMinX(pathRect), CGRectGetMidY(pathRect));
    CGPoint endPoint = CGPointMake(CGRectGetMaxX(pathRect), CGRectGetMidY(pathRect));
    
    CGContextSaveGState(context);
    CGContextAddPath(context, path);
    CGContextClip(context);
    CGContextDrawLinearGradient(context, gradient, startPoint, endPoint, 0);
    CGContextRestoreGState(context);
    
    CGGradientRelease(gradient);
    CGColorSpaceRelease(colorSpace);
}

- (void)viewDidLoad {
    [super viewDidLoad];
    // Do any additional setup after loading the view.
    
    //  创建CGContextRef
    UIGraphicsBeginImageContext(self.view.bounds.size);
    CGContextRef gc = UIGraphicsGetCurrentContext();
    
    //  创建CGMutablePathRef
    CGMutablePathRef path = CGPathCreateMutable();
    
    //  绘制Path
    CGRect rect = CGRectMake(0, 100, 300, 200);
    CGPathMoveToPoint(path, NULL, CGRectGetMinX(rect), CGRectGetMinY(rect));
    CGPathAddLineToPoint(path, NULL, CGRectGetMidX(rect), CGRectGetMaxY(rect));
    CGPathAddLineToPoint(path, NULL, CGRectGetWidth(rect), CGRectGetMaxY(rect));
    CGPathCloseSubpath(path);
    
    //  绘制渐变
    [self drawLinearGradient:gc path:path startColor:[UIColor greenColor].CGColor endColor:[UIColor redColor].CGColor];
    
    //  注意释放CGMutablePathRef
    CGPathRelease(path);
    
    //  从Context中获取图像，并显示在界面上
    UIImage *img = UIGraphicsGetImageFromCurrentImageContext();
    UIGraphicsEndImageContext();
    
    UIImage *imgView = [[UIImageView alloc]initWithImage:img];
    [self.view addSubview:imgView];
    
}

@end
```

### CGContextDrawRadialGradient(圆半径方向颜色渐变)

``` objective-c
- (void)drawRadialGradient:(CGContextRef)context
                      path:(CGPathRef)path
                startColor:(CGColorRef)startColor
                  endColor:(CGColorRef)endColor
{
    CGColorSpaceRef colorSpace = CGColorSpaceCreateDeviceRGB();
    CGFloat locations[] = { 0.0, 1.0 };
    
    NSArray *colors = @[(__bridge id) startColor, (__bridge id) endColor];
    
    CGGradientRef gradient = CGGradientCreateWithColors(colorSpace, (__bridge CFArrayRef) colors, locations);
    
    
    CGRect pathRect = CGPathGetBoundingBox(path);
    CGPoint center = CGPointMake(CGRectGetMidX(pathRect), CGRectGetMidY(pathRect));
    CGFloat radius = MAX(pathRect.size.width / 2.0, pathRect.size.height / 2.0) * sqrt(2);
    
    CGContextSaveGState(context);
    CGContextAddPath(context, path);
    CGContextEOClip(context);
    
    CGContextDrawRadialGradient(context, gradient, center, 0, center, radius, 0);
    
    CGContextRestoreGState(context);
    
    CGGradientRelease(gradient);
    CGColorSpaceRelease(colorSpace);
}

- (void)viewDidLoad 
{
    [super viewDidLoad];
    // Do any additional setup after loading the view.
    
    //创建CGContextRef
    UIGraphicsBeginImageContext(self.view.bounds.size);
    CGContextRef gc = UIGraphicsGetCurrentContext();
    
    //创建CGMutablePathRef
    CGMutablePathRef path = CGPathCreateMutable();
    
    //绘制Path
    CGRect rect = CGRectMake(0, 100, 300, 200);
    CGPathMoveToPoint(path, NULL, CGRectGetMinX(rect), CGRectGetMinY(rect));
    CGPathAddLineToPoint(path, NULL, CGRectGetMidX(rect), CGRectGetMaxY(rect));
    CGPathAddLineToPoint(path, NULL, CGRectGetWidth(rect), CGRectGetMaxY(rect));
    CGPathAddLineToPoint(path, NULL, CGRectGetWidth(rect), CGRectGetMinY(rect));
    CGPathCloseSubpath(path);
    
    //绘制渐变
    [self drawRadialGradient:gc path:path startColor:[UIColor greenColor].CGColor endColor:[UIColor redColor].CGColor];
    
    //注意释放CGMutablePathRef
    CGPathRelease(path);
    
    //从Context中获取图像，并显示在界面上
    UIImage *img = UIGraphicsGetImageFromCurrentImageContext();
    UIGraphicsEndImageContext();
    
    UIImageView *imgView = [[UIImageView alloc] initWithImage:img];
    [self.view addSubview:imgView];
}
```

### CAShapeLayer作为layer的mask属性

CALayer的mask属性可以作为遮罩让layer显示mask遮住(非透明)的部分;CAShapeLayer为CALayer的子类，通过path属性可以生成不同的形状，将CAShapeLayer对象用作layer的mask属性的话，可以生成不同形的图层。故生成颜色渐变有以下几个步骤

1. 生成一个imageView(也可以为layer)，image的属性为颜色渐变的图片
2. 生成一个CAShapeLayer对象，根据path属性指定所需的形状
3. 将CAShapeLayer对象赋值给imageView的mask属性
