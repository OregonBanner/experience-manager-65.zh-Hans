---
title: HTTP2内容交付
description: HTTP/2改进了浏览器和服务器的通信方式，允许更快地传输信息，同时降低所需的处理能力。
uuid: d9deb945-bdf5-4d6b-95c8-8bae4442e618
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: c8e145ad-f021-4043-8190-62151775e296
role: Business Practitioner, Administrator
exl-id: 9eb9f309-33e5-4694-84d2-fb2cd3de50a6
feature: 发布，配置
source-git-commit: b1e0ea01688095b29d8fb18baf6fa0bda660dad5
workflow-type: tm+mt
source-wordcount: '732'
ht-degree: 2%

---

# HTTP/2内容交付{#http-delivery-of-content}

Adobe 很高兴地宣布推出 HTTP/2 内容交付功能，这意味着性能将全面提升。

>[!NOTE]
>
>此功能要求您使用与Adobe Experience Manager Dynamic Media捆绑在一起的现成CDN。 此功能不支持任何其他自定义CDN。

## 什么是HTTP/2?{#what-is-http}

HTTP/2改进了浏览器和服务器的通信方式，允许更快地传输信息，同时降低所需的处理能力。

以下网站以简短而简单的方式介绍了HTTP/2及其好处：

[关于HTTP/2您必须了解的信息](https://www.engadget.com/2015-02-24-what-you-need-to-know-about-http-2.html)

## 迁移到HTTP/2进行内容交付有哪些主要优势？{#what-are-the-key-benefits-of-moving-to-http-for-content-delivery}

性能改进可能差别很大。 它基于许多因素，例如网站代码、Dynamic Media的使用方式、消费者的设备、屏幕和位置。

Adobe自己的测试产生了以下结果：

* 对于图像，响应时间缩短了7%-28%，具体取决于设备和浏览器。 在iOS设备上，性能提升最为显着。
* 对于查看器，加载时间性能提高了15%。

以下演示说明了HTTP/1加载与HTTP/2加载之间的区别：

[https://http2.akamai.com/demo](https://http2.akamai.com/demo)

## 我是否有资格切换到HTTP/2?{#am-i-eligible-to-switch-over-to-http}

要使用HTTP/2，您必须满足以下要求：

* 对富媒体请求使用安全HTTPS。
* 将Adobe捆绑的CDN（内容交付网络）用作Dynamic Media许可证的一部分。
* 使用专用（非公司 — h.assetsadobe#.com）域。

   如果您已经有专用域，则可以通过技术支持方式选择加入。

   如果您没有专用域，Adobe计划在2018年将您的转换计划为HTTP/2。

## 为我的Dynamic Media帐户启用HTTP/2的过程是什么？{#what-is-the-process-for-enabling-http-for-my-dynamic-media-account}

启动切换到HTTP/2的请求；它不会自动为您完成。

1. 要切换到HTTP/2，请启动Adobe客户关怀请求。 请参阅[访问Adobe Experience Manager支持门户](https://helpx.adobe.com/experience-manager/kb/accessing-aem-support-portal.html)。

   1. 在支持请求中提供以下信息：

      1. 主要联系人姓名、电子邮件、电话。
      1. 要过渡到HTTP/2的所有域。
      1. 验证是否对富媒体请求使用安全HTTPS。
      1. 验证您是否通过Adobe使用CDN，以及是否通过直接关系进行管理。
      1. 确认您使用专用域。 如果您使用Dynamic Media，则使用专用域。
   1. 客户关怀团队会根据请求提交的顺序将您添加到HTTP/2客户等待列表。
   1. 当Adobe准备好处理您的请求时，客户关怀团队会联系您以协调过渡并设置目标日期。
   1. 完成后会通知您，并可以验证是否成功过渡到HTTP2。

      由于浏览器未声明这一事实，因此需要下载扩展。

      对于Firefox和Chrome，有一个名为“HTTP/2和SPDY指示器”的扩展。 浏览器仅安全支持http/2，因此需要使用https调用URL进行验证。 如果支持http/2，则扩展将以蓝色Flash符号和标题“X-Firefox-Spdy”的形式指示：&quot;h2&quot;。


## 我何时可以转换到HTTP/2?{#when-can-i-expect-to-be-transitioned-over-to-http}

请求会按照客户关怀团队收到请求的顺序进行处理。

>[!NOTE]
>
>可能会有较长的前置时间，因为过渡到HTTP/2涉及清除缓存。 因此，一次只能处理少数客户过渡。

## 迁移到HTTP/2有哪些风险？{#what-are-the-risks-with-moving-to-http}

过渡到HTTP/2会清除CDN中的缓存，因为它涉及到迁移到新的CDN配置。

非缓存内容会直接点击Adobe的源服务器，直到再次重建缓存为止。 因此，Adobe计划一次处理一些客户过渡，以便在从源中提取请求时保持可接受的性能。

## 如何验证URL或网站是否已通过HTTP/2激活？{#how-can-you-verify-whether-a-url-or-website-is-activated-with-http}

由于浏览器未声明这一事实，因此需要下载扩展。

对于Firefox和Chrome，有一个名为“HTTP/2和SPDY指示器”的扩展。 浏览器仅安全支持http/2，因此需要使用https调用URL进行验证。 如果支持http/2，则扩展将以蓝色Flash符号和标头`X-Firefox-Spdy`的形式指示：`h2`。
