---
title: 在生产就绪模式下运行AEM
seo-title: Running AEM in Production Ready Mode
description: 了解如何在生产就绪模式下运行AEM。
seo-description: Learn how to run AEM in Production Ready Mode.
uuid: f48c8bae-c72f-4772-967e-f1526f096399
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: 32da99f0-f058-40ae-95a8-2522622438ce
exl-id: 3c342014-f8ec-4404-afe5-514bdb651aae
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '383'
ht-degree: 3%

---

# 在生产就绪模式下运行AEM{#running-aem-in-production-ready-mode}

在AEM 6.1中，Adobe引入了 `"nosamplecontent"` runmode旨在自动完成准备AEM实例以在生产环境中部署所需的步骤。

新的运行模式不仅将自动配置实例以遵循安全检查列表中所述的安全最佳实践，还将删除该过程中所有示例geometrixx应用程序和配置。

>[!NOTE]
>
>由于实际原因，AEM生产就绪模式将仅涵盖保护实例所需的大多数任务，因此强烈建议您查阅 [安全检查列表](/help/sites-administering/security-checklist.md) 开始使用生产环境。
>
>另外，请注意，在生产就绪模式下运行AEM将有效地禁用对CRXDE Lite的访问。 如果出于调试目的需要，请参阅 [在AEM中启用CRXDE Lite](/help/sites-administering/enabling-crxde-lite.md).

![chlimage_1-83](assets/chlimage_1-83a.png)

要在生产就绪模式下运行AEM，您只需将 `nosamplecontent` 通过 `-r` runmode切换到您现有的启动参数：

```shell
java -jar aem-quickstart.jar -r nosamplecontent
```

例如，您可以使用生产就绪来启动具有MongoDB持久性的创作实例，如下所示：

```shell
java -jar aem-quickstart.jar -r author,crx3,crx3mongo,nosamplecontent -Doak.mongo.uri=mongodb://remoteserver:27017 -Doak.mongo.db=aem-author
```

## 更改生产就绪模式的部分 {#changes-part-of-the-production-ready-mode}

更具体地说，当在生产就绪模式下运行AEM时，将执行以下配置更改：

1. 的 **CRXDE支持包** ( `com.adobe.granite.crxde-support`)在生产就绪模式下默认处于禁用状态。 它可以随时从Adobe公共Maven存储库安装。 AEM 6.1需要使用版本3.0.0。

1. 的 **对存储库的Apache Sling简单WebDAV访问** ( `org.apache.sling.jcr.webdav`)包将仅在 **作者** 实例。

1. 新创建的用户需要在首次登录时更改密码。 这不适用于管理员用户。
1. **生成调试信息** 对于 **Apache Sling Java脚本处理程序**.

1. **映射的内容** 和 **生成调试信息** 对于 **Apache Sling JSP脚本处理程序**.

1. 的 **Day CQ WCM过滤器** 设置为 `edit` on **作者** 和 `disabled` on **发布** 实例。

1. 的 **AdobeGraniteHTML库管理器** 配置了以下设置：

   1. **缩小：** `enabled`
   1. **调试：** `disabled`
   1. **Gzip:** `enabled`
   1. **时间：** `disabled`

1. 的 **Apache SlingGETServlet** 默认情况下，设置为支持安全配置，如下所示：

| **配置** | **创作** | **发布** |
|---|---|---|
| TXT呈现版本 | 已禁用 | 已禁用 |
| HTML呈现 | 已禁用 | 已禁用 |
| JSON呈现版本 | 已启用 | 已启用 |
| XML呈现版本 | 已禁用 | 已禁用 |
| json.maximumresults | 1000 | 100 |
| 自动索引 | 已禁用 | 已禁用 |
