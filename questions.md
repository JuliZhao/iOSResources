#问题总结

##1. 在利用终端安装CocoaPods中遇到如下错误：
![](image/q1.jpg)
<br>解决方案在终端输入：
```
	sudo gem install -n /usr/local/bin cocoapods
```
##2. 怎么在Mac电脑上将手机软件打开，获取包文件
> 解决方法 : 将后缀改为.ipa 然后下图

![](image/q2.jpg)
##3. 使用AFNetworking进行网络请求时报下面错误
```
	Error Domain=com.alamofire.error.serialization.response Code=-1016 "Request failed: unacceptable content-type: application/x-javascript" UserInfo={com.alamofire.serialization.response.error.response=<NSHTTPURLResponse: 0x7fbddbc18350> { URL: http://api2.pianke.me/pub/today } { status code: 200, headers {
    "Cache-Control" = "no-store, no-cache, must-revalidate, post-check=0, pre-check=0";
    Connection = "keep-alive";
    "Content-Encoding" = gzip;
    "Content-Type" = "application/x-javascript; charset=utf-8";
    Date = "Wed, 02 Dec 2015 03:38:36 GMT";
    Etag = a8bc877f523a4096caa746bc2fa8d2a3;
    Expires = "Thu, 19 Nov 1981 08:52:00 GMT";
    Pragma = "no-cache";
    Server = nginx;
    "Set-Cookie" = "PHPSESSID=s0upj58k0ghbfj15r3fp8dcmm2; path=/; domain=pianke.me";
    "Transfer-Encoding" = Identity;
    Vary = "Accept-Encoding";
} }
``` 
原因: 后台返回的数据的文件格式是javascript的.AFNetworking 解析不了.所以需要我们告诉AFNetworking返回数据时javascript格式的,这样AFNetworking就可以解析了(默认ANF 是按照json格式处理的,如果返回时html也会报错)
解决方案:
```
	AFHTTPRequestOperationManager *manager = [AFHTTPRequestOperationManager manager];
	manager.responseSerializer.acceptableContentTypes = [NSSet setWithObject:@"application/x-javascript"];
```