---
title: 最佳实践
seo-title: 最佳实践
description: Adobe工程和咨询团队为AEM开发人员开发了一整套最佳做法
seo-description: Adobe工程和咨询团队为AEM开发人员开发了一整套最佳做法
uuid: f962c31f-8140-482f-b189-16376e23bfed
contentOwner: Justin Edelson
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 99678c1a-81f3-4fb3-bf73-98f0691c3fb6
translation-type: tm+mt
source-git-commit: e562939f1c64d8345b4c2a28e4b882200d9e4c07

---


# 最佳实践{#best-practices}

## 开发人员的最佳实践——快速入门 {#best-practices-for-developers-getting-started}

Adobe工程和咨询团队为AEM开发人员开发了一整套最佳做法。 Adobe开发人员在为客户实施开发核心AEM产品更新和客户代码时，会遵守这些最佳实践。

在开始AEM开发项目之前，请首先查看以下最佳实践：

* [开发实践](/help/sites-developing/development-practices.md)
* [内容架构](/help/sites-developing/content-architecture.md)
* [软件架构](/help/sites-developing/software-architecture.md)
* [编码提示](/help/sites-developing/coding-tips.md)
* [代码缺陷](/help/sites-developing/code-pitfalls.md)
* [JCR交互](/help/sites-developing/jcr-integration.md)
* [OSGi捆绑套件](/help/sites-developing/osgi-bundles.md)
* [Java API最佳实践](https://docs.adobe.com/content/help/en/experience-manager-learn/foundation/development/understand-java-api-best-practices.html)

### 其他最佳实践信息 {#additional-best-practices-information}

以下区域提供了专门用于制定最佳实践的文档：

* [站点](#sites)
* [社区](/help/sites-developing/best-practices.md#communities)
* [工具/HTL](/help/sites-developing/best-practices.md#tooling-htl)

以下各表中介绍了具体的文档并提供了相应链接。

有关管理、部署和维护或创作的最佳实践，请参阅以下任一内容：

* [管理最佳实践](/help/sites-administering/administer-best-practices.md)
* [创作最佳实践](/help/sites-authoring/best-practices.md)
* [部署最佳实践](/help/sites-deploying/best-practices.md)

## 站点 {#sites}

在管理和创作网站内容方面具有一些最佳实践，如下所述：

<table>
 <tbody>
  <tr>
   <td>标准触屏优化UI背后的一些理论。</td>
   <td><p><a href="/help/sites-developing/touch-ui-concepts.md">触屏优化UI:概念</a></p> <p><a href="/help/sites-developing/touch-ui-structure.md">触屏优化UI:结构</a></p> </td>
   <td>这些文档概述了触屏优化UI的概念和结构。</td>
  </tr>
  <tr>
   <td>触屏优化UI:自定义控制台 </td>
   <td><a href="/help/sites-developing/customizing-consoles-touch.md">自定义触屏优化UI控制台</a></td>
   <td>此文档描述了扩展触屏优化UI控制台的最佳方式。</td>
  </tr>
  <tr>
   <td>触屏优化UI:自定义页面创作</td>
   <td><a href="/help/sites-developing/customizing-page-authoring-touch.md">自定义触屏优化UI页面创作</a></td>
   <td>介绍如何扩展触屏优化UI的页面创作。</td>
  </tr>
  <tr>
   <td>工作流</td>
   <td><a href="/help/sites-developing/workflows-best-practices.md">开发和扩展工作流</a></td>
   <td><p>工作流使您能够自动化Adobe Experience Manager(AEM)活动，并可以代表AEM环境中发生的大量处理，因此强烈建议仔细计划您的工作流实施。</p> </td>
  </tr>
 </tbody>
</table>

## 社区 {#communities}

[AEM Communities](/help/communities/overview.md) 简化了内部部署社区的创建和管理。

下面介绍了社区的一些最佳实践：

|  |  |  |
|---|---|---|
| 使用用户生成内容(UGC)的最佳实践 | [编码准则](/help/communities/code-guide.md) | 为社交组件框架(SCF)开发灵活、可 [移植代码的指南](/help/communities/scf.md) 。 |
| 社区组件的示例使用 | [社区组件指南](/help/communities/components-guide.md) | 交互式开发工具。 |

## 工具/HTL {#tooling-htl}

HTML模板语言(HTL)是AEM 6.0中引入的一个新的HTML模板系统。它取代了JSP和ESP作为AEM的首选模板系统。

|  |  |  |
|---|---|---|
| HTL概述 | [HTL概述和语法](https://docs.adobe.com/content/help/zh-Hans/experience-manager-htl/using/overview.html) | 本文档介绍HTL是什么，如何移到HTL，示例项目、语法、表达式和语句 |
| 在Java中使用API | [HTL Java Use-API](https://helpx.adobe.com/experience-manager/htl/using/use-api.html) | HTL Java Use-API使HTL文件能够访问自定义Java类中的帮助程序方法。 |

>[!NOTE]
>
>下面的多部分教程可能是设置新AEM项目的最佳实践（详细介绍核心组件、可编辑模板、客户端库和组件开发）的最佳方法：
>[Getting Started with AEM Sites - WKND Tutorial](https://helpx.adobe.com/experience-manager/kt/sites/using/getting-started-wknd-tutorial-develop.html)

