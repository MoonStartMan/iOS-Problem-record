# Objective-C中new与alloc/init的区别

## new源码

``` Objective-C

+ new {
	id newObject = (*_alloc)((Class)self, 0);
	Class metaClass = self -> isa;
	if (class_getVersion(metaClass) > 1)
		return [newObject init];
	else 
		return newObject;
}

```

## alloc/init源码

而 alloc/init 像这样

``` Objective-C

+ alloc {
	return (*_zoneAlloc)((Class)self, 0, malloc_default_zone());
}

- init {
	return self;
}

```

通过源码中我们发现，[className new]基本等同于[[className alloc] init]，区别只在于alloc分配内存的时候使用了zone。

## zone

zone是给对象分配内存的时候，把关联的对象分配到一个相邻的内存区域内，以便于调用消耗很少的代价，提升了程序处理速度。

## 为什么不推荐使用new？

不知大家发现了没有，如果使用new的话，初始化方法被固定死只能调用init。而你无法调用initXXX方法。

1. alloc这个方法只是给对象分配了内存，并没有初始化实例变量。
2. 后来发现"显式调用总比隐式调用更好"，所以后来就把两个方法分开了。

## 区别

采用new的方式只能采用默认的init方法完成初始化，采用alloc的方式可以用其他定制的初始化方法。