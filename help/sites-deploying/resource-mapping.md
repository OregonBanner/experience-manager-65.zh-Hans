---
title: 资源映射
seo-title: Resource Mapping
description: 了解如何使用资源映射为AEM定义重定向、虚URL和虚拟主机。
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
ht-degree: 4%

---

# 资源映射{#resource-mapping}

资源映射用于为AEM定义重定向、虚URL和虚拟主机。

例如，您可以使用这些映射执行以下操作：

* 为所有请求添加前缀 `/content` 这样网站访客就不会看到内部结构。
* 定义一个重定向，以便所有请求都指向 `/content/en/gateway` 您的网站页面将被重定向到 `https://gbiv.com/`.

一个可能的HTTP映射将所有请求作为前缀 `localhost:4503` 替换为 `/content`. 像这样的映射可用于对访问网站的访客隐藏内部结构，因为它允许：

`localhost:4503/content/we-retail/en/products.html`

访问方式：

`localhost:4503/we-retail/en/products.html`

因为映射将自动添加前缀 `/content` 到 `/we-retail/en/products.html`.

>[!CAUTION]
>
>虚URL不支持正则表达式模式。

>[!NOTE]
>
>请参阅Sling文档，以及 [资源解析的映射](https://sling.apache.org/site/resources.html) 和 [资源](https://sling.apache.org/site/mappings-for-resource-resolution.html) 以进一步了解。

## 查看映射定义 {#viewing-mapping-definitions}

JCR资源解析器评估（自上而下）以查找匹配项的两个列表中的映射。

这些列表（连同配置信息）可在 **JCR ResourceResolver** Felix控制台选项；例如， `https://<*host*>:<*port*>/system/console/jcrresolver`：

* Configuration显示当前配置(为定义 [Apache Sling资源解析程序](/help/sites-deploying/osgi-configuration-settings.md#apacheslingresourceresolver))。

* 配置测试允许您输入URL或资源路径。 单击 **解决** 或 **映射** 以确认系统如何转换条目。

* **解析程序映射条目**
ResourceResolver.resolve方法用于将URL映射到资源的条目列表。

* **映射映射条目**
ResourceResolver.map方法用来将资源路径映射到URL的条目列表。

这两个列表显示了各种条目，包括由应用程序定义为默认值的条目。 这些规则通常旨在简化用户的URL。

列表对 **图案**，与请求匹配的正则表达式，带有 **替换** 这定义了要强制执行的重定向。

例如：

**图案** `^[^/]+/[^/]+/welcome$`

将触发：

**替换** `/libs/cq/core/content/welcome.html`.

要重定向请求：

`https://localhost:4503/welcome` ``

到:

`https://localhost:4503/libs/cq/core/content/welcome.html`

新的映射定义将在存储库中创建。

>[!NOTE]
>
>有许多资源可帮助解释如何定义正则表达式；例如 [https://www.regular-expressions.info/](https://www.regular-expressions.info/).

### 在AEM中创建映射定义 {#creating-mapping-definitions-in-aem}

在AEM的标准安装中，您可以找到以下文件夹：

`/etc/map/http`

这是为HTTP协议定义映射时使用的结构。 其他文件夹( `sling:Folder`)可以在下创建 `/etc/map` 任何其他要映射的协议。

#### 配置到/content的内部重定向 {#configuring-an-internal-redirect-to-content}

要创建为https://localhost:4503/的任何请求添加前缀的映射，请执行以下操作 `/content`：

1. 使用CRXDE导航到 `/etc/map/http`.

1. 创建新节点：

   * **类型** `sling:Mapping`
此节点类型适用于此类映射，不过其用法不是强制性的。

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
就好象：
`localhost:4503/content/geometrixx/en/products.html`
已被请求。

>[!NOTE]
>
>参见 [资源](https://sling.apache.org/site/mappings-for-resource-resolution.html) 有关sling可用属性及其配置方式的更多信息，请参阅Sling文档。

>[!NOTE]
>
>您可以使用 `/etc/map.publish` 保存发布环境的配置。 然后必须复制这些文件，并且新位置( `/etc/map.publish`)配置的 **映射位置** 的 [Apache Sling资源解析程序](/help/sites-deploying/osgi-configuration-settings.md#apacheslingresourceresolver) 发布环境的。
