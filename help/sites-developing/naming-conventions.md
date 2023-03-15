---
title: 命名约定
seo-title: Naming Conventions
description: 存储库中的节点遵循Java内容存储库的命名约定
seo-description: Nodes in the repository are subject to naming conventions of the Java Content Repository
uuid: 0515c5c5-3e93-4710-983f-c08c146467fc
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 198098c0-432b-4a93-a94e-2552337435dd
exl-id: 01c6bb29-1d2d-4a45-b291-0e8d97c01a08
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '301'
ht-degree: 16%

---

# 命名约定{#naming-conventions}

存储库中的节点遵循的命名约定 [Java内容存储库](/help/sites-developing/the-basics.md#java-content-repository). 但是，AEM对页面节点名称施加了进一步的约定。

## 页面的命名约定 {#naming-conventions-for-pages}

这些命名惯例在各级实施：

* JcrUtil：的AEM实现 [JCR实用程序](#jcr-utilities).
* PageManager： [页面管理器](#page-manager) 提供页面级别操作的方法。
* 根据使用的UI：

   * [标准、触屏优化UI](#standard-ui)
   * [经典 UI](#classic-ui)

### JCR实用程序 {#jcr-utilities}

[JcrUtil](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/index.html?com/day/cq/commons/jcr/JcrUtil.html) 是JCR实用程序的AEM实施。 验证名称特别感兴趣的是它控制的字符映射以及以下验证：

* `isValidName`

   * 检查名称是否不为空且仅包含有效字符。
   * 可用于检查建议的名称是否有效。

* `createValidName`

   * 这会根据任意字符串创建一个有效标签。
   * 它可用于从标题创建名称。

### 页面管理器 {#page-manager}

[PageManager](https://helpx.adobe.com/cn/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/PageManager.html) 提供页面级别操作的方法，基于 [JCRUtil](#jcr-utilities).

### 标准 UI {#standard-ui}

标准触屏UI：

* 在执行以下任一操作时，根据PageManager施加的限制验证名称：

   * 提供了页面标题以转换为节点名称
   * 提供了明确的节点名称

### 经典 UI {#classic-ui}

经典 UI 实施更严格的限制：

* 在以下情况之一时验证显式节点名称的名称：

   * 提供了页面标题以转换为节点名称
   * 提供了明确的节点名称

* 有效字符(从经典UI中创建页面时，实际上只有这些字符有效，即使 `PageManagerImpl` 将允许附加字符)：

   * “a”至“z”
   * “A”至“Z”
   * “0”至“9”
   * _（下划线）
   * `-` （短划线/减号）
