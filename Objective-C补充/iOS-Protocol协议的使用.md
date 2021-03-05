# iOS-Protocol协议的使用

## 说明

1. 协议声明了可以被任何类实现的方法
2. 协议不是类,它是定义了一个其他对象可以实现的接口
3. 如果在某个类中实现了协议中的某个方法，也就是这个类实现了那个协议。
4. 协议经常用来实现委托对象。一个委托对象是一种用来协同或者代表其他对象的特殊对象。
5. 委托，就是调用自己定义的方法，别的类来实现。
6. 新特性说明
@optional预编译指令:表示可以选择实现的方法。
@required预编译指令:表示必须强制实现的方法。

## 定义协议

``` Objective-C
#import <Foundation/Foundation.h>

NS_ASSUME_NONNULL_BEGIN

@protocol dataProtocol <NSObject>

@required
- (NSString *)sendName;
- (NSString *)sendAge;

@optional
- (NSString *)sendPhone;

@end

NS_ASSUME_NONNULL_END

```

## 例子

### sendViewController.m

``` Objective-C

#import "dataProtocol.h"
#import "SendViewController.h"
#import "sendUITextField.h"
#import "ReceiveViewController.h"

@property (strong, nonatomic) sendUITextField *nameTextField;
@property (strong, nonatomic) sendUITextField *ageTextField;
@property (strong, nonatomic) sendUITextField *phoneTextField;
@property (strong, nonatomic) UIButton *sendButton;

- (void)touchesBegan:(NSSet<UITouch *> *)touches withEvent:(UIEvent *)event {
    [self.view endEditing:YES];
}

- (void)sendMessage{
    ReceiveViewController *receiveVC = [[ReceiveViewController alloc] init];
    receiveVC.delegate = (id)self;
    [self.navigationController pushViewController:receiveVC animated:YES];
}

#pragma mark DataProtocol

- (NSString *)sendName{
    return _nameTextField.text;
}

- (NSString *)sendAge{
    return _ageTextField.text;
}

- (NSString *)sendPhone{
    return _phoneTextField.text;
}

```


### ReceiveViewController.m

``` Objective-C

#import "ReceiveViewController.h"
#import "ReceiveLabel.h"
#import <Masonry/Masonry.h>

@interface ReceiveViewController ()

@property (nonatomic, strong) ReceiveLabel* nameLabel;
@property (nonatomic, strong) ReceiveLabel* ageLabel;
@property (nonatomic, strong) ReceiveLabel* phoneLabel;

@end

- (void)viewDidLoad {
    [super viewDidLoad];
@implementation ReceiveViewController
@synthesize delegate = _delegate;

    self.nameLabel.text = [_delegate sendName];
    self.ageLabel.text = [_delegate sendAge];
    self.phoneLabel.text = [_delegate sendPhone];
}

```