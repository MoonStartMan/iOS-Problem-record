# UICollectionView-layoutAttributesForItemAtIndexPath

## 出现问题场景

UICollectionViewCell被点击的时候，UIScrollView跟着滑动。

## 错误原因：

使用cellForItemAtIndexPath,导致后面的UICollectionViewCell快速回到第一页时候,UIScrollView所回到的位置不对。

## 解决办法

使用layoutAttributesForItemAtIndexPath而非cellForItemAtIndexPath。