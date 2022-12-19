---
title: 在AEM中启用CRXDE Lite
seo-title: Enabling CRXDE Lite in AEM
description: 了解如何在AEM中启用CRXDE Lite。
seo-description: Learn how to enable CRXDE Lite in AEM.
uuid: d7a3db67-6384-463b-9aa9-f08ecc6c99c6
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: 72df3ece-badf-466b-8f9a-0ec985d87741
exl-id: bf51def2-1dd4-4bd3-b989-685058f0ead8
source-git-commit: a4183bb9d72763ebea3b464c77fce978c723e053
workflow-type: tm+mt
source-wordcount: '258'
ht-degree: 0%

---

# 在AEM中启用CRXDE Lite{#enabling-crxde-lite-in-aem}

为确保AEM安装尽可能安全，安全检查列表建议 [禁用WebDAV](/help/sites-administering/security-checklist.md#disable-webdav) 在生产环境中。

但是，CRXDE Lite取决于 `org.apache.sling.jcr.davex` 捆绑以正常运行，因此禁用WebDAV也会有效地禁用CRXDE Lite。

发生此情况时，请浏览 `https://serveraddress:4502/crx/de/index.jsp` 将显示一个空的根节点，并且所有用于CRXDE Lite资源的HTTP请求都将失败：

```xml
404 Resource at '/crx/server/crx.default/jcr:root/.1.json' not found: No resource found
```

虽然此建议旨在尽可能减少攻击表面，但系统管理员有时可能需要访问CRXDE Lite，以浏览内容或调试生产实例上的问题。

您可以通过以下任一方式启用CRXDE Lite [OSGi设置](#enabling-crxde-lite-osgi) 或 [cURL命令](#enabling-crxde-lite-curl).

>[!WARNING]
>
>由于这些方法的操作方式略有不同，因此您应使用 ***e*** OSGI ***或*** cURL。
>
>这两种方法是 ***not*** 可互换。

## 使用OSGI启用CRXDE Lite {#enabling-crxde-lite-osgi}

如果禁用，则可以按照以下过程打开CRXDE Lite:

1. 转到OSGi组件控制台(位于 `http://localhost:4502/system/console/components`
1. 搜索以下组件：

   * `org.apache.sling.jcr.davex.impl.servlets.SlingDavExServlet`

1. 单击该扳手旁边的扳手图标可查看其配置选项：

   ![chlimage_1-80](assets/chlimage_1-80a.png)

1. 创建以下配置：

   * **根路径:** `/crx/server`
   * 勾选下方的方框 **使用绝对URI**.

1. 使用完CRXDE Lite后，请确保再次禁用WebDAV。

## 使用cURL启用CRXDE Lite {#enabling-crxde-lite-curl}

您还可以通过运行以下命令通过cURL启用CRXDE Lite:

```shell
curl -u admin:admin -F "jcr:primaryType=sling:OsgiConfig" -F "alias=/crx/server" -F "dav.create-absolute-uri=true" -F "dav.create-absolute-uri@TypeHint=Boolean" http://localhost:4502/apps/system/config/org.apache.sling.jcr.davex.impl.servlets.SlingDavExServlet
```

## 其他资源 {#other-resources}

有关AEM 6安全功能的更多信息，请参阅以下页面：

* [AEM安全检查列表](/help/sites-administering/security-checklist.md)
* [在生产就绪模式下运行AEM](/help/sites-administering/production-ready.md)
