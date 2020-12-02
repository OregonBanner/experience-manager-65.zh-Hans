---
title: 预览表单
seo-title: 预览表单
description: 您可以在发布或激活表单之前对其进行预览，以确保其达到预期。 预览选项可能因支持的表单类型而异。
seo-description: 您可以在发布或激活表单之前对其进行预览，以确保其达到预期。 预览选项可能因支持的表单类型而异。
uuid: 9ec359ea-f518-441c-9c3d-e3c1ea07a532
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 377d804d-4a75-4c93-8125-d2660cf56418
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '392'
ht-degree: 2%

---


# 预览表单{#previewing-a-form}

## 概述 {#overview}

在AEM Forms，您可以预览存储库中存在的表单和文档。 预览有助于准确了解表单在发布给最终用户时的外观和行为。

预览表单时，表单会以交互式界面呈现，用户可以用数据填写表单。 预览文档时，这些文档以非交互模式呈现，用户只能视图。 对于表单，还提供“自定义预览”的其他选项。 使用此选项，您可以使用XML文件中的数据预览表单。 数据会填充正在预览的表单的部分或全部字段。

下表列表了针对不同类型受支持表单的可用预览选项：

<table>
 <tbody>
  <tr>
   <td><strong>资产类型</strong><br /> </td>
   <td><strong>可用预览选项</strong><br /> </td>
  </tr>
  <tr>
   <td>文档</td>
   <td>PDF预览</td>
  </tr>
  <tr>
   <td>PDF表单</td>
   <td>PDF预览和预览（使用数据<br />） </td>
  </tr>
  <tr>
   <td>自适应表单</td>
   <td>HTML预览和HTML预览（含数据）</td>
  </tr>
  <tr>
   <td>表单模板</td>
   <td>PDF预览、带数据的PDF预览、HTML预览、带数据的HTML预览<br /> </td>
  </tr>
 </tbody>
</table>

## 预览表单{#previewing-a-form-1}

1. 选择要预览的资产，然后单击操作工具栏中的预览![aem6forms_预览](assets/aem6forms_preview.png)。

   >[!NOTE]
   >
   >要选择资产，请从默认的卡列表切换到视图视图。 单击![aem6forms_viewlist](assets/aem6forms_viewlist.png)或![aem6forms_viewcard](assets/aem6forms_viewcard.png)切换视图。

1. 单击预览列表可显示适用于选定资产类型的可能预览选项。 单击所需的选项，以在新选项卡中呈现选定的资产。

   您的选择包括：

   * 预览为HTML
   * 使用数据预览
   * 预览为PDF（可用于表单模板）

## 使用数据预览 {#preview-with-data}

当您选择&#x200B;**带数据的预览**&#x200B;时，您可以看到表单中输入的实际数据的外观。 预览“数据”选项允许您上传包含示例用户数据的XML。 示例用户数据用于以您选择的格式填充预览表单。

1. 选择资产，单击预览![aem6forms_预览](assets/aem6forms_preview.png)，然后选择预览&#x200B;**数据**。
1. 在“预览表单”对话框中，将FormData作为XML文件提供。 单击“预览”以使用XML中的合并数据呈现表单。

