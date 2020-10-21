# UIScrollView

## 什么是UIScrollView

+ 移动设备的屏幕大小是及其有限的，因此直接展示在用户眼前的内容也是相当有限
+ 当展示的内容较多，超出一个屏幕时，用户可通过滚动手势来查看屏幕以外的内容
+ 普通UIView不具备滚动功能，不适合显示过多的内容
+ UIScrollView是一个能够滚动的视图控件，可以用来展示大量的内容，并且可以通过滚动查看所有的内容
+ 举例：手机上的"设置"

## UIScrollView的基本使用

+ 将需要展示的内容添加到UIScrollView中
+ 设置UIScrollView的contentSize属性，告诉UIScrollView所有内容的尺寸，也就是告诉它滚动的范围(能滚多远，滚到哪里是尽头)
+ 用户可以用过手势拖动来查看超出边框并被隐藏的内容。

## UIScrollView无法滚动的解决办法

+ 如果UIScrollView无法滚动，可能是以下原因:
	+ 没有设置contentSize(或者contentSize的尺寸小于等于scrollView的尺寸)
	+ scrollEnabled = NO;


## UIScrollView的相关代码

``` objective-c
-(UIScrollView *)scrollView {
	if(!_scrollView) {
		//	初始化配置scrollView
		_scrollView = [[UIScrollView alloc]init];
		_scrollView.frame = CGRectMake(20, 50, self.view.bounds.size.width-40, 400);
		_scrollView.backgroundColor = [UIColor redColor];
    _scrollView.contentSize = CGSizeMake(800, 50);
    //	是否能够滚动
    _scrollView.scrollEnabled = YES;
    //	是否能跟用户交互(能不能响应用户的拖拽，点击 等操作)
    //	注意点：如果设置该属性为NO,scrollView以及它所有的子控件都不能跟用户交互
    _scrollView.userInteractionEnabled = YES;
    
    //	是否有弹簧效果
    self.scrollView.bounces = YES;
    
    //	不管有没有设置contentSize，总是有弹簧效果
    self.scrollView.alwaysBounceHorizontal = YES;
    self.scrollView.alwaysBounceVertical = YES;
    
    //	是否显示滚动条
    self.scrollView.showsHorizontalScrollIndicator = NO;
    self.scrollView.showsVerticalScrollIndicator = NO;
    
    //	注意点：千万不要通过索引去subviews这个数组中访问scrollView的子控件
    NSLog(@"%@",self.scrollView.subviews);
    [self.scrollView.subviews.firstObject removeFromSuperview];
	}
	return _scrollView;
}


- (void)viewDidLoad {
	[super viewDidLoad];
	[self.view addSubview:self.scrollView];
}
```


## UIScrollView属性

### CGPointMake

内容的偏移量
作用：控制scrollView内容滚动的位置

``` objective-c
self.scrollView.contentOffset = CGPointMake(200, 0);
```