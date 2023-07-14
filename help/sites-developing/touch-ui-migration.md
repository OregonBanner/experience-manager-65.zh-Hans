---
title: 迁移到触控UI
description: 迁移到触控UI
contentOwner: AEM Docs
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: introduction
docset: aem65
exl-id: 33dc1ee7-1e34-43d8-9265-c66535f5e002
source-git-commit: 260f71acd330167572d817fdf145a018b09cbc65
workflow-type: tm+mt
source-wordcount: '659'
ht-degree: 5%

---

# 迁移到触控UI{#migration-to-the-touch-ui}

从版本6.0开始，Adobe Experience Manager (AEM)引入了一个新的用户界面，称为 *触屏优化UI* (也简称为 *触控UI*)。 它与Adobe Experience Cloud和整个Adobe用户界面准则保持一致。 这已成为AEM中的标准UI，具有称为 *经典UI*.

如果您一直在将AEM与经典UI一起使用，请采取措施迁移您的实例。 本页旨在通过提供指向单个资源的链接来充当跳板。

>[!NOTE]
>
>此类迁移项目可能会对您的实例产生重大影响。 参见 [管理项目 — 最佳实践](/help/managing/best-practices.md) 推荐的指南。

## 基础知识 {#the-basics}

迁移时，请注意经典用户界面和触屏UI之间的以下主要差异：

<table>
 <tbody>
  <tr>
   <td>经典 UI</td>
   <td>触屏优化UI</td>
  </tr>
  <tr>
   <td>在JCR存储库中作为节点结构描述。 表示UI元素的每个节点都称为 <em>ExtJS小组件</em> 并在客户端上渲染的客户 <code>ExtJS</code>.</td>
   <td>在JCR存储库中还描述为一个节点结构。 但是，在这种情况下，每个节点都引用一个Sling资源类型（Sling组件），该资源类型负责其渲染。 因此，UI（基本上）呈现在服务器端。</td>
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
   <td><p>JavaScript位置：</p>
    <ul>
     <li>命令部件直接使用侦听器嵌入或在clientlibs中管理。</li>
    </ul> </td>
   <td><p>JavaScript位置：</p>
    <ul>
     <li>必须部分不能嵌入对话定义中；责任分离。</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>事件处理：</p>
    <ul>
     <li>对话框构件直接引用JavaScript代码。</li>
    </ul> </td>
   <td><p>事件处理：</p>
    <ul>
     <li>JavaScript观察对话框事件。</li>
    </ul> </td>
  </tr>
  <tr>
   <td>渲染由客户端完成：
    <ul>
     <li>客户端动态创建UI组件。</li>
     <li>客户端从服务器请求（拉取）组件定义（作为JSON）。</li>
    </ul> </td>
   <td>渲染由服务器完成：
    <ul>
     <li>客户端请求页面以及相关UI。</li>
     <li>服务器将UI作为HTML文档发送（推送）；使用Coral UI组件。<br /> </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

换句话说，将UI的一部分从经典UI迁移到触屏UI意味着移植 *ExtJS小组件* 到 *Sling组件*. 为便于实现，触屏UI基于Granite UI框架，该框架已为UI提供了一些Sling组件（称为Granite UI组件）。

在开始之前，请检查状态和相关建议：

* [触屏UI功能状态](/help/release-notes/touch-ui-features-status.md)
* [客户的用户界面Recommendations](/help/sites-deploying/ui-recommendations.md)

触屏UI的开发基础提供了坚实的基础：

* [AEM触屏优化UI的概念](/help/sites-developing/touch-ui-concepts.md)
* [AEM触屏优化UI的结构](/help/sites-developing/touch-ui-structure.md)

## 迁移页面创作 {#migrating-page-authoring}

对话框是迁移组件时的主要因素：

* [开发AEM组件](/help/sites-developing/developing-components.md) （带有触屏优化UI）
* [从经典组件迁移](/help/sites-developing/developing-components.md#migrating-from-a-classic-component)
* [AEM现代化工具](/help/sites-developing/modernization-tools.md)  — 帮助您将经典UI组件的对话框转换为Touch UI

   * 触屏UI中有一个兼容层，用于在“触屏UI包装器”中打开经典UI对话框，但此功能有限，不建议长期使用。

* [在触屏UI中自定义对话框字段](https://helpx.adobe.com/experience-manager/kt/eseminars/gems/aem-customizing-dialog-fields-in-touch-ui.html)
* [创建新的Granite UI字段组件](/help/sites-developing/granite-ui-component.md)
* [自定义页面创作](/help/sites-developing/customizing-page-authoring-touch.md) （带有触屏优化UI）

## 迁移控制台 {#migrating-consoles}

您还可以自定义控制台：

* [自定义控制台](/help/sites-developing/customizing-consoles-touch.md) （适用于触屏优化UI）

## 相关注意事项 {#related-considerations}

尽管与迁移到触屏UI没有直接关系，但有一些相关问题值得同时考虑，因为它们也是推荐的实践：

* [模板](/help/sites-developing/templates.md) - [可编辑的模板](/help/sites-developing/page-templates-editable.md)
* [核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html)
* [HTL](https://experienceleague.adobe.com/docs/experience-manager-htl/content/overview.html)

>[!NOTE]
>
>另请参阅 [开发 — 最佳实践](/help/sites-developing/best-practices.md).

## 更多资源 {#further-resources}

有关开发AEM的完整信息，请参阅以下内容下的资源收集：

* [开发用户指南](/help/sites-developing/home.md)
* [Granite UI文档](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/index.html)
* [AEM 6.5 SitesTutorials和视频](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/overview.html)
* [AEM Sites 开发快速入门 – WKND 教程](/help/sites-developing/getting-started.md)
* [AEM Gems](https://experienceleague.adobe.com/docs/events/experience-manager-gems-recordings/overview.html?lang=en)
* [AEM 现代化工具](https://opensource.adobe.com/aem-modernize-tools/)

>[!CAUTION]
>
>AEM现代化工具是社区共同努力的结果，Adobe不支持或不保证这些工具。
