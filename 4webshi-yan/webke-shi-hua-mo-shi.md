## Web可视化试验过程 {#web可视化试验过程}

在这部分中，我们以通过改变按钮颜色，预期提升按钮点击率为例，来说明如何使用H5可视化编辑器。先通过一张简单的流程图了解所需的步骤，再一步步进行具体操作： ![](http://doc.appadhoc.com/_images/design/visualflow.png "具体操作")

### 1 试验方案 {#1-试验方案}

一个完整的A/B 测试需要根据目前已有的用户数据进行分析判断，推断并建立假设，才能针对性的做出改变和调整，**根据具体需求，构建产品A/B 测试的需求文档，即明确本次试验的几个要素。**

在本次示例中，设计试验版本为红色按钮，对照组为原始的绿色按钮，优化指标为按钮的点击次数。

### 2 新建试验 {#new}

进入您的应用界面，此处示例为\[AppAdhocH5页面DEMO\]，选择 **新建试验** 。 ![](http://doc.appadhoc.com/_images/expsetting/create_h5visual.png "具体操作")

为了方便寻找，可以将此次测试的内容设置为试验名称。

选择分层：您可以为每一个新创建的试验设置所在层，在同一层的试验流量互斥，可以保证试验互不干扰。如果两个试验在不同层，那么流量可能会重叠，同一个用户可能会同时进入不同层的多个试验。如果选择分层，请自行确保试验内容互不干扰。详情参考[分层流量](http://doc.appadhoc.com/expFlow/stratifiedFlow.html)。

在此步骤中需要填写您本次试验页面的链接。请注意链接的大小写是否正确，以及页面中有无多余的参数。 在完全匹配模式下，用户访问的网页链接需要与您填写的地址完全对应才会进入试验。

请注意填写的页面链接是否包含非关键参数。

例如链接 [http://example.com/A.html?xxx](http://example.com/A.html?xxx) 其中?xxx可能表示渠道参数等，其实际页面地址为 [http://example.com/A.html](http://example.com/A.html) 。

如果您填写 .../A.html ，则用户访问 .../A.html 或者 .../A.html?xxx 都可以正常进入试验。

如果填写 .../A.html?xxx ，则用户访问.../A.html 时不会进入试验。

在模糊匹配模式下，可使用通配符\*代替任意字符串，例如：[http://www.appadhoc.com/\*.html。](http://www.appadhoc.com/*.html。)

同时 ，您需要填写一个真实的完整链接用于加载编辑器，例如：[http://www.appadhoc.com/index.html。](http://www.appadhoc.com/index.html。)

在使用模糊匹配规则时，可通过此链接 [http://www.appadhoc.com/url-match-test.html](http://www.appadhoc.com/url-match-test.html) 来进行验证是否匹配成功，链接匹配成功才会命中试验。

---

在进行下一步前，请确保已经在试验页面的head部分加入[SDK初始化](http://doc.appadhoc.com/sdk/htmlSDK.html#init)代码。

---

### 3 试验版本 {#ver}

点击下一步进入网页可视化编辑器，AppAdhoc A/B Testing已自动创建试验版本一，同时可看到需测试页面的原始版本。  
在编辑器中，选择您需要编辑的元素，然后根据菜单展示功能进行操作即可。需要注意的是，编辑器只能选中子元素，如果您想要编辑的元素无法选中， 请尝试选中相关元素后，选择上级元素。  
![](http://doc.appadhoc.com/_images/expsetting/h5editor.png "具体操作")

退出可视化编辑器后在”试验版本“面板中编辑版本一的名称和说明，在这里我们将其命名为「演示版本一」。

操作完成后记得点击保存按钮，如果不保存退出编辑器将会丢失所做的操作。

### 4 优化指标 {#stat}

退出编辑器后，您可以找到优化指标表格，查看并管理已添加的指标

![](http://doc.appadhoc.com/_images/expsetting/create_stat1.png "使用步骤")

* 点击「跟踪元素点击」，进入可视化编辑器添加优化指标。
* 点击「添加编程指标」，可直接绑定编程优化指标，请注意在代码中集成，并保证指标名称一致。
* 新建优化指标，请注意命名格式，以英文字母开头，可以使用数字和下划线。
* 已创建过的优化指标将会保留，在其他试验中可以直接选择已有优化指标添加，如果是编程指标，代码无需更改。

**（1）追踪元素点击**  
如果只需要知道某个元素的点击次数，可以在编辑器中选中元素，然后选择 **跟踪元素点击** ，关联指定的优化指标即可。

创建按钮点击次数为新的优化指标BtnClick，命名支持英文、数字和下划线。

![](http://doc.appadhoc.com/_images/expsetting/h5editor1.png "使用步骤")

**（2）编程指标**  
有时想要统计的数据不是单纯的点击事件，而是“支付成功”这类需要逻辑判断的事件，您需要通过代码来定义事件并上报。在上述表格中选择添加编程指标，填写指标名称及说明。之后在代码中，触发事件的地方集成代码，其中"event\_name"需要替换为您的优化指标名称：

```
adhoc('track', 'event_name', 1);
```

---

event\_name为实验平台填写的优化指标名称，请确保与平台优化指标名称保持一致。

---

有关优化指标的集成详情参考[集成说明](http://doc.appadhoc.com/sdk/htmlSDK.html#stat)。

有关复合指标的说明请参考[此处](http://doc.appadhoc.com/expFlow/stat.html#comstat)。

### 5 集成调试 {#debug}

在编辑器中操作完毕后，记得点击保存，然后退出编辑器。  
确认试验版本和优化指标内容无误，点击完成创建，将会跳转到集成调试界面。在此界面中，点击预览版本，可以直接在浏览器中预览页面的真实效果，此预览链接转发有效。  
![](http://doc.appadhoc.com/_images/debug/h5visual.png "使用步骤")

操作后，也会获取到对应的指标数据，可以在此界面中预览。调试数据不会影响到真实试验数据。  
![](http://doc.appadhoc.com/_images/debug/data.png "使用步骤")

### 6 调整流量 {#flow}

点击完成调试，将会跳转到运行控制界面。在此界面中您可以调整试验流量、运行或结束试验。

请为此次试验分配流量，访问到链接的用户将会按照您设定的百分比看到所展现的页面。未参与到试验中的用户将会看到原始页面，并且不会上报数据。  
即使是试验开始运行后，也可以调整流量，所做的调整将会及时生效。

**请注意100%的流量不代表所有用户都会参与试验，以及在同一层中，某试验占用的流量不能再被分配到其他试验中**。 有关流量的详细说明请参考[流量分配](http://doc.appadhoc.com/expFlow/stratifiedFlow.html)。 ![](http://doc.appadhoc.com/_images/expsetting/flow.png "使用步骤")

### 7 运行试验 {#7-运行试验}

恭喜！现在可以开始运行您的A/BTesting方案了，记得关注试验数据，以便及时调整流量，做出应对策略。有关数据分析请参考[此处](http://doc.appadhoc.com/runAnalysis)。

