---
title: 外部化URL
seo-title: 外部化URL
description: Externalizer是一种OSGI服务，它允许您以编程方式将资源路径转换为外部和绝对URL
seo-description: Externalizer是一种OSGI服务，它允许您以编程方式将资源路径转换为外部和绝对URL
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
source-wordcount: '523'
ht-degree: 0%

---

# 外部化URL{#externalizing-urls}

在AEM中，**Externalizer**&#x200B;是一种OSGI服务，它允许您以编程方式转换资源路径(例如，`/path/to/my/page`)通过预配置的DNS来预定路径，从而将其置于外部和绝对URL（例如`https://www.mycompany.com/path/to/my/page`）中。

由于实例在Web层后面运行时无法知道其外部可见URL，并且由于有时必须在请求范围之外创建链接，因此此服务提供了一个中心位置来配置这些外部URL并构建它们。

本页介绍如何配置&#x200B;**Externalizer**&#x200B;服务及其使用方法。 有关更多详细信息，请参阅[Javaocs](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/Externalizer.html)。

## 配置外部器服务{#configuring-the-externalizer-service}

**Externalizer**&#x200B;服务允许您集中定义多个域，这些域可用于以编程方式为资源路径添加前缀。 每个域都由一个唯一名称来标识，该名称用于以编程方式引用该域。

要为&#x200B;**Externalizer**&#x200B;服务定义域映射，请执行以下操作：

1. 通过&#x200B;**Tools**&#x200B;导航到配置管理器，然后导航到&#x200B;**Web控制台**，或输入：

   `https://<host>:<port>/system/console/configMgr`

1. 单击&#x200B;**Day CQ Link Externalizer**&#x200B;以打开配置对话框。

   >[!NOTE]
   >
   >到配置的直接链接为`https://<host>:<port>/system/console/configMgr/com.day.cq.commons.impl.ExternalizerImpl`

   ![aem-externalizer-01](assets/aem-externalizer-01.png)

1. 定义&#x200B;**Domains**&#x200B;映射：映射由唯一名称组成，该名称可在代码中用于引用域、空格和域：

   `<unique-name> [scheme://]server[:port][/contextpath]`

   其中：

   * **** 架构通常为http或https，但也可以是ftp等。

      * 如有需要，可使用https强制使用https链接
      * 如果客户端代码在请求将URL外部化时不覆盖方案，则将使用该URL。
   * **** server是主机名（可以是域名或ip地址）。
   * **port** （可选）是端口号。
   * **contextpath** （可选）仅在将AEM安装为位于其他上下文路径下的web应用程序时才设置。

   例如：`production https://my.production.instance`

   以下映射名称是预定义的，且必须始终设置，因为AEM依赖于这些映射名称：

   * `local`  — 本地实例
   * `author`  — 创作系统DNS
   * `publish`  — 面向公众的网站DNS

   >[!NOTE]
   >
   >自定义配置允许您添加新类别，如`production`、`staging`，甚至外部非AEM系统，如`my-internal-webservice`。 避免在项目代码库中的不同位置对此类URL进行硬编码非常有用。

1. 单击&#x200B;**Save**&#x200B;以保存更改。

>[!NOTE]
>
>Adobe建议您[将配置添加到存储库](/help/sites-deploying/configuring.md#addinganewconfigurationtotherepository)。

### 使用外部器服务{#using-the-externalizer-service}

此部分显示如何使用&#x200B;**Externalizer**&#x200B;服务的一些示例：

1. **要在JSP中获取Externalizer服务，请执行以下操作：**

   ```java
   Externalizer externalizer = resourceResolver.adaptTo(Externalizer.class);
   ```

1. **要将路径外部化为“publish”域，请执行以下操作：**

   ```java
   String myExternalizedUrl = externalizer.publishLink(resolver, "/my/page") + ".html";
   ```

   假设域映射：

   * `publish https://www.website.com`

   `myExternalizedUrl` 最后是值：

   * `https://www.website.com/contextpath/my/page.html`


1. **要将路径外部化为“author”域，请执行以下操作：**

   ```java
   String myExternalizedUrl = externalizer.authorLink(resolver, "/my/page") + ".html";
   ```

   假设域映射：

   * `author https://author.website.com`

   `myExternalizedUrl` 最后是值：

   * `https://author.website.com/contextpath/my/page.html`


1. **要将路径外部化为“本地”域，请执行以下操作：**

   ```java
   String myExternalizedUrl = externalizer.externalLink(resolver, Externalizer.LOCAL, "/my/page") + ".html";
   ```

   假设域映射：

   * `local https://publish-3.internal`

   `myExternalizedUrl` 最后是值：

   * `https://publish-3.internal/contextpath/my/page.html`


1. 您可以在[Javaocs](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/Externalizer.html)中找到更多示例。
