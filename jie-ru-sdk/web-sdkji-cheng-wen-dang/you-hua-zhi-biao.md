
---

### 上报指标 {#stat}

指标用于量化试验结果的好坏，AppAdhoc 后台中的试验图表根据此数据生成。在可视化试验和多链接合并试验中，您也可以通过此方法定义上报指标。

注意：指标值应由PM或相关AB Test需求制定人员在后台提前录入完毕，如下图“优化指标”红线部分：

![](http://doc.appadhoc.com/_images/expsetting/stat.png "优化指标")

比如在进入某一逻辑分支后，可以统计点击次数。将上图中的指标“clickTimes”传入函数实现上报指标, 每次累加1：

```
<
button href="" onclick="adhoc('track', 'clickTimes', 1)"
>
统计点击次数
<
/button
>
```

| 函数名称 | 函数值 | 说明 |
| :--- | :--- | :--- |
| onclick | onclick | 点击事件 |
| track | track | track方法用于上报优化指标 |
| startname | clickTimes | 优化指标名称 |
| number | 1 | 上报点击次数PV自动+1 |

#### 跳转链接的指标统计 {#跳转链接的指标统计}

针对跳转链接的事件跟踪，为保证事件成功上报，请使用以下方法。此回调方法将返回指标上报是否成功的结果，您可根据返回的结果进一步处理。

```
<
!-- a标签 --
>
<
a href="http://example.com/link"  onclick="adhoc('track', 'statname', 1, function(){ location.href = 'url' }); return false;"
>
 跳转链接 
<
/a 
>
```

```
<
!-- 非a标签 --
>
<
div onclick="adhoc('track', 'statname', 1, function(){ location.href = 'url' });" 
>
<
/div
>
```

| 上报函数位置 | 说明 | 函数值 |
| :--- | :--- | :--- |
| a | 跳转按钮标签\(优化指标埋点位置\) | a |
| div | 父类控件可直接添加按钮\(优化指标埋点位置\) | div |
| location.href | 跳转链接地址，用于测试整体页面改版转化率的AB测试 | ‘ url ’\(链接地址写这里\) |
| function | 调用方法名称 | 函数名 |

---

