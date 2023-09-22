---
title: 一致性和遍历检查
description: 了解如何执行一致性和遍历检查。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
feature: Configuring
exl-id: 10dde29b-5dc7-4d4e-80ae-3d4fd0397f7e
source-git-commit: b66ec42c35b5b60804015d340b8194bbd6ef3e28
workflow-type: tm+mt
source-wordcount: '153'
ht-degree: 0%

---

# 一致性和遍历检查{#consistency-and-traversal-checks}

升级时，可能会由于工作区不一致而出现问题。 您可以运行测试升级以查看这是否是问题，也可以将一致性检查作为预防性操作运行。

如果运行因工作区不一致而失败的测试升级，则会在crx-quickstart/logs/crx/error.log中看到与以下内容类似的条目：

```xml
*ERROR* TarPersistenceManager: No bundle found for uuid 'deadbeef-cafe-babe-cafe-babecafebabe'
 ...
*ERROR* RepositoryImpl: Failed to initialize workspace 'crx.default'
javax.jcr.RepositoryException: Error indexing workspace: Error indexing workspace: Error indexing workspace
...
```

## 执行一致性检查 {#perform-a-consistency-check}

要执行一致性检查，请导航到JMX Mbean的管理页面 **com.adobe.granite（存储库）**. 从AEM主屏幕，转到：

**工具> Web控制台>主页（位于菜单栏上）> JMX > com.adobe.granite （存储库）**

在默认安装中，可以在此处找到它：  **[|向我显示|](http://localhost:4502/system/console/jmx/com.adobe.granite%3Atype%3DRepository)**

在 **操作** 部分，您可以找到两种方法： **`traversalCheck`** 和 **`consistencyCheck`**. 要运行检查，请单击操作并输入所需的参数。

![chlimage_1-117](assets/chlimage_1-117.png)
