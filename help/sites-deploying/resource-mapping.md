---
title: 资源映射
seo-title: 资源映射
description: 了解如何使用资源映射来定义AEM的重定向、虚URL和虚拟主机。
seo-description: 了解如何使用资源映射来定义AEM的重定向、虚URL和虚拟主机。
uuid: 2ca2d0e4-6f90-4ecc-82db-26991f08c66f
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
discoiquuid: 3582a4d8-a47b-467a-9e25-cb45f969ec93
docset: aem65
feature: 配置
exl-id: 3eebdd38-da5b-4c38-868a-22c3c7a97b66
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '538'
ht-degree: 1%

---

# 资源映射{#resource-mapping}

资源映射用于定义AEM的重定向、虚URL和虚拟主机。

例如，您可以将以下映射用于：

* 为所有请求添加`/content`前缀，以便隐藏网站访客的内部结构。
* 定义重定向，以便所有到网站`/content/en/gateway`页面的请求都被重定向到`https://gbiv.com/`。

一个可能的HTTP映射将所有请求都前缀为具有`/content`的`localhost:4503`。 此类映射可用于隐藏网站访客的内部结构，因为它允许：

`localhost:4503/content/we-retail/en/products.html`

访问时：

`localhost:4503/we-retail/en/products.html`

因为映射会自动将前缀`/content`添加到`/we-retail/en/products.html`。

>[!CAUTION]
>
>虚URL不支持正则表达式模式。

>[!NOTE]
>
>有关更多信息，请参阅Sling文档以及[资源分辨率的映射](https://sling.apache.org/site/resources.html)和[资源](https://sling.apache.org/site/mappings-for-resource-resolution.html)。

## 查看映射定义{#viewing-mapping-definitions}

这些映射构成两个列表，JCR资源解析程序将对其进行评估（从上到下）以查找匹配项。

可以在Felix控制台的&#x200B;**JCR ResourceResolver**&#x200B;选项下查看这些列表（连同配置信息）；例如，`https://<*host*>:<*port*>/system/console/jcrresolver`:

* 配置
显示当前配置（如为[Apache Sling资源解析程序](/help/sites-deploying/osgi-configuration-settings.md#apacheslingresourceresolver)定义的）。

* 配置测试
这允许您输入URL或资源路径。 单击**Resolve**&#x200B;或&#x200B;**Map**&#x200B;以确认系统将如何转换条目。

* **解析程**
序映射条目ResourceResolver.resolve方法用于将URL映射到资源的条目列表。

* **映射映**
射条目ResourceResolver.map方法用于将资源路径映射到URL的条目列表。

这两个列表显示了各种条目，包括应用程序定义为默认值的条目。 这些URL通常旨在简化用户的URL。

该列表将与请求匹配的正则表达式&#x200B;**Pattern**&#x200B;与定义强制实施的重定向的&#x200B;**Replacement**&#x200B;配对。

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
>有许多资源可帮助解释如何定义正则表达式；例如[https://www.regular-expressions.info/](https://www.regular-expressions.info/)。

### 在AEM {#creating-mapping-definitions-in-aem}中创建映射定义

在AEM的标准安装中，您可以找到文件夹：

`/etc/map/http`

这是定义HTTP协议映射时使用的结构。 在`/etc/map`下可为要映射的任何其他协议创建其他文件夹(`sling:Folder`)。

#### 配置到/content的内部重定向{#configuring-an-internal-redirect-to-content}

要创建将任何请求添加到https://localhost:4503/的映射，请使用`/content`:

1. 使用CRXDE导航到`/etc/map/http`。

1. 创建新节点：

   * **** `sling:Mapping`
类型此节点类型专门用于此类映射，但不强制使用。

   * **名称** `localhost_any`

1. 单击&#x200B;**Save All**。
1. **** 将以下属性添加到此节点：

   * **名称** `sling:match`

      * **类型** `String`

      * **值** `localhost.4503/`
   * **名称** `sling:internalRedirect`

      * **类型** `String`

      * **值** `/content/`


1. 单击&#x200B;**Save All**。

这将处理如下请求：
`localhost:4503/geometrixx/en/products.html`
假如：
`localhost:4503/content/geometrixx/en/products.html`
被要求。

>[!NOTE]
>
>请参阅Sling文档中的[资源](https://sling.apache.org/site/mappings-for-resource-resolution.html) ，以了解有关可用Sling属性以及如何配置这些属性的更多信息。

>[!NOTE]
>
>您可以使用`/etc/map.publish`保存发布环境的配置。 然后，必须复制这些资源，并为发布环境的[Apache Sling资源解析程序](/help/sites-deploying/osgi-configuration-settings.md#apacheslingresourceresolver)的&#x200B;**映射位置**&#x200B;配置的新位置(`/etc/map.publish`)。
