当在集成调试或功能测试中出现无法正确显示版本或无法上报指标的问题时，可按照以下步骤排查。

# **H5/Web试验**

### **1.    检查请求是否正常**

![](/assets/问题排查1.png)

在sdk集成正确的情况下，进入试验页面，应该出现两个请求：get\_flags\_async和tracker。

l  如果没有看到这两个请求，那表示sdk集成不正确，请重新按照步骤集成sdk；

l  如果出现红色异常请求，则可能是本地网络问题。

#### **2.    检验变量返回是否正常**

![](/assets/问题排查2.png)

检验flags变量返回值是否与页面展示版本相吻合。如果不吻合，则可能为sdk集成有误，请重新检查sdk集成。

#### **3.    检验指标上报是否正常**

![](/assets/问题排查3.png)

检验3项：

Experiment\_ids：当显示以“Control”开头的字符串，表明不在试验里。当显示以“Debug”开头的字符串时，表明是调试模式。其余情况均为正常试验。

Key：对应的指标名称

Value：指标值

如果3项中有问题，可能为sdk集成问题，请重新集成sdk。





若经过以上步骤排查，依然没有解决问题，请及时联系对应的CSM。



# **Android和iOS试验**

       Android，iOS的排查需要用到Charles等抓包工具。Charles的设置方法可参考：；（注意iOS10.3版本以上需要额外证书：[http://www.neglectedpotential.com/2017/04/trusting-custom-root-certificates-on-ios-10-3/](http://www.neglectedpotential.com/2017/04/trusting-custom-root-certificates-on-ios-10-3/)）

### **1.    检查请求是否正常**

![](/assets/问题排查4.png)

在sdk集成正确的情况下，进入试验页面，应该出现两个请求：get\_flags\_async和tracker。

l  如果没有看到这两个请求，那表示sdk集成不正确，请重新按照步骤集成sdk；

l  如果出现unknow，则是charles没有配置成功，请检查配置。

### **2.    检验变量返回是否正常**

![](/assets/问题排查5.png)

检验flags变量返回值是否与页面展示版本相吻合。如果不吻合，则可能为sdk集成有误，请重新检查sdk集成。

### **3.    检验指标上报是否正常**

![](/assets/问题排查6.png)

检验3项：

Experiment\_ids：当显示以“Control”开头的字符串，表明不在试验里。当显示以“Debug”开头的字符串时，表明是调试模式。其余情况均为正常试验。

Key：对应的指标名称

Value：指标值

如果3项中有问题，可能为sdk集成问题，请重新集成sdk。





若经过以上步骤排查，依然没有解决问题，请及时联系对应的CSM。



  


