---
title: 在AEM中启用CRXDE Lite
seo-title: 在AEM中启用CRXDE Lite
description: 了解如何在AEM中启用CRXDE Lite。
seo-description: 了解如何在AEM中启用CRXDE Lite。
uuid: d7a3db67-6384-463b-9aa9-f08ecc6c99c6
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: 72df3ece-badf-466b-8f9a-0ec985d87741
translation-type: tm+mt
source-git-commit: a833a34bbeb938c72cdb851a46b2ffd97aee9f6d

---


# 在AEM中启用CRXDE Lite{#enabling-crxde-lite-in-aem}

为确保AEM安装尽可能安全，安全清单建议在生产环境 [中禁用WebDAV](/help/sites-administering/security-checklist.md#disable-webdav) 。

但是，CRXDE Lite依赖于捆绑包才能正 `org.apache.sling.jcr.davex` 常工作，因此禁用WebDAV也将有效地禁用CRXDE Lite。

如果发生这种情况，浏览到 `https://serveraddress:4502/crx/de/index.jsp` 将显示空的根节点，并且对CRXDE Lite资源的所有HTTP请求都将失败：

```xml
404 Resource at '/crx/server/crx.default/jcr:root/.1.json' not found: No resource found
```

虽然此建议旨在尽可能减少攻击面，但系统管理员有时可能需要访问CRXDE Lite，以浏览生产实例上的内容或调试问题。

如果禁用，您可以按照以下过程打开CRXDE Lite:

1. 转到OSGi组件控制台，网址为 `http://localhost:4502/system/console/components`
1. 搜索以下组件：

   * `org.apache.sling.jcr.davex.impl.servlets.SlingDavExServlet`

1. 单击扳手图标旁边的扳手图标可查看其配置选项：

   ![chlimage_1-80](assets/chlimage_1-80a.png)

1. 创建以下配置：

   * **根路径:** `/crx/server`
   * 勾选“使用绝 **对URI”下的框**。

1. 使用完CRXDE Lite后，请确保再次禁用WebDAV。

您还可以通过cURL启用CRXDE Lite，方法是运行以下命令：

```shell
curl -u admin:admin -F "jcr:primaryType=sling:OsgiConfig" -F "alias=/crx/server" -F "dav.create-absolute-uri=true" -F "dav.create-absolute-uri@TypeHint=Boolean" http://localhost:4502/apps/system/config/org.apache.sling.jcr.davex.impl.servlets.SlingDavExServlet
```

## 其他资源 {#other-resources}

有关AEM 6安全功能的详细信息，请参阅以下页面：

* [AEM安全核对清单](/help/sites-administering/security-checklist.md)
* [在生产就绪模式下运行AEM](/help/sites-administering/production-ready.md)

