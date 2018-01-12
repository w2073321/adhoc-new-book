### 导入SDK {#导入sdk}

[Objective-C](javascript:;)

将下载得到的 AdhocSDK.framework 拖入到的Xcode工程目录Supporting Files中，在弹出的options界面中勾选 Copy items if needed，并确保 Add to targets 勾选相应的 target：

![](http://doc.appadhoc.com/_images/code/ios1.png "引入SDK")

检查 TARGETS --&gt; Build Phases --&gt; Link Binary With Libraries 选项下是否已经加入 AdhocSDK.framework，如果没有，请手动加入。并手动链接libsqlite3.dylib和libicucore.tbd：

![](http://doc.appadhoc.com/_images/code/ios2.png "引入SDK")

在 TARGETS --&gt; Build Settings 选项下 Other Linker Flags 中设置链接器参数： -ObjC。

![](http://doc.appadhoc.com/_images/code/ios3.png "链接器参数")

### 权限设置 {#权限设置}

1.在info.plist文件中添加相机权限： ![](http://doc.appadhoc.com/_images/code/ios5.png "相机")

2.为了保证用户的唯一性，SDK将设备ID存储在本地Keychain中，iOS10需在Capabilities中打开Keychain sharing ![](http://doc.appadhoc.com/_images/code/ios6.png "相机")

