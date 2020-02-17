---
title: HTTP2内容交付常见问题解答
seo-title: HTTP2内容交付常见问题解答
description: 了解HTTP2内容交付。
seo-description: 了解HTTP2内容交付。
uuid: e837c3e0-6e48-46f1-b510-847c9976807a
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: afbe9f80-c2a3-4a46-b9d6-4c9406667d7f
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# HTTP2内容交付常见问题解答{#http-delivery-of-content-faq}

Adobe很高兴地宣布推出HTTP/2内容交付。 使用HTTP/2时，您会注意到总体性能有所提高。

## 什么是HTTP/2? {#what-is-http}

HTTP/2改进了浏览器和服务器的通信方式，允许更快地传输信息，同时降低所需的处理能力。

以下网站以简单快捷的方式介绍了HTTP/2及其优点：

[https://www.engadget.com/2015/02/24/what-you-need-to-know-about-http-2/](https://www.engadget.com/2015/02/24/what-you-need-to-know-about-http-2/)

## 转到HTTP/2进行内容交付有哪些主要优点？ {#what-are-the-key-benefits-of-moving-to-http-for-content-delivery}

性能改进因网站代码、Scene7的使用方式、消费者设备、屏幕和位置等因素而异。

Adobe自己的测试产生了以下结果：

* 对于图像，响应时间根据设备和浏览器的不同提高了7%-28%。 在iOS设备上，性能提高最显着。
* 对于查看器，加载时间性能提高了15%。

以下演示说明了HTTP/1与HTTP/2加载之间的区别：

[https://http2.akamai.com/demo](https://http2.akamai.com/demo)

## 我是否有资格切换到HTTP/2? {#am-i-eligible-to-switch-over-to-http}

要使用HTTP/2，您必须满足以下要求：

* 为富媒体请求使用安全HTTPS。
* 将Adobe捆绑的CDN（内容交付网络）作为Dynamic Media Classic许可证的一部分。
* 使用专用域(即或 `images.company.com``mycompany.scene7.com`)，而不是通用Dynamic Media Classic域(即、、 `s7d1.scene7.com`或 `s7d2.scene7.com``s7d13.scene7.com`)。

   要查找您的域，请 [登录每个公司帐户的Scene7 Publishing System](https://www.adobe.com/marketing-cloud/experience-manager/scene7-login.html) 实例。

   单击“ **[!UICONTROL 设置”>“应用程序设置”>“常规设置”]**。 查找标有“已发布服务 **器名称”的字段**。 如果您当前使用的是通用Scene7域，则可以请求移至您自己的自定义域作为此过渡的一部分。

## 为我的Dynamic Media Classic帐户启用HTTP/2的过程是什么？ {#what-is-the-process-for-enabling-http-for-my-scene-account}

您必须发起Adobe技术支持(`s7support@adobe.com`)请求，以切换到HTTP/2;它不会自动为您完成。

1. 在您的支持请求中提供以下信息：

   * 主要联系人姓名、电子邮件和电话号码。
   * 要过渡到HTTP2的所有域。 就是， `images.company.com` 或者 `mycompany.scene7.com`。
   要查找您的域，请 [登录每个公司帐户的Scene7 Publishing System](https://www.adobe.com/marketing-cloud/experience-manager/scene7-login.html) 实例。

   单击“ **[!UICONTROL 设置”>“应用程序设置”>“常规设置”]**。 查找标有“已发布服务 **[!UICONTROL 器名称”的字段]**。

   * 验证是否对富媒体请求使用安全HTTPS。
   * 验证您是否通过Adobe使用CDN，而不是以直接关系进行管理。
   * 验证您使用的是专用域。 即，或 `images.company.com` 者， `mycompany.scene7.com`不是通用的Scene7域， `s7d1.scene7.com`如 `s7d2.scene7.com`、 `s7d13.scene7.com`。
   要查找您的域，请 [登录每个公司帐户的Scene7 Publishing System](https://www.adobe.com/marketing-cloud/experience-manager/scene7-login.html) 实例。

   单击“ **[!UICONTROL 设置”>“应用程序设置”>“常规设置”]**。 查找标有“已发布服务 **[!UICONTROL 器名称”的字段]**。 如果您当前使用的是通用Scene7域，则可以请求移至您自己的自定义域作为此过渡的一部分。

   1. 技术支持会根据请求的提交顺序将您添加到HTTP/2客户等候列表。
   1. 当Adobe准备好处理您的请求时，支持部门将与您联系以协调过渡并设置目标日期。
   1. 完成后，您将收到通知，并可以验证是否成功过渡到HTTP2。



## 我何时可以期望转换为HTTP/2? {#when-can-i-expect-to-be-transitioned-over-to-http}

请求的处理顺序由技术支持部门接收。

>[!NOTE]
>
>可能存在较长的提前期，因为向HTTP/2的过渡涉及清除缓存。 因此，一次只能处理几个客户过渡。

## 转向HTTP/2有哪些风险？ {#what-are-the-risks-with-moving-to-http}

过渡到HTTP/2会清除CDN中的缓存，因为它涉及到新的CDN配置。

非缓存内容会直接点击Adobe的源服务器，直到重新构建缓存。 因此，Adobe计划一次处理几个客户过渡，以便在从我们的来源提取请求时保持可接受的性能。

## 如何验证是否使用HTTP/2激活了URL或网站？ {#how-can-you-verify-whether-a-url-or-website-is-activated-with-http}

您需要下载外部才能与Web浏览器一起使用。 对于Firefox和Chrome，有一个名为 **[!UICONTROL HTTP/2和SPDY Indicator的扩展]**。 浏览器仅安全地支持HTTP/2，因此必须使用HTTPS调用URL进行验证。 如果支持HTTP/2，则这由蓝色Flash符号形式的扩展和标题“X-Firefox-Spdy”表示：“h2”。
