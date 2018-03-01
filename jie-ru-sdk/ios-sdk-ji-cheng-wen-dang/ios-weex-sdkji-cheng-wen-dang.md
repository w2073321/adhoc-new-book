# **Weex-adhoc**

## 安装

```
$ npm install -g weex-toolkit
```

检测是否安装成功

```
$ weex -v //查看当前weex版本
```

## 配置

链接原生库

```
$ weex platform add ios
$ weex platform add android
```

### iOS SDK 初始化

1.在platform/ios中找到对应的pod文件，pod AdhocSDK,然后用Xcode打开工程

找到podflie文件添加weexSDK

```
defcommon
pod'WeexSDK'
pod'AdhocSDK'
pod'WeexPluginLoader'
pod'SDWebImage','3.7.5'
pod'SocketRocket','0.4.2'
end
```

2.找到AppDelegate.m文件，引用头文件：

`#import "AdhocSDK.h"`

在@selector\(application:didFinishLaunchingWithOptions:\)中：

```
AdhocSDKConfig *config = [AdhocSDKConfig defaultConfig];
config.appKey = @“ADHOC_xxx”;
[AdhocSDK startWithConfigure:config options:launchOptions];
```

### weex SDK 封装

自定义WXAdhocModule类,导入AdhocSDK.framework的头文件,把AdhocSDK中方法再一次封装，并对外暴露给weex方法调用

```
#import"WXAdhocModule.m"

WX_EXPORT_METHOD(@selector(adhoc_getFlag:default:callback:))
WX_EXPORT_METHOD(@selector(adhoc_track:value:))
WX_EXPORT_METHOD(@selector(adhoc_trackAttribute:value:attribute:))
WX_EXPORT_METHOD(@selector(adhoc_getCurrentExperimentsCallback:))

(void)adhoc_getFlag:(NSString*)flag_name default:(id)default_value callback:(WXModuleKeepAliveCallback)callback
{
callback([AdhocSDKgetFlag:flag_namedefault:default_value],YES);
}
(void)adhoc_track:(NSString*)stat_name value:(NSString*)stat_value
{
[AdhocSDKtrack:stat_namevalue:@([stat_valueintegerValue])];
}
(void)adhoc_trackAttribute:(NSString*)stat_name value:(NSNumber*)stat_value attribute:(NSString*)stat_attribute
{
NSData*JSONData = [stat_attributedataUsingEncoding:NSUTF8StringEncoding];
NSDictionary*responseJSON = [NSJSONSerializationJSONObjectWithData:JSONDataoptions:NSJSONReadingMutableLeaveserror:nil];
[AdhocSDKtrack:stat_namevalue:stat_valueattribute:responseJSON];
}
(void)adhoc_getCurrentExperimentsCallback:(WXModuleKeepAliveCallback)callback
{
callback([AdhocSDKgetCurrentExperiments],YES);
}
```

##### 在@selector\(application:didFinishLaunchingWithOptions:\) 中的初始化方法之后，添加：

```
[wxsdkEngine registerModule:@“synctest”withClass:[wxSyncTestModule class]];
[wxsdkEngine registerModule:@“adhoc”withClass:[wxAdhocModule class]];
```

##### 注意：关于方法的封装可参考demo，如果有自己的方法封装规则可按照自己的规则方式，最终目的是把参数传给原生方法，调用原生framework.

### 获取试验变量

##### 打开src文件夹下面index.vue文件添加试验变量

```
getFlagClick (event) {
adhocModal.adhoc_getFlag('weexTest','weex',function(ret){
modal.toast({
message: JSON.stringify(ret),
duration: 0.8
})
})
},
```

##### 打开src文件夹下面index.vue文件添加优化指标

```
track (event) {
modal.toast({
message: 'track',
duration: 0.8
})
adhocModal.adhoc_track('weexName','1');
},
```

### webview

##### 若使用到webview，并且在webview中需要做track数据上报，需要手动集成AdhocSDK.h中的webview方法，找到WeexSDK WXWebComponent.m文件，在- \(BOOL\)webView:\(UIWebView \*\)webView shouldStartLoadWithRequest:\(NSURLRequest \*\)request navigationType:\(UIWebViewNavigationType\)navigationType中添加\[AdhocSDK adhocUIWebViewExecute:request webView:webView\];方法，来实现weex web和js交互.

```
(BOOL)webView:(UIWebView*)webView shouldStartLoadWithRequest:(NSURLRequest*)request navigationType:(UIWebViewNavigationType)navigationType
{
if(_startLoadEvent) {
NSMutableDictionary<NSString*,id> *data = [NSMutableDictionarynew];
[datasetObject:request.URL.absoluteString?:@""forKey:@"url"];
[selffireEvent:@"pagestart"params:data];
}
BOOLtmp = [AdhocSDKadhocUIWebViewExecute:requestwebView:webView];
returnYES;
}
```







