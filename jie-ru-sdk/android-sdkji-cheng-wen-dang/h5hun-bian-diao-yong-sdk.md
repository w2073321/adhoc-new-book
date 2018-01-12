### Android /H5 混合SDK {#导入sdk}

该SDK用于Android Hybrid 模式下,H5页面的以下情形：

* 用户以app或单个设备为单位，进行H5页面的试验

* 离线缓存模式H5页面的试验

SDK的使用方法如下：

### 1.导入SDK {#加入网络和sdcard读写权限}

将下载得到的 SDK JAR拖入到的AndroidStudio / Eclipse 工程根目录libs中\(没有则新建\)，右键Add as Library添加到库：（示意图，实际包名以最新版本为准）

![](http://doc.appadhoc.com/_images/code/android1.png "导入SDK")

手动添加Hybrid所需文件，如果使用Webview，手动添加‘adhoc.js’到当前项目

### 2.SDK初始化 {#加入网络和sdcard读写权限}

导入com.通过webview实例调用setWebView方法，设置AdhocWebClient对象，或者继承AdhocWebViewClient类，代码如下：

WebViewwebView = \(WebView\) findViewById\(R.id.webView\);

webView.getSettings\(\).setJavaScriptEnabled\(true\);

webView.setWebViewClient\(new AdhocWebViewClient\(\)\);

### 3.开始试验 {#加入网络和sdcard读写权限}

在上面两步操作之后，就可以在相应的H5页面进行试验，试验方式与基本的web sdk试验方式基本一致

1\)      在相关\`html\`文件中引入\`adhoc.js\`文件

2\)      获取试验变量

AdhocHybrid.getFlag\(flag\_name/变量名称,default\_value, callBack\)

3\)      在callback函数里根据变量的值展示相应的试验版本

4\)      上报指标

AdhocHybrid.track\(stat\_name/指标名称, stat\_value/上报值,stat\_attribute/事件属性\)

恭喜，您完成了AppAdhoc AB Testing SDK的埋点集成工作，请通知PM或相关AB Test需求制定人员，点下开始试验按钮吧！

注意：确保app\_key, 试验变量字符串，指标字符串与后台截图处一一对应，否则可能出现异常或无试验数据情况。



