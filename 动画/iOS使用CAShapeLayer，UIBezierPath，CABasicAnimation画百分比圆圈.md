# iOS使用CAShapeLayer，UIBezierPath，CABasicAnimation画百分比圆圈

## 普通的用法(学习)

``` Objective-C

- (void)viewDidLoad {
	[super viewDidLoad];
	
	CAShapeLayer *shapeLayer = [CAShapeLayer layer];
	shapeLayer.frame = CGRectMake(50, 50, 150, 150);
	shapeLayer.strokeEnd = 1.0f;
	shapeLayer.strokeStart = 0.0f;
	shapeLayer.lineWidth = 10;	//	设置线宽
	shapeLayer.lineCap = kCALineCapRound;	//	设置线头形状
	UIBezierPath *path = [UIBezierPath bezierPathWithOvalInRect:shapeLayer.frame];
	shapeLayer.path = path.CGPath;
	shapeLayer.fillColor = [UIColor clearColor].CGColor;
	shapeLayer.strokeColor = [UIColor redColor].CGColor;
	shapeLayer.fillRule = kCAFillRuleEvenOdd;	//	重点，填充规则
	
	CABasicAnimation *pathAnima = [CABasicAnimation animationWithKeyPath:@"strokeEnd"];
	pathAnima.duration = 10.0f;	//	动画时间
	pathAnima.timingFunction = [CAMediaTimingFunction functionWithName:kCAMediaTimingFunctionLinear];
	pathAnima.fromValue = [NSNumer numberWithFloat: 0.0f];	//	值开始
	pathAnima.toValue = [NSNumber numberWithFloat: 1.0f];	//	值结束
	pathAnima.fillMode = KCAFillModeBoth;	//	填充方式
	pathAnima.removedOnCompletion = NO;	//	完成后是否删除动画
	[shapeLayer addAnimation:pathAnima forKey:@"strokeEndAnimation"];
	[self.view.layer addSublayer:shapeLayer];
}

```

## 画圆弧

``` Objective-C
@interface LoadingView()<CAAnimationDelegate>

//  固定的圆圈 Path
@property (nonatomic, strong) UIBezierPath *trackPath;
//  固定的圆圈 Layer
@property (nonatomic, strong) CAShapeLayer *trackLayer;
//  可动的圆圈 Path
@property (nonatomic, strong) UIBezierPath *progressPath;
//  可动的圆圈 Layer
@property (nonatomic, strong) CAShapeLayer *progressLayer;
//  路径动画
@property (nonatomic, strong) CABasicAnimation *pathAnimation;

//  画两个圆形
- (void)startProgressAction:(CGRect)mybound;

@end

@implementation LoadingView

- (void)startProgressAction:(CGRect)mybound {
    //  固定的圆圈
    _trackPath = [UIBezierPath bezierPathWithArcCenter:self.center radius:(mybound.size.width - 2) / 2 startAngle:0 endAngle:M_PI*2 clockwise:YES];
    _trackLayer = [CAShapeLayer new];
    [self.layer addSublayer:_trackLayer];
    _trackLayer.fillColor = nil;
    _trackLayer.strokeColor = [UIColor grayColor].CGColor;
    _trackLayer.path = _trackPath.CGPath;
    _trackLayer.lineWidth = 4;
    _trackLayer.frame = mybound;
    
    //  可动的圆圈
    _progressPath = [UIBezierPath bezierPathWithArcCenter:self.center radius:(mybound.size.width - 2) / 2 startAngle:- M_PI_2 endAngle:(M_PI * 2) - M_PI_2 clockwise:YES];
    _progressLayer = [CAShapeLayer new];
    [self.layer addSublayer:_progressLayer];
    _progressLayer.fillColor = nil;
    _progressLayer.strokeColor = [UIColor redColor].CGColor;
    _progressLayer.lineCap = kCALineCapRound;
    _progressLayer.path = _progressPath.CGPath;
    _progressLayer.lineWidth = 4;
    _progressLayer.frame = mybound;
    _progressLayer.strokeEnd = 1;
    _progressLayer.strokeStart = 0;
}

- (void)updatePressPathStartVal:(CGFloat)startValue updatePressPathEndVal:(CGFloat)endValue {
    //  总的过渡时间
    CGFloat totalDuration = 5.0;
    //  当前动画所需要的时间
    CGFloat currentDuration = 0.0;
    currentDuration = (endValue - startValue) * totalDuration;
    self.pathAnimation.duration = currentDuration;
    self.pathAnimation.timingFunction = [CAMediaTimingFunction functionWithName:kCAMediaTimingFunctionLinear];
    self.pathAnimation.fromValue = [NSNumber numberWithFloat:startValue];
    self.pathAnimation.toValue = [NSNumber numberWithFloat:endValue];
    self.pathAnimation.fillMode = kCAFillModeBoth;
    self.pathAnimation.removedOnCompletion = NO;
    [self.progressLayer addAnimation:self.pathAnimation forKey:@"strokeEndAnimation"];
    self.progess = endValue;
}

@end

```