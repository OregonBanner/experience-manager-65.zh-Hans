---
title: 命名约定
seo-title: 命名约定
description: 存储库中的节点受Java内容存储库的命名约定的约束
seo-description: 存储库中的节点受Java内容存储库的命名约定的约束
uuid: 0515c5c5-3e93-4710-983f-c08c146467fc
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 198098c0-432b-4a93-a94e-2552337435dd
translation-type: tm+mt
source-git-commit: 5128a08d4db21cda821de0698b0ac63ceed24379

---


# 命名约定{#naming-conventions}

Nodes in the repository are subject to naming conventions of the [Java Content Repository](/help/sites-developing/the-basics.md#java-content-repository). 但是，AEM对页面节点名称有进一步约定。

## 页面命名约定 {#naming-conventions-for-pages}

这些命名约定在不同级别实施：

* JcrUtil:JCR实用程序的AEM [实施](#jcr-utilities)。
* PageManager:页面 [管理器](#page-manager) (Page Manager)提供了页面级别操作的方法。
* 根据所使用的UI:

   * [标准的触屏优化UI](#standard-ui)
   * [经典 UI](#classic-ui)

### JCR实用程序 {#jcr-utilities}

[JcrUtil](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/index.html?com/day/cq/commons/jcr/JcrUtil.html) 是JCR实用程序的AEM实现。 对于验证名称而言，特别感兴趣的是它控制的字符映射和以下验证：

* `isValidName`

   * 检查名称是否不为空并且仅包含有效字符。
   * 可用于检查建议的名称是否有效。

* `createValidName`

   * 这将从任意字符串创建有效标签。
   * 它可用于从标题创建名称。

### 页面管理器 {#page-manager}

[PageManager根据](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/PageManager.html) JCRUtil提供页面级操作的 [方法](#jcr-utilities)。

### 标准UI {#standard-ui}

标准的触屏优化UI:

* 在以下任一情况下，根据PageManager实施的限制验证名称：

   * 提供页面标题以转换为节点名称
   * 提供了明确的节点名称

### 经典 UI {#classic-ui}

经典 UI 实施更严格的限制：

* 在以下任一情况下验证显式节点名称时的名称：

   * 提供页面标题以转换为节点名称
   * 提供了明确的节点名称

* 有效字符(在经典UI中创建页面时，即使允许添加其他字符，但只有这些字符 `PageManagerImpl` 才实际有效):

   * “a”至“z”
   * “A”至“Z”
   * “0”至“9”
   * _（下划线）
   * `-` （短划线／减号）

