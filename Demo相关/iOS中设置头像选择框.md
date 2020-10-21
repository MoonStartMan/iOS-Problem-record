# iOS中设置头像选择框

## 声明

``` objective-c
//	HomeView.h
@property(nonatomic, strong) UIImageView *headImage;	//	头像
```

## 实现

``` objective-c
-(UIImageView *)headImage {
	if(!_headImage) {
		_headImage = [[UIImage alloc]init];//	分配内存 
		_headImage.backgroundColor =  [UIColor whiteColor];	//	设置背景色
		_headImage.layer.cornerRadius = 10;	//	设置圆角大小
		_headImage.layer.masksToBounds = YES;	//	展示圆角效果
		_headImage.userInteractionEnabled = YES;	//	允许交互
		
		//	给图片添加点击手势
		UITapGestureRecognizer * tapGues = [[UITapGestureRecognizer alloc]initWithTarget:self action:@selector(clickImg:)];
		[_headImage addGestureRecognizer:tapGues];
	}
	return _headImage;
}
```

## 实现点击事件

``` objective-c
-(void)clickImg:(UITapGestureRecognizer *)tap
{
	if([_delegate respondsToSelector:@selector(selectImg)]) {
		[_delegate selectImg];
	}
}
```


## 选择图片代理方法实现

``` objective-c
-(void)selectImg {
	
	NSInteger sourceType =0;
	
	//0 - 图库, 1 - 相机.  2 - 相册
	if([UIImagePickerController]) {
		sorceType = UIImagePickerControllerSourceTypePhotoLibrary;
	}
	
	//	实例化图片来源类型
	UIImagePickerController *pick = [[UIImagePickerController alloc]init];
	pick.allowsEditing = YES;	//图片可缩放和操作
	pick.delegate = self;
	pick.sourceType = sourceType;
	[self presentViewController:pick animated: YES completion: nil];
}
```