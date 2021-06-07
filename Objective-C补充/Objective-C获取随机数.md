# Objective-C获取随机数

1. 获取一个随机整数范围在:[0, 100)包括0,不包括100

``` Objective-C

int x = arc4random() % 100;

```

2. 获取一个随机整数范围在: [500, 1000)，包括500，包括1000

``` Objective-C

int y = (arc4random() % 501) + 500;

```

3. 获取一个随机整数，范围在[from , to)，包括form，包括to

``` Objective-C
- (int)getRandomNumber: (int)from to :(int)to
{
	return (int)(from + arc4andom() % (to - from + 1));
}

```