# OC中__kindof的用法

## 使用方法

假如我们声明了如下属性:

``` Objective-C

@property (nonatomic, strong) NSArray *viewCollection;

```

看属性名我们会认为它是元素为UIView的数组,但这只是猜测,它并不能保证这个数组的元素就是UIView,除非通过阅读完整的代码来确认。

这种情况下,我们就可以使用泛型和__kindof来解决这个问题。

使用泛型，我们可以这样声明这个数组:

``` Objective-C

@property (nonatomic, strong) NSArray<UIView *> *viewCollection;

```

这样我们知道这个数组被指定了元素为UIView类型。

但是呢，这样声明的数组它只能包含UIView类型的元素,如果元素被赋值为UIWebView或UIButton这样的子类型,编译器就会报警告。

为了解决这个问题,kindof就应运而生。

``` Objective-C

@property (nonatomic, strong) NSArray<__kindof UIView *> *viewCollection;

```

用这种结构声明,这个数组就可以包含UIView以及UIView的子类型，例如UIWebView或UIButton。

## 总结

返回类或子类