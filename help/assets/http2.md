---
title: HTTP2 内容交付
description: 了解HTTP/2如何改进浏览器和服务器的通信方式，实现更快的信息传输，同时降低所需的处理能力。
uuid: d9deb945-bdf5-4d6b-95c8-8bae4442e618
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: c8e145ad-f021-4043-8190-62151775e296
role: User, Admin
exl-id: 9eb9f309-33e5-4694-84d2-fb2cd3de50a6
feature: Publishing,Configuration
source-git-commit: 7f8cfe155af3b8831e746ced89c11c971e429f69
workflow-type: tm+mt
source-wordcount: '735'
ht-degree: 3%

---

# HTTP/2 内容交付 {#http-delivery-of-content}

Adobe 很高兴地宣布推出 HTTP/2 内容交付功能，这意味着性能将全面提升。

>[!NOTE]
>
>此功能要求您使用与Adobe Experience Manager Dynamic Media捆绑在一起的现成CDN。 此功能不支持任何其他自定义CDN。

## 什么是HTTP/2？ {#what-is-http}

HTTP/2改进了浏览器和服务器的通信方式，允许更快地传输信息，同时减少所需的处理能力。

以下网站以简明扼要的方式介绍了HTTP/2及其好处：

[您必须了解的HTTP/2相关信息](https://www.engadget.com/2015-02-24-what-you-need-to-know-about-http-2.html)

## 使用HTTP/2进行内容交付有哪些主要好处？ {#what-are-the-key-benefits-of-moving-to-http-for-content-delivery}

性能改进可能大相径庭。 它基于许多因素，如网站代码、Dynamic Media的使用方式、消费者的设备、屏幕和位置。

Adobe自己的测试产生了以下结果：

* 对于图像，响应速度提高了7%-28%，具体取决于设备和浏览器。 性能提升最显着的是iOS设备。
* 对于查看者，加载时间性能提升了15%。

以下演示说明了HTTP/1与HTTP/2加载之间的区别：

[https://http2.akamai.com/demo](https://http2.akamai.com/demo)

## 我是否有资格切换到HTTP/2？ {#am-i-eligible-to-switch-over-to-http}

要使用HTTP/2，您必须满足以下要求：

* 对富媒体请求使用安全HTTPS。
* 使用Adobe捆绑的CDN（内容分发网络）作为Dynamic Media许可证的一部分。
* 使用专用（非company-h.assetsadobe#.com）域。

  如果您已经拥有专用域，则可以通过Adobe客户支持选择加入。

  如果您没有专用域，Adobe计划于2018年安排您过渡到HTTP/2。

## 为我的Dynamic Media帐户启用HTTP/2的过程是怎样的？ {#what-is-the-process-for-enabling-http-for-my-dynamic-media-account}

您启动切换到HTTP/2的请求；不会自动为您完成此操作。

1. 要切换到HTTP/2，请启动Adobe客户支持请求。 请参阅 [打开支持工单](https://experienceleague.adobe.com/?support-solution=General&amp;lang=en&amp;support-tab=home#support).

   1. 在您的支持请求中提供以下信息：

      1. 主要联系人姓名、电子邮件、电话。
      1. 要转换为HTTP/2的所有域。
      1. 验证您是否使用安全HTTPS处理富媒体请求。
      1. 验证您是否通过Adobe使用CDN，以及是否未通过直接关系进行管理。
      1. 验证您是否使用专用域。 如果您使用Dynamic Media，则使用专用域。

   1. 客户支持部门会根据提交请求的顺序将您添加到HTTP/2客户轮候表中。
   1. 当Adobe准备好处理您的请求时，客户支持将联系您以协调过渡并设置目标日期。
   1. 完成后，您将收到通知，并且可以验证是否成功过渡到HTTP2。

      由于浏览器未说明这一事实，因此有必要下载扩展。

      对于Firefox和Chrome，有一个名为“HTTP/2和SPDY Indicator”的扩展。 浏览器仅安全支持http/2，因此有必要使用https调用URL进行验证。 如果支持http/2，则由扩展以蓝色Flash符号和标头“X-Firefox-Spdy”的形式表示：“h2”。

## 我何时可以过渡到HTTP/2？ {#when-can-i-expect-to-be-transitioned-over-to-http}

请求将按照客户支持部门接收它们的顺序进行处理。

>[!NOTE]
>
>由于过渡到HTTP/2的过程涉及清除缓存，因此前置时间可能会很长。 因此，一次只能处理少数几个客户过渡。

## 迁移到HTTP/2会有什么风险？ {#what-are-the-risks-with-moving-to-http}

迁移到HTTP/2会清除CDN上的缓存，因为它涉及迁移到新的CDN配置。

非缓存的内容直接点击Adobe的原始服务器，直到再次重建缓存为止。 因此，Adobe计划一次处理几个客户过渡，以便在从源拉取请求时保持可接受的性能。

## 如何验证是否使用HTTP/2激活了URL或网站？ {#how-can-you-verify-whether-a-url-or-website-is-activated-with-http}

由于浏览器未说明这一事实，因此有必要下载扩展。

对于Firefox和Chrome，有一个名为“HTTP/2和SPDY Indicator”的扩展。 浏览器仅安全支持http/2，因此有必要使用https调用URL进行验证。 如果支持http/2，则它由扩展以蓝色Flash符号和标头形式指示 `X-Firefox-Spdy` ： `h2`.
