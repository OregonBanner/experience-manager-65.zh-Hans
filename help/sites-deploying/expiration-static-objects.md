---
title: 静态对象的过期
seo-title: 静态对象的过期
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
workflow-type: tm+mt
source-wordcount: '436'
ht-degree: 0%

---


# 静态对象的过期{#expiration-of-static-objects}

静态对象（例如，图标）不会更改。 因此，应配置系统，使其不会过期（在合理的时间段内），从而减少不必要的流量。

具有以下影响：

* 卸载来自服务器基础架构的请求。
* 当浏览器将对象缓存到浏览器缓存中时，提高页面加载性能。

过期由HTTP标准指定，涉及文件的“过期”（例如，请参见[RFC 2616](https://www.ietf.org/rfc/rfc2616.txt) &quot;超文本传输协议— HTTP 1.1&quot;的第14.21章）。 该标准使用标题允许客户端缓存对象，直到它们被视为过时；这些对象被缓存指定的时间量，而不对原始服务器进行任何状态检查。

>[!NOTE]
>
>此配置与调度程序完全分离（并且不适用）。
>
>调度程序的目的是在AEM之前缓存数据。

所有文件（不是动态的，并且随着时间不变）都可以且应该进行缓存。 Apache HTTPD服务器的配置可能如下所示——具体取决于环境:

>[!CAUTION]
>
>在定义对象被视为最新的时间段时，必须小心。 由于在指定的时间期已过&#x200B;*之前没有检查，因此客户端最终可以从缓存中显示旧内容。*

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

   这允许中间缓存（例如浏览器缓存）存储CSS、Javascript、PNG和GIF文件，最长一个月，直到它们过期。 这意味着无需从AEM或web服务器请求它们，但可以保留在浏览器缓存中。

   站点的其他部分不应缓存在作者实例上，因为它们随时可能发生更改。

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

   这允许中间缓存（例如浏览器缓存）在客户端缓存中存储CSS、Javascript、PNG和GIF文件，时间最长为一天。 尽管此示例说明了`/content`和`/etc/designs`下的所有项的全局设置，但您应该使其更精细。

   根据更新网站的频率，您还可以考虑缓存HTML页面。 合理的时间段为1小时：

   ```xml
   <Location /content>
     ExpiresByType text/html "access plus 1 hour"
   </Location>
   ```

配置静态对象后，在选择保存此类对象的页面时扫描`request.log`，以确认没有为静态对象发出（不必要的）请求。
