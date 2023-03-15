---
title: 静态对象过期
seo-title: Expiration of Static Objects
description: 了解如何配置AEM以使静态对象在合理的时间内不过期。
seo-description: Learn how to configure AEM so that static objects do not expire (for a reasonable period of time).
uuid: ee019a3d-4133-4d40-98ec-e0914b751fb3
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
discoiquuid: 73f37b3c-5dbe-4132-bb60-daa8de871884
feature: Configuring
exl-id: bfd5441c-19cc-4fa8-b597-b1221465f75d
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '414'
ht-degree: 0%

---

# 静态对象过期{#expiration-of-static-objects}

静态对象（例如图标）不会更改。 因此，系统应配置为它们不会过期（在合理的时间段内），从而减少不必要的流量。

这将产生以下影响：

* 从服务器基础架构卸载请求。
* 提高页面加载的性能，因为浏览器会在浏览器缓存中缓存对象。

过期时间由HTTP标准针对文件的“过期时间”指定(例如，请参阅以下文档的第14.21章： [RFC 2616](https://www.ietf.org/rfc/rfc2616.txt) “ Hypertext Transfer Protocol — HTTP 1.1”)。 此标准使用标头来允许客户端缓存对象，直到它们被视为过时；此类对象会缓存指定的时间量，而不会对原始服务器进行任何状态检查。

>[!NOTE]
>
>此配置与Dispatcher完全不同（并且不起作用）。
>
>Dispatcher的用途是将数据缓存到AEM之前。

所有非动态且不会随时间变化的文件，都可以并且应该进行缓存。 Apache HTTPD服务器的配置可能类似于以下内容之一，具体取决于环境：

>[!CAUTION]
>
>在定义将对象视为最新对象的时段时，必须小心。 因为有 *在指定的时间段到期之前不检查*，客户端最终可能会从缓存中显示旧内容。

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

   这允许中间缓存（例如浏览器缓存）将CSS、Javascript、PNG和GIF文件存储长达一个月，直到它们过期为止。 这意味着它们不需要从AEM或Web服务器请求，但可以保留在浏览器缓存中。

   网站的其他部分不应缓存在创作实例上，因为它们随时可能更改。

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

   这允许中间缓存（例如浏览器缓存）将CSS、Javascript、PNG和GIF文件存储在客户端缓存中长达一天。 尽管此示例说明了以下所有内容的全局设置 `/content` 和 `/etc/designs`，您应该让它更细微。

   根据站点更新的频率，您还可以考虑缓存HTML页面。 一个合理的时间段是1小时：

   ```xml
   <Location /content>
     ExpiresByType text/html "access plus 1 hour"
   </Location>
   ```

配置静态对象后，扫描 `request.log`，在选择包含此类对象的页面时，确认没有对静态对象发出任何（不必要的）请求。
