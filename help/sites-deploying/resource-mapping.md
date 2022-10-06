---
title: 资源映射
seo-title: Resource Mapping
description: 了解如何使用资源映射来定义AEM的重定向、虚URL和虚拟主机。
seo-description: Learn how to define redirects, vanity URLs and virtual hosts for AEM by using resource mapping.
uuid: 2ca2d0e4-6f90-4ecc-82db-26991f08c66f
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
discoiquuid: 3582a4d8-a47b-467a-9e25-cb45f969ec93
docset: aem65
feature: Configuring
exl-id: 3eebdd38-da5b-4c38-868a-22c3c7a97b66
source-git-commit: 7c24379c01f247f5ad45e3ecd40f3edef4ac3cfb
workflow-type: tm+mt
source-wordcount: '519'
ht-degree: 3%

---

# 资源映射{#resource-mapping}

资源映射用于定义AEM的重定向、虚URL和虚拟主机。

例如，您可以将以下映射用于：

* 为所有请求添加前缀 `/content` 以便对网站的访客隐藏内部结构。
* 定义重定向，以便 `/content/en/gateway` 将您网站的页面重定向到 `https://gbiv.com/`.

一个可能的HTTP映射会为所有请求添加前缀 `localhost:4503` with `/content`. 此类映射可用于隐藏网站访客的内部结构，因为它允许：

`localhost:4503/content/we-retail/en/products.html`

访问时：

`localhost:4503/we-retail/en/products.html`

因为映射将自动添加前缀 `/content` to `/we-retail/en/products.html`.

>[!CAUTION]
>
>虚URL不支持正则表达式模式。

>[!NOTE]
>
>请参阅Sling文档，以及 [资源解析的映射](https://sling.apache.org/site/resources.html) 和 [资源](https://sling.apache.org/site/mappings-for-resource-resolution.html) 以了解更多信息。

## 查看映射定义 {#viewing-mapping-definitions}

这些映射构成两个列表，JCR资源解析程序将对其进行评估（从上到下）以查找匹配项。

可以在 **JCR ResourceResolver** Felix控制台选项；例如， `https://<*host*>:<*port*>/system/console/jcrresolver`:

* 配置显示当前配置(如 [Apache Sling资源解析程序](/help/sites-deploying/osgi-configuration-settings.md#apacheslingresourceresolver))。

* 配置测试此操作允许您输入URL或资源路径。 单击 **解决** 或 **地图** 以确认系统将如何转换条目。

* **解析程序映射条目**
ResourceResolver.resolve方法用于将URL映射到资源的条目列表。

* **映射映射条目**
ResourceResolver.map方法用于将资源路径映射到URL的条目列表。

这两个列表显示了各种条目，包括应用程序定义为默认值的条目。 这些URL通常旨在简化用户的URL。

列表对 **图案**，与请求匹配的正则表达式，其中 **替换** 定义了重定向到实施。

例如：

**图案** `^[^/]+/[^/]+/welcome$`

将触发：

**替换** `/libs/cq/core/content/welcome.html`.

要重定向请求，请执行以下操作：

`https://localhost:4503/welcome` &quot;

到:

`https://localhost:4503/libs/cq/core/content/welcome.html`

将在存储库内创建新映射定义。

>[!NOTE]
>
>有许多资源可帮助解释如何定义正则表达式；例如 [https://www.regular-expressions.info/](https://www.regular-expressions.info/).

### 在AEM中创建映射定义 {#creating-mapping-definitions-in-aem}

在AEM的标准安装中，您可以找到文件夹：

`/etc/map/http`

这是定义HTTP协议映射时使用的结构。 其他文件夹( `sling:Folder`)可在下创建 `/etc/map` 的其他协议。

#### 配置到/content的内部重定向 {#configuring-an-internal-redirect-to-content}

创建映射，以将任何请求添加到https://localhost:4503/的前缀，其中 `/content`:

1. 使用CRXDE导航到 `/etc/map/http`.

1. 创建新节点：

   * **类型** `sling:Mapping`
此节点类型专门用于此类映射，但不强制使用。

   * **名称** `localhost_any`

1. 单击 **全部保存**.
1. **添加** 此节点的以下属性：

   * **名称** `sling:match`

      * **类型** `String`

      * **值** `localhost.4503/`
   * **名称** `sling:internalRedirect`

      * **类型** `String[]`

      * **值** `/content/`


1. 单击 **全部保存**.

这将处理如下请求：
`localhost:4503/geometrixx/en/products.html`
假如：
`localhost:4503/content/geometrixx/en/products.html`
被要求。

>[!NOTE]
>
>请参阅 [资源](https://sling.apache.org/site/mappings-for-resource-resolution.html) ，以进一步了解可用sling属性以及如何配置这些属性。

>[!NOTE]
>
>您可以使用 `/etc/map.publish` 来保存发布环境的配置。 然后，必须复制这些数据，并将新位置( `/etc/map.publish`) **映射位置** 的 [Apache Sling资源解析程序](/help/sites-deploying/osgi-configuration-settings.md#apacheslingresourceresolver) 的子目录访问Advertising Cloud帮助。
