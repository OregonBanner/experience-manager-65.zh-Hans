---
title: 将URL外部化
seo-title: Externalizing URLs
description: 外部化器是一种OSGI服务，允许您以编程方式将资源路径转换为外部和绝对URL
seo-description: The Externalizer is an OSGI service that allows you to programmatically transform a resource path into an external and absolute URL
uuid: 65bcc352-fc8c-4aa0-82fb-1321a035602d
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 938469ad-f466-42f4-8b6f-bfc060ae2785
docset: aem65
exl-id: 971d6c25-1fbe-4c07-944e-be6b97a59922
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '500'
ht-degree: 0%

---

# 将URL外部化{#externalizing-urls}

在AEM中， **外部化器** 是一种OSGI服务，允许您以编程方式转换资源路径(例如， `/path/to/my/page`)转换为外部和绝对URL(例如， `https://www.mycompany.com/path/to/my/page`)，方法是使用预配置的DNS为路径添加前缀。

由于如果实例在Web层后面运行，则它无法知道自己的外部可见URL，而且有时必须在请求范围之外创建链接，因此，此服务提供了一个中心位置来配置这些外部URL并构建它们。

本页介绍如何配置 **外部化器** 服务和使用方法。 欲知更多详情，请参阅 [Javadocs](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/Externalizer.html).

## 配置Externalizer服务 {#configuring-the-externalizer-service}

此 **外部化器** 服务允许您集中定义多个域，这些域可用于以编程方式为资源路径添加前缀。 每个域由唯一名称标识，该名称用于以编程方式引用该域。

要为定义域映射，请执行以下操作 **外部化器** 服务：

1. 通过以下方式导航到配置管理器 **工具**，则 **Web控制台**，或输入：

   `https://<host>:<port>/system/console/configMgr`

1. 单击 **Day CQ链接外部化器** 以打开配置对话框。

   >[!NOTE]
   >
   >配置的直接链接是 `https://<host>:<port>/system/console/configMgr/com.day.cq.commons.impl.ExternalizerImpl`

   ![aem-externalizer-01](assets/aem-externalizer-01.png)

1. 定义 **域** 映射：映射由唯一名称组成，该名称可在代码中用于引用域、空间和域：

   `<unique-name> [scheme://]server[:port][/contextpath]`

   其中：

   * **方案** 通常为http或https，但也可以是ftp等。

      * 如果需要，可使用https实施https链接
      * 如果客户端代码在请求URL外部化时未覆盖方案，则将使用该架构。
   * **服务器** 是主机名（可以是域名或ip地址）。
   * **端口** （可选）是端口号。
   * **contextpath** （可选）仅当AEM作为Web应用程序安装在其他上下文路径下时，才会设置。

   例如：`production https://my.production.instance`

   以下映射名称是预定义名称，必须始终设置为AEM依赖于它们：

   * `local`  — 本地实例
   * `author`  — 创作系统DNS
   * `publish`  — 面向公众的网站DNS

   >[!NOTE]
   >
   >自定义配置允许您添加新类别，例如 `production`， `staging` 甚至外部非AEM系统，例如 `my-internal-webservice`. 避免在项目代码库中的不同位置对这些URL进行硬编码很有用。

1. 单击 **保存** 以保存更改。

>[!NOTE]
>
>Adobe建议您 [将配置添加到存储库](/help/sites-deploying/configuring.md#addinganewconfigurationtotherepository).

### 使用Externalizer服务 {#using-the-externalizer-service}

此部分显示一些示例，说明 **外部化器** 服务可用于：

1. **要在JSP中获取Externalizer服务，请执行以下操作：**

   ```java
   Externalizer externalizer = resourceResolver.adaptTo(Externalizer.class);
   ```

1. **要将路径与“发布”域外部化，请执行以下操作：**

   ```java
   String myExternalizedUrl = externalizer.publishLink(resolver, "/my/page") + ".html";
   ```

   假定域映射：

   * `publish https://www.website.com`

   `myExternalizedUrl` 最终得到值：

   * `https://www.website.com/contextpath/my/page.html`


1. **要将具有“作者”域的路径外部化，请执行以下操作：**

   ```java
   String myExternalizedUrl = externalizer.authorLink(resolver, "/my/page") + ".html";
   ```

   假定域映射：

   * `author https://author.website.com`

   `myExternalizedUrl` 最终得到值：

   * `https://author.website.com/contextpath/my/page.html`


1. **要将具有“本地”域的路径外部化，请执行以下操作：**

   ```java
   String myExternalizedUrl = externalizer.externalLink(resolver, Externalizer.LOCAL, "/my/page") + ".html";
   ```

   假定域映射：

   * `local https://publish-3.internal`

   `myExternalizedUrl` 最终得到值：

   * `https://publish-3.internal/contextpath/my/page.html`


1. 有关更多示例，请参见 [Javadocs](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/Externalizer.html).
