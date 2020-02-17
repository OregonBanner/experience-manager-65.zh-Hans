---
title: 一致性和遍历检查
seo-title: 一致性和遍历检查
description: 了解如何执行一致性和遍历检查。
seo-description: 了解如何执行一致性和遍历检查。
uuid: 0304e378-7c60-4bf5-9052-d01149d2a6df
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
discoiquuid: af9a3e9d-194a-42e5-be28-b238e0c1e55e
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 一致性和遍历检查{#consistency-and-traversal-checks}

升级时，可能会因工作区不一致而出现问题。 您可以运行测试升级来查看这是否是问题，也可以运行一致性检查作为预防性操作。

如果运行由于工作区不一致而失败的测试升级，您将看到与crx-quickstart/logs/crx/error.log中的以下条目类似的条目：

```xml
*ERROR* TarPersistenceManager: No bundle found for uuid 'deadbeef-cafe-babe-cafe-babecafebabe'
 ...
*ERROR* RepositoryImpl: Failed to initialize workspace 'crx.default'
javax.jcr.RepositoryException: Error indexing workspace: Error indexing workspace: Error indexing workspace
...
```

## 执行一致性检查 {#perform-a-consistency-check}

要执行一致性检查，请导航到JMX Mbean**com.adobe.granite（存储库）**的管理页。 从AEM主屏幕，转到：

**“工具”>“Web控制台”>“主”（在菜单栏上）>“JMX”>“com.adobe.granite（存储库）”**

**[在默认安装中，它位于以下位置：  |显示我|](http://localhost:4502/system/console/jmx/com.adobe.granite%3Atype%3DRepository)**

在页 **面的** “操作”部分，您将找到两种方法： **`traversalCheck`** 和 **`consistencyCheck`**。 要执行检查，请单击操作并输入所需的参数。

![chlimage_1-117](assets/chlimage_1-117.png)

