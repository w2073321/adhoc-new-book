### 微信和小程序集成注意点 {#stat}

adhoc\('init',{

appKey:'your appkey',//客户的appKey，必填

clientId:undefined,//客户自定义的clientId，选填

custom:{},//客户自定义tag，选填

defaultFlags:{},//自定义默认flags，在获取flag失败时使用，选填

stopUrlParams:false,//多链接模式跳转试验版本时是否带上原始版本的url参数，选填

filterUrlParams:false,//多链接模式和可视化是否完全匹配url参数\(如果要开启的话，需要在多链接的所有版本中都设置为true\)，选填

protocol:window.location.protocol,//sdk发送请求所使用的协议，选填

domain:'appadhoc.com',//私有化部署设置域名，选填

crossDomain:undefined//跨页面统计设置主域名，选填

}\);

1.初始化就只能放在openid的callback中

问题：刚才出现了一种现象，清完数据进来，第一次进来是手机号绑定，再进来一次是芝麻信用绑定，之后又进来5次，每次都是芝麻信用绑定整个过程都是使用的同一台设备,

原因：绑定微信openid后，如果用户访问渠道分为微信朋友圈公众号，网页链接两种。

[https://wechat-staging.letote.cn/plans?utm\_source=xxx&utm\_campaign=xxx&utm\_medium=kol](https://wechat-staging.letote.cn/plans?utm_source=xxx&utm_campaign=xxx&utm_medium=kol)

如果客户使用staging链接访问页面，customer id的hash值作为用户访问的唯一标识，这样adhoc会判定同一台设备为两个用户和微信进入版本不是同一个唯一标识。

我猜测问题可能和flag.get\(key\)的时机有关系，因为只有等adhoc\("getflag"，callback\)callback返回后才是真正的版本，在这个之前调用返回的是初始化时填写的默认值

解决方案：如果H5页面入口包含朋友圈和网页链接两种方式，建议将staging网页链接中的customer id改成和微信的openid一样的标识，不然adhoc会识别在同一台设备上，通过不同方式进入页面的用户为两个不同的用户。

