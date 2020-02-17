---
title: 静态对象的到期
seo-title: 静态对象的到期
description: 了解如何配置AEM以使静态对象不会过期（在合理的时间段内）。
seo-description: 了解如何配置AEM以使静态对象不会过期（在合理的时间段内）。
uuid: ee019a3d-4133-4d40-98ec-e0914b751fb3
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
discoiquuid: 73f37b3c-5dbe-4132-bb60-daa8de871884
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 静态对象的到期{#expiration-of-static-objects}

静态对象（例如，图标）不会更改。 因此，应配置系统，使其不会过期（在合理的时间段内），从而减少不必要的流量。

其影响如下：

* 卸载来自服务器基础架构的请求。
* 当浏览器将对象缓存到浏览器缓存中时，提高页面加载的性能。

HTTP标准中关于文件“过期”的规定已过期(例如，请参阅 [RFC 2616](https://www.ietf.org/rfc/rfc2616.txt) &quot;超文本传输协议— HTTP 1.1&quot;的第14.21章)。 该标准使用标题允许客户端缓存对象，直到它们被视为过时；这些对象被高速缓存指定的时间长度，而不对源服务器进行任何状态检查。

>[!NOTE]
>
>此配置与调度程序完全分开（并且不适用于）。
>
>调度程序的目的是在AEM前缓存数据。

所有文件（不是动态的，并且不随时间而更改）都可以且应该缓存。 Apache HTTPD服务器的配置可能如下所示——具体取决于环境：

>[!CAUTION]
>
>在定义将对象视为最新的时间段时，必须小心。 由于在指定 *的时间段到期之前没有检查*，客户端最终可以从缓存中呈现旧内容。

1. **对于作者实例：**

   ```xml
   LoadModule expires_module modules/mod_expires.so
   <Location /libs>
     ExpiresByType text/css "access plus 1 month"
     ExpiresByType text/javascript "access plus 1 month"
     ExpiresByType image/png "access plus 1 month"
     ExpiresByType image/gif "access plus 1 month"
   </Location>
   ```

   这允许中间缓存（例如浏览器缓存）在最长一个月的时间内存储CSS、Javascript、PNG和GIF文件，直到它们过期。 这意味着无需从AEM或Web服务器请求它们，但可以保留在浏览器缓存中。

   站点的其他部分不应缓存在作者实例上，因为这些部分随时可能会发生更改。

1. **对于Publish实例：**

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

   这允许中间缓存（例如浏览器缓存）在客户端缓存中存储CSS、Javascript、PNG和GIF文件，最长一天。 尽管此示例说明了下面和中所有内容的全 `/content` 局设置 `/etc/designs`，但您应使其更细致。

   根据站点的更新频率，您还可以考虑缓存HTML页面。 合理的时间段为1小时：

   ```xml
   <Location /content>
     ExpiresByType text/html "access plus 1 hour"
   </Location>
   ```

在配置静态对象后，在选择包含这些对象的页面时， `request.log`扫描以确认不会为静态对象发出（不必要的）请求。
