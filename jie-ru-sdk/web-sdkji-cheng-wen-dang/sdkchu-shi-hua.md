### JS SDK初始化 {#init}

在您的参加试验的页面head部分，直接引入SDK：

```
……
<head>
<script src='https://sdk.appadhoc.com/ab.plus.js'>
</script>
<script>
        adhoc('init', {
            appKey: 'your app key',
            defaultFlags: {isNewHomePage: false} //仅用于编程模式：设置试验变量默认值（获取试验变量失败时使用）
        })
</script>
</head>
……
```

在可视化模式试验中，不需要设置变量默认值。  
注意：如果没有初始化，其他 API 调用均会出错，建议在 ab.plus.js 加载之后尽快调用试验变量。

“app\_key” 是在登录 AppAdhoc 后台创建“应用”之后获得的该“应用”的授权标识。

可在AppAdhoc控制台应用列表找到，如下图红线部分：

![](http://doc.appadhoc.com/_images/app/appkey.png "app\_key")

请勿在SDK基础上进行自行封装，以免影响到试验逻辑，造成试验无法正常运行。如果确有自行封装的需求，请与客户经理联系，获取注意事项。

