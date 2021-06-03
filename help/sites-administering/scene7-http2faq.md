---
title: HTTP2 内容交付常见问题解答
description: 了解HTTP2内容交付。
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
exl-id: 2428914c-5fb0-439e-a1ef-8ee30b890f58
source-git-commit: b1e0ea01688095b29d8fb18baf6fa0bda660dad5
workflow-type: tm+mt
source-wordcount: '773'
ht-degree: 1%

---

# HTTP2 内容交付常见问题解答{#http-delivery-of-content-faq}

Adobe很兴奋地宣布推出HTTP/2内容交付。 使用HTTP/2时，您会注意到整体性能有所提高。

## 什么是HTTP/2?{#what-is-http}

HTTP/2改进了浏览器和服务器的通信方式，允许更快地传输信息，同时降低所需的处理能力。

以下网站以简短而简单的方式介绍了HTTP/2及其好处：

[https://www.engadget.com/2015/02/24/what-you-need-to-know-about-http-2/](https://www.engadget.com/2015/02/24/what-you-need-to-know-about-http-2/)

## 迁移到HTTP/2进行内容交付有哪些主要优势？{#what-are-the-key-benefits-of-moving-to-http-for-content-delivery}

性能改进因以下因素而异：网站代码、使用Dynamic Media的方式、消费者的设备、屏幕和位置等。

Adobe自己的测试产生了以下结果：

* 对于图像，响应时间缩短了7%-28%，具体取决于设备和浏览器。 在iOS设备上，性能提升最为显着。
* 对于查看器，加载时间性能提高了15%。

以下演示说明了HTTP/1加载与HTTP/2加载之间的区别：

[https://http2.akamai.com/demo](https://http2.akamai.com/demo)

## 我是否有资格切换到HTTP/2?{#am-i-eligible-to-switch-over-to-http}

要使用HTTP/2，您必须满足以下要求：

* 对富媒体请求使用安全HTTPS。
* 将Adobe捆绑的CDN（内容交付网络）用作Dynamic Media许可证的一部分。
* 使用专用域（即`images.company.com`或`mycompany.scene7.com`），而不使用通用的Dynamic Media域（即`s7d1.scene7.com`、`s7d2.scene7.com`或`s7d13.scene7.com`）。

   要查找您的域，请打开[Dynamic Media Classic桌面应用程序](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started)，然后登录到您的公司帐户或帐户。 然后点按&#x200B;**[!UICONTROL 设置>应用程序设置>常规设置]**。 查找标有&#x200B;**Published Server Name**&#x200B;的字段。 如果您当前使用的是通用Dynamic Media域，则可以在此过渡中请求移至您自己的自定义域。

## 为我的Dynamic Media帐户启用HTTP/2的过程是什么？{#what-is-the-process-for-enabling-http-for-my-scene-account}

1. 您必须[使用Admin Console创建支持案例](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/support-for-experience-cloud.ug.html)，并请求切换到HTTP/2;它不会自动为您完成。
1. 在支持案例中提供以下信息：

   * 主要联系人姓名、电子邮件和电话号码。
   * 要过渡到HTTP2的所有域。 即`images.company.com`或`mycompany.scene7.com`。

      要查找您的域，请打开[Dynamic Media Classic桌面应用程序](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started)，然后登录到您的公司帐户或帐户。 然后点按&#x200B;**[!UICONTROL 设置]** > **[!UICONTROL 应用程序设置]** > **[!UICONTROL 常规设置]**。 查找标有&#x200B;**[!UICONTROL Published Server Name]**&#x200B;的字段。

   * 确认您对富媒体请求使用安全HTTPS。
   * 验证您是否通过Adobe使用CDN，以及是否通过直接关系进行管理。
   * 验证您使用的是专用域。 即`images.company.com`或`mycompany.scene7.com`，而不是通用的Dynamic Media域，如`s7d1.scene7.com`、`s7d2.scene7.com`、`s7d13.scene7.com`。

      要查找您的域，请打开[Dynamic Media Classic桌面应用程序](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started)，然后登录到您的公司帐户或帐户。 然后点按&#x200B;**[!UICONTROL 设置]** > **[!UICONTROL 应用程序设置]** > **[!UICONTROL 常规设置]**。 查找标有&#x200B;**[!UICONTROL Published Server Name]**&#x200B;的字段。 如果您当前使用的是通用Dynamic Media域，则可以在此过渡中请求移至您自己的自定义域。

1. 技术支持将您根据请求提交的顺序添加到HTTP/2客户等待列表。
1. 当Adobe准备好处理您的请求时，支持团队将与您联系以协调过渡并设置目标日期。
1. 完成后，系统会通知您，并可以验证是否成功过渡到HTTP2。

## 我何时可以转换到HTTP/2?{#when-can-i-expect-to-be-transitioned-over-to-http}

请求的处理顺序与技术支持部门接收请求的顺序一致。

>[!NOTE]
>
>可能会有较长的前置时间，因为过渡到HTTP/2涉及清除缓存。 因此，一次只能处理少数客户过渡。

## 迁移到HTTP/2有哪些风险？{#what-are-the-risks-with-moving-to-http}

过渡到HTTP/2会清除CDN中的缓存，因为它涉及到迁移到新的CDN配置。

非缓存内容会直接点击Adobe的源服务器，直到再次重建缓存为止。 因此，Adobe计划一次处理一些客户过渡，以便在从我们的来源提取请求时保持可接受的性能。

## 如何验证URL或网站是否已通过HTTP/2激活？{#how-can-you-verify-whether-a-url-or-website-is-activated-with-http}

您需要下载外部版本才能与Web浏览器一起使用。 对于Firefox和Chrome，有一个名为&#x200B;**[!UICONTROL HTTP/2和SPDY Indicator]**&#x200B;的扩展。 浏览器仅安全支持HTTP/2，因此需要通过HTTPS调用URL进行验证。 如果支持HTTP/2，则扩展将以蓝色Flash符号和标题“X-Firefox-Spdy”的形式指示此参数：&quot;h2&quot;。
