# iOS开发获取系统相册最后一张图片、截屏广播

iOS8以上可以使用 #import <Photos/Photos.h>  来获取系统的照片

+ PHAsset: 代表照片库中的一个资源，跟 ALAsset 类似，通过 PHAsset 可以获取和保存资源
+ PHFetchOptions: 获取资源时的参数，可以传 nil，即使用系统默认值
+ PHFetchResult: 表示一系列的资源集合，也可以是相册的集合
+ PHAssetCollection: 表示一个相册或者一个时刻，或者是一个「智能相册（系统提供的特定的一系列相册，例如：最近删除，视频列表，收藏等等，如下图所示）
+ PHImageManager: 用于处理资源的加载，加载图片的过程带有缓存处理，可以通过传入一个 + + + PHImageRequestOptions 控制资源的输出尺寸等规格
+ PHImageRequestOptions: 如上面所说，控制加载图片时的一系列参数

## 列出所有相册智能相册

``` Objective-C

PHFetchResult *smartAlbums = [PHAssetCollection fetchAssetCollectionsWithType:PHAssetCollectionTypeSmartAlbum subtype:PHAssetCollectionSubtypeAlbumRegular options: nil ];

```

## 列出所有用户创建的相册

``` Objective-C

PHFetchResult *topLevelUserCollections = [PHCollectionList fetchTopLevelUserCollectionsWithOptions: nil ];

```

## 获取所有资源的集合，并按资源的创建时间排序

``` Objective-C

PHFetchOptions *options = [[PHFetchOptions alloc] init];
options.sortDescriptors = @[[ NSSortDescriptor sortDescriptorWithKey: @"creationDate" ascending: YES ]];
PHFetchResult *assetsFetchResults = [PHAsset fetchAssetsWithOptions:options];

```

## 在资源的集合中获取第一个集合，并获取其中的图片

``` Objective-C

PHCachingImageManager *imageManager = [[PHCachingImageManager alloc] init];
PHAsset *asset = assetsFetchResults[0];
[imageManager requestImageForAsset:asset
  targetSize:SomeSize
  contentMode:PHImageContentModeAspectFill
  options: nil
  resultHandler:^(UIImage *result, NSDictionary *info) {

		// 得到一张 UIImage，展示到界面上

}];

```

``` Objective-C

- (void)latestAsset

{
    PHFetchOptions *options = [[PHFetchOptions alloc] init];

    PHFetchResult *assetsFetchResults = [PHAsset fetchAssetsWithOptions:options];

    PHAsset *phasset = [assetsFetchResults lastObject];

    PHCachingImageManager *imageManager = [[PHCachingImageManager alloc] init];

    [imageManager requestImageForAsset:phasset targetSize:CGSizeMake(300, 300) contentMode:PHImageContentModeAspectFill options:nil resultHandler:^(UIImage * _Nullable result, NSDictionary * _Nullable info) {

        

    }];

}

```