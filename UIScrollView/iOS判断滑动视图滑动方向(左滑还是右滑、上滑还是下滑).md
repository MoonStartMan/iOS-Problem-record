# iOS判断滑动视图滑动方向(左滑还是右滑、上滑还是下滑)

``` Objective-C

//	实现scrollView代理
-(void)scrollViewWillBeginDragging:(UIScrollView *)scrollView {
	//	全局变量记录滑动前的contentOffset
	
	//	判断上下滑动时候记录Y
	lastContentOffsetY = scrollView.contentOffset.y;
	
	//	判断左右滑动的时候记录X
	lastContentOffsetX = scrollView.contentOffset.x;
}

```

``` Objective-C

- (void)scrollViewDidScroll:(UIScrollView *)scrollView{
	if (scrollView.contentOffset.y < lastContentOffset ){
//向上
		NSLog(@"上滑");
	} else if (scrollView.contentOffset.y > lastContentOffset ){
//向下
		NSLog(@"下滑");
   }
//判断左右滑动时
	if (scrollView.contentOffset.x < lastContentOffset ){
		//向右
		NSLog(@"左滑");
	} else if (scrollView. contentOffset.x > lastContentOffset ){
		//向左
		NSLog(@"右滑");
    }
}

```