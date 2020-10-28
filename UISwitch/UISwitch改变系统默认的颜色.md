# UISwitch改变系统默认的颜色

``` objective-c

UISwitch *switchBtn = [[UISwitch alloc] init];
/* Adjust the off-mode tint color */
switchBtn.tintColor = [UIColor redColor];

/* Adjust the on-mode tint color */
switchBtn.onTintColor = [UIColor brownColor];

/* Also change the knob's tint color */
switchBtnh.thumbTintColor = [UIColor greenColor];

```