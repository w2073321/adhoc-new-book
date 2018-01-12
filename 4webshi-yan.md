## Web平台的A/B测试 {#web平台的ab测试}

本章将介绍web页面或网站进行A/B测试的几种方式。

在开始A/B测试前，请确保您已经[创建应用](http://doc.appadhoc.com/appExp/createApp.html)并且进行试验的页面已经正确[集成SDK](http://doc.appadhoc.com/sdk/htmlSDK.html)。

* 可视化模式试验： 针对单个页面，进行简单的图片、文本替换和编辑，元素位置移动等操作，完全通过界面操作生成试验方案。 此模式适用于比较独立的页面，局部的测试内容，只要网页中集成了SDK，就不再需要进行代码工作。 [如何操作](http://doc.appadhoc.com/H5exp/Visual.html)

* 编程模式试验： 使用SDK中给出的API来定义试验版本和统计事件，功能灵活，能够生成更加复杂的测试方案。 [如何操作](http://doc.appadhoc.com/H5exp/coding.html)

* 多链接合并试验 将多个URL作为不同的试验版本，当访问特定的URL时，会分流到各试验版本中。 此模式更适用于变化较大，功能较单一的推广营销页面。 [如何操作](http://doc.appadhoc.com/H5exp/URLsplite.html)

* 针对频繁进行的着陆页优化试验，AppAdhoc提供一种新的操作方式，避免重复进行埋点，可以更方便的发布试验。[如何操作](http://doc.appadhoc.com/appExp/lpotest.html)



