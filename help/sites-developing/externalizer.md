---
title: 将URL外置
seo-title: 将URL外置
description: Externalizer是一项OSGI服务，它允许您以编程方式将资源路径转换为外部和绝对URL
seo-description: Externalizer是一项OSGI服务，它允许您以编程方式将资源路径转换为外部和绝对URL
uuid: 65bcc352-fc8c-4aa0-82fb-1321a035602d
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 938469ad-f466-42f4-8b6f-bfc060ae2785
docset: aem65
translation-type: tm+mt
source-git-commit: ec528e115f3e050e4124b5c232063721eaed8df5

---


# 将URL外置{#externalizing-urls}

在AEM中， **Externalizer** 是一项OSGI服务，允许您以编程方式转换资源路径(例如，( `/path/to/my/page`例如， `https://www.mycompany.com/path/to/my/page`)通过预配置DNS来预装路径。

由于实例在Web层后面运行时无法知道其外部可见URL，并且由于有时必须在请求范围之外创建链接，因此此服务提供了一个中心位置来配置这些外部URL并构建它们。

本页介绍如何配置 **Externalizer** 服务以及如何使用它。 有关详细信息，请参阅 [Javadocs](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/Externalizer.html)。

## 配置Externalizer服务 {#configuring-the-externalizer-service}

Externalizer **** service允许您集中定义多个域，这些域可用于以编程方式为资源路径添加前缀。 每个域都由唯一名称标识，该名称用于以编程方式引用该域。

要为 **Externalizer服务定义域映射** :

1. 通过工具，然后通过 **Web控制台**，导航 **到配置管理器**，或输入：

   `https://<host>:<port>/system/console/configMgr`

1. 单击 **Day CQ Link Externalizer** ，打开配置对话框。

   >[!NOTE]
   >
   >到配置的直接链接是 `https://<host>:<port>/system/console/configMgr/com.day.cq.commons.impl.ExternalizerImpl`

   ![aem-externalizer-01](assets/aem-externalizer-01.png)

1. 定义域 **映射** :映射由唯一名称组成，该名称可在代码中用于引用域、空格和域：

   `<unique-name> [scheme://]server[:port][/contextpath]`

   其中：

   * **方案** 通常为http或https，但也可以是ftp等。

      * 根据需要使用https强制使用https链接
      * 如果客户端代码在请求将URL外部化时不覆盖该方案，则将使用它。
   * **server** 是主机名（可以是域名或IP地址）。
   * **port** （可选）是端口号。
   * **contextpath** （可选）仅在AEM作为Web应用程序安装在其他上下文路径下时才设置。
   例如：`production https://my.production.instance`

   以下映射名称是预定义的，并且必须始终设置，因为AEM依赖它们：

   * `local` -本地实例
   * `author` -创作系统DNS
   * `publish` -面向公众的网站DNS
   >[!NOTE]
   >
   >自定义配置允许您添加新类别，如 `production`, `staging` 甚至外部非AEM系统，如 `my-internal-webservice`。 避免在项目代码库中跨不同位置对此类URL进行硬编码很有用。

1. 单击 **保存** ，以保存更改。

>[!NOTE]
>
>Adobe建议您将 [配置添加到存储库](/help/sites-deploying/configuring.md#addinganewconfigurationtotherepository)。

### 使用Externalizer服务 {#using-the-externalizer-service}

此部分显示了如何使用 **Externalizer** 服务的几个示例：

1. **要在JSP中获取Externalizer服务，请执行以下操作：**

   ```java
   Externalizer externalizer = resourceResolver.adaptTo(Externalizer.class);
   ```

1. **要将路径外置为“publish”域，请执行以下操作：**

   ```java
   String myExternalizedUrl = externalizer.publishLink(resolver, "/my/page") + ".html";
   ```

   假设域映射：

   * `publish https://www.website.com`
   `myExternalizedUrl` 最后是以下值：

   * `https://www.website.com/contextpath/my/page.html`


1. **要将具有“author”域的路径外置，请执行以下操作：**

   ```java
   String myExternalizedUrl = externalizer.authorLink(resolver, "/my/page") + ".html";
   ```

   假设域映射：

   * `author https://author.website.com`
   `myExternalizedUrl` 最后是以下值：

   * `https://author.website.com/contextpath/my/page.html`


1. **要将路径外置为“local”域，请执行以下操作：**

   ```java
   String myExternalizedUrl = externalizer.externalLink(resolver, Externalizer.LOCAL, "/my/page") + ".html";
   ```

   假设域映射：

   * `local https://publish-3.internal`
   `myExternalizedUrl` 最后是以下值：

   * `https://publish-3.internal/contextpath/my/page.html`


1. 您可以在 [Javadocs中查找更多示例](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/Externalizer.html)。
