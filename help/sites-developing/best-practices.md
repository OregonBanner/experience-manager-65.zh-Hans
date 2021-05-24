---
title: 最佳实践
seo-title: 最佳实践
description: Adobe工程和咨询团队为AEM开发人员开发了一套全面的最佳实践
seo-description: Adobe工程和咨询团队为AEM开发人员开发了一套全面的最佳实践
uuid: f962c31f-8140-482f-b189-16376e23bfed
contentOwner: Justin Edelson
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 99678c1a-81f3-4fb3-bf73-98f0691c3fb6
exl-id: 0a478e80-c1b2-46c1-a6be-794d78b85d69
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '485'
ht-degree: 13%

---

# 最佳实践{#best-practices}

## 开发人员最佳实践 — 快速入门{#best-practices-for-developers-getting-started}

Adobe工程和咨询团队为AEM开发人员开发了一套全面的最佳实践。 Adobe开发人员在为客户实施开发核心AEM产品更新和客户代码时，会遵循这些最佳实践。

在开始AEM开发项目之前，请首先查看以下最佳实践：

* [开发实践](/help/sites-developing/development-practices.md)
* [内容架构](/help/sites-developing/content-architecture.md)
* [软件架构](/help/sites-developing/software-architecture.md)
* [编码提示](/help/sites-developing/coding-tips.md)
* [代码缺陷](/help/sites-developing/code-pitfalls.md)
* [JCR交互](/help/sites-developing/jcr-integration.md)
* [OSGi包](/help/sites-developing/osgi-bundles.md)
* [Java API最佳实践](https://docs.adobe.com/content/help/en/experience-manager-learn/foundation/development/understand-java-api-best-practices.html)

### 其他最佳实践信息{#additional-best-practices-information}

以下区域提供了专门用于制定最佳实践的文档：

* [站点](#sites)
* [社区](/help/sites-developing/best-practices.md#communities)
* [工具/HTL](/help/sites-developing/best-practices.md#tooling-htl)

以下各表中介绍了具体的文档并提供了相应链接。

有关管理、部署和维护或创作的最佳实践，请参阅以下内容之一：

* [管理最佳实践](/help/sites-administering/administer-best-practices.md)
* [创作最佳实践](/help/sites-authoring/best-practices.md)
* [部署最佳实践](/help/sites-deploying/best-practices.md)

## 站点 {#sites}

在管理和创作网站内容方面具有一些最佳实践，如下所述：

<table>
 <tbody>
  <tr>
   <td>标准触屏UI背后的一些理论。</td>
   <td><p><a href="/help/sites-developing/touch-ui-concepts.md">触屏优化UI:概念</a></p> <p><a href="/help/sites-developing/touch-ui-structure.md">触屏优化UI:结构</a></p> </td>
   <td>这些文档概述了触屏优化UI的概念和结构。</td>
  </tr>
  <tr>
   <td>触屏优化UI:自定义控制台 </td>
   <td><a href="/help/sites-developing/customizing-consoles-touch.md">自定义触屏优化UI控制台</a></td>
   <td>本文档介绍了扩展触屏UI控制台的最佳方法。</td>
  </tr>
  <tr>
   <td>触屏UI:自定义页面创作</td>
   <td><a href="/help/sites-developing/customizing-page-authoring-touch.md">自定义触屏优化UI页面创作</a></td>
   <td>介绍如何为触屏UI扩展页面创作。</td>
  </tr>
  <tr>
   <td>工作流</td>
   <td><a href="/help/sites-developing/workflows-best-practices.md">开发和扩展工作流</a></td>
   <td><p>工作流可让您自动执行Adobe Experience Manager(AEM)活动，并且可以代表AEM环境中发生的大量处理，因此强烈建议仔细规划工作流实施。</p> </td>
  </tr>
 </tbody>
</table>

## 社区 {#communities}

[AEM](/help/communities/overview.md) 社区简化了内部部署社区的创建和管理。

下面介绍了社区的一些最佳实践：

|  |  |  |
|---|---|---|
| 使用用户生成内容(UGC)的最佳实践 | [编码准则](/help/communities/code-guide.md) | 为[社交组件框架](/help/communities/scf.md)(SCF)开发灵活的可移植代码的准则。 |
| 社区组件的使用示例 | [社区组件指南](/help/communities/components-guide.md) | 交互式开发工具。 |

## 工具/HTL {#tooling-htl}

HTML模板语言(HTL)是一种新的HTML模板系统，随AEM 6.0的推出而成，它取代了JSP和ESP作为AEM的首选模板系统。

|  |  |  |
|---|---|---|
| HTL概述 | [HTL概述和语法](https://docs.adobe.com/content/help/zh-Hans/experience-manager-htl/using/overview.html) | 本文档介绍HTL是什么，如何迁移到HTL、示例项目、语法、表达式和语句 |
| 在java中使用API | [HTL Java Use-API](https://helpx.adobe.com/experience-manager/htl/using/use-api.html) | HTL Java Use-API允许HTL文件访问自定义Java类中的Helper方法。 |

>[!NOTE]
>
>以下多部分教程可能最符合设置新AEM项目的最佳实践，其中详细介绍了核心组件、可编辑模板、客户端库和组件开发：
>[AEM Sites - WKND 教程快速入门](https://helpx.adobe.com/experience-manager/kt/sites/using/getting-started-wknd-tutorial-develop.html)
