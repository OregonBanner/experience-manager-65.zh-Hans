---
title: 在Dynamic Media中激活热链接保护
description: 有关如何在Dynamic Media中激活热链接保护的信息。
contentOwner: Rick Brough
topic-tags: dynamic-media
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
content-type: reference
role: User, Admin
exl-id: 698e8bdb-9b31-49ab-8560-26b05109bb23
feature: Configuration
source-git-commit: 04050f31742c926b45235595f6318929d3767bd8
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 0%

---

# 在Dynamic Media中激活热链接保护 {#activating-hotlink-protection-in-dynamic-media}

热链接是指第三方网站使用HTML代码显示您网站中的图像的情况。 每次请求图片时，他们都会使用您的带宽，因为访客的浏览器会直接从您的服务器访问图片。 热链接 *保护* 是一种方法，用于阻止其他网站直接链接到您网页上的图片、CSS或JavaScript。 这种屏蔽有助于减少Dynamic Media帐户下不必要的带宽使用。

[Experience Manager客户支持](https://experienceleague.adobe.com/?support-solution=Experience+Manager#support) 可以在CDN（内容分发网络）级别配置反向链接过滤器，以便Dynamic Media内容仅提供给域中允许网站列表中的网站。

>[!NOTE]
>
>此功能要求您使用与Adobe Experience Manager Dynamic Media捆绑在一起的现成CDN。 此功能不支持任何其他自定义CDN。 要激活热链接保护，管理员必须创建Adobe客户支持支持工单以请求对您的Dynamic Media帐户进行配置更改。 激活热链接保护不需要额外付费。
