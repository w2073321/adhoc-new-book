### 编程模式：上报指标 {#stat}

指标用于量化试验结果的好坏，AppAdhoc 后台中的试验图表根据此数据生成。

![](http://doc.appadhoc.com/_images/expsetting/stat.png "优化指标")

比如在进入某一逻辑分支后，可以统计点击次数。将上图中的指标“clickTimes”传入函数track实现上报指标, 每次累加1：

[Objective-C](javascript:;)

\|

[Swift](javascript:;)

```
- (IBAction)btnClicked:(id)sender {
    [AdhocSDK track:@"clickTimes" value:@(1)];
}
```



/\*\*

统计需要的优化指标，用以实现科学有效的测试

@param stat\_name 后台设置的优化指标，名字须保持一致

@param stat\_value 当前优化指标单次统计的权重

@param stat\_attribute 当前数据的定向条件

\*/

* \(void\)track:\(NSString \*\)stat\_name value:\(NSNumber \*\)stat\_value attribute:\(NSDictionary \*\)stat\_attribute;

stat\_attribute该参数接口属于高级功能，如有需要请联系客户经理开通。定向试验受众功能。

