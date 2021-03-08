# iOS-自动消失提示框的实现

直接上代码

## 常用方法

``` Objective-C

UIAlertController *alert = [UIAlertController alertControllerWithTitle: "警告" message: "提示信息" preferredStyle: UIAlertControllerStyleAlert];
self presentViewController: alert animated: YES completion: nil];

```

## 实现dismiss:方法

``` Objective-C

- (void)dismiss:(UIAlertController *)alert {
	[alert dismissViewControllerAnimated: YES completion: nil];
}

```