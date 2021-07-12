---
title: 在AEM Forms中获取XDP和PDF文档
seo-title: 在AEM Forms中获取XDP和PDF文档
description: AEM Forms允许您上传表单和受支持的资产，以便与自适应表单结合使用。 您还可以通过ZIP批量上传表单和相关资源。
seo-description: AEM Forms允许您上传表单和受支持的资产，以便与自适应表单结合使用。 您还可以通过ZIP批量上传表单和相关资源。
uuid: cd49b4a8-c282-4059-95a0-c98f6c92ab14
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-manager
discoiquuid: 28b9f1d6-6a52-458f-a8ed-a206502eda0d
docset: aem65
role: Admin
exl-id: 9ecdc50a-31e3-46ae-948a-d1f6e6085734
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '708'
ht-degree: 0%

---

# 在AEM Forms中获取XDP和PDF文档{#getting-xdp-and-pdf-documents-in-aem-forms}

## 概述 {#overview}

您可以通过将表单上传到AEM Forms，将表单从本地文件系统导入CRX存储库。 以下资产类型支持上传操作：

* 表单模板（XFA表单）
* PDF forms
* 文档（平面PDF文档）

您可以单独或以ZIP存档形式上传受支持的资产类型。 您只能上传`Resource`类型的资产，并在ZIP存档中与XFA表单一起上传。

>[!NOTE]
>
>确保您是`form-power-users`组的成员，才能上传XDP文件。 请联系您的管理员以成为组的成员。

## 上传表单 {#uploading-forms}

1. 通过访问`https://'[server]:[port]'/aem/forms.html`登录AEM Forms用户界面。
1. 导航到要上传表单的文件夹，或包含表单的文件夹。
1. 在操作工具栏中，点按&#x200B;**创建>文件上传**。

   ![“创建”下的“来自本地存储的文件”选项](assets/step.png)

1. “上传表单”或“包”对话框允许您浏览并选择要上传的文件。 文件浏览器仅显示支持的文件格式（ZIP、XDP和PDF）。

   >[!NOTE]
   >
   >文件名只能包含字母数字字符、连字符或下划线。

1. 选择文件后单击上传以上传文件，或单击“取消”以取消上传。 弹出窗口会列出已添加的资产以及在当前位置更新的资产。

   >[!NOTE]
   >
   >对于ZIP文件，将显示所有受支持资产的相对路径。 ZIP中不支持的资产将被忽略，且不会列出。 但是，如果ZIP存档仅包含不支持的资产，则会显示错误消息，而不是弹出对话框。

   ![上传XFA表单时的“上传”对话框](assets/upload-scr.png)

1. 如果一个或多个资产的文件名无效，则会显示错误。 更正以红色突出显示的文件名并重新上传。

   ![上传XFA表单时出现错误消息](assets/upload-scr-err.png)

上传完成后，后台工作流会根据资产的预览为每个资产生成缩略图。 资产的较新版本（如果已上传）会覆盖现有资产。

### 保护模式 {#protected-mode}

AEM Forms服务器允许您运行JavaScript代码。 恶意JavaScript代码可能会损害AEM Forms环境。 保护模式可限制AEM Forms仅从受信任的资产和位置运行XDP文件。 AEM Forms UI中所有可用的XDP都被视为可信资产。

默认情况下，受保护模式处于打开状态。 如有必要，您可以禁用受保护模式：

1. 以管理员身份登录AEM Web Console。 URL是https://&#39;[server]:[port]&#39;/system/console/configMgr
1. 打开移动Forms配置进行编辑。
1. 取消选择“受保护模式”选项，然后单击&#x200B;**Save**。 已禁用受保护模式。

## 更新引用的XFA表单 {#updating-referenced-xfa-forms}

在AEM Forms中，XFA表单模板可以由自适应表单或其他XFA表单模板引用。 此外，模板可以引用资源或其他XFA模板。

引用XFA的自适应表单的字段与XFA中的可用字段绑定。 更新表单模板时，关联的自适应表单会尝试与XFA同步。 有关更多详细信息，请参阅[将自适应表单与关联的XFA](../../forms/using/synchronizing-adaptive-forms-xfa.md)同步。

删除表单模板会损坏从属自适应表单或表单模板。 这种自适应表单有时被非正式地称为肮脏表单。 在AEM Forms用户界面中，您可以通过以下两种方式找到脏表单。

* 资产列表的自适应表单缩略图上会显示一个警告图标，当您将指针悬停在警告图标上时，会显示以下消息。\
   `Schema/Form Template for this adaptive form has been updated so please go to Authoring mode and rebase it with new version.`

![更新关联的XFA后，自适应表单不同步的警告](assets/dirtyaf.png)

将维护一个标志，以指示自适应表单是否脏。 此信息可在表单属性页面上和表单元数据一起使用。 仅对于脏自适应表单，元数据属性`Model Refresh`显示`Recommended`值。

![表示自适应表单与XFA模型不同步](assets/model-refresh.png)
