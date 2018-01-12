### SDK初始化 {#init}

在调用SDK之前，记得在AppDelegate.m中引用头文件：

```
#import "AdhocSDK/AdhocSDK.h"
```

在@selector\(application:didFinishLaunchingWithOptions:\)中：

[Objective-C](javascript:;)

---

```
AdhocSDKConfig *config = [AdhocSDKConfig defaultConfig];
    //平台获得的Appkey必要
    config.appKey = @"ADHOC_5dc7130b-27ad-444e-9694-ececa7c88f89";
    //debug悬浮窗开关
    config.debugAssistiveShow = YES;
    //统计访问时长   
    config.backgroundInterval = 60;
    //统计crash崩溃次数     
    config.crashTrackEnabled = YES;
    //统计访问次数
    config.sessionTrackEnabled = YES;
    //统计访问时长
    config.durationTrackEnabled = YES;
    //设置定向条件
    config.customProperty = nil;
    //自定义clientid
    config.clientID  = @"adhoc_test_tuiku";
    [AdhocSDK startWithConfigure:config options:launchOptions];
```

---

| 参数名称 | 参数值 | 说明 |
| :--- | :--- | :--- |
| appkey | ADHOC\_ac66bf61-7608-4a5f-9bc4-9e7 | 创建应用的授权标识\(必要参数\) |
| customProperty | nill | 设置定向条件\(可选\) |
| clientid | adhoc\_test\_tuiku | 自定义clientid，高级功能\(联系客户经理开通\) |
| debugAssistiveShow | YES | debug模式开关\(可选\) |
| backgroundInterval | 60 | 统计app后台允许的最大停留时长\(可选\) |
| crashTrackEnabled | YES | 统计崩溃次数\(可选\) |
| sessionTrackEnabled | YES | 统计访问次数\(可选\) |
| durationTrackEnabled | YES | 统计app一次访问的时长\(可选\) |

并设置appKey为 AppAdhoc 后台的app\_key值。“app\_key” 是在登录 AppAdhoc 后,创建“应用”之后获得的授权标识。

可在AppAdhoc控制台应用列表找到， 如下图红线部分：

![](http://doc.appadhoc.com/_images/app/appkey.png "app\_key")

注:请不要延迟SDK的初始化，会导致无法监听到AppDelegate里的方法，无法加载Flags信息，可视化试验无法正常渲染。

请勿在SDK基础上进行自行封装，以免影响到试验逻辑，造成试验无法正常运行。

