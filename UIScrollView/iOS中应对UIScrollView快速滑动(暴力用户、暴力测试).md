# iOS中应对UIScrollView快速滑动(暴力用户、暴力测试)

1. 实现UIScrollViewDelegate

开始滑动

``` Objective-C

- (void)scrollViewBeginDecelerating: (UIScrollView *)scrollView

```

滑动过程

``` Objective-C

- (void)scrollViewDidEndDragging:(UIScrollView *)scrollView willDecelerate:(BOOL)decelerate

```

滑动结束

``` Objective-C

- (void)scrollViewDidEndDecelerating:(UIScrollView *)scrollView

```

第二种停止:当decelerate = true时,iOS才会调UIScrollView的delegate

``` Objective-C

- (void)scrollViewDidEndDragging:(UIScrollView *)scrollView willDecelerate:(BOOL)decelerate

```

注意: 无论用户如何滑动scrollView,只要有滑动,就会调scrollViewWillBeginDecelerating,只有scrollView当加速度停止之后,才会调用scrollViewDidEndDecelerating

2. 有了以上条件,就为限制加载提供了实现方式
