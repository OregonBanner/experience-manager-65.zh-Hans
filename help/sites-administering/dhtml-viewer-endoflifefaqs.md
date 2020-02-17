---
title: DHTML查看器生命周期结束常见问题解答
seo-title: DHTML查看器生命周期结束常见问题解答
description: 自2014年1月31日起，Scene7的DHTML查看器平台将正式终止。 此通知可解答常见问题，以便您准备过渡到我们的新HTML5查看器平台。
seo-description: 自2014年1月31日起，Scene7的DHTML查看器平台将正式终止。 此通知可解答常见问题，以便您准备过渡到我们的新HTML5查看器平台。
uuid: a78c03b3-6513-42e1-881f-6a9551659769
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: d94244ac-a5f6-4c95-ab8c-26b41d25863f
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# DHTML查看器生命周期结束常见问题解答{#dhtml-viewer-end-of-life-faqs}

自2014年1月31日起，Scene7的DHTML查看器平台将正式终止。 此通知可解答常见问题，以便您准备过渡到我们的新HTML5查看器平台。

**变化是什么？**

自2014年1月31日起，Scene7将正式终止对DHTML查看器平台的支持。

**生命终结意味着什么？**

寿命结束意味着Scene7将(1)不再向DHTML查看器平台添加任何功能增强功能(2)不再解决或发布DHTML查看器平台上的任何错误修复，并且(3)客户关怀将不再是疑难解答或提供对任何与DHTML相关的查看器问题或问题的支持。

**为什么Scene7会做出这一改变？**

Web标准不断发展，DHTML是一种较老的Web开发技术，正迅速被HTML5所取代。 DHTML作为平台的最大限制是它无法创建HTML5现在可以一致、更轻松地支持跨浏览器的丰富体验。 例如，此类限制包括缺乏对以下内容的跨浏览器支持：

* 自定义光标
* 圆角
* 动画（如页面翻转、放松）
* 效果（如阴影、发光）
* 完整的字体支持
* 无插件视频播放

特定于Scene7 DHTML查看器平台，基于JSP的解决方案和Javascript API均未针对移动设备进行优化，以利用多触和手势功能。 尽管在2011/2012年初发布的DHTML查看器针对移动设备进行了优化，但由于缺乏基于SDK组件的灵活开发框架，这些查看器难以自定义和维护。

受DHTML的这些限制以及HTML5作为跨桌面和移动设备的新兴标准的快速行业吸引力的推动，Scene7决定投资于基于HTML5的查看器平台。 这项投资将为我们的客户提供一个强大的平台，他们可以利用该平台构建更丰富、更具吸引力的交互式查看器，这些查看器可以触及包括桌面、iOS和Android设备在内的多个屏幕的用户。

**如何知道我的查看器是否使用DHTML平台？**

要确定贵公司所使用的查看器是否为DHTML并因此受此更改影响，请检查：

1. 贵公司使用下表中列出的现成Scene7查看器，其中“查看器技术”被指定为“DHTML”:

   [https://help.adobe.com/en_US/scene7/using/WS6E593DEA-7D81-4cd6-84B0-85E8BB274176.html#WS1c46793299cf21d77e926d1613177f0a020-8000](https://help.adobe.com/en_US/scene7/using/WS6E593DEA-7D81-4cd6-84B0-85E8BB274176.html#WS1c46793299cf21d77e926d1613177f0a020-8000)

1. 您的公司正在使用根据此表中现成的Scene7查看器创建为新预设的查看器，其中“查看器技术”被指定为“DHTML”:

   [https://help.adobe.com/en_US/scene7/using/WS6E593DEA-7D81-4cd6-84B0-85E8BB274176.html#WS1c46793299cf21d77e926d1613177f0a020-8000](https://help.adobe.com/en_US/scene7/using/WS6E593DEA-7D81-4cd6-84B0-85E8BB274176.html#WS1c46793299cf21d77e926d1613177f0a020-8000)

1. 您的公司使用基于JSP的DHTML解决方案创建的自定义查看器：

   [https://microsite.omniture.com/t2/help/en_US/s7/viewers_ref/index.html#JSP_Reference](https://microsite.omniture.com/t2/help/en_US/s7/viewers_ref/index.html#JSP_Reference)

1. 您的公司正在使用从Javascript API创建的自定义查看器：

   [https://microsite.omniture.com/t2/help/en_US/s7/viewers_ref/index.html#API_Reference](https://microsite.omniture.com/t2/help/en_US/s7/viewers_ref/index.html#API_Reference)

1. 您的公司使用的是使用DHTML多屏幕弹出API创建的自定义查看器：

   [https://microsite.omniture.com/t2/help/en_US/s7/viewers_ref/index.html#Multi-screen_Flyout_Viewer](https://microsite.omniture.com/t2/help/en_US/s7/viewers_ref/index.html#Multi-screen_Flyout_Viewer)

1. 您的公司使用的是使用DHTML桌面弹出API创建的自定义查看器：

   [https://microsite.omniture.com/t2/help/en_US/s7/viewers_ref/index.html#Desktop_Flyout_Viewer](https://microsite.omniture.com/t2/help/en_US/s7/viewers_ref/index.html#Desktop_Flyout_Viewer)

1. 您的公司正在使用DHTML查看器包中的设备检测库：

   在您的代码中查找“sj_deviceDetect.js”的JS包含。

   此处已由新的JS设备检测代码取代： [https://microsite.omniture.com/t2/help/en_US/s7/viewers_ref/index.html#Detecting_devices_and_browsers](https://microsite.omniture.com/t2/help/en_US/s7/viewers_ref/index.html#Detecting_devices_and_browsers) 。

**什么是替换查看器平台？**

DHTML的替换是Scene7 HTML5查看器平台，包括：

* HTML5开箱即用式查看器，可在各种查看器类型（包括基本缩放、弹出缩放、图像集、样本集、多维旋转和混合媒体）之间提供移动优化交互。 有关这些查看器的完整最新示例，请参阅： [https://microsite.omniture.com/t2/help/en_US/s7/vlist/vlist.html](https://microsite.omniture.com/t2/help/en_US/s7/vlist/vlist.html)
* HTML5查看器SDK支持对Adobe Scene7查看器进行大量自定义以用于支持HTML5的站点和设备（如iOS和Android），从而赋予查看器外观和交互性品牌最大的灵活性和创造性。 可重用性能优化组件的益处降低了查看器开发的总体成本并加快了自定义开发。

**HTML5查看器平台何时具备从DHTML查看器平台过渡所需的功能？**

Scene7于2011年秋季发布了第一个HTML5查看器SDK，并发布了版本5.5。此后，我们为平台添加了许多功能，并扩展了对越来越多类型查看器的支持。 对于大多数常见的查看器要求，HTML5查看器平台可能已具有您需要立即迁移的功能。 我们每季度都发布此查看器平台，继续大力投资。

要确定HTML5查看器平台今天是否满足查看器要求，请参阅以下文档：

[https://microsite.omniture.com/t2/help/en_US/s7/viewers_ref/index.html#About_HTML5_Viewers](https://microsite.omniture.com/t2/help/en_US/s7/viewers_ref/index.html#About_HTML5_Viewers) （适用于开箱即用查看器功能和自定义功能）

[https://help.adobe.com/en_US/scene7/using/WSd4272150f67705c11b002eec12fcba4dee6-8000.html](https://help.adobe.com/en_US/scene7/using/WSd4272150f67705c11b002eec12fcba4dee6-8000.html) （访问SDK API文档）

如果您仍不确定HTML5查看器SDK是否满足您的要求，请咨询我们的专业服务团队。

**如何将查看器转换到HTML5平台？**

要将查看器转换到HTML5平台，Scene7提供以下选项：

1. 使用Scene7现成HTML5查看器之一，其示例位于： [https://microsite.omniture.com/t2/help/en_US/s7/vlist/vlist.html](https://microsite.omniture.com/t2/help/en_US/s7/vlist/vlist.html)
1. 在SPS应用程序设置下配置一个Scene7现成HTML5查看器。 这允许您自定义某些行为，如查看器大小、过渡、缩放行为等： [https://help.adobe.com/en_US/scene7/using/WS6E593DEA-7D81-4cd6-84B0-85E8BB274176.html](https://help.adobe.com/en_US/scene7/using/WS6E593DEA-7D81-4cd6-84B0-85E8BB274176.html)
1. 通过修改CSS来更改可视设计（如按钮图稿、位置、透明度、背景颜色等），自定义Scene7现成HTML5查看器的外观： [https://microsite.omniture.com/t2/help/en_US/s7/viewers_ref/index.html#Customizing_HTML5_Viewers](https://microsite.omniture.com/t2/help/en_US/s7/viewers_ref/index.html#Customizing_HTML5_Viewers)
1. 使用SDK从头开始创建自定义HTML5查看器，可从以下网址下载该查看器： [https://help.adobe.com/en_US/scene7/using/WSd4272150f67705c11b002eec12fcba4dee6-8000.html](https://help.adobe.com/en_US/scene7/using/WSd4272150f67705c11b002eec12fcba4dee6-8000.html)。 您可以与专业服务部门合作构建自定义查看器或由您自己的Web开发团队构建它。

**那不支持HTML5的浏览器呢？**

HTML5在许多移动设备和Web浏览器中受支持，并且不断获得支持。 目前，即使Internet Explorer 8或更低版本不支持HTML5,Scene7也革新了我们的HTML5查看器平台，将支持扩展到IE 7和IE 8。 借助Scene7 HTML5查看器平台，您可以通过单个开发平台触及绝大多数桌面和移动用户。

自HTML5 SDK版本2.2.1起的当前系统要求为：

* Microsoft® Windows® XP或更高版本，Macintosh® OS X 10.6或更高版本
* Firefox 17、Safari 5.1、Chrome 23、Internet Explorer 7或更高版本
* iOS 3.2.2或更高版本
* 在iPhone3或更高版本以及iPad1或更高版本（本机浏览器）上认证
* Android OS 2.2或更高版本

要检查您的浏览器是否与我们的HTML5查看器平台兼容，请启动以下示例查看器：

[https://s7d1.scene7.com/s7viewers/html5/flyout.html?asset=Scene7SharedAssets/Sample%20Image](https://s7d1.scene7.com/s7viewers/html5/flyout.html?asset=Scene7SharedAssets/Sample%20Image)

如果通过将鼠标悬停在主图像上或将手指拖动到主图像上来查看放大的图像，则它是支持的浏览器／设备。

**如果我希望借助现有DHTML查看器保持生产实时状态，有哪些选项？**

尽管您仍可以与基于DHTML的查看器一起在生产中实时工作，但务必注意，2014年1月31日之后将不会出现增强、错误修复或客户关怀。 因此，我们强烈建议所有客户迁移到更强大的HTML5查看器平台。. 但是，如果您的业务状况在EOL日期之前阻止了此类迁移，则您可以选择与专业服务部门签订合同以延长支持的维护时间。 有关详细信息，请联系您的客户经理。

**我应与谁联系以获取更多信息？**

如果此常见问题解答未回答您的所有问题，请联系支持([s7support@adobe.com](mailto:s7support@adobe.com))或您的Adobe客户经理。
