---
title: HTTP2内容交付
description: HTTP/2改进了浏览器和服务器通信的方式，允许更快地传输信息，同时降低了所需的处理能力。
uuid: d9deb945-bdf5-4d6b-95c8-8bae4442e618
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: c8e145ad-f021-4043-8190-62151775e296
translation-type: tm+mt
source-git-commit: 0595d89409e0ca21f771be5c55c3ec9548a8449f

---


# HTTP2内容交付 {#http-delivery-of-content}

Adobe很高兴地宣布推出HTTP/2内容交付，同时提高性能的总体优势。

## 什么是HTTP/2? {#what-is-http}

HTTP/2改进了浏览器和服务器的通信方式，允许更快地传输信息，同时降低所需的处理能力。

以下网站以简单简单的方式介绍了HTTP/2及其优势：

[https://www.engadget.com/2015/02/24/what-you-need-to-know-about-http-2/](https://www.engadget.com/2015/02/24/what-you-need-to-know-about-http-2/)

## 转到HTTP/2进行内容交付有哪些主要优点？ {#what-are-the-key-benefits-of-moving-to-http-for-content-delivery}

性能改进因网站代码、Dynamic Media的使用方式、消费者设备、屏幕和位置等因素而异。

Adobe自己的测试产生了以下结果：

* 对于图像，响应时间根据设备和浏览器的不同提高了7%-28%。 在iOS设备上，性能提高最显着。
* 对于查看器，加载时间性能提高了15%。

以下演示说明了HTTP/1与HTTP/2加载之间的区别：

[https://http2.akamai.com/demo](https://http2.akamai.com/demo)

## 我是否有资格切换到HTTP/2? {#am-i-eligible-to-switch-over-to-http}

要使用HTTP/2，您必须满足以下要求：

* 为富媒体请求使用安全HTTPS。
* 将Adobe捆绑的CDN（内容交付网络）作为Dynamic media许可证的一部分。
* 使用专用（非公司-h.assetsadobe#.com）域。

   如果您已经有专用域，则可以通过技术支持选择加入。

   如果您没有专用域，Adobe将安排您在2018年过渡到HTTP/2。

## 为我的Dynamic Media帐户启用HTTP/2的过程是什么？ {#what-is-the-process-for-enabling-http-for-my-dynamic-media-account}

您必须启动切换到HTTP/2的请求；它不会自动为您完成。

1. 启动技术支持请求以切换到HTTP2。 请参 [阅访问AEM支持门户](https://helpx.adobe.com/experience-manager/kb/accessing-aem-support-portal.html)。

   1. 在您的支持请求中提供以下信息：

      1. 主要联系人姓名、电子邮件、电话。
      1. 要过渡到HTTP2的所有域。
      1. 验证您是否在对富媒体请求使用安全HTTPS。
      1. 验证您是否正通过Adobe使用CDN，且未以直接关系进行管理。
      1. 验证您使用的是专用域。 如果您使用Dynamic Media，则表示您已使用专用域。
   1. 技术支持将根据请求的提交顺序将您添加到HTTP/2客户等候列表。
   1. 当Adobe准备好处理您的请求时，支持部门将与您联系以协调过渡并设置目标日期。
   1. 完成后，您将收到通知，并可以验证是否成功转换到HTTP2。

      由于浏览器不声明这一事实，因此必须下载扩展。

      对于Firefox和Chrome，有一个名为“HTTP/2和SPDY Indicator”的扩展。 浏览器仅安全地支持http/2，因此必须使用https调用URL进行验证。 如果支持http/2，则此扩展以蓝色Flash符号和标题“X-Firefox-Spdy”的形式表示：“h2”。


## 我何时可以期望转换为HTTP/2? {#when-can-i-expect-to-be-transitioned-over-to-http}

请求将按技术支持收到的顺序进行处理。

>[!NOTE]
>
>可能存在较长的提前期，因为向HTTP/2的过渡涉及清除缓存。 因此，一次只能处理几个客户过渡。

## 转向HTTP/2有哪些风险？ {#what-are-the-risks-with-moving-to-http}

过渡到HTTP/2会清除CDN中的缓存，因为它涉及到新的CDN配置。

非缓存内容会直接点击Adobe的源服务器，直到重新构建缓存。 因此，Adobe计划一次处理几个客户过渡，以便在从我们的来源提取请求时保持可接受的性能。

## 如何验证是否使用HTTP/2激活了URL或网站？ {#how-can-you-verify-whether-a-url-or-website-is-activated-with-http}

由于浏览器不声明这一事实，因此必须下载扩展。

对于Firefox和Chrome，有一个名为“HTTP/2和SPDY Indicator”的扩展。 浏览器仅安全地支持http/2，因此必须使用https调用URL进行验证。 如果支持http/2，则此扩展以蓝色Flash符号和标题“X-Firefox-Spdy”的形式表示：“h2”。
