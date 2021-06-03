---
title: 在Dynamic Media中激活热链接保护
description: 有关如何在Dynamic Media中激活热链接保护的信息。
uuid: 5f93bc27-5edd-4143-8701-87896c52f0af
contentOwner: Rick Brough
topic-tags: dynamic-media
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
content-type: reference
discoiquuid: a70aa448-0f58-4ed2-9381-afcc76fa827f
role: Business Practitioner, Administrator
exl-id: 698e8bdb-9b31-49ab-8560-26b05109bb23
feature: 配置
source-git-commit: b1e0ea01688095b29d8fb18baf6fa0bda660dad5
workflow-type: tm+mt
source-wordcount: '197'
ht-degree: 0%

---

# 在Dynamic Media中激活热链接保护{#activating-hotlink-protection-in-dynamic-media}

热链接是指第三方网站使用HTML代码显示您网站中的图像时。 每次请求图片时，他们都会使用您的带宽，因为访客的浏览器直接从您的服务器访问图片。 热链接&#x200B;*protection*&#x200B;是一种方法，用于阻止其他网站直接链接到您网页上的图片、css或JavaScript。 这种防护措施有助于减少您的Dynamic Media帐户下不必要的带宽使用。

[Adobe](https://helpx.adobe.com/support.html) 支持可以在CDN（内容交付网络）级别配置反向链接过滤器，以便Dynamic Media内容仅提供给域中允许网站列表上的网站。

>[!NOTE]
>
>此功能要求您使用与Adobe Experience Manager Dynamic Media捆绑在一起的现成CDN。 此功能不支持任何其他自定义CDN。 要激活热链接保护，管理员必须创建Adobe客户关怀支持票证，以向您的Dynamic Media帐户请求配置更改。 激活热链路保护无需额外费用。
