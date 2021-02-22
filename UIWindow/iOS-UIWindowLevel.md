# iOS-UIWindowLevel

UIWindow在显示的时候会根据UIWindowLevel进行排序的，即Level高的将排在所有Level比他低的层级的前面。下面我们来看UIWindowLevel的定义:

``` Objective-C

const UIWindowLevel UIWindowLevelNormal;
const UIWindowLevel UIWindowLevelAlert;
const UIWindowLevel UIWindowLevelStatusBar;
typedef CGFloat UIWindowLevel;

```

## 排序

UIWindowLevelNormal(0.0) < UIWindowLevelStatusBar(1000.0) < UIWindowLevelAlert(2000.0)

