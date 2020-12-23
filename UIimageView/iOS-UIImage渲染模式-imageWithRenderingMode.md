# iOS-UIImage渲染模式-imageWithRenderingMode:

设置UIImage的渲染模式：UIImage.renderingMode

着色(Tint Color)是IOS7界面中的一个设置UIImage的渲染模式，你可以设置一个UIImage在渲染时是否使用当前视图的Tint Color。UIImage新增了一个只读属性:renderingMode,对应的还有一个新增方法:imageWithRenderingMode:，它使用UIImageRenderingMode枚举值来设置图片的renderingMode属性。该枚举中包含下列值：

``` Objective-C

1. UIImageRenderingModeAutomatic	//	根据图片的使用环境和所处的绘图上下文自动调整渲染模式。
2. UIImageRenderingModeAlwaysOriginal	//	始终绘制图片原始状态, 不使用Tint Color。
3. UIImageRenderingModeAlwaysTemplate	//	始终根据Tint Color绘制图片，忽略图片的颜色信息。

```

## 应用

1. renderingMode属性的默认值是UIImageRenderingModeAutomatic,即UIImage是否使用Tint Color取决于它显示的位置。


2. UIImageRenderingModeAlwaysOriginal:在navigationBar和tabbar，系统默认tabBarItem上的图片被选中时是蓝色的，而蓝色图片并不是我们想要的效果，这时就需要我们利用imageWithRenderingMode：UIImageRenderingModeAlwaysOriginal这个方法来让tabBarItem上的图片以本来面目显示出来。因此，你应该改写你的代码:

``` Objective-C

yourController.tabBarItem.image = [[UIImage imageNamed:@"tabbar_image_2"] imageWithRenderingMode:(UIImageRenderingModeAlwaysOriginal)];

yourController.tabBarItem.selectedImage = [[UIImage imageNamed:@"tabbar_HLimage_2"] imageWithRenderingMode:UIImageRenderingModeAlwaysOriginal];

```

3. UIImageRenderingModeAlwaysTemplate 如果你要用代码改变图片颜色(一般对于单一颜色的图片),可以这样写

``` Objective-C

UIImage *theImage =  [UIImage imageNamed:@"123.png"];
theImage = [theImage  imageWithRenderingMode:UIImageRenderingModeAlwaysTemplate];
imageView.image = theImage;
imageView.tintColor = [UIColor blueColor];

```