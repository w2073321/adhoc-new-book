### 获取试验信息和版本分配的api接口

试验集合

### Resource

GET：[https://experiment-control.appadhoc.com/apps/aeafe012-4c72-4752-99fc-72243d9d4c88/groups](https://experiment-control.appadhoc.com/apps/aeafe012-4c72-4752-99fc-72243d9d4c88/groups)

### Authorization

在参数列表里添加两个固定参数:

| 名字 | 类型 | 描述 | 示例 |
| :--- | :--- | :--- | :--- |
| appid | String | 应用appKey，请在AB测试后台“应用列表 ”页面获取 | appKey=aeafe012-4c72-4752-99fc-72243d9d4c88 |
| groups | String | 试验集合 | 606f249a-54a0-4a7c-a0a7-08e936b44f32 |
| Auth-key | Stirng | 登录时获得的Auth-key有效期七日 | Head中加入Auth-Key 606f249a-54a0-4a7c-a0a7-08e936b44f32 |



