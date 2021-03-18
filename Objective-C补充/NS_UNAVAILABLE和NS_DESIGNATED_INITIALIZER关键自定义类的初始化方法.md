# NS_UNAVAILABLE和NS_DESIGNATED_INITIALIZER关键自定义类的初始化方法

## NS_DESIGNATED_INITIALIZER

### 指定初始化器是用来解决什么问题的?

``` Objective-C

 //自定义 CustomView.h
 #import <UIKit/UIKit.h>
 
 @interface CustomView : UIView

- (instancetype)initWithFrame:(CGRect)frame andCornerRadius:(CGFloat)cornerRadius;
@end

//自定义CustomView.m

#import "CustomView.h"

@implementation CustomView

- (instancetype)initWithFrame:(CGRect)frame andCornerRadius:(CGFloat)cornerRadius {
    
    self = [super initWithFrame:frame];
    
    if (self) {
    	
    	self.layer.cornerRadius = cornerRadius;
    }
    
    return self;
}

```

如果通过CustomView *cV = [[CustomView alloc] initWithFrame: CGRectMake(x, y,width,height) andCornerRadius: 5];来实例化CustomView,是完全没有问题的,创建出一个圆角为5的view。但是,你能确保你自己每次都能记得用这个初始化方法来实例化CustomView吗?一个月以后呢?一年以后呢?更不用说你这个CustomView可能提供给别人使用。如果别人直接用CustomView继承过来的初始化方法来实例化一个对象:

``` Objective-C

CustomView *cV = [[CustomView alloc] initWithFrame: CGRectMake(x, y, width, height)];

```

这样创建的view肯定是不会有圆角的。
那么，我们怎么才能确保只要是CustomView的对象一定都有一个圆角呢?

### 指定初始化器

很明显,只要我们确保无论怎么初始化，都会调用我们指定的初始化方法(也就是指定初始化器- (instancetype)initWithFrame:(CGRect) frame andCornerRadius:(CGFloat)conrnerRadius;),就可以达到只要是CustomView的对象一定会有一个圆角。

这是我们可以把CustomView初始化方法 - (instancetype)initWithFrame:(CGRect)frame andCornerRadius:(CGFloat)cornerRadius;定义为指定初始化器 - (instancetype)initWithFrame:(CGRect)frame andCornerRadius:(CGFloat)cornerRadius NS_DESIGNATED_INITIALIZER;（指定初始化器：无论你调用对象的哪一个初始化方法，最终这个初始化方法都会直接或间接的来调用指定初始化器来创建对象）。

### 指定初始化器与父类的指定初始化器

刚才说到CustomView *cV = [[CustomView alloc] initWithFrame: CGRectMake(x, y, width, height)];这种方式创建CustomView对象是不会有圆角的(initWithFrame:是父类的指定初始化器, 也就是父类的任何初始化方法，内部最终还是会调用initWithFrame:方法来创建对象)。这时，我们只要重写父类的initWithFrame:方法，并在initWithFrame:方法中调用子类的初始化器方法可以达到无论通过哪种方式实例化的CustomView对象都会具有一个圆角。

``` Objective-C

#import <UIKit/UIKit.h>

@interface CustomView : UIView

- (instancetype)initWithFrame: (CGRect)frame andCornerRadius: (CGFloat)conrnerRadius NS_DESIGNATED_INITIALIZER;

@end

//自定义CustomView.m

#import "CustomView.h"

@implementation CustomView

- (instancetype)initWithFrame:(CGRect)frame andCornerRadius:(CGFloat)cornerRadius {
    
    self = [super initWithFrame:frame];
    
    if (self) {
    	
    	self.layer.cornerRadius = cornerRadius;
    }
    
    return self;
}

- (instacetype)initWithFrame:(CGRect)frame {
	
	return [self initWithFrame:frame andCornerRadius:1];//这里的1代表默认值，你可以根据情况自己定义 相当于如果没有指定圆角大小，那么圆角大小就是1
}

```

### 如果调用顶级父类的init方法会怎样？


``` Objective-C

CustomView *cV = [[CustomView alloc] init];

```

+ 这里就用到OC的消息传递相关的知识。

1. 查找当前当前对象(CustomView)的方法列表，发现没有init方法。
2. 查找父类(UIView)的方法列表，发现init方法。 为什么会在UIView中发现init方法呢？不是应该在UIResponder的方法列表中吗？前面提到过，子类会重写父类的指定初始化器(在这里UIResponder的指定初始化器就是 init。ps：本例中对于initWithCoder:不做讨论，可以自行查阅相关资料)。
3. 调用UIView的init方法，并在init方法中调用UIView的指定初始化器initWithFrame:，这时的初始化就变成了CustomView *cV = [[CustomView alloc] initWithFrame:];，而CustomView由于重写了父类的initWithFrame:方法，并且在initWithFrame:方法中调用了CustomView的指定初始化器— - (instancetype)initWithFrame:(CGRect)frame andCornerRadius:(CGFloat)cornerRadius;所以，这时会创建一个圆角为1的CustomView。


### 总结

1.当前指定初始化器的对象要重写父类的指定初始化器，在重写的父类初始化器中调用当前的初始化器。
2.指定初始化器中要调用父类的指定初始化器

## NS_UNAVAILABLE

如果加上此关键字，则不允许调用该方法。