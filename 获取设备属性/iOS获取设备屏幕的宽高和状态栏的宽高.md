# iOS获取设备屏幕的宽高和状态栏的宽高

## 获取设备屏幕的宽

``` objective-c
[UIScreen mainScreen].bounds.size.width
```

## 获取设备屏幕的高

``` objective-c
[UIScreen mainScreen].bounds.size.height
```

## 获取除去状态栏高度后的设备屏幕的宽

``` objective-c
[[UIScreen mainScreen]applicationFrame].size.width;
```

## 获取除去状态栏高度后的设备屏幕的高

``` objective-c
[[UIScreen mainScreen]applicationFrame].size.height;
```

## 获取状态栏的宽

``` objective-c
[[UIApplication shareApplication] statusBarFrame].size.width;
```

## 获取状态栏的高

``` objective-c
[[UIApplication shareApplication] statusBarFrame].size.height;
```