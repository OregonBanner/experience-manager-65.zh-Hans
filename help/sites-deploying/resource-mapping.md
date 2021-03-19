---
title: 资源映射
seo-title: 资源映射
description: 了解如何使用资源映射定义AEM的重定向、虚URL和虚拟主机。
seo-description: 了解如何使用资源映射定义AEM的重定向、虚URL和虚拟主机。
uuid: 2ca2d0e4-6f90-4ecc-82db-26991f08c66f
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
discoiquuid: 3582a4d8-a47b-467a-9e25-cb45f969ec93
docset: aem65
feature: 配置
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '538'
ht-degree: 1%

---


# 资源映射{#resource-mapping}

资源映射用于定义AEM的重定向、虚URL和虚拟主机。

例如，您可以使用这些映射来：

* 在所有请求前面添加`/content`前缀，以使内部结构在访客到您网站时处于隐藏状态。
* 定义重定向，以便将发往网站`/content/en/gateway`页面的所有请求重定向到`https://gbiv.com/`。

一个可能的HTTP映射将所有请求都前缀为`/content`的`localhost:4503`。 这样的映射可用于隐藏内部结构，使其从访客隐藏到网站，因为它允许：

`localhost:4503/content/we-retail/en/products.html`

要通过以下方式访问：

`localhost:4503/we-retail/en/products.html`

因为映射将自动将前缀`/content`添加到`/we-retail/en/products.html`。

>[!CAUTION]
>
>虚URL不支持正则表达式模式。

>[!NOTE]
>
>有关详细信息，请参阅Sling文档和[资源分辨率的映射](https://sling.apache.org/site/resources.html)和[资源](https://sling.apache.org/site/mappings-for-resource-resolution.html)。

## 查看映射定义{#viewing-mapping-definitions}

这些映射构成两个列表,JCR资源解析程序将计算（自上而下）以查找匹配项。

这些列表可以在Felix控制台的&#x200B;**JCR ResourceResolver**&#x200B;选项下查看（连同配置信息）；例如，`https://<*host*>:<*port*>/system/console/jcrresolver`:

* 配置
显示当前配置（如[Apache Sling资源解析器](/help/sites-deploying/osgi-configuration-settings.md#apacheslingresourceresolver)所定义）。

* 配置测试
这允许您输入URL或资源路径。 单击**解析**&#x200B;或&#x200B;**映射**&#x200B;以确认系统将如何转换条目。

* **解析程**
序映射条目ResourceResolver.resolve方法用于将URL映射到资源的条目的列表。

* **映射映**
射条目ResourceResolver.map方法用于将资源路径映射到URL的条目的列表。

两个列表显示各种条目，包括应用程序定义为默认值的条目。 这些URL通常旨在简化用户的URL。

列表将与请求匹配的常规表达式&#x200B;**模式**&#x200B;与定义要施加的重定向的&#x200B;**替换**&#x200B;配对。

例如：

**图案** `^[^/]+/[^/]+/welcome$`

将触发：

**替换** `/libs/cq/core/content/welcome.html`.

要重定向请求：

`https://localhost:4503/welcome` &quot;

到:

`https://localhost:4503/libs/cq/core/content/welcome.html`

将在存储库内创建新的映射定义。

>[!NOTE]
>
>有许多资源有助于解释如何定义常规表达式;例如[https://www.regular-expressions.info/](https://www.regular-expressions.info/)。

### 在AEM {#creating-mapping-definitions-in-aem}中创建映射定义

在AEM的标准安装中，您可以找到以下文件夹：

`/etc/map/http`

这是定义HTTP协议的映射时使用的结构。 可在`/etc/map`下为要映射的任何其他协议创建其他文件夹(`sling:Folder`)。

#### 配置到/content {#configuring-an-internal-redirect-to-content}的内部重定向

要创建将任何请求作为前缀的映射，请使用`/content`:

1. 使用CRXDE导航到`/etc/map/http`。

1. 创建新节点：

   * **类** `sling:Mapping`
型此节点类型用于此类映射，但其用途不是强制性的。

   * **名称** `localhost_any`

1. 单击&#x200B;**保存全部**。
1. **将** 以下属性添加到此节点：

   * **名称** `sling:match`

      * **类型** `String`

      * **值** `localhost.4503/`
   * **名称** `sling:internalRedirect`

      * **类型** `String`

      * **值** `/content/`


1. 单击&#x200B;**保存全部**。

此操作将处理以下请求：
`localhost:4503/geometrixx/en/products.html`
如：
`localhost:4503/content/geometrixx/en/products.html`
被要求。

>[!NOTE]
>
>请参阅Sling文档中的[资源](https://sling.apache.org/site/mappings-for-resource-resolution.html)，进一步了解可用的sling属性以及如何配置这些属性。

>[!NOTE]
>
>可使用`/etc/map.publish`保存发布环境的配置。 然后，必须复制这些资源，并为发布环境的[Apache Sling资源解析程序](/help/sites-deploying/osgi-configuration-settings.md#apacheslingresourceresolver)的&#x200B;**映射位置**&#x200B;配置的新位置(`/etc/map.publish`)。

