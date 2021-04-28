# ios子视图获取父视图的视图控制器的方法

``` Objective-C

- (UIViewController *)viewController

{

    for (UIView* next = [self superview]; next; next = next.superview) {

        UIResponder *nextResponder = [next nextResponder];

        if ([nextResponder isKindOfClass:[UIViewController class]]) {

            return (UIViewController *)nextResponder;

        }

    }

    return nil;

}

```

``` swift

 func nextresponsder(viewself:UIView)->UIViewController{
        var vc:UIResponder = viewself
     
        while vc.isKind(of: UIViewController.self) != true {
            vc = vc.next!
        }
        return vc as! UIViewController
    }

```