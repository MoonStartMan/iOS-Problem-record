# atomatic和nonatomic区别和理解

## 第一种

atomic和noatomic区别用来决定编译器生成的getter和setter是否为原子操作。atomic提供多线程安全。是描述该变量是否支持多线程的同步访问，如果选择atomic那么就是说，系统回自动创建lock锁，锁定变量。nonatomic禁止多线程，变量保护，提高性能。

``` Objective-C

//	atomic:默认是有该属性的，这个属性是为了保证程序在多线程情况下，编译器会自动生成一些互斥加锁代码，避免该变量的读写不同步问题。

```

``` Objective-C

//	noatomic:如果该对象无需考虑多线程的情况，请加入这个属性，这样会让编译器少生成一些互斥加锁代码，可以提高效率。

```

``` Objective-C

//	atomic的意思就是setter/getter这个函数，是一个原语操作。如果有多个线程同时调用setter的话，不会出现某一个线程执行完setter全部语句之前，另一个线程开始执行setter情况，相当于函数头尾加了锁一样，可以保证数据的完整性。nonatomic不保证setter/getter的原语行，所以你可能会取到不完整的东西。因此，在多线程的环境下原子操作是非常必需要的，否则有可能会引起错误的结果。

```

比如setter函数里面改变两个成员变量，如果你用nonatomic的话，getter可能会取到只更改了其中一个变量时候的状态，这样取到的东西会有问题，就是不完整的。当然如果不需要多线程支持的话，用nonatomic就够了，因为不涉及到线程锁的操作，所以它执行率相对快些。

下面是载录的网上一段加了atomic的例子:

``` Objective-C

{lock}
	if (property != newValue) {
		[property release];
		property = [newValue retain];
	}
{unlock}
```

``` Objective-C

可以看出来，用atomic会在多线程的设值取值时加锁，中间的执行层是处于被保护的一种状态，atomic是oc使用的一种线程保护技术，基本上来讲，就是防止在写入完成的时候被另一个线程读取，造成数据错误。而这种机制是耗费系统资源的，所以在iPhone这种小型设备上，如果没有使用多线程间的通讯编程，那么nonatomic是一个非常好的选择。

```

## 第二种

atomic和noatomic用来决定编译器生成的getter和setter是否为原子操作。

### atomic

设置成员变量的@property属性时，默认为atomic，提供多线程安全。

在多线程环境下，原子操作是必要的，否则有可能引起错误的结果。加了atomic，setter函数会变成下面这样:

``` Objective-C

{lock}
	if (property != newValue) {
		[property release];
		property = [newValue retain];
	}
{unlock}

```

### nonatomic

3禁止多线程，变量保护，提高性能。

3atomic是Objc使用的一种线程保护技术，基本上来讲，是防止在未完成的时候被另外一个线程读取，造成数据错误。而这种机制是耗费系统资源的，所以在iPhone这种小型设备上，如果没有使用多线程间的通讯编程，那么nonatomic是一个非常好的选择。

3指出访问器不是原子操作，而默认地，访问器是原子操作。这也就是说，在多线程环境下，解析的访问器提供一个对属性的安全访问，从获取器得到的返回值或者通过设置器设置的值可以一次完成，即便是别的线程也正在对其进行访问。如果你不指定 nonatomic ，在自己管理内存的环境中，解析的访问器保留并自动释放返回的值，如果指定了 nonatomic ，那么访问器只是简单地返回这个值。

作者：Silence_广
链接：https://www.jianshu.com/p/64520f3e79d3
来源：简书
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。