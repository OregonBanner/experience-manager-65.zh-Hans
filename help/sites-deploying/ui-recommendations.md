---
title: 客户的Recommendations用户界面
description: 与经典用户界面和触屏优化用户界面相关的推荐列表。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
docset: aem65
exl-id: 7b71119a-ff58-47c0-aeef-a705ed8c40e0
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '788'
ht-degree: 0%

---

# 客户的Recommendations用户界面{#user-interface-recommendations-for-customers}

Adobe Experience Manager附带两个UI — 统一的Experience CloudUI（也称为触屏UI）和经典UI。

本文档旨在指导客户根据自己的情况选择要使用的UI。

利息条款：

* **UI（或标准UI）**
在5.6.0中引入的现代用户界面作为技术预览版，并在后续版本中进行了扩展。 它基于Adobe Experience Cloud的统一用户体验，以前称为触屏UI或触屏UI。

* **经典UI**
基于ExtJS技术的用户界面，该界面在2008年随CQ 5.1引入。

* **网站管理员**
用于管理站点层次结构（移动、激活、托管引用）和创建新页面的功能。

* **页面创作**
用于添加/编辑页面内容的功能。

* **DAM/Assets管理员**
用于管理数字资产（包括图像、视频、文档和下载）的功能。

* **ContextHub**
用于汇总访客相关信息并将其用于各种目的的功能。 提供一个用户界面来模拟访问站点的人。 从AEM 6.2开始，ContextHub取代了以前的技术Client Context。

## 常规 {#general}

在过去几年中，Adobe使用统一的用户界面更新了所有Adobe Experience Cloud解决方案。 整个Experience Cloud解决方案的用户都可以在如何使用和操作应用程序方面享受到一致的体验，这些模式都是通用的。 在每个版本中，Adobe都根据客户在各种解决方案中提供的反馈来优化其用户界面。

Adobe Experience Manager（以前称为CQ5）的原始用户界面，在2008年引入，供运行版本5.0-5.6.1的客户使用，现在位于AEM 6.5中。这可保证客户可以更新到6.5版本，并受益于具有新功能的更新平台，同时继续使用相同的用户界面。

Adobe建议客户计划在2018/19年度切换到新UI。 这可以在更新6.5期间完成，也可以在更新后的单独项目中完成，包括对自定义项和组件对话框所做的必要调整。

经典UI已在AEM 6.4中弃用，Adobe不打算进一步增强经典UI。 请注意，经典UI在被弃用时仍完全受支持。

### Rules和Recommendations {#rules-and-recommendations}

以下是Adobe Experience Manager 6.5产品管理中的推荐列表：

<table>
 <tbody>
  <tr>
   <th>我的项目……</th>
   <th>推荐</th>
  </tr>
  <tr>
   <td>刚刚开始使用Adobe Experience Manager。</td>
   <td>使用默认UI。</td>
  </tr>
  <tr>
   <td><p>已使用AEM一段时间。</p> <p>使用了现成的产品UI，并为站点开发了自定义组件。<br /> </p> </td>
   <td>
    <ol>
     <li>更新至6.5</li>
     <li>使用默认UI进行站点管理、资产等。 等等。<br /> </li>
     <li>配置“编辑页面”操作以打开经典UI页面编辑器。 请参阅 <a href="#selecting-your-ui">选择您的UI</a>.</li>
    </ol> <p>然后，在第二阶段：</p>
    <ol>
     <li>更新组件对话框以使用Coral 3对话框格式。 Adobe建议使用 <a href="/help/sites-developing/modernization-tools.md">AEM现代化工具</a> 以更新组件。</li>
    </ol> </td>
  </tr>
  <tr>
   <td>已构建一个使用ClientContext与集成的站点。<br /> </td>
   <td>
    <ol>
     <li>更新至6.5</li>
     <li>使用默认UI进行站点管理、资产等。 以此类推。</li>
     <li>配置“编辑页面”操作以打开经典UI页面编辑器。 请参阅 <a href="#selecting-your-ui">选择您的UI</a>.</li>
    </ol> <p>然后，在第二阶段：</p>
    <ol>
     <li>更新组件对话框以使用Coral 3对话框格式。 Adobe建议使用 <a href="/help/sites-developing/modernization-tools.md">AEM现代化工具</a> 以更新组件。</li>
     <li>配置ContextHub(ClientContext的替代项)并更新页面模板以使用ContextHub。 ContextHub具有允许加载自定义ClientContext存储的兼容模式。</li>
    </ol> </td>
  </tr>
  <tr>
   <td><p>已使用CQ/AEM多年。</p> <p>扩展了产品UI（例如站点管理员），并构建了具有大量编辑对话框的组件。</p> </td>
   <td><p>更新至6.5并将经典UI配置为所有用户的页面创作的默认用户界面。 请参阅 <a href="#selecting-your-ui">选择您的UI</a>.</p> <p>然后，启动一个项目以应用自定义并优化Coral 3格式的组件对话框。 请参阅 <a href="#resources-to-help">需要帮助的资源</a>.<br /> </p> </td>
  </tr>
 </tbody>
</table>

### 常见问题 {#faq}

请参阅知识库文章， [触控UI创作常见问题解答](https://helpx.adobe.com/experience-manager/kb/index/touchui_faq.html)，以了解详细信息；包括有关经典UI弃用计划的任何信息。

### 选择您的UI {#selecting-your-ui}

请参阅 [选择您的UI](/help/sites-authoring/select-ui.md) 有关根据需要配置系统的信息。

### 触屏优化UI状态 {#touch-enabled-ui-status}

有关AEM 6.5中针对触屏UI所做的增强功能的详细信息，请参阅 [新增功能](/help/release-notes/release-notes.md#what-s-new) 在发行说明中。

完整的概述，请参见 [触屏UI功能状态](/help/release-notes/touch-ui-features-status.md) 页面

### 需要帮助的资源 {#resources-to-help}

有关基本处理的背景信息：

* [创作页面](/help/sites-authoring/page-authoring.md).

有关详细开发信息：

* [触屏优化UI架构](/help/sites-developing/touch-ui-concepts.md).
* 使用 [AEM现代化工具](/help/sites-developing/modernization-tools.md) 将组件“编辑”对话框从经典UI转换为触控式UI。

* [触屏优化UI的结构](/help/sites-developing/touch-ui-structure.md).

* [在触屏UI中自定义控制台](/help/sites-developing/customizing-consoles-touch.md) （包括示例代码）。

* [在触屏UI中自定义页面创作](/help/sites-developing/customizing-page-authoring-touch.md) （包括示例代码）。

* [Granite UI文档](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html).
