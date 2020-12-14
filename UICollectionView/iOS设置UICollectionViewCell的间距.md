# iOS设置UICollectionViewCell的间距

## sectionInset:

设置上左下右的距离

``` Objective-C

(UIEdgeInsetsMake(CGFloat top, CGFloat left, CGFloat bottom, CGFloat right));

```

### 项目中代码

``` Objective-C

layout.sectionInset = UIEdgeInsetsMake(0, 20, 0, 0);

```

## minimumInteritemSpacing

设置两个cell之间的间距（左右）

### 项目中代码

``` Objective-C

layout.minimumInteritemSpacing = 25;

```

## minimumLineSpacing

设置两个cell之间的间距（上下）

### 项目中使用代码

``` Objective-C

layout.minimumLineSpacing = 25;

```