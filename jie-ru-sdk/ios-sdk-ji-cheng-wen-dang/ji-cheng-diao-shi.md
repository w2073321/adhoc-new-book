### 集成调试 {#debug}

集成调试只是为验证SDK的集成是否成功（并不是真正开始试验！）。

[Objective-C](javascript:;)

\|

[Swift](javascript:;)

在SDK启动时设置是否显示调试按钮

```
AdhocSDKConfig *config = [AdhocSDKConfig defaultConfig];
     //开启DEBUG模式
    config.debugAssistiveShow = YES;


[AdhocSDK startWithConfigure:config options:launchOptions];
```

在Debug模式下启动APP，会出现下图中的悬浮图标：

![](http://doc.appadhoc.com/_images/debug/ios.png "在debug模式下启动APP的悬浮图标")

点击上面的悬浮图标，扫描后台系统“集成调试”中的二维码，进入相应试验：

![](http://doc.appadhoc.com/_images/debug/scan.png "app\_key")

### 开始试验 {#开始试验}

恭喜，您完成了AppAdhoc AB Testing SDK的埋点集成工作，请通知PM或相关AB Test需求制定人员，点下开始试验按钮吧！

注意：确保app\_key, 试验变量字符串，指标字符串与后台截图处一一对应，否则可能出现异常或无试验数据情况。

