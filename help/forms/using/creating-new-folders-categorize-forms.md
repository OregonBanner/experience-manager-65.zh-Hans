---
title: 创建新文件夹以对表单分类
seo-title: 创建新文件夹以对表单分类
description: 使用文件夹组织表单模板、PDF、资源和自适应表单。
seo-description: 使用文件夹组织表单模板、PDF、资源和自适应表单。
uuid: 63fcb807-c9cf-49ae-ad69-6b1187543470
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-manager
discoiquuid: 2a8f4380-8d0f-4354-b2da-4e0c02a545e3
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 创建新文件夹以对表单分类 {#create-new-folders-to-categorize-forms}

您可以使用文件夹更好地组织资产。 由于AEM Forms支持多种类型的资产（表单模板、PDF、文档、资源和自适应表单以及各种元数据），因此，您可以使用文件夹根据所需的条件对表单进行分类。

AEM Forms允许您更改文件夹的标题。 标题与存储库中存储文件夹的节点的名称不同。 而是将标题作为文件夹的元数据进行维护。 如果更改文件夹的标题，则文件夹内存在的任何资产的路径均不受影响。

## 创建文件夹 {#create-a-folder}

您可以通过以下方式之一在AEM Forms中创建文件夹：

* 上传包含所需文件夹结构中的资产的ZIP文件(请参 [阅在AEM Forms中获取XDP和PDF文档](/help/forms/using/get-xdp-pdf-documents-aem.md))

* 创建新的空文件夹

1. 登录到AEM Forms用户界面（位于） `https://<server>:<port>/aem/forms.html`。
1. 导览至要创建文件夹的位置。
1. 单击工 ![具栏中的aem6forms_add](assets/aem6forms_add.png) 图标，然后选择创建 **[!UICONTROL 文件夹]**。

1. 输入以下详细信息：

   * **** 标题：显示文件夹的名称
   * **** 名称：(必 *需)* ，要将文件夹存储在存储库中的节点名称
   >[!NOTE]
   >
   >默认情况下，名称字段的值会从标题中自动填充。 名称只能包含字母数字字符或连字符(-)和下划线(_)特殊字符。 在标题中输入的任何其他特殊字符将自动替换为连字符，并提示您确认新名称。 您可以选择继续使用建议的名称或进一步编辑它。

1. 单击 **[!UICONTROL 提交]。**

   资产列表中的当前位置会显示包含您定义的标题的新文件夹。

   如果存在具有指定名称的文件夹，则提交失败并显示错误。 通过将鼠标悬停在名称字段旁边显示的 ![](assets/aem6forms_error_alert.png) aem6forms_error_alert图标上，可以查看错误消息。

### 编辑文件夹标题 {#edit-the-folder-title-br}

1. 选择要编辑其标题的文件夹。
1. 单击工具 ![栏中的编辑aem6forms_edit](assets/aem6forms_edit.png) 图标。
1. 输入新标题。 文本字段会预填充文件夹标题的当前值。 您可以将其更改为新值。
1. 单击 **[!UICONTROL 提交]。**

