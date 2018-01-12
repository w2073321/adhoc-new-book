### 编程模式：根据“试验变量”展示相应内容 {#flag}

试验变量的值决定了展示的内容或程序的逻辑。试验变量在编程模式试验中创建，可视化试验无需此步骤。

注意：试验变量值应由PM或相关A/B Testing需求制定人员在后台提前录入完毕，如下图“版本管理”红线部分：

![](http://doc.appadhoc.com/_images/expsetting/flag.png "your\_app\_key")

获取变量的值，请在使用到该变量处添加以下代码：

请注意不要在Appllication 类文件中添加获取变量方法。

```
//获取Boolean类型的试验变量isNewHomePage的值，第二个参数为设定默认值，在网络异常时将按照该默认值执行
if
 (AdhocTracker.getFlag(
"isNewHomePage"
, 
false
)) {
//跳转至新首页
} 
else
 {
//跳转至旧首页
}
```

|  |
| :--- |


| 函数名称 | 函数值 | 函数含义 |
| :--- | :--- | :--- |
| getFlag | getFlag | 调用方法名 |
| isNewHomePage | false | 试验变量名称 |

其中，'isNewHomePage' 即是“试验变量“，应与上图中红线标识保持一致。

请注意在用户访问到试验页面时，需要调用过所有变量才算作进入试验，否则将不会统计试验数据。

