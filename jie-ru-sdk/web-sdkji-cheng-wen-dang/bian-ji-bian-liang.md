
---

### 编程模式：根据“试验变量”展示相应内容 {#flag}

在编程模式中“试验变量”的值决定了展示的内容或程序的逻辑。多链接试验和可视化试验不需要此步骤。

注意：试验变量值应由PM或相关A/B Testing需求制定人员在后台提前录入完毕，如下图“版本管理”红线部分：

展示相应内容需要两步：

1.获取AppAdoc 后台试验变量

通过在您的 Web 页面上参与实验的控件处调用 adhoc\('getFlags', callback\) 来完成的：\(以一个按钮为例\)

带跳转链接的控件

```
!-- a标签 --
>
<
a href="http://example.com/link"  onclick="adhoc('getFlags', 'applyFlags');"
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
div onclick="adhoc('getFlags', 'applyFlags');" 
>
<
/div
>
```

```
不带跳转链接的控件
<
button href="" onclick="adhoc('getFlags', applyFlags)"
>
测试获得试验变量
<
/button
>
```

| 函数名称 | 函数值 | 函数含义 |
| :--- | :--- | :--- |
| getFlags | getFlags | 调用方法名 |
| callback | applyFlags | 回调函数名称 |

2.定义 callback 函数，在函数中根据此页面所使用的试验变量值，显示不同的页面内容。 callback 是一个 callback 函数，需要在页面代码中定义该函数，在此函数中完成模块相关的操作，模块 flags 通过函数参数传入。![](http://doc.appadhoc.com/_images/expsetting/flag.png "app\_key")

```
……
<
body
>
<
script
>
    function applyFlags(flags) {
      if (flags.get('isNewHomePage') === true) {
        var text = " Hey，我是试验版 :) ";
      } else {
        var text = " Hey, 我是原始版本！";
      }
      document.getElementById('flags').innerHTML = text;
    }
<
/script
>
……
```

| 函数名称 | 函数值 | 说明 |
| :--- | :--- | :--- |
| flag\_name | isNewHomePage | 变量名称 |
| callback | applyFlages | 返回值名称 |
| flags.get | 方法名称 | 获取flag值的get方法 |

其中，'isNewHomePage' 即是“试验变量“，应与上图中红线标识保持一致，上面的示例代码在获取是否是新的首页后，操作了DOM。

请注意在用户访问到试验页面时，需要触发试验内包含的所有变量才算作进入试验，否则将不会上报试验数据。

在此示例中，“flags.get\('isNewHomePage'\)”算作触发变量“isNewHomePage”。请勿在非试验页面或公用head模板中调用。

注意：如果网络速度较慢，在此 callback 中处理页面的展示可能会造成页面的闪烁。对于涉及到的界面变动部分，建议使用[adhoc\('hide'\)](http://www.appadhoc.com/jsapi/reference/adhoc.html#.hide)和[adhoc\('show'\)](http://www.appadhoc.com/jsapi/reference/adhoc.html#.show)方法控制元素的隐藏和展示时机。

---



