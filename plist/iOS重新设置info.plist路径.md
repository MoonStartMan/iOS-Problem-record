# iOS重新设置info.plist路径

## 报错

```

The file "info.plist" couldn't be opened because there is no such file.

```

## 解决办法

```
到BuildSetting里面把它的路径改为全局的。
$(SRCROOT)+/原地址
```

## 环境变量宏

环境变量宏(Build Setting Macros)

### 引用格式

同Build Phases Run Script中的语法。

``` 
$(MACRO)
```

``` 
PROJECT = HelloWorld

PROJECT_DIR =~/Projects/Learn Objective-C/HelloWorld

PROJECT_FILE_PATH =${PROJECT_DIR}/HelloWorld.xcodeproj

PROJECT_NAME = HelloWorld

SOURCE_ROOT =${PROJECT_DIR}

SRCROOT =${PROJECT_DIR}

SDKROOT = /Applications/Xcode.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.9.sdk

SDK_DIR = /Applications/Xcode.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.9.sdk

SDK_NAME = macosx10.9
```

### $(SRCROOT)和$(PROJECT_DIR)的区别

+ $(SRCROOT)项目根目录下
+ $(PROJECT_DIR)整个项目

PS：往项目添加文件时，若文件不在工程目录中，而在工程父目录中，可写成$(SRCROOT)/../XXSDK/XXX.framework。其中/../就是指向父目录。

