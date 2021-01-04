# iOS-layer设置阴影

## 第一种通过layer直接设置

``` Objective-C

self.view.backgroundColor = [UIColor colorWithRed:128/255.0 green:138/255.0 blue:135/255.0 alpha:1.0];
    
UIView *view = [[UIView alloc] initWithFrame:CGRectMake((self.view.frame.size.width - 50)/2, (self.view.frame.size.height-50)/2, 50, 50)];
    
[self.view addSubview:view];
    
view.backgroundColor = [UIColor redColor];
view.layer.masksToBounds =YES;
view.layer.shadowRadius = 8;
view.layer.shadowOffset = CGSizeMake(0, 2);
view.layer.shadowColor = [UIColor colorWithRed:42/255.0 green:47/255.0 blue:59/255.0 alpha:0.3].CGColor;
view.layer.shadowOpacity = 0.5;
view.layer.cornerRadius = 5;

```

## 第二种路径阴影

``` Objective-C

UIView *pathView = [[UIView alloc] initWithFrame:CGRectMake((self.view.frame.size.width - 50)/2, (self.view.frame.size.height-50)/2+150, 50, 50)];
    
pathView.layer.shadowColor = [UIColor yellowColor].CGColor;//   shadowColor阴影颜色
pathView.layer.shadowOffset = CGSizeMake(0, 0);  //  shadowOffset阴影偏移，默认(0, -3)，这个跟shadowRadius配合使用
pathView.layer.shadowOpacity = 1;// 阴影透明度,默认为0
pathView.layer.shadowRadius = 3;//  阴影半径，默认3
    
pathView.backgroundColor = [UIColor greenColor];
    
    UIBezierPath *path = [UIBezierPath bezierPath]; float width = pathView.bounds.size.width;
float height = pathView.bounds.size.height;
float x = pathView.bounds.origin.x;
float y = pathView.bounds.origin.y;
float addWH = 10;
    
CGPoint topLeft = pathView.bounds.origin;
CGPoint topMiddle = CGPointMake(x+(width/2), y-addWH);
CGPoint topRight = CGPointMake(x+width, y);
    
CGPoint rightMiddle = CGPointMake(x+width+addWH, y+(height/2));
    
CGPoint bottomRight = CGPointMake(x+width, y+height);
CGPoint bottomMiddle = CGPointMake(x+(width/2), y+height+addWH);
CGPoint bottomLeft = CGPointMake(x,  y+height);
    
CGPoint leftMiddle = CGPointMake(x-addWH, y+(height/2));
    
[path moveToPoint: topLeft];
    
//  添加四个二次元曲线

[path addQuadCurveToPoint:topRight controlPoint:topMiddle];
[path addQuadCurveToPoint:bottomRight controlPoint: rightMiddle];
[path addQuadCurveToPoint:bottomLeft controlPoint:bottomMiddle];
[path addQuadCurveToPoint:topLeft controlPoint:leftMiddle];
    
//  设置阴影路径
    
pathView.layer.shadowPath = path.CGPath;
[self.view addSubview:pathView];

```