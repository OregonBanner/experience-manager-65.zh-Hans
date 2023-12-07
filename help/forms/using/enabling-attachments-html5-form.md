---
title: 为HTML5表单启用附件
description: 默认情况下，禁用HTML5表单的附件支持。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
feature: Mobile Forms
exl-id: 68912260-179a-4d1b-b944-0a1777c021ac
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '339'
ht-degree: 1%

---

# 为HTML5表单启用附件 {#enabling-attachments-for-an-html-form}

您可以通过HTML5表单上传、预览和提交附件。 默认情况下，附件支持处于禁用状态。 要启用附件支持：

1. 创建 [自定义配置文件](/help/forms/using/custom-profile.md) 带有 `mfAttachmentOptions` 多选字符串属性。 中的每个字符串 `mfAttachmentOptions` 属性必须具有 `property=value` 用于配置文件附件小部件的选项的格式。 此 `property` 和 `value` 可以具有以下任一值：

   | 属性 | 价值 |
   |--- |---|
   | multiSelect | true或false（默认为true） |
   | fileSizeLimit | 以MB为单位的数字（默认为2 MB）。 例如，5。 |
   | 按钮文本 | 弹出窗口的按钮文本（默认为“附加”） |
   | 接受 | 要接受的文件类型的逗号分隔列表（默认为“audio/&amp;ast；， video/&amp;ast；， image/&amp;ast；， text/&amp;ast；， .pdf”） |

   例如：

   ![配置选项](assets/mfAttachmentOptions.png)

   根据需要，您还可以为以下对象指定更多自定义选项 `mfAttachmentOptions` 属性。

   >[!NOTE]
   >
   >在Microsoft Internet Explorer 9中，用户可以附加大于指定限制的文件。 这是一个已知问题。

1. 使用 [元数据编辑器](/help/forms/using/manage-form-metadata.md) 选择您在上面为HTML5表单创建的自定义配置文件。
1. 使用自定义配置文件呈现表单模板，表单工具栏上会显示附件图标。

   >[!NOTE]
   >
   >Forms Portal开箱即用地提供启用了草稿和附件功能的自定义配置文件。 欲知关于 **另存为草稿** 配置文件，请参阅 [将HTML5表单另存为草稿](/help/forms/using/saving-html5-form-draft.md).

1. 单击附件图标，将出现一个附件选择对话框。 浏览并选择附件，然后单击 **附加**.

   >[!NOTE]
   >
   >要预览附件，请单击附件名称。

   >[!NOTE]
   >
   >文件预览选项不适用于匿名用户。

## 附件提交格式 {#attachment-submission-format}

启用附件后，HTML5表单提交多部分数据。 多部分提交数据包括两部分 **dataXml** 和 **附件**.

>[!NOTE]
>
>要获得向后兼容性，如果 `mfAllowAttachments` 选项已关闭，则HTML5表单不会发送多部分数据。 它发送简单数据xml于 **application/xml** 格式。

如果mfAllowAttachments标志处于打开状态， [提交服务代理服务](/help/forms/using/service-proxy.md) 此外，还会发布包含dataXml和附件的多部分数据。
