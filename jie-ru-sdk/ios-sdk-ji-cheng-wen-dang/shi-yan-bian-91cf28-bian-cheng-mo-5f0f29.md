### 编程模式：根据“试验变量”展示相应内容 {#flag}

在编程模式中，“试验变量”的值决定了展示的内容或程序的逻辑。可视化试验可跳过此步骤。

注意：试验变量值应由PM或相关A/B Testing需求制定人员在后台提前录入完毕，如下图“版本管理”红线部分：

![](http://doc.appadhoc.com/_images/expsetting/flag.png "app\_key")在调用SDK之前，记得在AppDelegate.m中引用头文件：

```
#import "AdhocSDK/AdhocSDK.h"
```

展示相应内容需要两步：

1.获取AppAdoc 后台试验变量

[Objective-C](javascript:;)

\|

[Swift](javascript:;)

```
[AdhocSDK getFlag:@"isNewHomePage" default:@(NO)]
```

2.再根据所获取的试验变量设置来执行不同版本的代码，在相应的测试页面添加代码

[Objective-C](javascript:;)

\|

[Swift](javascript:;)

```
- (void)viewWillAppear:(BOOL)animated {
      [super viewWillAppear:animated];
      //获取Boolean类型的试验变量isNewHomePage的值
      BOOL isNewHomePage = [[AdhocSDK getFlag:@" isNewHomePage " default:@(NO)] boolValue];
      if (isNewHomePage) {
          //跳转至新首页
      } else {
          //跳转至旧首页
      }
  }
```

---

| 参数名称 | 参数值 | 说明 |
| :--- | :--- | :--- |
| getFlag | isNewHomePage | 区别实验版本的标识，与平台变量名称一致 |
| fefault | false | 对应试验版本返回值 |

其中，'isNewHomePage' 即是“试验变量“，应与上图中红线标识保持一致。

请注意在用户访问到试验页面时，需要触发所有变量才算作进入试验，否则将不会上报试验数据。在此示例中，“AdhocSDK getFlag:@" isNewHomePage " default:@\(NO\)\] boolValue”算作触发变量“isNewHomePage”。

