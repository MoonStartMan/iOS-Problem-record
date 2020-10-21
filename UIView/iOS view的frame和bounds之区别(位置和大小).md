# iOS view的frame和bounds之区别(位置和大小)

## frame与bounds

### frame

``` objective-c
-(CGRect)frame {
	return CGRectMake(self.frame.origin.x, self.frame.origin.y, self.frame.size.width, self.frame.size.height);
}
```

### bounds

``` objective-c
-(CGRect)bounds {
	return CGRectMake(0, 0, self.frame.size.width, self.frame.size.height);
}
```

bounds的原点是(0, 0)点 (就是view本身的坐标系统，默认永远都是0，0点，除非认为setbounds),而frame的原点却是任意的(相对于父视图中的坐标位置)。

``` objective-c
frame: 该view在父view坐标系统中的位置和大小。(参照点是，父亲的坐标系统)。
bounds: 该view在本地坐标系统中的位置和大小。(参照点是，本地坐标系统，就相当于ViewB自己的坐标系统，以0,0点为起点)
center: 该view的中心点在父view坐标系统中的位置和大小。(参照点是：父亲的坐标系统)。
```