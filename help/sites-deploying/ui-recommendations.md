---
title: 客户用户界面Recommendations
seo-title: 客户用户界面Recommendations
description: 与经典和触屏优化用户界面相关的推荐列表。
seo-description: 与经典和触屏优化用户界面相关的推荐列表。
uuid: 9ec2c9de-a79e-4f2c-a90f-b38ba9553e07
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 8f06d4b6-7d30-4ebc-9c6a-3bb8607a9be8
docset: aem65
translation-type: tm+mt
source-git-commit: 5597fb39500ac1f85d03263bfa1e5239d35d2a2c
workflow-type: tm+mt
source-wordcount: '815'
ht-degree: 1%

---


# 客户的用户界面Recommendations{#user-interface-recommendations-for-customers}

Adobe Experience Manager提供两种UI-统一Experience CloudUI（也称为触屏优化UI）和经典UI。

此文档旨在引导客户根据自己的情况选择要使用的UI。

利息条款：

* **UI（或标准UI）**
5.6.0中引入的现代化用户界面是一种技术预览，在后续发行版中进行了扩展。它基于Adobe Experience Cloud的统一用户体验，以前称为触屏优化UI或触屏优化UI。

* **基**
于ExtJS技术的经典UIser界面，2008年CQ 5.1中引入了该界面。

* **站点**
管理用于管理站点层次结构（移动、激活、管理引用）和创建新页面的功能。

* **页面**
创作用于添加／编辑页面内容的功能。

* **DAM/资产管**
理用于管理数字资产(包括图像、视频、文档、下载)的功能。

* **ContextHubCapabilities**
，可聚合有关访客的信息并将其用于各种用途。提供用户界面以模拟访问网站的人员。 从AEM 6.2开始，ContextHub取代了之前的技术Client Context。

## 常规 {#general}

在过去几年中，Adobe通过统一的用户界面更新了所有Adobe Experience Cloud解决方案。 Experience Cloud解决方案中的用户在如何使用和操作应用程序方面拥有一致的常见模式体验。 在每个版本中，Adobe都根据跨各种解决方案工作的客户的反馈来改进其用户界面。

AEM 6.5中提供了Adobe Experience Manager公司（以前称为CQ5）的原始用户界面（运行版本5.0-5.6.1的客户在2008年推出）。这保证客户可以更新到6.5，并从具有新功能的更新平台受益，同时继续使用相同的用户界面。

Adobe建议客户计划在2018/19年切换到新UI。 这可以在6.5的更新期间完成，也可以在更新后的单独项目中完成，其中包括对自定义和组件对话框进行必要的调整。

AEM 6.4中已弃用经典UI,Adobe不打算进一步增强经典UI。 请注意，经典 UI 在弃用期间仍完全受支持。

### 规则和Recommendations{#rules-and-recommendations}

以下是Adobe Experience Manager6.5产品管理部的一列表建议：

<table>
 <tbody>
  <tr>
   <th>我的项目……</th>
   <th>推荐</th>
  </tr>
  <tr>
   <td>刚开始使用Adobe Experience Manager。</td>
   <td>使用默认UI。</td>
  </tr>
  <tr>
   <td><p>已使用AEM一段时间。</p> <p>已使用现成产品UI并为站点开发自定义组件。<br /> </p> </td>
   <td>
    <ol>
     <li>更新到6.5</li>
     <li>使用默认UI进行站点管理、资产…… 以此类推。<br /> </li>
     <li>配置“编辑页面”操作以打开经典UI页面编辑器。 请参阅<a href="#selecting-your-ui">选择UI</a>。</li>
    </ol> <p>然后，在第二阶段：</p>
    <ol>
     <li>更新组件对话框以使用Coral 3对话框格式。 Adobe建议使用<a href="/help/sites-developing/dialog-conversion.md">对话框转换工具</a>更新组件。</li>
    </ol> </td>
  </tr>
  <tr>
   <td>已构建一个使用集成ClientContext的站点。<br /> </td>
   <td>
    <ol>
     <li>更新到6.5</li>
     <li>使用默认UI进行站点管理、资产…… 以此类推。</li>
     <li>配置“编辑页面”操作以打开经典UI页面编辑器。 请参阅<a href="#selecting-your-ui">选择UI</a>。</li>
    </ol> <p>然后，在第二阶段：</p>
    <ol>
     <li>更新组件对话框以使用Coral 3对话框格式。 Adobe建议使用<a href="/help/sites-developing/dialog-conversion.md">对话框转换工具</a>更新组件。</li>
     <li>配置ContextHub(ClientContext的替换)并更新页面模板以使用ContextHub。 请注意，ContextHub具有允许加载自定义ClientContext存储的兼容模式。</li>
    </ol> </td>
  </tr>
  <tr>
   <td><p>已使用CQ/AEM多年。</p> <p>已扩展产品UI（例如，站点管理），并构建了包含大量编辑对话框的组件。</p> </td>
   <td><p>更新到6.5并将经典UI配置为所有用户进行页面创作的默认UI。 请参阅<a href="#selecting-your-ui">选择UI</a>。</p> <p>然后开始项目以应用Coral 3格式的自定义和优化组件对话框。 请参阅帮助</a>的<a href="#resources-to-help">资源。<br /> </a></p> </td>
  </tr>
 </tbody>
</table>

### 常见问题解答{#faq}

有关详细信息，请参阅知识库文章[触屏UI创作常见问题解答](https://helpx.adobe.com/experience-manager/kb/index/touchui_faq.html);包括有关经典UI的弃用计划的任何信息。

### 选择您的UI {#selecting-your-ui}

有关根据需要配置系统的信息，请参阅[选择您的UI](/help/sites-authoring/select-ui.md)。

### 触屏优化UI状态{#touch-enabled-ui-status}

有关AEM 6.5中触屏优化UI的增强功能的详细信息，请参阅发行说明中的[新增功能](/help/release-notes/release-notes.md#what-s-new)。

完整概述请参阅[触屏UI功能状态](/help/release-notes/touch-ui-features-status.md)页

### 帮助{#resources-to-help}的资源

有关基本操作的背景信息：

* [创作页面](/help/sites-authoring/page-authoring.md).

有关详细的开发信息：

* [触屏优化UI架构](/help/sites-developing/touch-ui-concepts.md)。
* 使用[对话框转换工具](/help/sites-developing/dialog-conversion.md)将组件编辑对话框从经典UI转换为触屏优化UI。

* [触屏优化UI的结构](/help/sites-developing/touch-ui-structure.md)。

* [在触屏优化UI中自定义控制台](/help/sites-developing/customizing-consoles-touch.md) （包括示例代码）。

* [在触屏优化UI中自定义页面创作](/help/sites-developing/customizing-page-authoring-touch.md) （包括示例代码）。

* [AEM Gem会话（针对触屏优化自定义）](https://docs.adobe.com/content/ddc/en/gems/user-interface-customization-for-aem-6.html)。
* [Granite UI文档](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html)。

