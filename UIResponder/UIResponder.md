# UIResponder

在iOS中UIResponder类是专门用来响应用户的操作处理各种事件的，包括触摸事件(Touch Events)、运动事件(Motion Events)、远程控制事件(Remote Control Events)。我们知道UIApplication、UIView、UIViewController这几个类是直接继承自UIResponder,所以这些类都可以响应事件。当然我们自定义的继承自UIView的View以及自定义的继承自UIViewController的控制器都可以响应事件。本文将详细介绍UIResponder类。

## 一、使用详解

### 1.通过响应者链查找视图的视图控制器

``` Objective-C
/**
 *  查找视图的视图控制器
 *
 *  @param view 视图
 *
 *  @return 返回视图的控制器
 */
- (UIViewController *)getControllerFromView:(UIView *)view {
    // 遍历响应者链。返回第一个找到视图控制器
    UIResponder *responder = view;
    while ((responder = [responder nextResponder])){
        if ([responder isKindOfClass: [UIViewController class]]){
            return (UIViewController *)responder;
        }
    }
    // 如果没有找到则返回nil
    return nil;
}

```

### 2.设置与取消第一响应者

``` Objective-C

//
//  FirstResponderView.m
//  UIResponder-Demo
//
//  Created by 王潇 on 2021/3/3.
//

#import "FirstResponderView.h"

@implementation FirstResponderView

/** 演示设置为第一响应者 */
- (void)setBecomeFirstResponder {
    //  判断对象是否已经是第一响应者
    if ([self isFirstResponder]) {
        return;
    }
    //  判断对象是否允许成为第一响应者
    if ([self canBecomeFirstResponder]) {
        //  设置第一响应者
        [self becomeFirstResponder];
    }
}

/** 演示放弃第一响应者 */
- (void)setResignFirstResponder {
    //  判断对象是否不是第一响应者
    if (![self isFirstResponder]) {
        return;
    }
    //  判断对象是否允许放弃第一响应者
    if ([self canResignFirstResponder]) {
        //  设置放弃第一响应者
        [self resignFirstResponder];
    }
}

/** 重写方法,允许对象成为第一响应者 */
- (BOOL)canBecomeFirstResponder {
    return YES;
}

@end

```

UIView默认不允许设置为第一响应者,因此设置UIView为第一响应者需要重写canBecomeFirstResponder方法并返回YES。设置为第一响应者后，对象则可以接受远程控制事件进行处理(如耳机线控)。UITextField、UITextView成为第一响应者后会弹出输入键盘，取消第一响应者则会隐藏输入键盘。

### 3.触摸相关方法，一般用于响应屏幕触摸

``` Objective-C

/** 手指按下时响应 */
- (void)touchesBegan:(NSSet<UITouch *> *)touches withEvent:(UIEvent *)event {
    [super touchesBegan:touches withEvent:event];
    NSLog(@"--->手指按下时响应");
}

/** 手指移动时响应 */
- (void)touchesMoved:(NSSet<UITouch *> *)touches withEvent:(UIEvent *)event {
    [super touchesMoved:touches withEvent:event];
    NSLog(@"--->手指移动时响应");
}

/** 手指抬起时响应 */
- (void)touchesEnded:(NSSet<UITouch *> *)touches withEvent:(UIEvent *)event {
    [super touchesEnded:touches withEvent:event];
    NSLog(@"--->手指抬起时响应");
}

/** 触摸取消(意外中断，如:电话，Home键退出等) */
- (void)touchesCancelled:(NSSet<UITouch *> *)touches withEvent:(UIEvent *)event {
    [super touchesCancelled:touches withEvent:event];
    NSLog(@"--->取消触摸响应");
}

```

### 4.加速相关方法

``` Objective-C

/** 开始加速 */
- (void)motionBegan:(UIEventSubtype)motion withEvent:(UIEvent *)event {
    [super motionBegan:motion withEvent:event];
    NSLog(@"--->开始加速");
}

/** 结束加速 */
- (void)motionEnded:(UIEventSubtype)motion withEvent:(UIEvent *)event {
    [super motionEnded:motion withEvent:event];
    NSLog(@"--->结束加速");
}

/** 加速取消 (取消中断, 如:电话,Home键退出等) */
- (void)motionCancelled:(UIEventSubtype)motion withEvent:(UIEvent *)event {
    [super motionCancelled:motion withEvent:event];
    NSLog(@"--->加速取消");
}

```

### 5.远程控制方法，一般用于耳机线控

``` Objective-C

//
//  AudioView.m
//  UIResponder-Demo
//
//  Created by 王潇 on 2021/3/3.
//

#import "AudioView.h"
#import <AVFoundation/AVFoundation.h>

@implementation AudioView

- (instancetype)initWithFrame:(CGRect)frame
{
    self = [super initWithFrame:frame];
    if (self) {
        //  启动接受远程事件
        [[UIApplication sharedApplication] beginReceivingRemoteControlEvents];
        //  设置成为第一响应者
        [self becomeFirstResponder];
        //  播放一段静音文件，使APP获取音频的控制权
        NSURL *audioURL = [NSURL fileURLWithPath:[[NSBundle mainBundle] pathForResource:@"mute_60s" ofType:@"mp3"]];
        AVAudioPlayer *audioPlayer = [[AVAudioPlayer alloc] initWithContentsOfURL:audioURL error:nil];
        [audioPlayer play];
    }
    return self;
}

/** 允许对象成为第一响应者 */
- (BOOL)canBecomeFirstResponder {
    return YES;
}

/** 远程控制事件响应 */
- (void)remoteControlReceivedWithEvent:(UIEvent *)event {
    NSLog(@"--->耳机线控响应");
}

- (void)dealloc {
    //  停止接受远程事件
    [[UIApplication sharedApplication] endReceivingRemoteControlEvents];
    //  放弃第一响应者
    [self resignFirstResponder];
}

@end

```

耳机线控要注意三点要素:
(1)启动接受远程事件:[[UIApplication sharedApplication] beginReceivingRemoteControlEvents];
(2)设置成为第一响应者 (UIViewController,AppDelegate中不需要设置)

``` Objective-C

//	设置成为第一响应者
[self becomeFirstResponder];

/** 允许对象成为第一响应者 */
- (BOOL)canBecomeFirstResponder {
	return YES;
}

```

(3)获取音频的控制权

``` Objective-C

//	播放一段静音文件，使APP获取音频的控制权
NSURL *audioURL = [NSURL fileURLWithPath: [[NSBundle mainBundle] pathForResource: @"mute_60s" ofType: @"mp3"]];
AVAudioPlayer *audioPlayer = [[AVAudioPlayer alloc] initWithContentsOfURL: audioURL error: nil];
[audioPlayer play];

```

### 6.在UILabel中实现长按菜单(复制、粘贴等)

``` Objective-C

//
//  MenuLabel.m
//  UIResponder-Demo
//
//  Created by 王潇 on 2021/3/3.
//

#import "MenuLabel.h"

@implementation MenuLabel

- (instancetype)initWithFrame:(CGRect)frame
{
    self = [super initWithFrame:frame];
    if (self) {
        //  启用用户交互
        self.userInteractionEnabled = YES;
        //  添加长按手势
        UILongPressGestureRecognizer *longPressGesture = [[UILongPressGestureRecognizer alloc] initWithTarget:self action:@selector(longPressMenu:)];
        longPressGesture.minimumPressDuration = 0.2;
        [self addGestureRecognizer:longPressGesture];
    }
    return self;
}

/** 允许对象成为第一响应者 */
- (BOOL)canBecomeFirstResponder {
    return YES;
}

/** 长按响应 */
- (void)longPressMenu: (UILongPressGestureRecognizer *)sender {
    if (sender.state == UIGestureRecognizerStateBegan) {
        //  设置成为第一响应者
        [self becomeFirstResponder];
        //  显示菜单
        UIMenuController *menuCtrl = [UIMenuController sharedMenuController];
        [menuCtrl setTargetRect:self.frame inView:self.superview];
        [menuCtrl setMenuVisible:YES animated:YES];
    }
}

/** 返回需要显示的菜单按钮 */
- (BOOL)canPerformAction:(SEL)action withSender:(id)sender {
    //  只显示复制、粘贴按钮
    if (action == @selector(copy:) || action == @selector(paste:)) {
        return YES;
    }
    return NO;
}

/** 实现复制方法 */
- (void)copy:(id)sender {
    UIPasteboard *paste = [UIPasteboard generalPasteboard];
    paste.string = self.text;
}

/** 实现粘贴方法 */
- (void)paste:(id)sender {
    UIPasteboard *paste = [UIPasteboard generalPasteboard];
    self.text = paste.string;
}

@end

```

为UILabel添加长按菜单需要注意几点：
(1)启用用户交互: self.userInteractionEnabled = YES;
(2)在显示菜单之前设置对象成为第一响应者(UIViewController,AppDelegate中不需要设置)

``` Objective-C

/** 允许对象成为第一响应者 */
- (BOOL)canBecomeFirstResponder {
	return YES;
}

//	设置成为第一响应者
[self becomeFirstResponder];

```

(3)返回菜单需要显示的按钮,并重写实现对应方法

``` Objective-C

/** 返回需要显示的菜单按钮 */
- (BOOL)canPerformAction:(SEL)action withSender:(id)sender {
    //  只显示复制、粘贴按钮
    if (action == @selector(copy:) || action == @selector(paste:)) {
        return YES;
    }
    return NO;
}

/** 实现复制方法 */
- (void)copy:(id)sender {
    UIPasteboard *paste = [UIPasteboard generalPasteboard];
    paste.string = self.text;
}

/** 实现粘贴方法 */
- (void)paste:(id)sender {
    UIPasteboard *paste = [UIPasteboard generalPasteboard];
    self.text = paste.string;
}

```

(4)注册长按手势，显示菜单

``` Objective-C

//  添加长按手势
        UILongPressGestureRecognizer *longPressGesture = [[UILongPressGestureRecognizer alloc] initWithTarget:self action:@selector(longPressMenu:)];
        longPressGesture.minimumPressDuration = 0.2;
        [self addGestureRecognizer:longPressGesture];

/** 长按响应 */
- (void)longPressMenu: (UILongPressGestureRecognizer *)sender {
    if (sender.state == UIGestureRecognizerStateBegan) {
        //  设置成为第一响应者
        [self becomeFirstResponder];
        //  显示菜单
        UIMenuController *menuCtrl = [UIMenuController sharedMenuController];
        [menuCtrl setTargetRect:self.frame inView:self.superview];
        [menuCtrl setMenuVisible:YES animated:YES];
    }
}

```

### 7.使用NSUndoManager实现画板撤销/重做功能

``` Objective-C 

//  DrawingBoardView.h
//  UIResponder-Demo
//
//  Created by 王潇 on 2021/3/3.
//

#import <UIKit/UIKit.h>

NS_ASSUME_NONNULL_BEGIN

/** 画板View */

@interface DrawingBoardView : UIView

@end

/** 划线Model */
@interface LineModel : NSObject

@property (nonatomic) CGPoint begin;
@property (nonatomic) CGPoint end;

@end

NS_ASSUME_NONNULL_END

```

``` Objective-C

//
//  DrawingBoardView.m
//  UIResponder-Demo
//
//  Created by 王潇 on 2021/3/3.
//

#import "DrawingBoardView.h"

/** 画板View */
@interface DrawingBoardView()

@property (nonatomic, strong) LineModel *currentLine;
@property (nonatomic, strong) NSMutableArray<LineModel *> *touchArray;

@end

@implementation LineModel

@end

@implementation DrawingBoardView

- (instancetype)initWithFrame:(CGRect)frame
{
    self = [super initWithFrame:frame];
    if (self) {
        [self initSubView];
        self.backgroundColor = [UIColor whiteColor];
        self.touchArray = [NSMutableArray array];
    }
    return self;
}

- (void)drawRect:(CGRect)rect {
    //  获得上下文
    CGContextRef context = UIGraphicsGetCurrentContext();
    //  设置样式
    CGContextSetLineCap(context, kCGLineCapSquare);
    //  设置宽度
    CGContextSetLineWidth(context, 5.0);
    //  设置颜色
    CGContextSetStrokeColorWithColor(context, [[UIColor redColor] CGColor]);
    
    for (LineModel *line in self.touchArray) {
        //  开始绘制
        CGContextBeginPath(context);
        //  移动画笔到起点
        CGContextMoveToPoint(context, line.begin.x, line.begin.y);
        //  添加下一点
        CGContextAddLineToPoint(context, line.end.x, line.end.y);
        //  绘制完成
        CGContextStrokePath(context);
    }
}

/** 划线开始 */
- (void)touchesBegan:(NSSet<UITouch *> *)touches withEvent:(UIEvent *)event {
    //  标记开始撤销分组
    [self.undoManager beginUndoGrouping];
    
    for (UITouch *touch in touches) {
        //  记录起始点
        CGPoint locTouch = [touch locationInView:self];
        _currentLine = [[LineModel alloc] init];
        _currentLine.begin = locTouch;
        _currentLine.end = locTouch;
    }
}

/** 划线结束 */
- (void)touchesEnded:(NSSet<UITouch *> *)touches withEvent:(UIEvent *)event {
    //  结束标记撤销分组
    [self.undoManager endUndoGrouping];
}

/** 添加划线 */
- (void)addLine: (LineModel *)line {
    //  添加划线并重绘画板
    [self.touchArray addObject:line];
    [self setNeedsDisplay];
    //  注册撤销方法
    [[self.undoManager prepareWithInvocationTarget:self] removeLine:line];
}

/** 移除划线 */
- (void)removeLine: (LineModel *)line {
    if ([self.touchArray containsObject:line]) {
        //  移除划线并重绘画板
        [self.touchArray removeObject:line];
        [self setNeedsDisplay];
        //  注册撤销方法
        [[self.undoManager prepareWithInvocationTarget:self] addLine:line];
    }
}

/** 撤销按钮点击响应 */
- (void)undoButtonAction: (id)sender {
    if ([self.undoManager canUndo]) {
        [self.undoManager undo];
    }
}

/** 重做按钮点击响应 */
- (void)redoButtonAction: (id)sender {
    if ([self.undoManager canRedo]) {
        [self.undoManager redo];
    }
}

/** 初始化子控件 */
- (void)initSubView {
    //  撤销按钮
    UIButton *undoButton = [UIButton buttonWithType:UIButtonTypeSystem];
    undoButton.frame = CGRectMake(0, 64, 70, 50);
    [undoButton setTitle:@"uodo撤销" forState:UIControlStateNormal];
    [undoButton sizeToFit];
    [undoButton addTarget:self action:@selector(undoButtonAction:) forControlEvents:UIControlEventTouchUpInside];
    [self addSubview:undoButton];
    //  重做按钮
    UIButton *redoButton = [UIButton buttonWithType:UIButtonTypeSystem];
    redoButton.frame = CGRectMake(CGRectGetWidth(self.frame)-70, 64, 70, 50);
    [redoButton setTitle:@"redo重做" forState:UIControlStateNormal];
    [redoButton sizeToFit];
    [redoButton addTarget:self action:@selector(redoButtonAction:) forControlEvents:UIControlEventTouchUpInside];
    [self addSubview: redoButton];
}

@end

```

实现撤销/重做注意以下几点:
(1)在调用方法时需要添加注册一个对应的撤销方法

``` Objective-C

//	注册撤销方法
[[self.undoManager prepareWithInvocationTarget:self] removeLine: line];

```

(2)撤销/重做只需要调用undoManager中的相应方法即可

``` Objective-C

/** 撤销按钮点击响应 */
- (void)undoButtonAction:(id)sender {
    if ([self.undoManager canUndo]) {
        [self.undoManager undo];
    }
}
 
/** 重做按钮点击响应 */
- (void)redoButtonAction:(id)sender {
    if ([self.undoManager canRedo]) {
        [self.undoManager redo];
    }
}

```

(3)如果需要多个动作一起撤销则需要标记分组

``` Objective-C

    // 标记开始撤销分组
    [self.undoManager beginUndoGrouping];
    // 结束标记撤销分组
    [self.undoManager endUndoGrouping];

```

### 8.自定义快捷键

``` Objective-C

//
//  KeyCommandView.m
//  UIResponder-Demo
//
//  Created by 王潇 on 2021/3/3.
//

#import "KeyCommandView.h"

@implementation KeyCommandView

- (instancetype)initWithFrame:(CGRect)frame
{
    self = [super initWithFrame:frame];
    if (self) {
        //  设置成为第一响应者
        [self becomeFirstResponder];
    }
    return self;
}

/** 允许对象成为第一响应者 */
- (BOOL)canBecomeFirstResponder {
    return YES;
}

/** 返回快捷命令数组 */
- (NSArray<UIKeyCommand *>*)keyCommands {
    return @[
        [UIKeyCommand keyCommandWithInput:UIKeyInputEscape modifierFlags:UIKeyModifierShift action:@selector(pressedShiftAndEscapeKey:) discoverabilityTitle:@"自定义[shift+ESC]快捷键"],
    [UIKeyCommand keyCommandWithInput:@"a" modifierFlags:UIKeyModifierShift action:@selector(pressedShiftAndAKey:) discoverabilityTitle:@"自定义[Shift+A]快捷键"]
    ];
}


/** Shift+Esc快捷命令响应 */
-(void)pressedShiftAndEscapeKey:(UIKeyCommand *)keyCommand {
    UIAlertView *alertView = [[UIAlertView alloc] initWithTitle:keyCommand.discoverabilityTitle message:[NSString stringWithFormat:@"按下快捷辅键:[%@]", keyCommand.input] delegate:nil cancelButtonTitle:@"确定" otherButtonTitles:nil];
    [alertView show];
}
 
/** Shift+A快捷命令响应 */
-(void)pressedShiftAndAKey:(UIKeyCommand *)keyCommand {
    UIAlertView *alertView = [[UIAlertView alloc] initWithTitle:keyCommand.discoverabilityTitle message:[NSString stringWithFormat:@"按下快捷辅键:[%@]", keyCommand.input] delegate:nil cancelButtonTitle:@"确定" otherButtonTitles:nil];
    [alertView show];
}

@end

```

自定义快捷键需要注意两点:

(1)设置对象成为第一响应者(UIViewController，AppDelegate中不需要设置)

``` Objective-C

// 设置成为第一响应者
[self becomeFirstResponder];
 
/** 允许对象成为第一响应者 */
- (BOOL)canBecomeFirstResponder {
    return YES;
}

```

(2)重写keyCommands

``` Objective-C

/** 返回快捷命令数组 */
-(NSArray<UIKeyCommand *> *)keyCommands {
    return @[
             [UIKeyCommand keyCommandWithInput:UIKeyInputEscape modifierFlags:UIKeyModifierShift action:@selector(pressedShiftAndEscapeKey:) discoverabilityTitle:@"自定义[Shift+Esc]快捷键"],
             [UIKeyCommand keyCommandWithInput:@"a" modifierFlags:UIKeyModifierShift action:@selector(pressedShiftAndAKey:) discoverabilityTitle:@"自定义[Shift+A]快捷键"]
             ];
}

```

### 9.自定义UITextField输入键盘

``` Objective-C

//
//  CustomInputView.m
//  UIResponder-Demo
//
//  Created by 王潇 on 2021/3/3.
//

#import "CustomInputView.h"

#define MAIN_SCREEN_WIDTH [[UIScreen mainScreen] bounds].size.width  //  屏幕的width

@interface CustomInputView()

@property (nonatomic, strong) UITextField *textField;
@property (nonatomic, strong) UIView *customInputView;
@property (nonatomic, strong) UIToolbar *customAccessoryView;

@end

@implementation CustomInputView

- (instancetype)initWithFrame:(CGRect)frame
{
    self = [super initWithFrame:frame];
    if (self) {
        //  添加TextField
        [self addSubview: self.textField];
    }
    return self;
}

/** 懒加载textField */
- (UITextField *)textField {
    if (!_textField) {
        //  初始化textField
        _textField = [[UITextField alloc] initWithFrame:CGRectMake(50, 100, MAIN_SCREEN_WIDTH - 100, 30)];
        _textField.borderStyle = UITextBorderStyleRoundedRect;
        _textField.placeholder = @"测试";
        //  设置自定义键盘View
        _textField.inputView = self.customInputView;
        _textField.inputAccessoryView = self.customAccessoryView;
    }
    return _textField;
}

/** 懒加载customInputView */
- (UIView *)customInputView {
    if (_customInputView) {
        _customInputView = [[UIView alloc]initWithFrame:CGRectMake(0, 0, MAIN_SCREEN_WIDTH, 220)];
        _customInputView.backgroundColor = [UIColor lightGrayColor];
        UILabel *label = [[UILabel alloc] initWithFrame:CGRectMake(0, 100, MAIN_SCREEN_WIDTH, 40)];
        label.textAlignment = NSTextAlignmentCenter;
        label.text = @"自定义inputView";
        [_customInputView addSubview:label];
    }
    return _customInputView;
}

/** 懒加载customAccessoryView */
- (UIToolbar *)customAccessoryView {
    if (!_customAccessoryView) {
        _customAccessoryView = [[UIToolbar alloc]initWithFrame:CGRectMake(0, 0, MAIN_SCREEN_WIDTH, 40)];
        _customAccessoryView.barTintColor = [UIColor orangeColor];
        UIBarButtonItem *space = [[UIBarButtonItem alloc] initWithBarButtonSystemItem:UIBarButtonSystemItemFlexibleSpace target:self action:nil];
        UIBarButtonItem *done = [[UIBarButtonItem alloc] initWithTitle:@"完成" style:UIBarButtonItemStyleDone target:self action:@selector(done)];
        [_customAccessoryView setItems:@[space, space, done]];
    }
    return _customAccessoryView;
}

/** 响应完成按钮 */
- (void)done {
    [self.textField resignFirstResponder];
}

@end

```