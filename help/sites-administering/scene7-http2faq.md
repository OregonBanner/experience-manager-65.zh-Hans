---
title: HTTP2 内容投放常见问题解答
description: 了解HTTP2内容交付以及它如何提高Web内容的整体性能。
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
exl-id: 2428914c-5fb0-439e-a1ef-8ee30b890f58
source-git-commit: 06a6d4e0ba2aeaefcfb238233dd98e8bbd6731da
workflow-type: tm+mt
source-wordcount: '782'
ht-degree: 1%

---

# HTTP2 内容投放常见问题解答{#http-delivery-of-content-faq}

Adobe很高兴地宣布推出HTTP/2内容交付功能。 使用HTTP/2时，会注意到整体性能提升。

## 什么是HTTP/2？ {#what-is-http}

HTTP/2改进了浏览器和服务器的通信方式，允许更快地传输信息，同时减少所需的处理能力。

以下网站以简明扼要的方式介绍了HTTP/2及其好处：

[您必须了解的HTTP/2相关信息](https://www.engadget.com/2015-02-24-what-you-need-to-know-about-http-2.html).

## 使用HTTP/2进行内容交付有哪些主要好处？ {#what-are-the-key-benefits-of-moving-to-http-for-content-delivery}

性能提升差异很大，具体取决于网站代码、Dynamic Media使用方式、客户设备、屏幕和位置等因素。

Adobe自己的测试产生了以下结果：

* 对于图像，响应速度提高了7%-28%，具体取决于设备和浏览器。 性能提升最显着的是iOS设备。
* 对于查看者，加载时间性能提升了15%。

以下演示说明了HTTP/1与HTTP/2加载之间的区别：

[https://http2.akamai.com/demo](https://http2.akamai.com/demo)

## 我是否有资格切换到HTTP/2？ {#am-i-eligible-to-switch-over-to-http}

要使用HTTP/2，您必须满足以下要求：

* 对富媒体请求使用安全HTTPS。
* 使用Adobe捆绑的CDN（内容分发网络）作为Dynamic Media许可证的一部分。
* 使用专用域(即， `images.company.com` 或 `mycompany.scene7.com`)，而不是通用的Dynamic Media域(即， `s7d1.scene7.com`， `s7d2.scene7.com`，或 `s7d13.scene7.com`)。

  要查找您的域，请打开 [Dynamic Media Classic桌面应用程序](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started)，然后登录到您的公司帐户或帐户。 然后导航到 **[!UICONTROL 设置]** > **[!UICONTROL 应用程序设置]** > **[!UICONTROL 常规设置]**. 查找标记为的字段 **已发布的服务器名称**. 如果您当前使用的是通用Dynamic Media域，则可以请求在此过渡中迁移到您自己的自定义域。

## 为我的Dynamic Media帐户启用HTTP/2的过程是怎样的？ {#what-is-the-process-for-enabling-http-for-my-scene-account}

1. [使用Admin Console创建支持案例](https://helpx.adobe.com/cn/enterprise/using/support-for-experience-cloud.html) 和请求切换到HTTP/2；它不会自动为您完成。
1. 在您的支持案例中提供以下信息：

   * 主要联系人姓名、电子邮件和电话号码。
   * 要转换为HTTP2的所有域。 那就是， `images.company.com` 或 `mycompany.scene7.com`.

     要查找您的域，请打开 [Dynamic Media Classic桌面应用程序](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started)，然后登录到您的公司帐户或帐户。 然后导航到 **[!UICONTROL 设置]** > **[!UICONTROL 应用程序设置]** > **[!UICONTROL 常规设置]**. 查找标记为的字段 **[!UICONTROL 已发布的服务器名称]**.

   * 确认您使用安全HTTPS处理富媒体请求。
   * 验证您是否通过Adobe使用CDN，而不是通过直接关系进行管理。
   * 验证您使用的是专用域。 那就是， `images.company.com` 或 `mycompany.scene7.com`，而不是常规Dynamic Media域，例如 `s7d1.scene7.com`， `s7d2.scene7.com`， `s7d13.scene7.com`.

     要查找您的域，请打开 [Dynamic Media Classic桌面应用程序](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started)，然后登录到您的公司帐户或帐户。 然后导航到 **[!UICONTROL 设置]** > **[!UICONTROL 应用程序设置]** > **[!UICONTROL 常规设置]**. 查找标记为的字段 **[!UICONTROL 已发布的服务器名称]**. 如果您当前使用的是通用Dynamic Media域，则可以请求在此过渡中迁移到您自己的自定义域。

1. Adobe客户支持根据提交请求的顺序将您添加到HTTP/2客户轮候表中。
1. 当Adobe准备好处理您的请求时，支持团队会联系您以协调过渡并设置目标日期。
1. 完成后，您将收到通知，并且可以验证是否成功过渡到HTTP2。

## 我何时可以过渡到HTTP/2？ {#when-can-i-expect-to-be-transitioned-over-to-http}

将按照Adobe客户支持部门接收请求的顺序处理请求。

>[!NOTE]
>
>由于过渡到HTTP/2的过程涉及清除缓存，因此需要较长的准备时间。 因此，一次只能处理少数几个客户过渡。

## 迁移到HTTP/2会有什么风险？ {#what-are-the-risks-with-moving-to-http}

迁移到HTTP/2会清除CDN上的缓存，因为它涉及迁移到新的CDN配置。

非缓存的内容直接点击Adobe的原始服务器，直到再次重建缓存为止。 由于此操作，Adobe计划一次处理几个客户过渡，以便在从Adobe来源拉取请求时保持可接受的性能。

## 如何验证是否使用HTTP/2激活了URL或网站？ {#how-can-you-verify-whether-a-url-or-website-is-activated-with-http}

下载可以在Web浏览器中使用的扩展。 对于Firefox和Chrome，扩展名为 **[!UICONTROL HTTP/2和SPDY指示器]**. 浏览器仅安全支持HTTP/2，因此需要使用HTTPS调用URL进行验证。 如果支持HTTP/2，则扩展将以蓝色Flash符号和标头“X-Firefox-Spdy”的形式表示：“h2”。
