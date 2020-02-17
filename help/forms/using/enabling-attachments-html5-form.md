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

---


# 为HTML5表单启用附件 {#enabling-attachments-for-an-html-form}

您可以上传、预览和提交带有HTML5表单的附件。 默认情况下，附件支持处于禁用状态。 要启用附件支持，请执行以下操作：

1. 使用多选字 [符串属性创建自定](/help/forms/using/custom-profile.md) 义配置文件 `mfAttachmentOptions`。
1. 在自定义配置文件中，指 `fileSizeLimit`定属 `multiSelect`性、 `buttonTex`属性和t以配置文件附件构件的选项。 根据需要，您还可以指定更多自定义属性。

1. 在自定义配置文件中，使用以下配置：

   * **multiSelect** -> true或false（默认为true）
   * **fileSizeLimit** -> value_in_mb（例如5）（默认为2 MB）
   * **buttonText** ->弹出窗口的按钮文本（默认情况下为“附加”）
   * **accept** ->文件类型接受（默认情况下为“audio/&amp;ast;, video/&amp;ast;, image/&amp;ast;, text/&amp;ast;, .pdf”）
   >[!NOTE]
   >
   >在Microsoft Internet Explorer 9中，用户可以附加大于指定限制的文件。 这是一个已知问题。

1. 使用元 [数据编辑器](/help/forms/using/manage-form-metadata.md) ，选择您为HTML 5表单在上面创建的自定义配置文件。
1. 使用自定义配置文件渲染您的表单模板，附件图标将显示在表单工具栏上。

   >[!NOTE]
   >
   >开箱即用的表单门户提供了一个自定义配置文件，并启用了草稿和附件功能。 有关另存为草稿配 **置文件的详细信息** ，请参阅 [将HTML5表单另存为草稿](/help/forms/using/saving-html5-form-draft.md)。

1. 单击附件图标，将显示附件选择对话框。 浏览并选择附件，然后单击“附 **加”**。

   >[!NOTE]
   >
   >要预览附件，请单击附件名称。

   >[!NOTE]
   >
   >匿名用户无法使用文件预览选项。

## 附件提交格式 {#attachment-submission-format}

启用附件后，HTML5表单会提交多部件数据。 多部分提交数据具有两部分 **dataXml** 和 **附件**。

>[!NOTE]
>
>为了向后兼容， `mfAllowAttachments` 如果关闭此选项，则HTML5表单不会发送多部分数据。 它以application/xml格式发送 **简单的数据xml** 。

如果mfAllowAttachments标志打开，则提交服务代理服 [务也会发布包含dataXml和附件的多部分数据](/help/forms/using/service-proxy.md) 。
