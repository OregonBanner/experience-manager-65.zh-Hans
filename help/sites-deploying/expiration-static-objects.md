---
title: 静态对象的过期
seo-title: 静态对象的过期
description: 了解如何配置AEM，以便静态对象不会过期（在合理的时间段内）。
seo-description: 了解如何配置AEM，以便静态对象不会过期（在合理的时间段内）。
uuid: ee019a3d-4133-4d40-98ec-e0914b751fb3
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
discoiquuid: 73f37b3c-5dbe-4132-bb60-daa8de871884
feature: 配置
exl-id: bfd5441c-19cc-4fa8-b597-b1221465f75d
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '437'
ht-degree: 0%

---

# 静态对象的过期{#expiration-of-static-objects}

静态对象（例如，图标）不会发生更改。 因此，应该配置系统，以便它们不会过期（在合理的时间段内），从而减少不必要的流量。

这具有以下影响：

* 卸载来自服务器基础架构的请求。
* 当浏览器在浏览器缓存中缓存对象时，提高页面加载的性能。

过期由HTTP标准指定，内容涉及文件的“过期”（例如，请参阅[RFC 2616](https://www.ietf.org/rfc/rfc2616.txt) &quot;超文本传输协议 — HTTP 1.1&quot;的第14.21章）。 此标准使用标头来允许客户端缓存对象，直到它们被视为过时；这些对象被缓存指定的时间长度，而不对原始服务器进行任何状态检查。

>[!NOTE]
>
>此配置与调度程序完全分离（且不适用于）。
>
>Dispatcher的用途是在AEM之前缓存数据。

所有非动态且随时间不变的文件都可以且应该缓存。 Apache HTTPD服务器的配置可能如下所示之一 — 具体取决于环境：

>[!CAUTION]
>
>在定义将对象视为最新的时间段时，必须小心。 由于在指定的时间段到期之前没有检查&#x200B;*，因此客户端最终可以从缓存中显示旧内容。*

1. **对于创作实例：**

   ```xml
   LoadModule expires_module modules/mod_expires.so
   <Location /libs>
     ExpiresByType text/css "access plus 1 month"
     ExpiresByType text/javascript "access plus 1 month"
     ExpiresByType image/png "access plus 1 month"
     ExpiresByType image/gif "access plus 1 month"
   </Location>
   ```

   这允许中间缓存（例如浏览器缓存）最多存储一个月的CSS、Javascript、PNG和GIF文件，直到它们过期。 这意味着无需从AEM或Web服务器请求它们，但可以保留在浏览器缓存中。

   网站的其他部分不应缓存在创作实例上，因为它们随时可能发生更改。

1. **对于发布实例：**

   ```xml
   LoadModule expires_module modules/mod_expires.so
   <Location /content>
     ExpiresByType text/css "access plus 1 day"
     ExpiresByType text/javascript "access plus 1 day"
     ExpiresByType image/png "access plus 1 day"
     ExpiresByType image/gif "access plus 1 day"
   </Location>
   <Location /etc/designs>
     ExpiresByType text/css "access plus 1 day"
     ExpiresByType text/javascript "access plus 1 day"
     ExpiresByType image/png "access plus 1 day"
     ExpiresByType image/gif "access plus 1 day"
   </Location>
   ```

   这允许中间缓存（例如浏览器缓存）在客户端缓存中存储长达一天的CSS、Javascript、PNG和GIF文件。 尽管此示例说明了`/content`和`/etc/designs`下所有内容的全局设置，但您应该使其更加精细。

   根据网站更新频率，还可以考虑缓存HTML页面。 合理的时间段为1小时：

   ```xml
   <Location /content>
     ExpiresByType text/html "access plus 1 hour"
   </Location>
   ```

配置静态对象后，在选择保存此类对象的页面时，扫描`request.log`，以确认没有为静态对象发出（不必要的）请求。
