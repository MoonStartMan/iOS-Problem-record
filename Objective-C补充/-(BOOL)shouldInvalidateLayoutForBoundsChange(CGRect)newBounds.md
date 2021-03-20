# -(BOOL)shouldInvalidateLayoutForBoundsChange:(CGRect)newBounds;

- (BOOL)shouldInvalidateLayoutForBoundsChange:(CGRect)newBounds

当边界改变时,是否应该刷新布局。如果YES则在边界变化(一般是scroll到其他地方)时,将重新计算需要的布局信息。

在根据位置提供不同layout属性的时候,需要记得让-shouldInvalidateLayoutForBoundsChange:返回YES,这样当边界改变的时候,-invalidateLayout会自动被发送,才能让layout得到刷新。
