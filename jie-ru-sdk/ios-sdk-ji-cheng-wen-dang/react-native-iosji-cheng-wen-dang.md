# React-native-ios/Android

## 安装

```
npm install react-native-adhoc --save
```

## 配置

### 链接原生库

```
react-native link
```

### iOS SDK 初始化

找到 AppDelegate.m 文件， 引用头文件：

`#import "AdhocSDK.h"`

在 @selector\(application:didFinishLaunchingWithOptions:\) 中：

```
AdhocSDKConfig *config = [AdhocSDKConfig defaultConfig];
config.appKey = @“ADHOC_xxx”;
config.debugAssistiveShow = YES;
[AdhocSDK startWithConfigure:config options:launchOptions];
```

### Android SDK 初始化

在Application的onCreate方法中初始化原生SDK

```
AdhocConfig adhocConfig = new AdhocConfig.Builder()
        //设置App上下文(必要参数)
        .context(this)
        //设置Appkey(必要参数)
        .appKey(key)
        //全部配置参考官网
        .build();

AdhocTracker.init(adhocConfig);

```

## SDK

所有的 API 都能在 [react-native-adhoc/index.js](https://github.com/AppAdhoc/react-native-adhoc/blob/master/index.js) 中查到。

引入 react-native-adhoc

```
import  AdhocSDK  from 'react-native-adhoc'
```

#### API

* getFlag\(String, Any, Function\)

  获取后台设置的指定的实验变量的值，实验变量的名字注意与后台保持一致

  ```
  AdhocSDK.getFlag('flag_nameXXX', 7, flagValue =
  >
   {

  });
  ```

* track\(String, Number\)

  统计需要的优化指标，用以实现科学有效的测试

  ```
  AdhocSDK.track('stat_nameXXX', 7);
  ```

* trackWithAttribute\(String, Number, Dictionary\)

  统计需要的优化指标（可以添加附加信息），用以实现科学有效的测试

  ```
  AdhocSDK.trackWithAttribute('stat_nameXXX', 7, {name: 'Tom', age: 18});
  ```

* trackPageView\(\)

  统计页面 PV

  ```
  AdhocSDK.trackPageView();
  ```

* getCurrentExperiments\(Function\)

  获取当前设备所在实验的实验名列表

  ```
  AdhocSDK.getCurrentExperiments(experiments =
  >
   {

  });
  ```

* getCurrentExperimentsAndExperimentsID\(Function\)

  获取当前设备所在实验的实验名列表和实验ID

  ```
  AdhocSDK.getCurrentExperimentsAndExperimentsID(experiments =
  >
   {

  });
  ```

* asynchronousGetFlag\(String, Any, Number, Function\)

  异步方式从服务器直接获取实验变量的值

  ```
  AdhocSDK.asynchronousGetFlag('flagName', 'defaultValue', 10, flagValue =
  >
   {

  });
  ```

* handleWebViewMessage\(Object, String\)

  WebView 调用 flag 接口

  ```
  <
  WebView
            ref={'webview'}
            source={require('./index.html')}
            style={{width: 375, height: 220}}
            onMessage={(e) =
  >
   {
              AdhocSDK.handleWebViewMessage(this.refs.webview, e.nativeEvent.data);
            }}
          /
  >
  ```



