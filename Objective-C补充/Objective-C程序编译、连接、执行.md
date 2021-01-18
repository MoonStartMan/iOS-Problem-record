# Objective-C程序编译、连接、执行.

## 在.m文件中写上符合OC语法规范的源代码

## 使用编译器将源代码编译为目标文件.

	cc -C xx.m
	
	a. 预处理
	b. 检查语法
	c. 编译
	
## 连接

	cc xx.o
	
	如果程序中使用了框架中的函数或者类,那么在链接的时候,就必须要告诉编译器去哪一个框架中找这个函数或者类。
	
	cc xx.o -framework 框架名称
	cc main.o -framework Foundation
	
## 连接成功后 就会生成1个a.out可执行文件 执行就可以了。

