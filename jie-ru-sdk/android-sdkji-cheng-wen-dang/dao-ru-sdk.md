### 导入SDK {#导入sdk}

将下载得到的 SDK JAR拖入到的AndroidStudio / Eclipse 工程根目录libs中\(没有则新建\)，右键Add as Library添加到库：（示意图，实际包名以最新版本为准）

![](http://doc.appadhoc.com/_images/code/android1.png "导入SDK")

然后在libs文件夹和添加的\*.jar文件下鼠标单击菜单 add as library

![](/assets/05085215-d1249c6b36cb4803bcf633f91c96122c.png)

然后在选择项目单击Open Module Settings，在Dependencies中选择添加文件

![](/assets/导如文件.png)

### 加入网络和SDCARD读写权限 {#加入网络和sdcard读写权限}

在项目中找到项目配置文件 AndroidManifest.xml，加入网络访问权限和SDCARD读写权限：

```
<
uses-permission android:name="android.permission.INTERNET"/
>
<
uses-permission android:name="android.permission.ACCESS_NETWORK_STATE"/
>
<
uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE"/
>
```



