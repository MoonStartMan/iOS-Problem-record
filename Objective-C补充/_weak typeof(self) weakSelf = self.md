# _weak typeof(self) weakSelf = self

block对于其变量都会形成strong reference(强引用)，对self也形成strong refernce，而如果self本身对block也是strong reference的话，就会形成strong reference循环，造成内存泄露。为了防止这种情况发生，在block外部应该创建一个week(__block) reference(弱引用类型)

所以在block内如果有self的话，一般都会在block外面加一句__block typeof(self) weakSelf = self;

``` Objective-C

__weak typeof(self)weakSelf = self;
[weakSelf addLegendFooterWithRefreshingBlock: ^{
	//	do something
	[weakSelf.footer endRefreshing];
}];

```

## 内存管理原则

1. 默认strong,可选weak。strong下不管成员变量还是property，每次使用指针指向一个对象，等于自动调用retain()，并对旧对象调用release()，所以设为nil等于release。
2. 只要某个对象被任一strong指针指向指针指向，那么它将不会被摧毁，否则立即释放，不用等runloop结束。所有strong指针变量不需要在dealloc中手动设为nil，iOS会自动处理，debug可以看到全部设置为nil，最先声明的变量最后调用dealloc释放。
3. 优先使用私有成员变量，除非需要公开属性采用property。
4. 避免循环引用，否则手动设置nil释放。
5. block方法常用声明:@property  (copy) void(^MyBlock)(void);如果超出当前作用域之后仍然继续使用block,那么最好使用copy关键字,拷贝到堆区，防止栈区变量销毁。
6. 创建block匿名函数之前一般需要对self进行weak化,否则造成循环引用无法释放controller。