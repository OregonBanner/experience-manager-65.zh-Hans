---
title: 重用自适应表单
seo-title: 重用自适应表单
description: 您可以重复使用现有的自适应表单来创建新的自适应表单。
seo-description: 您可以重复使用现有的自适应表单来创建新的自适应表单。
uuid: f1d0fb70-e255-4dd9-8e6d-fd65eaf2e81a
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: ef564750-f107-41cb-887e-fc6d22b7d32e
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '553'
ht-degree: 0%

---


# 重用自适应表单{#reusing-adaptive-forms}

## 简介 {#introduction}

如果要使用现有自适应表单的某些属性生成新表单，您只需使用复制粘贴功能。 此外，还可以将新的自适应表单粘贴到所需的文件夹路径。 将复制所有元数据属性，并复制基于XFA和XSD的自适应表单的XFA和XSD。

>[!NOTE]
>
>不会复制状态和审阅详细信息。 例如，如果您的自适应表单已发布，然后您复制它，则粘贴的自适应表单将处于未发布状态。 同样，如果复制的资产正在审核中，则粘贴的资产也不在同一审核中。

### 复制自适应表单{#copy-an-adaptive-form}

使用以下任一方法复制自适应表单：

1. 单击“快速操作”中的复制![aem6forms_copy](assets/aem6forms_copy.png)图标。

   >[!NOTE]
   >
   >快速操作是鼠标悬停时在缩略图上显示的操作项。

1. 选择自适应表单。 不同视图的选择过程不同。

   如果您处于卡视图，请通过单击选择![aem6forms_check-circle](assets/aem6forms_check-circle.png)图标进入选择模式，然后单击要复制的所有自适应表单。

   如果您处于列表视图，请单击所有自适应表单的复选框以选择它们。

   >[!NOTE]
   >
   >所有选定的资产都必须是自适应表单，因为仅自适应表单支持复制粘贴功能，并且所有选定的资产都必须位于同一文件夹中。

   选择资产后，单击工具栏中显示的复制![aem6forms_copy](assets/aem6forms_copy.png)图标以复制选定的自适应表单。

### 粘贴自适应表单{#paste-an-adaptive-form}

单击复制操作会自动退出选择模式，并使粘贴![aem6forms_paste](assets/aem6forms_paste.png)图标可见。 现在，转到所需的文件夹路径并单击粘贴![aem6forms_paste](assets/aem6forms_paste.png)图标以粘贴复制的自适应表单。

如果粘贴到同一文件夹中，或者此目标文件夹中存在节点名称相同（存储在CRX存储库中）的其他文件，则1会附加到后缀中(例如，myaf变为myaf1，如果myaf1存在于同一位置，则myaf变为myaf2。 所有其他属性仍与原始自适应表单相同。

单击粘贴![aem6forms_paste](assets/aem6forms_paste.png)图标后，它将再次变为隐藏状态。 一次只能粘贴一次。 要再次创建同一资产的副本，请再次复制。

### 更改新自适应表单{#change-contents-of-new-adaptive-form}的内容

可以使用以下方法更改粘贴的自适应表单的内容，使其与复制的表单不同：

1. **更改元数据属性：**

   您可以更改自适应表单的元数据属性，例如标题和说明。 有关元数据属性及其更改方式的详细信息，请参阅[管理表单元数据](/help/forms/using/manage-form-metadata.md)

1. **为基于XFA/XSD的自适应Forms更改XFA/XSD:**

   您可以更改自适应表单中使用的XFA/XSD。 要了解如何更改这些自适应表单，请参阅[管理表单元数据](/help/forms/using/manage-form-metadata.md)

1. **重新发布:**

   粘贴的资产与复制的资产不同。 您可以将其作为新资产发布，以使其对最终用户可用。 要了解如何发布资产，请参阅[发布和取消发布表单](/help/forms/using/publishing-unpublishing-forms.md)

