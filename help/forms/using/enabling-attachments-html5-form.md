---
title: 为HTML5表单启用附件
seo-title: 为HTML5表单启用附件
description: 默认情况下，HTML5表单的附件支持处于禁用状态。
seo-description: 默认情况下，HTML5表单的附件支持处于禁用状态。
uuid: 2c62ac3e-4b27-46c7-a61d-a805fb5d26fb
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 8eebfcd6-0597-44ed-b718-bf9a1baa6c12
translation-type: tm+mt
source-git-commit: 00e14be8a0775149b3ee7ce8cd781dd7f1e49e4f
workflow-type: tm+mt
source-wordcount: '335'
ht-degree: 0%

---


# 为HTML5表单{#enabling-attachments-for-an-html-form}启用附件

您可以上传、预览和提交带有HTML5表单的附件。 默认情况下，附件支持处于禁用状态。 要启用附件支持，请执行以下操作：

1. 创建具有多选字符串属性`mfAttachmentOptions`的[自定义用户档案](/help/forms/using/custom-profile.md)。
1. 在自定义用户档案中，指定属性`fileSizeLimit`、`multiSelect`和`buttonTex`t以配置文件附件构件的选项。 根据需要，还可以指定更多自定义属性。

1. 在自定义用户档案中，使用以下配置：

   * **multiSelect** -> true或false（默认为true）
   * **fileSizeLimit** -> value_in_mb（例如5）（默认为2 MB）
   * **buttonText** ->弹出窗口的按钮文本（默认情况下为“附加”）
   * **accept** ->文件类型接受（默认情况下为“audio/&amp;ast;、video/&amp;ast;、image/&amp;ast;、text/&amp;ast;、.pdf”）

   >[!NOTE]
   >
   >在Microsoft Internet Explorer 9中，用户可以附加大于指定限制的文件。 这是一个已知问题。

1. 使用[元数据编辑器](/help/forms/using/manage-form-metadata.md)选择您在上面为HTML 5表单创建的自定义用户档案。
1. 使用自定义用户档案渲染表单模板，附件图标将显示在表单工具栏上。

   >[!NOTE]
   >
   >开箱即用的表单门户提供启用了草稿和附件功能的自定义用户档案。 有关&#x200B;**另存为草稿**&#x200B;用户档案的详细信息，请参阅[将HTML5表单另存为草稿](/help/forms/using/saving-html5-form-draft.md)。

1. 单击附件图标，将显示附件选择对话框。 浏览并选择附件，然后单击&#x200B;**连接**。

   >[!NOTE]
   >
   >要预览附件，请单击附件名称。

   >[!NOTE]
   >
   >匿名用户不能使用文件预览选项。

## 附件提交格式{#attachment-submission-format}

启用附件后，HTML5表单将提交多部件数据。 多部分提交数据具有两部分&#x200B;**dataXml**&#x200B;和&#x200B;**附件**。

>[!NOTE]
>
>为了向后兼容，如果`mfAllowAttachments`选项关闭，则HTML5表单不会发送多部件数据。 它以&#x200B;**application/xml**&#x200B;格式发送简单数据xml。

如果mfAllowAttachments标志处于打开状态，[submit service proxy service](/help/forms/using/service-proxy.md)还会发布包含dataXml和附件的多部件数据。
