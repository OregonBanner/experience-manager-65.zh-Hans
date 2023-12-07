---
title: 重用自适应表单
description: 您可以重用现有的自适应表单来创建新的自适应表单。
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
feature: Adaptive Forms
exl-id: d8ee4e82-3137-430e-aa47-b00191f2729c
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '593'
ht-degree: 11%

---

# 重用自适应表单 {#reusing-adaptive-forms}

<span class="preview">Adobe 建议使用现代、可扩展的数据捕获[核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html)，以[创建新的自适应表单](/help/forms/using/create-an-adaptive-form-core-components.md)或[将自适应表单添加到 AEM Sites 页面](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md)。这些组件代表有关创建自适应表单的重大改进，确保实现令人印象深刻的用户体验。本文介绍了使用基础组件创作自适应表单的旧方法。</span>

| 版本 | 文章链接 |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/manage-metadata/reusing-adaptive-forms.html) |
| AEM 6.5 | 本文 |

## 简介 {#introduction}

如果要使用现有自适应表单的某些属性来生成新表单，则只需使用复制粘贴功能即可。 此外，还可将新的自适应表单粘贴到所需的文件夹路径中。 将复制所有元数据属性，并复制基于XFA和XSD的自适应表单的XFA和XSD。

>[!NOTE]
>
>不会复制状态和审阅详细信息。 例如，如果自适应表单已发布，然后您复制该表单，则粘贴的自适应表单将处于未发布状态。 同样，如果复制的资产正在审核中，则粘贴的资产不在同一审核中。

### 复制自适应表单 {#copy-an-adaptive-form}

使用以下任一方法复制自适应表单：

1. 单击复制 ![aem6forms_copy](assets/aem6forms_copy.png) 图标（位于快速操作中）。

   >[!NOTE]
   >
   >快速操作是在鼠标悬停时显示在缩略图上的操作项。

1. 选择自适应表单。 不同视图的选择过程不同。

   如果您在卡片视图中，则单击选定内容以转到选择模式 ![aem6forms_check-circle](assets/aem6forms_check-circle.png) 图标，然后单击要复制的所有自适应表单。

   如果您在列表视图中，请单击所有自适应表单的复选框以将其选中。

   >[!NOTE]
   >
   >所有选定的资源都必须是自适应表单，因为仅自适应表单支持复制粘贴功能，并且所有选定的资源都必须存在于同一文件夹中。

   选择资源后，单击副本 ![aem6forms_copy](assets/aem6forms_copy.png) 工具栏中显示的图标以复制选定的自适应表单。

### 粘贴自适应表单 {#paste-an-adaptive-form}

单击复制操作将自动退出选择模式并进行粘贴 ![aem6forms_paste](assets/aem6forms_paste.png) 图标可见。 现在，转到所需的文件夹路径并单击粘贴 ![aem6forms_paste](assets/aem6forms_paste.png) 图标以粘贴复制的自适应表单。

如果在同一文件夹中粘贴或此目标文件夹中存在具有相同节点名称（存储在CRX存储库中）的其他文件，则会在后缀中附加1(例如，myaf变为myaf1，如果myaf1存在于同一位置，则myaf变为myaf2。 所有其他属性仍保持与原始自适应表单相同。

单击粘贴后 ![aem6forms_paste](assets/aem6forms_paste.png) 图标，则它会再次隐藏。 同时，您只能粘贴一次。 要再次创建同一资产的副本，请再次复制该副本。

### 更改新自适应表单的内容 {#change-contents-of-new-adaptive-form}

可以使用以下方法更改粘贴的自适应表单的内容，使其与复制的表单不同：

1. **更改元数据属性：**

   您可以更改自适应表单的元数据属性，例如标题和描述。 有关元数据属性及其更改方式的更多详细信息，请参阅 [管理表单元数据](/help/forms/using/manage-form-metadata.md)

1. **为基于XFA/XSD的自适应Forms更改XFA/XSD：**

   您可以更改自适应表单中使用的XFA/XSD。 要了解如何更改这些自适应表单，请参阅 [管理表单元数据](/help/forms/using/manage-form-metadata.md)

1. **重新发布：**

   粘贴的资产与复制的资产不同。 您可以将其发布为新资源，以供最终用户使用。 要了解如何发布资源，请参阅 [发布和取消发布表单](/help/forms/using/publishing-unpublishing-forms.md)
