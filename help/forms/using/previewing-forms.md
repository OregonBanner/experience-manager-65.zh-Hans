---
title: 预览表单
description: 您可以在发布或激活表单之前预览表单，以确保表单符合预期。 预览选项可能因支持的表单类型而异。
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
feature: Adaptive Forms
exl-id: aed5703e-4fe6-4839-9657-c660ac48521e
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '406'
ht-degree: 15%

---

# 预览表单 {#previewing-a-form}

<span class="preview">Adobe 建议使用现代、可扩展的数据捕获[核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html)，以[创建新的自适应表单](/help/forms/using/create-an-adaptive-form-core-components.md)或[将自适应表单添加到 AEM Sites 页面](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md)。这些组件代表有关创建自适应表单的重大改进，确保实现令人印象深刻的用户体验。本文介绍了使用基础组件创作自适应表单的旧方法。</span>

## 概述 {#overview}

在AEM Forms中，您可以预览存储库中存在的表单和文档。 预览有助于了解表单在发布给最终用户时的具体外观和行为。

在预览表单时，它们会在交互式界面中呈现，用户可以用数据填充表单。 预览文档时，它们以非交互模式呈现，用户只能查看文档。 对于表单，还提供了自定义预览的附加选项。 使用此选项，您可以使用XML文件中的数据预览表单。 数据会填满正在预览的表单的部分或所有字段。

下表列出了适用于不同类型受支持表单的预览选项：

<table>
 <tbody>
  <tr>
   <td><strong>资源类型</strong><br /> </td>
   <td><strong>可用的预览选项</strong><br /> </td>
  </tr>
  <tr>
   <td>文档</td>
   <td>PDF预览</td>
  </tr>
  <tr>
   <td>PDF表单</td>
   <td>使用数据预览和预览PDF<br /> </td>
  </tr>
  <tr>
   <td>自适应表单</td>
   <td>包含数据的HTML预览和HTML预览</td>
  </tr>
  <tr>
   <td>表单模板</td>
   <td>PDF预览、包含数据的PDF预览、HTML预览、包含数据的HTML预览<br /> </td>
  </tr>
 </tbody>
</table>

## 预览表单 {#previewing-a-form-1}

1. 选择要预览的资源，然后单击预览 ![aem6forms_preview](assets/aem6forms_preview.png) （在操作工具栏中）。

   >[!NOTE]
   >
   >要选择资产，请从默认信息卡视图切换到列表视图。 单击 ![aem6forms_viewlist](assets/aem6forms_viewlist.png) 或 ![aem6forms_viewcard](assets/aem6forms_viewcard.png) 以切换视图。

1. 单击预览会列出适用于所选资源类型的可能预览选项。 单击所需选项可在新选项卡中呈现所选资源。

   您的选项包括：

   * HTML预览
   * 使用数据预览
   * PDF预览（适用于表单模板）

## 使用数据预览 {#preview-with-data}

当您选择时 **使用数据预览**，您可以查看输入真实数据的表单的外观。 使用数据预览选项允许您上传包含示例用户数据的XML。 示例用户数据用于以您选择的格式填充预览表单。

1. 选择资源，单击预览 ![aem6forms_preview](assets/aem6forms_preview.png)，并选择 **使用数据预览**.
1. 在“预览表单”对话框中，将FormData作为XML文件提供。 单击预览以使用XML中的合并数据呈现表单。
