# iOS页面跳转的几种方式

## 选项卡UITabBarController控制器

通过调用UITabBarController的addChildViewController方法添加子控制器

``` Objective-C

UITabBarController *tabbarVC = [[UITabBarController alloc] init];
FirstViewController *FVC = [[FirstViewController] init];
FVC.tabBarItem.title = @"控制器1";
FVC.tabBarItem.image = [UIImage imageNamed: @"first.png"];
SecondViewController *SVC = [[SecondViewController] init];
SVC.tabBarItem.title = @"控制器2";
SVC.tabBarItem.image = [UIImage imageNamed: @"new.png"];
//	添加自控制器(这些子控制器会自动添加到UITabBarController的 viewControllers数组中)
[tabbarVC addChildViewController: FVC];
[tabbarVC addChildViewController: SVC];
```

### 优点：

代码量较少

### 缺点：

tabbar的ios原生样式不太好看，(不常用，目前不建议使用)，如果要使用，建议自定义tabbar

## 导航控制器UINavigationController

### 在FVC的button的监听方法中调用:

``` Objective-C

[self.navigationController pushViewController:newC animated:YES];//	跳转到下一页

```

### 在SVC的方法中调用:

``` Objective-C

[self.navigationController popViewControllerAnimated:YES];//	返回上一页面

```

### 当有多次跳转发生并希望返回根控制器时，调用:

``` Objective-C

[self.navigationController popToRootViewControllerAnimated: YES];//	返回根控制器，即最开始的页面

```

## 利用Modal形式展示控制器

在FVC中调用:

``` Objective-C
[self presentViewController: SVC animated: YES completion: nil];
```

在SVC中调用:

``` Objective-C
[self dismissViewControllerAnimated: YES completion: nil];
```

