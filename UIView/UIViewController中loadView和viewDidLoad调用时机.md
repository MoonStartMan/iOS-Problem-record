# UIViewController中loadView和viewDidLoad调用时机

## loadView

### 调用时机

当访问UIViewController中的self.view时,如果view为nil就会去调用此方法。

举个例子,比如在viewDidLoad方法中有如下代码:

``` Objective-C

UILabel *label = [[UILabel alloc] initWithFrame:CGRectMake(375/2 - 60, 20, 120, 40)];
label.text = @"Hello";
label.backgroundColor = [UIColor greenColor];
label.textAlignment = NSTextAlignmentCenter;
[self.view addSubview:label];

```

当程序走到第五行时,发现self.view为nil,就会去调用loadView。

### 注意事项

如果用storyboard创建了view并初始化了view controller(新建SingleView Application中的Main.storyboard和ViewController类)，这时候就不用去重写loadView方法。如果重写了的话，程序启动会先调用loadView，执行完后进入viewDidLoad方法。此时如果在loadView方法中没有给self.view赋值，并且在viewDidLoad方法中用到self.view的话，程序就会进入死循环。

### 何时需要重写此方法呢？

完全通过代码创建view,而不是通过xib或者StoryBoard。
注意此时不要调用[super loadView],造成不必要的系统开销。

### 补充不重写情况下默认的实现机制

1. 查找与UIViewController相关联的xib文件

``` Objective-C

[[MainViewController alloc] initWithNibName: @"MainViewController" bundle: nil];

```

2. 执行步骤1如果没有找到的话,就会去加载跟UIViewController同名的xib文件

``` Objective-C

[[MainViewController alloc] init];

```

3. 执行步骤2还是没有找到的话,就会创建一个空白的UIView,并赋值给UIViewController的view

``` Objective-C

self.view = [[UIView alloc] initWithFrame: [[UIScreen mainScreen]] bounds];

```

## viewDidLoad

### 调用时机

在view创建完毕后,不管是通过xib、storyboard还是loadView自定义view

### 作用

界面初始化的操作,加载数据等。