---
title: 迁移到触屏UI
seo-title: 迁移到触屏UI
description: 迁移到触屏UI
seo-description: 迁移到触屏UI
uuid: 47c43b56-532b-4ada-8503-04d66bab3564
contentOwner: aheimoz
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: introduction
discoiquuid: b315720f-e9b8-4063-99e2-1b9aa6bba460
docset: aem65
translation-type: tm+mt
source-git-commit: 5597fb39500ac1f85d03263bfa1e5239d35d2a2c
workflow-type: tm+mt
source-wordcount: '685'
ht-degree: 6%

---


# 迁移到触屏UI{#migration-to-the-touch-ui}

从6.0版开始，Adobe Experience Manager(AEM)引入了称为&#x200B;*触屏优化UI*（也称为&#x200B;*触屏优化UI*）的新用户界面。 它符合Adobe Marketing Cloud和Adobe用户界面的总体准则。 这已成为AEM中标准UI，其传统的、面向桌面的界面称为&#x200B;*经典UI*。

如果您已经将AEM与经典UI结合使用，则需要采取措施来迁移实例。 本页旨在通过提供指向各个资源的链接充当跳板。

>[!NOTE]
>
>此类迁移项目可能会对您的实例产生重大影响。 有关建议的准则，请参阅[管理项目——最佳实践](/help/managing/best-practices.md)。

## 基本信息 {#the-basics}

迁移时，您应注意经典UI和触屏UI之间的以下（主要）区别：

<table>
 <tbody>
  <tr>
   <td>经典 UI</td>
   <td>触屏优化 UI</td>
  </tr>
  <tr>
   <td>在JCR存储库中描述为节点结构。 每个表示UI元素的节点都称为<em>ExtJS构件</em>，并由<code>ExtJS</code>在客户端呈现。</td>
   <td>在JCR存储库中也描述为节点结构。 但是，在这种情况下，每个节点都引用Sling资源类型（Sling组件），它负责其呈现。 因此UI（基本上）在服务器端呈现。</td>
  </tr>
  <tr>
   <td><p><code>sling:resourceType</code></p>
    <ul>
     <li>未使用</li>
    </ul> </td>
   <td><code>sling:resourceType</code>
    <ul>
     <li>已使用</li>
     <li>例如<br /> <code>cq/gui/components/authoring/dialog</code><br /> </li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>对话框节点：</p>
    <ul>
     <li>名称: <code>dialog</code></li>
     <li>jcr:primaryType: <code>cq:Dialog</code></li>
    </ul> </td>
   <td><p>对话框节点：</p>
    <ul>
     <li>名称: <code>cq:dialog</code></li>
     <li>jcr:primaryType: <code>nt:unstructured</code></li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>Javascript位置：</p>
    <ul>
     <li>使用监听器直接嵌入或在客户端库中管理必需部分。</li>
    </ul> </td>
   <td><p>Javascript位置：</p>
    <ul>
     <li>必要部分不能嵌入对话框定义；责任分离。</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>事件处理：</p>
    <ul>
     <li>对话框构件直接引用Javascript代码。</li>
    </ul> </td>
   <td><p>事件处理：</p>
    <ul>
     <li>Javascript会遵守对话事件。</li>
    </ul> </td>
  </tr>
  <tr>
   <td>由客户端完成渲染：
    <ul>
     <li>客户端动态创建UI组件。</li>
     <li>客户端从服务器请求（拉取）组件定义(JSON)。</li>
    </ul> </td>
   <td>服务器完成渲染：
    <ul>
     <li>客户端请求页面以及相关UI。</li>
     <li>服务器将UI作为HTML文档发送（推送）;使用Coral UI组件。<br /> </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

换言之，将UI的某一部分从经典UI迁移到触屏UI意味着将&#x200B;*ExtJS构件*&#x200B;移植到&#x200B;*Sling组件*。 为了简化此操作，触屏UI基于Granite UI框架，该框架已经为UI提供了一些Sling组件（称为Granite UI组件）。

在开始之前，请检查状态和相关建议：

* [触屏UI功能状态](/help/release-notes/touch-ui-features-status.md)
* [客户用户界面Recommendations](/help/sites-deploying/ui-recommendations.md)

触屏UI开发的基础知识将提供坚实的基础：

* [AEM触屏优化UI的概念](/help/sites-developing/touch-ui-concepts.md)
* [AEM触屏优化UI的结构](/help/sites-developing/touch-ui-structure.md)

## 迁移页面创作{#migrating-page-authoring}

迁移组件时，对话框是主要因素：

* [开发AEM组件](/help/sites-developing/developing-components.md) （使用触屏优化UI）
* [从经典组件迁移](/help/sites-developing/developing-components.md#migrating-from-a-classic-component)
* [对话框转换工具](/help/sites-developing/dialog-conversion.md) -帮助您将经典UI组件的对话框转换为触屏UI

   * 触屏UI中有一个兼容层，用于在“触屏UI包装器”中打开经典UI对话框，但功能有限，长期而言不推荐使用。

* [在触屏UI中自定义对话框字段](https://helpx.adobe.com/experience-manager/kt/eseminars/gems/aem-customizing-dialog-fields-in-touch-ui.html)
* [创建新的Granite UI字段组件](/help/sites-developing/granite-ui-component.md)
* [自定义页面创作](/help/sites-developing/customizing-page-authoring-touch.md) （使用触屏优化UI）

## 迁移控制台{#migrating-consoles}

您还可以自定义控制台：

* [自定义控制台](/help/sites-developing/customizing-consoles-touch.md) （适用于触屏优化UI）

## 相关注意事项{#related-considerations}

尽管与迁移到触屏UI并不直接相关，但是也存在一些相关问题值得考虑，因为它们也是推荐的做法：

* [模板](/help/sites-developing/templates.md) -可 [编辑模板](/help/sites-developing/page-templates-editable.md)
* [核心组件](https://docs.adobe.com/content/help/zh-Hans/experience-manager-core-components/using/introduction.html)
* [HTL](https://docs.adobe.com/content/help/zh-Hans/experience-manager-htl/using/overview.html)

>[!NOTE]
>
>另请参阅[开发——最佳实践](/help/sites-developing/best-practices.md)。

## 其他资源{#further-resources}

有关开发AEM的完整信息，请参阅以下资源集合：

* [开发用户指南](/help/sites-developing/home.md)
* [Granite UI文档](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/index.html)
* [AEM 6.5站点Tutorials和视频](https://docs.adobe.com/content/help/en/experience-manager-learn/sites/overview.html)
* [AEM Sites 开发入门- WKND 教程](/help/sites-developing/getting-started.md)
* [AEM Gems](https://helpx.adobe.com/experience-manager/kt/eseminars/gems/aem-index.html)
* [AEM 现代化工具](https://opensource.adobe.com/aem-modernize-tools/)

>[!CAUTION]
>
>AEM现代化工具是一项社区工作，不受Adobe支持或担保。

