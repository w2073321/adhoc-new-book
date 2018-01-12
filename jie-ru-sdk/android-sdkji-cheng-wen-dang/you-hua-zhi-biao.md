1. ### 编程模式：上报指标 {#stat}

指标用于量化试验结果的好坏，AppAdhoc 后台中的试验图表根据此数据生成。 在可视化试验中，您也可以通过此方法定义上报指标。

![](http://doc.appadhoc.com/_images/expsetting/stat.png "优化指标")

比如在进入某一逻辑分支后，可以统计点击次数。将上图中的指标“clickTimes”传入函数track实现上报指标, 每次累加1：

```
AdhocTracker.track("clickTines", 1);
```

| 上报参数 | 参数值 | 说明 |
| :--- | :--- | :--- |
| trackname | clickTines | 优化指标名称 |
| number | 1 | PV上报自动+1统计数据 |

### 混淆相关 {#混淆相关}

在proguard-rules.txt文件中加入：

```
-keep classcom.adhoc.** {*;}-keep classandroid.support.v4.view.ViewPager{*;}
-keep classandroid.support.v7.widget.RecyclerView{*;}
```

### 集成调试 {#debug}

集成调试只是为验证SDK的集成是否成功（并不是真正开始试验！），详见[移动调试工具](http://doc.appadhoc.com/sdk/testTools.html)。

### 开始试验 {#开始试验}

恭喜，您完成了AppAdhoc AB Testing SDK的埋点集成工作，请通知PM或相关AB Test需求制定人员，点下开始试验按钮吧！

注意：确保app\_key, 试验变量字符串，指标字符串与后台截图处一一对应，否则可能出现异常或无试验数据情况。

