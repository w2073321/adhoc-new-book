## iOS /H5 混合SDK\(优化版\)

#### 1.导入SDK

导入[iOS 的SDK](http://doc.appadhoc.com/sdk/iosSDK.html#sdk)，与编程模式导入方法相同

#### 2.初始化SDK

将下载得到的 AdhocSDK.framework 拖入到xcode工程里，集成方法与SDK集成相同

注:请不要延迟SDK的初始化，会导致无法监听到AppDelegate里的方法，无法加载Flags信息，可视化试验无法正常渲染。

请勿在SDK基础上进行自行封装，以免影响到试验逻辑，造成试验无法正常运行。

#### 3.调用SDK

\(1\).在在调用UIwebview的控制器.M文件中，添加UIwebview的代理方法

@interfaceAdhocUIWebViewVC \(\) &lt;UIWebViewDelegate&gt;

在调用UIwebview的控制器页面添加如下代码

* \(BOOL\)webView:\(UIWebView\*\)webViewshouldStartLoadWithRequest:\(NSURLRequest\*\)requestnavigationType:\(UIWebViewNavigationType\)navigationType; {

//调用SDK协议方法

if\(\[AdhocSDKadhocUIWebViewExecute:requestwebView:webView\]\) {

returnNO;

```
}
```

returnYES;

}

\(2\).如果使用WKwebview请检查 TARGETS--&gt; Build Phases --&gt; Link Binary With Libraries 选项下是否已经加入 AdhocSDK.framework，如果没有，请手动加入。并手动链接webkit.framework

在调用WKwebview的控制器.M文件中，添加WKwebview的代理方法&lt;WKNavigationDelegate,WKUIDelegate&gt;\(\)

在调用WKwebview的控制器页面添加如下代码

-\(void\)webView:\(WKWebView \*\)webView decidePolicyForNavigationAction:\(WKNavigationAction \*\)navigationActiondecisionHandler:\(void \(^\)\(WKNavigationActionPolicy\)\)decisionHandler; {

//调用SDK协议方法,这里调用JS的SDK

```
[AdhocSDK adhocWKWebViewExecute:navigationAction.request webView:webView];
```

decisionHandler\(WKNavigationActionPolicyAllow\);

}

#### 4.设置变量值

adhocShop//优化指标名称

在参加试验的web页面下添加如下方法

function adhocShop\(flag\_value\) {

```
            if (flag_value == true) {

                //我是实验一

            } else {

                //我是实验二

            }
```

再点击事件的触发条件div或者a后面添加如下代码

onclick="adhoc\('track', 'BtnClick', 1\)"

注意adhocShop这两个函数名称必须保持一致

恭喜，您完成了AppAdhoc AB Testing 跨平台SDK的埋点集成工作，请通知PM或相关AB Test需求制定人员，点下开始试验按钮吧！

