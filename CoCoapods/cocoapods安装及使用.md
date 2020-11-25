# cocoapods

## 安装cocoapods

### 安装cocoapods命令

```
sudo gem install cocoapods
```

## 切换代理

### 移除原代理

```
gem sources --remove https://rubygems.org/
```

### 添加新代理

```
gem sources --add https://gems.ruby-china.com/
```

## 使用cocoapods

### 切换到当前目录

```
cd desktop
cd xxxx(项目)
```

### 创建Podfile

```
vim Podfile
```

### 在Podfile输入相关代码

1. 键盘输入i，进入编辑模式，输入

```
platform :ios, '8.1'
use_frameworks!
target '工程名' do
	pod 'Masonry'
end
```

2. 然后按ESC
3. 按住shift的同时按住冒号键（:）,然后输入wq(保存)

### 安装输入的相关插件

```
pod install
```

### 项目式安装

```
pod init;
```

#### 生成以下文件目录

``` 
# Uncomment the next line to define a global platform for your project
# platform :ios, '9.0'

target 'MIX' do
  # Comment the next line if you don't want to use dynamic frameworks
  use_frameworks!

  # Pods for MIX
  pod 'Masonry'

end

```

#### 在Pods里面写入需要安装的插件

```
pod 'Masonry'
```