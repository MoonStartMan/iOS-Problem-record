# iOS-Problem-record

<p align="center">
  <img src="https://img.shields.io/badge/Objective--C-blue.svg" alt="Objective-C">
  <img src="https://img.shields.io/badge/iOS-9.0+-blue.svg" alt="iOS 9.0+">
  <img src="https://img.shields.io/badge/Xcode-8.0+-brightgreen.svg" alt="Xcode 8.0+">
  <img src="https://img.shields.io/badge/License-MIT-green.svg" alt="MIT License">
</p>

<p align="center">
  <b>iOS 开发问题记录与解决方案仓库</b>
</p>

## 项目简介

这是一个记录 iOS (Objective-C) 开发过程中遇到的各种问题及其解决方案的仓库。本仓库涵盖了从基础 UI 到高级功能的各类问题，旨在帮助 iOS 开发者快速定位和解决开发中遇到的常见问题。

## 问题统计

| 问题类型 | 问题数量 | 状态 |
|---------|---------|------|
| Objective-C 类问题 | 20 | 持续更新 |
| UIKit 类问题 | 89 | 持续更新 |
| Cocoapods 类问题 | 1 | 持续更新 |
| Xcode 类问题 | 1 | 持续更新 |
| Debugger 类问题 | 1 | 持续更新 |
| 报错类问题 | 2 | 持续更新 |
| 其他问题 | 6 | 持续更新 |
| 动画问题 | 2 | 持续更新 |
| 相册类问题 | 1 | 持续更新 |
| **合计** | **121+** | 持续更新 |

## 内容分类

### Objective-C 基础
涵盖 Objective-C 语言的核心概念和常见问题：

- 属性修饰符详解 (strong, weak, copy, assign)
- Block 使用与循环引用
- KVO/KVC 使用
- 内存管理
- Runtime 机制
- 多线程编程

### UIKit
UIKit 开发中常见的问题和解决方案：

#### 视图相关
- UIView 基础操作
- 获取设备屏幕尺寸
- 状态栏高度获取
- 适配 iPhone X 及以上机型

#### 控件使用
- UIButton 创建与点击事件
- UILabel 富文本设置
- UIImageView 图片处理
- UITextField 输入处理
- UIScrollView 滚动视图
- UITableView 表格视图
- UICollectionView 集合视图

#### 布局相关
- Auto Layout 约束设置
- Masonry 使用技巧
- 自适应布局
- 屏幕旋转处理

#### 动画效果
- UIView 动画
- Core Animation
- 转场动画
- 自定义动画

### 手势处理
- 添加各种手势识别器
- 手势冲突处理
- 捏合缩放实现
- 拖拽功能实现

### 网络请求
- NSURLSession 使用
- AFNetworking 集成
- 网络模型封装
- 数据解析

### 数据存储
- NSUserDefaults 使用
- Plist 文件操作
- Core Data 基础
- 文件读写

### Cocoapods
- CocoaPods 安装配置
- Podfile 编写
- 常见问题解决
- 私有库创建

### Xcode 使用
- 常见编译错误
- 调试技巧
- 断点使用
- Instruments 性能分析

### 项目配置
- Info.plist 配置
- 图标和启动图设置
- 权限申请
- 证书配置

## 如何使用

1. **浏览问题**: 根据问题类型进入相应目录
2. **搜索问题**: 使用 GitHub 搜索功能查找特定问题
3. **提交问题**: 如果你遇到了新问题，欢迎提交 Issue 或 PR

## 问题示例

### 获取设备屏幕尺寸

```objc
// 屏幕宽度
CGFloat screenWidth = [UIScreen mainScreen].bounds.size.width;

// 屏幕高度
CGFloat screenHeight = [UIScreen mainScreen].bounds.size.height;

// 状态栏高度 (适配 iPhone X 及以上)
CGFloat statusBarHeight;
if (@available(iOS 13.0, *)) {
    UIWindowScene *windowScene = (UIWindowScene *)[UIApplication sharedApplication].connectedScenes.allObjects.firstObject;
    statusBarHeight = windowScene.statusBarManager.statusBarFrame.size.height;
} else {
    statusBarHeight = [UIApplication sharedApplication].statusBarFrame.size.height;
}

// 导航栏高度
CGFloat navBarHeight = 44.0;

// TabBar 高度 (适配 iPhone X 及以上)
CGFloat tabBarHeight = (statusBarHeight > 20) ? 83.0 : 49.0;

// 安全区域高度
CGFloat safeAreaBottom = (statusBarHeight > 20) ? 34.0 : 0;
```

### UILabel 富文本设置

```objc
// 创建富文本
NSString *text = @"这是普通文字，这是红色文字，这是粗体文字";
NSMutableAttributedString *attributedString = [[NSMutableAttributedString alloc] initWithString:text];

// 设置颜色
[attributedString addAttribute:NSForegroundColorAttributeName 
                         value:[UIColor redColor] 
                         range:NSMakeRange(7, 6)];

// 设置字体
[attributedString addAttribute:NSFontAttributeName 
                         value:[UIFont boldSystemFontOfSize:18] 
                         range:NSMakeRange(16, 6)];

// 设置下划线
[attributedString addAttribute:NSUnderlineStyleAttributeName 
                         value:@(NSUnderlineStyleSingle) 
                         range:NSMakeRange(0, text.length)];

// 应用到 Label
UILabel *label = [[UILabel alloc] init];
label.attributedText = attributedString;
```

### 设置圆角 (layer)

```objc
// 设置圆角
UIView *view = [[UIView alloc] init];
view.layer.cornerRadius = 10.0;
view.layer.masksToBounds = YES;

// 设置指定圆角 (iOS 11+)
UIBezierPath *path = [UIBezierPath bezierPathWithRoundedRect:view.bounds 
                                           byRoundingCorners:UIRectCornerTopLeft | UIRectCornerTopRight 
                                                 cornerRadii:CGSizeMake(10, 10)];
CAShapeLayer *maskLayer = [[CAShapeLayer alloc] init];
maskLayer.frame = view.bounds;
maskLayer.path = path.CGPath;
view.layer.mask = maskLayer;

// 设置阴影
view.layer.shadowColor = [UIColor blackColor].CGColor;
view.layer.shadowOffset = CGSizeMake(0, 2);
view.layer.shadowOpacity = 0.3;
view.layer.shadowRadius = 4.0;
```

### Block 传值

```objc
// 定义 Block 类型
typedef void(^ReturnValueBlock)(NSString *value);

// 在发送方声明 Block 属性
@interface SecondViewController : UIViewController
@property (nonatomic, copy) ReturnValueBlock returnBlock;
@end

// 发送数据
- (void)sendDataBack {
    if (self.returnBlock) {
        self.returnBlock(@"返回的数据");
    }
    [self.navigationController popViewControllerAnimated:YES];
}

// 在接收方实现 Block
- (void)goToSecondVC {
    SecondViewController *secondVC = [[SecondViewController alloc] init];
    secondVC.returnBlock = ^(NSString *value) {
        NSLog(@"接收到的数据: %@", value);
    };
    [self.navigationController pushViewController:secondVC animated:YES];
}
```

## 技术栈

- **编程语言**: Objective-C
- **开发环境**: Xcode 8.0+
- **最低支持系统**: iOS 9.0+
- **框架**: UIKit, Foundation, Core Animation

## 项目结构

```
iOS-Problem-record/
├── Objective-C/
│   └── ...
├── UIKit/
│   ├── UIButton/
│   ├── UILabel/
│   ├── UIImageView/
│   ├── UITableView/
│   ├── UICollectionView/
│   └── ...
├── 手势/
│   └── ...
├── 网络请求/
│   └── ...
├── 数据存储/
│   └── ...
├── Cocoapods/
│   └── ...
├── Xcode/
│   └── ...
├── StoryBoard/
│   └── ...
├── layer/
│   └── ...
└── README.md
```

## 贡献指南

欢迎贡献你的问题和解决方案！

1. Fork 本仓库
2. 创建你的问题分支 (`git checkout -b add/new-problem`)
3. 添加问题描述和解决方案
4. 提交更改 (`git commit -m 'Add: 问题描述'`)
5. 推送到分支 (`git push origin add/new-problem`)
6. 打开 Pull Request

### 提交规范

- 问题描述清晰
- 提供最小可复现代码
- 给出完整的解决方案
- 如有必要，附上截图

## 许可证

本项目采用 MIT 许可证 - 详情请参阅 [LICENSE](LICENSE) 文件

## 致谢

感谢所有为这个项目贡献问题和解决方案的开发者！

## 联系方式

- GitHub: [@MoonStartMan](https://github.com/MoonStartMan)
- 如有问题或建议，欢迎提交 Issue

---

<p align="center">如果这个项目对您有帮助，请给个 ⭐️ 支持一下！<br>让我们一起完善 iOS 开发知识库！</p>
