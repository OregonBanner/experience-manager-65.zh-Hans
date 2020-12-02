---
title: DHTML 查看器生命周期结束常见问题解答
seo-title: DHTML 查看器生命周期结束常见问题解答
description: 自2014年1月31日起，Scene7的DHTML查看器平台将正式停用。 此通知为您提供常见问题解答，以便您能够为此过渡准备到我们新的HTML5查看器平台。
seo-description: 自2014年1月31日起，Scene7的DHTML查看器平台将正式停用。 此通知为您提供常见问题解答，以便您能够为此过渡准备到我们新的HTML5查看器平台。
uuid: a78c03b3-6513-42e1-881f-6a9551659769
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: d94244ac-a5f6-4c95-ab8c-26b41d25863f
translation-type: tm+mt
source-git-commit: 283802809d665cd979e2f1a4fa969b6ddc491ed6
workflow-type: tm+mt
source-wordcount: '1665'
ht-degree: 0%

---


# DHTML 查看器生命周期结束常见问题解答{#dhtml-viewer-end-of-life-faqs}

自2014年1月31日起，Scene7的DHTML查看器平台将正式停用。 此通知为您提供常见问题解答，以便您能够为此过渡准备到我们新的HTML5查看器平台。

**有什么变化？**

自2014年1月31日起，Scene7将正式终止对DHTML查看器平台的支持。

**生命终结意味着什么？**

寿命结束意味着Scene7将(1)不再向DHTML查看器平台添加任何功能增强功能(2)不再解决或发布DHTML查看器平台上的任何错误修复，并且(3)客户关怀将不再是与DHTML相关的查看器问题或问题的疑难解答或支持。

**Scene7为何要做出这一改变？**

Web标准不断发展，DHTML是一种较旧的Web开发技术，正迅速被HTML5所取代。 作为平台，DHTML的最大局限性在于它无法创造HTML5现在可以一致、更轻松地支持跨浏览器的丰富体验。 例如，此类限制包括缺乏对以下产品的跨浏览器支持：

* 自定义光标
* 圆角
* 动画（如页面翻转、放松）
* 效果（如阴影、发光）
* 完整的字体支持
* 无插件视频播放

特定于Scene7DHTML查看器平台，基于JSP的解决方案和Javascript API未针对移动设备进行优化，以利用多触和手势功能。 尽管2011/2012年初发布的DHTML查看器针对移动设备进行了优化，但由于缺少基于SDK组件的灵活开发框架，它们很难进行自定义和维护。

受DHTML的这些限制以及HTML5作为跨桌面和移动设备的新兴标准的快速行业吸引力的推动，Scene7已决定投资于基于HTML5的查看器平台。 这项投资将优惠我们的客户一个强大的平台，他们可以利用该平台构建更丰富、更具吸引力的交互式查看器，这些查看器可以触及使用多种屏幕的用户，包括桌面、iOS和Android设备。

**如何知道我的查看器是否使用DHTML平台？**

要确定您的公司使用的查看器是DHTML，并因此受此更改影响，请检查：

1. 您的公司正在使用此表中列出的现成Scene7查看器，其中“查看器技术”被指定为“DHTML”:

   [https://help.adobe.com/en_US/scene7/using/WS6E593DEA-7D81-4cd6-84B0-85E8BB274176.html#WS1c46793299cf21d77e926d1613177f0a020-8000](https://help.adobe.com/en_US/scene7/using/WS6E593DEA-7D81-4cd6-84B0-85E8BB274176.html#WS1c46793299cf21d77e926d1613177f0a020-8000)

1. 您的公司正在使用根据本表中现成的Scene7查看器创建为新预设的查看器，其中“查看器技术”被指定为“DHTML”:

   [https://help.adobe.com/en_US/scene7/using/WS6E593DEA-7D81-4cd6-84B0-85E8BB274176.html#WS1c46793299cf21d77e926d1613177f0a020-8000](https://help.adobe.com/en_US/scene7/using/WS6E593DEA-7D81-4cd6-84B0-85E8BB274176.html#WS1c46793299cf21d77e926d1613177f0a020-8000)

1. 公司正在使用从基于JSP的DHTML解决方案创建的自定义查看器：

   [https://microsite.omniture.com/t2/help/en_US/s7/viewers_ref/index.html#JSP_Reference](https://microsite.omniture.com/t2/help/en_US/s7/viewers_ref/index.html#JSP_Reference)

1. 您的公司正在使用从Javascript API创建的自定义查看器：

   [https://microsite.omniture.com/t2/help/en_US/s7/viewers_ref/index.html#API_Reference](https://microsite.omniture.com/t2/help/en_US/s7/viewers_ref/index.html#API_Reference)

1. 您的公司正在使用使用DHTML多屏幕弹出API创建的自定义查看器：

   [https://microsite.omniture.com/t2/help/en_US/s7/viewers_ref/index.html#Multi-screen_Flyout_Viewer](https://microsite.omniture.com/t2/help/en_US/s7/viewers_ref/index.html#Multi-screen_Flyout_Viewer)

1. 您的公司正在使用使用DHTML桌面弹出API创建的自定义查看器：

   [https://microsite.omniture.com/t2/help/en_US/s7/viewers_ref/index.html#Desktop_Flyout_Viewer](https://microsite.omniture.com/t2/help/en_US/s7/viewers_ref/index.html#Desktop_Flyout_Viewer)

1. 您的公司正在使用DHTML查看器包中的设备检测库：

   在您的代码中查找“sj_deviceDetect.js”的JS。

   此代码已被新的JS设备检测代码替换：[https://microsite.omniture.com/t2/help/en_US/s7/viewers_ref/index.html#Detecting_devices_and_browsers](https://microsite.omniture.com/t2/help/en_US/s7/viewers_ref/index.html#Detecting_devices_and_browsers)。

**什么是替换查看器平台？**

DHTML的替代产品是Scene7HTML5查看器平台，包括：

* HTML5开箱即用式查看器，在各种查看器类型（包括基本缩放、弹出缩放、图像集、样本集、多维旋转和混合媒体）上提供移动优化交互。 有关这些查看器的完整最新示例，请参阅：[https://microsite.omniture.com/t2/help/en_US/s7/vlist/vlist.html](https://microsite.omniture.com/t2/help/en_US/s7/vlist/vlist.html)
* HTML5查看器SDK，支持针对HTML5支持的站点和设备（如iOS和Android）对Adobe Scene7查看器进行大量自定义，为品牌化查看器外观和交互性赋予最大的灵活性和创造性。 可重用性能优化组件的优势降低了查看器开发的总体成本并加快了自定义开发。

**HTML5查看器平台何时具备过渡DHTML查看器平台所需的功能？**

Scene7于2011年秋发布了第一个HTML5查看器SDK，并发布了5.5版。自那以后，我们为该平台添加了许多功能，并扩展了对越来越多类型查看器的支持。 对于大多数常见的查看器要求，HTML5查看器平台可能已具备您需要立即迁移的功能。 我们每季度都发布此查看器平台，并继续大力投资。

要确定HTML5查看器平台现在能否满足查看器要求，请参阅以下文档：

[https://microsite.omniture.com/t2/help/en_US/s7/viewers_ref/index.html#About_HTML5_Viewers](https://microsite.omniture.com/t2/help/en_US/s7/viewers_ref/index.html#About_HTML5_Viewers) （适用于开箱即用查看器功能和自定义功能）

[https://help.adobe.com/en_US/scene7/using/WSd4272150f67705c11b002eec12fcba4dee6-8000.html](https://help.adobe.com/en_US/scene7/using/WSd4272150f67705c11b002eec12fcba4dee6-8000.html) （访问SDK API文档）

如果您仍不确定HTML5查看器SDK是否满足您的要求，请咨询我们的专业服务团队。

**如何将我的查看者过渡到HTML5平台？**

要将观众过渡到HTML5平台，Scene7优惠了以下选项：

1. 使用Scene7现成的HTML5查看器，其示例可在以下网址找到：[https://microsite.omniture.com/t2/help/en_US/s7/vlist/vlist.html](https://microsite.omniture.com/t2/help/en_US/s7/vlist/vlist.html)
1. 在SPS应用程序设置下配置一个Scene7现成的HTML5查看器。 这将允许您自定义某些行为，如查看器大小、过渡、缩放行为等：[https://help.adobe.com/en_US/scene7/using/WS6E593DEA-7D81-4cd6-84B0-85E8BB274176.html](https://help.adobe.com/en_US/scene7/using/WS6E593DEA-7D81-4cd6-84B0-85E8BB274176.html)
1. 通过修改CSS来更改可视设计（如按钮图稿、位置、透明度、背景颜色等），自定义Scene7现成HTML5查看器的外观：[https://microsite.omniture.com/t2/help/en_US/s7/viewers_ref/index.html#Customizing_HTML5_Viewers](https://microsite.omniture.com/t2/help/en_US/s7/viewers_ref/index.html#Customizing_HTML5_Viewers)
1. 使用SDK从头开始创建自定义HTML5查看器，可从以下网址下载：[https://help.adobe.com/en_US/scene7/using/WSd4272150f67705c11b002eec12fcba4dee6-8000.html](https://help.adobe.com/en_US/scene7/using/WSd4272150f67705c11b002eec12fcba4dee6-8000.html)。 您可以与专业服务联系以构建自定义查看器，也可以由您自己的Web开发团队构建。

**不支持HTML5的浏览器如何？**

HTML5在许多移动设备和Web浏览器上都受支持，并且继续受到欢迎。 目前，尽管Internet Explorer 8或更低版本不支持HTML5，但Scene7已创新HTML5查看器平台，将支持扩展至IE 7和IE 8。 借助Scene7HTML5查看器平台，您可以通过单个开发平台触及绝大多数桌面和移动用户。

HTML5 SDK版本2.2.1的当前系统要求为：

* Microsoft® Windows® XP或更高版本，Macintosh® OS X 10.6或更高版本
* Firefox 17、Safari 5.1、Chrome 23、Internet Explorer 7或更高版本
* iOS 3.2.2或更高版本
* 在iPhone3或更高版本以及iPad1或更高版本（本机浏览器）上认证
* Android OS 2.2或更高版本

要检查您的浏览器是否与我们的HTML5查看器平台兼容，请启动以下示例查看器：

[https://s7d1.scene7.com/s7viewers/html5/flyout.html?asset=Scene7SharedAssets/Sample%20Image](https://s7d1.scene7.com/s7viewers/html5/flyout.html?asset=Scene7SharedAssets/Sample%20Image)

如果您通过悬停鼠标或将手指拖动到主图像上来查看放大的图像，则它是支持的浏览器／设备。

**如果要借助现有DHTML查看器保持生产实时状态，有哪些选项？**

尽管您仍可以与基于DHTML的查看器一起在生产环境中实时工作，但务必注意，2014年1月31日之后将不会进行任何增强、错误修复或客户关怀。 因此，我们强烈建议所有客户迁移到更强大的HTML5查看器平台。. 但是，如果您的业务状况在EOL日期之前阻止了此类迁移，您可以选择与专业服务部门签订合同，以延长支持的维护时间。 有关详细信息，请联系您的客户经理。

**我应与谁联系以了解更多信息？**

如果此常见问题解答未回答您的所有问题，请[使用Admin Console创建支持案例](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/support-for-experience-cloud.ug.html)或与Adobe客户经理联系。
