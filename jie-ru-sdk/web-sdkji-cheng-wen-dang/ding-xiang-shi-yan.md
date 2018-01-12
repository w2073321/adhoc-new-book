
---

### 高级功能 自定义受众定向（需要联系管理员开启） {#orientation}

AppAdhoc Web SDK 会自动把浏览器名称、版本、语言等用户标签自动上传，开发者也可以根据需要给当前用户打上合适的自定义标签，进而实现将不符合条件的用户排除在此次试验之外。比如只想要女性用户，或30岁以下的用户参与试验等。最好在init前调用。

注意：自定义受众定向条件应由PM或相关AB Test需求制定人员在后台提前录入完毕。

在运行控制/右侧定向试验：

![](http://doc.appadhoc.com/_images/audience/button.png "受众定向")

选择分组，点击编辑用户群：

![](http://doc.appadhoc.com/_images/audience/dialog.png "受众定向")

即得到受众条件的key，在下图例子中，“sex”是key：

![](http://doc.appadhoc.com/_images/audience/setting1.png "受众定向")

自定义受众定向：

普通自定义初始化方法，将图下代码加入参与实验的页面head部分：

```
……
<
head
>
<
script src='https://sdk.appadhoc.com/ab.plus.js'
>
<
/script
>
<
script
>
        adhoc('init', {
            appKey: 'your app key',
            custom: {sex: 'male', age: '20'}//自定义受众条件            
        })
<
/script
>
<
/head
>
……
```

| 函数名称 | 函数值 | 说明 |
| :--- | :--- | :--- |
| init | init | 初始化方法名 |
| custom | custom | 自定义受众条件方法名 |
| sex | male | 受众条件\(必须与平台填写条件一致\) |
| age | 20 | 受众条件\(必须与平台填写条件一直\) |
| your appkey | ADHOC\_ac66bf61\_7608\_4a5f\_9e7c0f9694f | 创建应用的授权标识 |

“app\_key” 是在登录 AppAdhoc 后台创建“应用”之后获得的该“应用”的授权标识。

可在AppAdhoc控制台应用列表找到，如下图红线部分：

![](http://doc.appadhoc.com/_images/app/appkey.png "app\_key")

---

API 参考

[Web SDK API 参考](http://www.appadhoc.com/jsapi/reference/adhoc.html)

### 开始试验 {#开始试验}

恭喜，您完成了AppAdhoc AB Testing Web SDK的埋点集成工作，请通知PM或相关AB Test需求制定人员，点下开始试验按钮吧！

注意：确保app\_key, 试验变量字符串，指标字符串与后台截图处一一对应，否则可能出现异常或无试验数据情况。

