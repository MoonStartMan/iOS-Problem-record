# UIScrollView滑动监听相关



``` Objective-C

- (void)scrollViewDidScroll:(UIScrollView *)scrollView {
    NSLog(@"scrollViewDidScroll");
    CGFloat y = scrollView.contentOffset.y;
    CGFloat asd = kScreenHeight - scrollView.size.height - 20;
    if (y <= 0) {
        //下滑
    } else {
        //上滑

    }
}

```

手指离开屏幕的时候UIScrollView还在缓慢减速滑动，如果想它立马停止滑动，只需要实现下面的代理方法

``` Objective-C

//手指离开立即停止
- (void)scrollViewWillBeginDecelerating:(UIScrollView *)scrollView
{
    [scrollView setContentOffset:scrollView.contentOffset animated:NO];
}

```