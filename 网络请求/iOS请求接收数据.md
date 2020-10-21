# iOS请求接收数据

## 在Xcode里面设置允许发送HTTP请求

1. 找到info.plist文件
2. 右键找到"Open As"并点击"Source Code"。
3. 在里面添加以下代码

``` Info.plist
<key>NSAppTransportSecurity</key>
    <dict>
        <key>NSAllowsArbitraryLoads</key>
        <true />
    </dict>
```

此时已经可以发送HTTP请求了。

## 体验HTTP请求(老方法)

### 方法:sendAsynchronousRequest(异步请求)

``` objective-C
//	发送请求

NSURL *url = [NSURL URLWithString: @"http://www.baidu.com"];

//	请求
NSURLRequest *request = [NSURLRequest requestWithURL: url];

//  发送异步请求
[NSURLConnection sendAsynchronousRequest: request queue:[NSOperationQueue mainQueue] completionHandler:^(NSURLResponse * _Nullable response, NSData * _Nullable data, NSError * _Nullable connectionError){
	//	response  服务器的响应头
	//	data   服务器返回的响应头
	//	connectionError  连接错误
	
	//  判断请求是否有误
  if(!connectionError) {
  	//	把二进制数据转换成NSString
  	NSString *html = [[NSString alloc] initWithData: data encoding: NSUTF8StringEncoding];
  	NSLog(@"@%@",html);
  } else {
  	NSlog(@"连接错误 %@",connectionError);
  }
}];
```