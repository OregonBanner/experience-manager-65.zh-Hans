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
exl-id: 33dc1ee7-1e34-43d8-9265-c66535f5e002
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '685'
ht-degree: 6%

---

# 迁移到触屏UI{#migration-to-the-touch-ui}

从版本6.0开始，Adobe Experience Manager(AEM)引入了称为&#x200B;*触屏优化UI*（也称为&#x200B;*触屏优化UI*）的新用户界面。 它符合Adobe Marketing Cloud和整体Adobe用户界面准则。 在AEM中，这已成为标准UI，该UI具有以桌面为导向的旧版界面，称为&#x200B;*经典UI*。

如果您一直在将AEM与经典UI结合使用，则需要采取措施来迁移实例。 本页旨在通过提供指向各个资源的链接来充当跳板。

>[!NOTE]
>
>此类迁移项目可能会对您的实例产生重大影响。 请参阅[管理项目 — 最佳实践](/help/managing/best-practices.md)以了解推荐的准则。

## 基本信息 {#the-basics}

在迁移时，您应该了解经典UI和触屏UI之间的以下（主要）区别：

<table>
 <tbody>
  <tr>
   <td>经典 UI</td>
   <td>触屏优化 UI</td>
  </tr>
  <tr>
   <td>在JCR存储库中描述为节点的结构。 表示UI元素的每个节点都称为<em>ExtJS小组件</em>，并由<code>ExtJS</code>在客户端呈现。</td>
   <td>JCR存储库中也描述为节点的结构。 但是，在这种情况下，每个节点都引用Sling资源类型（Sling组件），负责其渲染。 因此UI（基本上）在服务器端呈现。</td>
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
     <li>使用侦听器直接嵌入必需部分，或在clientlib中管理必需部分。</li>
    </ul> </td>
   <td><p>Javascript位置：</p>
    <ul>
     <li>不能在对话框定义中嵌入必要部分；责任分离。</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>事件处理：</p>
    <ul>
     <li>对话框小组件直接引用Javascript代码。</li>
    </ul> </td>
   <td><p>事件处理：</p>
    <ul>
     <li>Javascript会观察对话事件。</li>
    </ul> </td>
  </tr>
  <tr>
   <td>由客户端完成渲染：
    <ul>
     <li>客户端动态创建UI组件。</li>
     <li>从服务器发出客户端请求（提取）组件定义（JSON格式）。</li>
    </ul> </td>
   <td>由服务器完成渲染：
    <ul>
     <li>客户端请求页面以及相关的UI。</li>
     <li>服务器将UI作为HTML文档发送（推送）；使用Coral UI组件。<br /> </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

换言之，将UI的某个部分从经典UI迁移到触屏UI意味着将&#x200B;*ExtJS小组件*&#x200B;迁移到&#x200B;*Sling组件*。 为了简化此过程，触屏UI基于Granite UI框架，该框架已经为UI提供了一些Sling组件（称为Granite UI组件）。

开始之前，请检查状态和相关推荐：

* [触屏UI功能状态](/help/release-notes/touch-ui-features-status.md)
* [面向客户的用户界面Recommendations](/help/sites-deploying/ui-recommendations.md)

触屏UI开发的基础知识将提供坚实的基础：

* [AEM触屏UI的概念](/help/sites-developing/touch-ui-concepts.md)
* [AEM触屏UI的结构](/help/sites-developing/touch-ui-structure.md)

## 迁移页面创作{#migrating-page-authoring}

在迁移组件时，对话框是一个主要因素：

* [开发AEM组件](/help/sites-developing/developing-components.md) （使用触屏UI）
* [从经典组件迁移](/help/sites-developing/developing-components.md#migrating-from-a-classic-component)
* [AEM现代化工具](/help/sites-developing/modernization-tools.md)  — 可帮助您将经典UI组件的对话框转换为触屏UI

   * 触屏UI中有一个兼容层，用于在“触屏UI包装器”中打开经典UI对话框，但该对话框的功能有限，长期而言，不建议使用该兼容层。

* [在触屏UI中自定义对话框字段](https://helpx.adobe.com/experience-manager/kt/eseminars/gems/aem-customizing-dialog-fields-in-touch-ui.html)
* [创建新的Granite UI字段组件](/help/sites-developing/granite-ui-component.md)
* [自定义页面创作](/help/sites-developing/customizing-page-authoring-touch.md) （使用触屏优化UI）

## 迁移控制台{#migrating-consoles}

您还可以自定义控制台：

* [自定义控制台](/help/sites-developing/customizing-consoles-touch.md) （适用于触屏UI）

## 相关注意事项{#related-considerations}

尽管与迁移到触屏UI并非直接相关，但仍有一些相关问题值得同时考虑，因为也推荐使用以下实践：

* [模板](/help/sites-developing/templates.md)  — 可编 [辑的模板](/help/sites-developing/page-templates-editable.md)
* [核心组件](https://docs.adobe.com/content/help/zh-Hans/experience-manager-core-components/using/introduction.html)
* [HTL](https://docs.adobe.com/content/help/zh-Hans/experience-manager-htl/using/overview.html)

>[!NOTE]
>
>另请参阅[开发 — 最佳实践](/help/sites-developing/best-practices.md)。

## 其他资源{#further-resources}

有关开发AEM的完整信息，请参阅以下资源收集：

* [Developing用户指南](/help/sites-developing/home.md)
* [Granite用户界面文档](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/index.html)
* [AEM 6.5 SitesTutorials和视频](https://docs.adobe.com/content/help/en/experience-manager-learn/sites/overview.html)
* [AEM Sites 开发入门- WKND 教程](/help/sites-developing/getting-started.md)
* [AEM Gems](https://helpx.adobe.com/experience-manager/kt/eseminars/gems/aem-index.html)
* [AEM 现代化工具](https://opensource.adobe.com/aem-modernize-tools/)

>[!CAUTION]
>
>AEM现代化工具是社区共同努力的结果，不受Adobe支持或保证。
