---
title: 下载XFA或PDF表单模板
description: 您可以将表单从存储库导出到本地系统，并将下载的表单迁移到新存储库。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-manager
role: Admin
exl-id: 5b7b9816-38c1-4780-b1fc-8184971f3772
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '311'
ht-degree: 0%

---

# 下载XFA或PDF表单模板 {#download-an-xfa-or-a-pdf-form-template}

顾名思义，下载操作允许您将表单从存储库导出到本地系统。 与上传操作结合使用时，此操作可帮助您将表单从一个存储库迁移到另一个存储库。

在AEM Forms中，以下资源类型支持下载操作：

* 表单模板(XFA Forms)
* PDF forms
* 文档(平面PDF文件)

AEM Forms支持单独下载这些表单类型，或将其下载到包含一个或多个受支持表单的文件夹中。

除了这些资源外，您还可以下载 `Resource` 资源类型（如果文件夹中存在该资源）。 提供此功能是为了让您下载XFA表单以及表单引用的资源。

## 下载一个或多个表单 {#download-one-or-more-forms}

1. 登录到AEM Forms用户界面，网址为 `https://<server>:<port>/aem/forms.html`.

1. 导航到要下载的资源的位置。

1. 选择资源。 单击 **[!UICONTROL 下载]** ![aem6forms_download](assets/aem6forms_download.png) 图标。

   >[!NOTE]
   >
   >您只能选择一个要下载的表单。 如果要下载多个表单，必须将它们下载为文件夹。

1. 在出现的对话框中，单击 **[!UICONTROL 下载]**.

   AEM Forms会生成一个包含选定文件或选定文件夹的ZIP文件。

   如果您正在下载文件夹，则该文件夹中支持的资源将下载到其现有层次结构中。

   ZIP文件将保存到 `Downloads` 个文件夹。

## 上载操作的相关注意事项 {#related-considerations-for-the-upload-operation}

* 您可以将ZIP文件上传到同一存储库或其他存储库中的任何其他位置
* 上传操作期间，将保留文件夹中资产的层次结构
* 下载之前对下载的资产所做的任何元数据更改都会在上传时反映出来
