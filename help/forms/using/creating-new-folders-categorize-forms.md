---
title: 创建新文件夹以对表单进行分类
seo-title: 创建新文件夹以对表单进行分类
description: 使用文件夹组织表单模板、PDF、资源和自适应表单。
seo-description: 使用文件夹组织表单模板、PDF、资源和自适应表单。
uuid: 63fcb807-c9cf-49ae-ad69-6b1187543470
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-manager
discoiquuid: 2a8f4380-8d0f-4354-b2da-4e0c02a545e3
role: Admin
exl-id: f8af1ac3-6a95-4f91-8979-6b41a7e02ca4
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '411'
ht-degree: 0%

---

# 创建新文件夹以对表单进行分类 {#create-new-folders-to-categorize-forms}

您可以使用文件夹更好地组织资产。 由于AEM Forms支持多种类型的资产（表单模板、PDF、文档、资源和自适应表单，以及各种元数据），因此您可以使用文件夹根据所需的条件对表单进行分类。

AEM Forms允许您更改文件夹的标题。 标题与存储库中存储文件夹的节点名称不同。 标题而是作为文件夹的元数据进行维护。 如果更改文件夹的标题，则文件夹内存在的任何资产的路径都不会受到影响。

## 创建文件夹 {#create-a-folder}

您可以通过以下方式之一在AEM Forms中创建文件夹：

* 上传包含所需文件夹结构中资产的ZIP文件(请参阅[在AEM Forms中获取XDP和PDF文档](/help/forms/using/get-xdp-pdf-documents-aem.md))

* 创建新的空文件夹

1. 登录到位于`https://<server>:<port>/aem/forms.html`的AEM Forms用户界面。
1. 导航到要创建文件夹的位置。
1. 单击工具栏中的![aem6forms_add](assets/aem6forms_add.png)图标，然后选择&#x200B;**[!UICONTROL 创建文件夹]**。

1. 输入以下详细信息：

   * **标题：** 文件夹的显示名称
   * **名称：** *（必需）* 要在存储库中存储文件夹的节点名称

   >[!NOTE]
   >
   >默认情况下，会从标题中自动填充name字段的值。 名称只能包含字母数字字符，或连字符(-)和下划线(_)特殊字符。 在标题中输入的任何其他特殊字符会自动替换为连字符，系统会提示您确认新名称。 您可以选择继续使用建议的名称，也可以进一步对其进行编辑。

1. 单击&#x200B;**[!UICONTROL Submit]。**

   资产列表中的当前位置将显示一个新文件夹，其中包含您定义的标题。

   如果存在具有指定名称的文件夹，则提交会失败，并出现错误。 您可以通过将鼠标悬停在名称字段旁边显示的错误![aem6forms_error_alert](assets/aem6forms_error_alert.png)图标上来查看错误消息。

### 编辑文件夹标题 {#edit-the-folder-title-br}

1. 选择要编辑其标题的文件夹。
1. 单击工具栏中的编辑![aem6forms_edit](assets/aem6forms_edit.png)图标。
1. 输入新标题。 文本字段已预填充文件夹标题的当前值。 您可以将其更改为新值。
1. 单击&#x200B;**[!UICONTROL Submit]。**
