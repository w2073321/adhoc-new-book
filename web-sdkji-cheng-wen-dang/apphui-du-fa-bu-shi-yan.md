## 试验场景

本例中，我们针对iOS app里一个新的功能模块进行灰度发布。把“流量直充”功能换成新的“诈骗短信鉴定”功能，新的功能模块如下：

![](/assets/灰度发布试验场景.png)

### 

#### 灰度发布试验目标

* 确保用户使用新功能稳定，如果有bug，将bug影响降低到最低。
* 新功能不会影响整体app使用情况，核心指标：七日留存率不能下降，业务指标：新功能入口转化不少于旧入口转化。
* 本次灰度发布针对北京地区用户率先实施，iOS平台。

## 创建试验

本例中，需要创建关于iOS的编程试验，一般创建过程参考：[iOS 试验](http://doc.appadhoc.com/mobileexp/Visualios.html)。

##### 区分灰度版本

在平台上创建变量is\_new\_function，包含两个值，true和false。通过变量值来区分新功能版本和旧功能版本，true表示用户看到新功能，false表示用户看到旧功能

##### ![](/assets/灰度发布创建试验变量.png)灰度受众

根据需求，需要创建针对北京的受众定向灰度发布（一般步骤参考：受众定向）。

1.首先创建受众分组“北京用户”

![](/assets/灰度发布创建受众群体.png)

2.试验中选中“北京用户”分群

![](/assets/灰度发布创建受众用户群体.png)

## 代码集成

一般的iOS代码集成参考：[iOS sdk集成](http://doc.appadhoc.com/sdk/iosSDK.html)，与本例灰度发布相关的代码集成步骤包括：

助您执行操作。

* ##### 区分灰度版本

在用户进入首页时，通过Get\_flags获取变量值，由此来决定用户看到新功能的首页还是旧功能的首页，通过分支结构让用户进入不同的首页，从而进入不同的功能流程。

```
AdhocSDK.getFlag("is_new_function", default: false).boolValue



override func viewWillAppear(animated: Bool) {

      super.viewWillAppear(animated)

          //获取Boolean类型的试验变量is_new_function的值

      let isNewFunction = AdhocSDK.getFlag("is_new_function",         default: false).boolValue

      if isNewHomePage == true {

          //展示新功能

      } else {

          //展示旧功能

      }

  }
```

* ##### 灰度受众

北京地区的用户维度数据，需要通过接口上报吆喝，代码集成如下：

（在初始化代码中）

```
 config.customProperty = [“district”: Beijing]
```

* ##### 指标上报

在用户点击功能模块时上报指标function\_click

```
func btnClicked(btn: UIButton) {

    AdhocSDK.track("clickTimes", value: 1)

}
```

以上步骤设置完成之后，便可以开始灰度发布。

## 开始灰度发布

在上线集成好新功能的app版本之后，便可以在平台上点击“开始”，开始灰度发布。

![](/assets/灰度发布开始发布.png)

开始之后，应当按照一定的策略调节流量，如：先放5%的流量给新功能，观察指标表现，然后以2天为一个周期，流量不断放大为2倍，直到全量发布。

在灰度发布过程中，应当密切关注两类指标：

技术指标：如新功能是否存在崩溃，后台服务器压力是否大等等

业务指标：新功能入口转化率，七日留存率。

## 全量发布或回滚

在灰度发布的过程中，若技术指标和业务指标均符合预期，则可以按照流量调节策略，直到全量发布。

一旦在某一个节点发生问题，如后台服务器压力过高，则停止流量调节，保持在原地，根据是否可以快速解决问题决定是否继续灰度发布；如客户反馈bug增多，则应当迅速回滚（新功能版本流量调节至0），减少损失。

## 

### 



