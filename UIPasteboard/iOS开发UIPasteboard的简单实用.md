# iOS开发UIPasteboard的简单实用

## UIPasteboard简介

+ 顾名思义,UIPasteboard是剪切板功能,因为iOS的原生控件UITextField、UITextView、UIWebView
+ 我们在使用时如果长按，就会出现复制、剪切、选中、全选、粘贴等功能，这个就是利用了系统剪切板功能来实现的
+ 而每一个App都可以去访问系统剪切板

## pasteboard的创建

``` Objective-C

//	获取系统剪切板
UIPasteboard *pasteboard = [UIPasteboard generalPastboard];

//	将 label 的文字存储到剪切板
pasteboard.string = self.label.text;

//	将剪切板的文字赋值给label
self.label.text = pasteboard.string;

```