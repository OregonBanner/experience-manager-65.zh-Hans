---
title: 资源映射
seo-title: 资源映射
description: 了解如何使用资源映射为AEM定义重定向、虚URL和虚拟主机。
seo-description: 了解如何使用资源映射为AEM定义重定向、虚URL和虚拟主机。
uuid: 2ca2d0e4-6f90-4ecc-82db-26991f08c66f
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
discoiquuid: 3582a4d8-a47b-467a-9e25-cb45f969ec93
docset: aem65
translation-type: tm+mt
source-git-commit: 44eb94b917fe88b7c90c29ec7da553e15be391db

---


# 资源映射{#resource-mapping}

资源映射用于为AEM定义重定向、虚URL和虚拟主机。

例如，您可以使用这些映射来：

* 在所有请求前加 `/content` 上前缀，这样内部结构就会对网站的访客隐藏起来。
* 定义重定向，以便将发往网站 `/content/en/gateway` 页面的所有请求重定向到 `https://gbiv.com/`。

一个可能的HTTP映射将所有请求作为前缀 `localhost:4503` 与一起 `/content`。 这样的映射可用于在访问网站的访客中隐藏内部结构，因为它允许：

`localhost:4503/content/we-retail/en/products.html`

要通过以下方式访问：

`localhost:4503/we-retail/en/products.html`

因为映射会自动向添加前 `/content` 缀 `/we-retail/en/products.html`。

>[!CAUTION]
>
>虚URL不支持正则表达式模式。

>[!NOTE]
>
>有关详细信息，请参 [阅Sling文档和Mappings for Resource Resolution](https://sling.apache.org/site/resources.html)[和Resources](https://sling.apache.org/site/mappings-for-resource-resolution.html) 。

## 查看映射定义 {#viewing-mapping-definitions}

这些映射构成两个列表，JCR资源解析程序将对这两个列表进行计算（从上到下）以查找匹配项。

这些列表可以在Felix控制台的 **JCR ResourceResolver** （JCR资源解析程序）选项下查看（以及配置信息）;例如， `https://<*host*>:<*port*>/system/console/jcrresolver`:

* 配置显示当前配置(如 [Apache Sling资源解析程序所定义](/help/sites-deploying/osgi-configuration-settings.md#apacheslingresourceresolver))。

* 配置测试允许您输入URL或资源路径。 单 **击“解析** ”或“映 **射”** ，确认系统将如何转换条目。

* **解析程序映**&#x200B;射条目ResourceResolver.resolve方法用来将URL映射到资源的条目列表。

* **映射映射条目** ResourceResolver.map方法用于将资源路径映射到URL的条目列表。

这两个列表显示各种条目，包括应用程序定义为默认值的条目。 这些URL通常旨在简化用户的URL。

列表将Pattern **（与请求匹配的正则表达式）与** Replacement **(替换** )配对，该Replacement（替换）定义了要实施的重定向。

例如，:

**图案**`^[^/]+/[^/]+/welcome$`

将触发：

**替换** `/libs/cq/core/content/welcome.html`.

要重定向请求，请执行以下操作：

`https://localhost:4503/welcome` ``

到:

`https://localhost:4503/libs/cq/core/content/welcome.html`

将在存储库中创建新的映射定义。

>[!NOTE]
>
>有许多资源有助于解释如何定义正则表达式；例如 [https://www.regular-expressions.info/](https://www.regular-expressions.info/)。

### 在AEM中创建映射定义 {#creating-mapping-definitions-in-aem}

在AEM的标准安装中，您可以找到以下文件夹：

`/etc/map/http`

这是定义HTTP协议映射时使用的结构。 其他文件夹( `sling:Folder`)可以根据您要映射的 `/etc/map` 任何其他协议创建。

#### 配置内部重定向到/content {#configuring-an-internal-redirect-to-content}

要创建将任何请求作为https://localhost:4503/前缀的映射，请执行以下操 `/content`作：

1. 使用CRXDE导航到 `/etc/map/http`。

1. 创建新节点：

   * **类型**`sling:Mapping`此节点类型适用于此类映射，但其用途不是强制性的。

   * **名称** `localhost_any`

1. 单击“ **全部保存**”。
1. **向此节点添加** 以下属性：

   * **名称** `sling:match`

      * **类型** `String`

      * **值**`localhost.4503/`
   * **名称** `sling:internalRedirect`

      * **类型** `String`

      * **值**`/content/`


1. 单击“ **全部保存**”。

此操作将处理以下请求：就`localhost:4503/geometrixx/en/products.html`像：已`localhost:4503/content/geometrixx/en/products.html`被要求。

>[!NOTE]
>
>请参 [阅Sling Documentation中的](https://sling.apache.org/site/mappings-for-resource-resolution.html) “资源”，进一步了解sling属性的可用性以及配置方式。

>[!NOTE]
>
>您可以使 `/etc/map.publish` 用来保存发布环境的配置。 然后，必须复制这些资源，并为发布环境的 `/etc/map.publish`**Apache Sling Resource Resolver的Mapping Location（映射位置）配置新位置(**[](/help/sites-deploying/osgi-configuration-settings.md#apacheslingresourceresolver) )。

