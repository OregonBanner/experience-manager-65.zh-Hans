---
title: 创建新文件夹以对表单进行分类
seo-title: Create new folders to categorize forms
description: 使用文件夹整理表单模板、PDF、资源和自适应表单。
seo-description: Use folders to organize your form templates, PDFs, resources, and adaptive forms.
uuid: 63fcb807-c9cf-49ae-ad69-6b1187543470
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-manager
discoiquuid: 2a8f4380-8d0f-4354-b2da-4e0c02a545e3
role: Admin
exl-id: f8af1ac3-6a95-4f91-8979-6b41a7e02ca4
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '392'
ht-degree: 1%

---

# 创建新文件夹以对表单进行分类 {#create-new-folders-to-categorize-forms}

您可以使用文件夹更好地组织资源。 由于AEM Forms支持多种类型的资源(表单模板、PDF、文档、资源和自适应表单以及各种元数据)，因此您可以使用文件夹根据所需的标准对表单进行分类。

AEM Forms允许您更改文件夹的标题。 标题与存储库中存储文件夹的节点名称不同。 相反，标题将保留为文件夹的元数据。 如果更改文件夹的标题，则该文件夹中存在的任何资源的路径都不会受到影响。

## 创建文件夹 {#create-a-folder}

您可以通过以下方式之一在AEM Forms中创建文件夹：

* 上传包含所需文件夹结构中的资产的ZIP文件(请参阅 [在AEM Forms中获取XDP和PDF文档](/help/forms/using/get-xdp-pdf-documents-aem.md))

* 创建空文件夹

1. 登录到AEM Forms用户界面，网址为 `https://<server>:<port>/aem/forms.html`.
1. 导航到要创建文件夹的位置。
1. 单击 ![aem6forms_add](assets/aem6forms_add.png) 图标，然后选择 **[!UICONTROL 创建文件夹]**.

1. 输入以下详细信息：

   * **标题：** 文件夹的显示名称
   * **名称：** *（必需）* 要在存储库中存储文件夹的节点名称

   >[!NOTE]
   >
   >默认情况下，“名称”字段的值会自动从标题中填充。 名称只能包含字母数字字符，或连字符(-)和下划线(_)特殊字符。 在标题中输入的任何其他特殊字符都会自动替换为连字符，并提示您确认新名称。 您可以选择使用建议的名称继续操作或进一步编辑它。

1. 单击&#x200B;**[!UICONTROL “提交”。]**

   具有您定义的标题的新文件夹将显示在资产列表中的当前位置。

   如果存在具有指定名称的文件夹，则提交会失败并出现错误。 您可以通过将鼠标悬停在错误上来查看错误消息 ![aem6forms_error_alert](assets/aem6forms_error_alert.png) 显示在“名称”字段旁边的图标。

### 编辑文件夹标题 {#edit-the-folder-title-br}

1. 选择要编辑其标题的文件夹。
1. 单击编辑 ![aem6forms_edit](assets/aem6forms_edit.png) 图标。
1. 输入新标题。 该文本字段已预填充为文件夹标题的当前值。 您可以将其更改为新值。
1. 单击&#x200B;**[!UICONTROL “提交”。]**
