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
feature: 移动设备表单
exl-id: 68912260-179a-4d1b-b944-0a1777c021ac
source-git-commit: 6e2a0f053a1f6989524e9ae2b1dcb001b0397ac6
workflow-type: tm+mt
source-wordcount: '353'
ht-degree: 1%

---

# 为HTML5表单启用附件 {#enabling-attachments-for-an-html-form}

您可以上传、预览和提交带有HTML5表单的附件。 默认情况下，附件支持处于禁用状态。 要启用附件支持，请执行以下操作：

1. 创建具有`mfAttachmentOptions`多选字符串属性的[自定义配置文件](/help/forms/using/custom-profile.md)。 `mfAttachmentOptions`属性中的每个字符串都必须具有`property=value`格式，才能配置文件附件小组件的选项。 `property`和`value`可以具有以下任意值：

   | 属性 | 值 |
   |--- |---|
   | multiSelect | true或false（默认为true） |
   | fileSizeLimit | 以MB为单位的数量（默认为2 MB）。 例如，5. |
   | buttonText | 弹出窗口的按钮文本（默认情况下为“附加”） |
   | 接受 | 要接受的文件类型列表（默认情况下为“audio/&amp;ast;, video/&amp;ast;, image/&amp;ast;, text/&amp;ast;, .pdf”）（以逗号分隔） |

   例如：

   ![配置选项](assets/mfAttachmentOptions.png)

   您还可以根据需要为`mfAttachmentOptions`属性指定更多自定义选项。

   >[!NOTE]
   >
   >在Microsoft Internet Explorer 9中，用户可以附加超过指定限制的文件。 这是一个已知问题。

1. 使用[元数据编辑器](/help/forms/using/manage-form-metadata.md)选择您上面为HTML 5表单创建的自定义配置文件。
1. 使用自定义配置文件渲染表单模板，附件图标将显示在表单工具栏上。

   >[!NOTE]
   >
   >Forms Portal开箱即用地提供启用了草稿和附件功能的自定义配置文件。 有关&#x200B;**另存为草稿**&#x200B;配置文件的更多信息，请参阅[将HTML5表单另存为草稿](/help/forms/using/saving-html5-form-draft.md)。

1. 单击附件图标，将出现附件选择对话框。 浏览并选择附件，然后单击&#x200B;**Attach**。

   >[!NOTE]
   >
   >要预览附件，请单击附件名称。

   >[!NOTE]
   >
   >匿名用户无法使用文件预览选项。

## 附件提交格式 {#attachment-submission-format}

启用附件后，HTML5表单会提交多部分数据。 多部分提交数据包含两部分：**dataXml**&#x200B;和&#x200B;**附件**。

>[!NOTE]
>
>为了向后兼容，如果`mfAllowAttachments`选项处于关闭状态，则HTML5表单不会发送多部分数据。 它以&#x200B;**application/xml**&#x200B;格式发送简单数据xml。

如果mfAllowAttachments标志处于打开状态，则[submit service proxy service](/help/forms/using/service-proxy.md)还会使用dataXml和附件发布多部分数据。
