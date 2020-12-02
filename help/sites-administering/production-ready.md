---
title: 在生产就绪模式下运行AEM
seo-title: 在生产就绪模式下运行AEM
description: 了解如何在生产就绪模式下运行AEM。
seo-description: 了解如何在生产就绪模式下运行AEM。
uuid: f48c8bae-c72f-4772-967e-f1526f096399
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: 32da99f0-f058-40ae-95a8-2522622438ce
translation-type: tm+mt
source-git-commit: 1c1ade947f2cbd26b35920cfd10b1666b132bcbd
workflow-type: tm+mt
source-wordcount: '397'
ht-degree: 3%

---


# 在生产就绪模式下运行AEM{#running-aem-in-production-ready-mode}

在AEM 6.1中，Adobe引入了新的`"nosamplecontent"`运行模式，旨在自动执行准备AEM实例以部署到生产环境所需的步骤。

新的运行模式不仅将自动配置实例以符合安全清单中描述的安全最佳实践，还将删除该过程中的所有示例geometrixx应用程序和配置。

>[!NOTE]
>
>由于实际原因，AEM生产就绪模式将仅涵盖保护实例所需的大多数任务，因此强烈建议您在与生产环境一起使用之前先查阅[安全清单](/help/sites-administering/security-checklist.md)。
>
>另外，请注意，在生产就绪模式中运行AEM将有效地禁用对CRXDE Lite的访问。 如果出于调试目的需要，请参阅[在AEM](/help/sites-administering/enabling-crxde-lite.md)中启用CRXDE Lite。

![chlimage_1-83](assets/chlimage_1-83a.png)

要在生产就绪模式下运行AEM，您只需通过`-r` runmode开关将`nosamplecontent`添加到现有启动参数：

```shell
java -jar aem-quickstart.jar -r nosamplecontent
```

例如，您可以使用生产就绪启动具有MongoDB持久性的创作实例，如下所示：

```shell
java -jar aem-quickstart.jar -r author,crx3,crx3mongo,nosamplecontent -Doak.mongo.uri=mongodb://remoteserver:27017 -Doak.mongo.db=aem-author
```

## 更改生产就绪模式{#changes-part-of-the-production-ready-mode}的一部分

更具体地说，在生产就绪模式下运行AEM时将执行以下配置更改：

1. 默认情况下，在生产就绪模式下禁用&#x200B;**CRXDE支持包**(`com.adobe.granite.crxde-support`)。 它可以随时从Adobe公共Maven存储库安装。 AEM 6.1需要版本3.0.0。

1. 对存储库&#x200B;**(`org.apache.sling.jcr.webdav`)的** Apache Sling Simple WebDAV Access捆绑包将仅在&#x200B;**author**&#x200B;实例上可用。

1. 新创建的用户需要在首次登录时更改口令。 这不适用于管理员用户。
1. **为Apache** Java脚本处理程序 **生成禁用的调试信息**。

1. **映射** 内容 **和生成** 调试信息已对Apache Sling JSP脚 **本处理程序禁用**。

1. **Day CQ WCM过滤器**&#x200B;在&#x200B;**author**&#x200B;上设置为`edit`，在&#x200B;**publish**&#x200B;实例上设置为`disabled`。

1. **AdobeGranite HTML库管** 理器配置了以下设置：

   1. **小型：** `enabled`
   1. **调试：** `disabled`
   1. **Gzip:** `enabled`
   1. **时间：** `disabled`

1. 默认情况下，**Apache SlingGETServlet**&#x200B;设置为支持安全配置，如下所示：

| **配置** | **创作** | **发布** |
|---|---|---|
| TXT再现 | 已禁用 | 已禁用 |
| HTML再现 | 已禁用 | 已禁用 |
| JSON再现 | 已启用 | 已启用 |
| XML再现 | 已禁用 | 已禁用 |
| json.maximumresults | 1000 | 100 |
| 自动索引 | 已禁用 | 已禁用 |

