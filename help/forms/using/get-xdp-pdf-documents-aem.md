---
title: 在AEM Forms中获取XDP和PDF文档
seo-title: Getting XDP and PDF documents in AEM Forms
description: 通过AEM Forms，可上传要与自适应表单一起使用的表单和支持的资源。 您还可以以ZIP格式批量上传表单和相关资源。
seo-description: AEM Forms lets you upload forms and supported assets to use with adaptive forms. You can also bulk upload forms and related resources as a ZIP.
uuid: cd49b4a8-c282-4059-95a0-c98f6c92ab14
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-manager
discoiquuid: 28b9f1d6-6a52-458f-a8ed-a206502eda0d
docset: aem65
role: Admin
exl-id: 9ecdc50a-31e3-46ae-948a-d1f6e6085734
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '671'
ht-degree: 0%

---

# 在AEM Forms中获取XDP和PDF文档{#getting-xdp-and-pdf-documents-in-aem-forms}

## 概述 {#overview}

通过将中的上传到AEM Forms，您可以将表单从本地文件系统导入CRX存储库。 以下资源类型支持上传操作：

* 表单模板（XFA表单）
* PDF forms
* 单据(平面PDF单据)

您可以单独上传支持的资源类型，也可以以ZIP存档的形式上传。 您可以上传以下类型的资产： `Resource`，仅与ZIP存档中的XFA表单一起提供。

>[!NOTE]
>
>确保您是 `form-power-users` 组才能上传XDP文件。 请与管理员联系以成为组的成员。

## 正在上传表单 {#uploading-forms}

1. 通过访问登录到AEM Forms用户界面 `https://'[server]:[port]'/aem/forms.html`.
1. 导航到要在其中上传表单的文件夹或包含表单的文件夹。
1. 在操作工具栏中，点按 **“创建”>“文件上传”**.

   ![创建下的本地存储中的文件选项](assets/step.png)

1. 上传表单或包对话框允许您浏览并选择要上传的文件。 文件浏览器仅显示支持的文件格式(ZIP、XDP和PDF)。

   >[!NOTE]
   >
   >文件名只能包含字母数字字符、连字符或下划线。

1. 选择文件后单击“上传”可上传文件，或单击“取消”可取消上传。 弹出窗口会列出在当前位置添加的资源和更新的资源。

   >[!NOTE]
   >
   >对于ZIP文件，将显示所有受支持资源的相对路径。 ZIP文件中不受支持的资源将被忽略并且不会列出。 但是，如果ZIP存档仅包含不支持的资源，则会显示错误消息，而不是弹出对话框。

   ![上传XFA表单时的“上传”对话框](assets/upload-scr.png)

1. 如果一个或多个资源的文件名无效，则会显示错误。 更正以红色突出显示的文件名并重新上传。

   ![上传XFA表单时出现错误消息](assets/upload-scr-err.png)

上传完成后，后台工作流会根据资源的预览为每个资源生成缩略图。 较新版本的资源（如果上传）会覆盖现有资源。

### 保护模式 {#protected-mode}

AEM Forms服务器允许您运行JavaScript代码。 恶意JavaScript代码可能会损害AEM Forms环境。 保护模式限制AEM Forms仅从受信任的资产和位置运行XDP文件。 AEM Forms UI中可用的所有XDP都被视为受信任的资产。

默认情况下，保护模式处于打开状态。 如有必要，您可以禁用保护模式：

1. 以管理员身份登录到AEM Web Console。 URL为https://&#39;[服务器]：[端口]&#39;/system/console/configMgr
1. 打开Mobile Forms配置以进行编辑。
1. 取消选择“保护模式”选项，然后单击 **保存**. 已禁用保护模式。

## 更新引用的XFA表单 {#updating-referenced-xfa-forms}

在AEM Forms中，XFA表单模板可由自适应表单或其他XFA表单模板引用。 此外，模板可以引用资源或其他XFA模板。

引用XFA的自适应表单的字段与XFA中可用的字段绑定。 在更新表单模板时，关联的自适应表单尝试与XFA同步。 有关更多详细信息，请参阅 [将自适应表单与关联的XFA同步](../../forms/using/synchronizing-adaptive-forms-xfa.md).

删除表单模板会损坏相关的自适应表单或表单模板。 此类自适应表单有时被非正式地称为脏表单。 在AEM Forms用户界面中，您可以通过以下两种方式找到已修改的表单。

* 资产列表中的自适应表单缩略图上会显示一个警告图标，当您将指针悬停在警告图标上时，会显示以下消息。\
  `Schema/Form Template for this adaptive form has been updated so go to Authoring mode and rebase it with new version.`

![更新关联的XFA后自适应表单不同步的警告](assets/dirtyaf.png)

将维护一个标志以指示自适应表单是否已修改。 此信息可在表单属性页面和表单元数据旁找到。 仅适用于已修改的自适应表单，即元数据属性 `Model Refresh` 显示 `Recommended` 值。

![指示自适应表单与XFA模型不同步](assets/model-refresh.png)
