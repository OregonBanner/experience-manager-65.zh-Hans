---
title: 下载XFA或PDF表单模板
seo-title: 下载XFA或PDF表单模板
description: 您可以将表单从存储库导出到本地系统，并将下载的表单迁移到新存储库。
seo-description: 您可以将表单从存储库导出到本地系统，并将下载的表单迁移到新存储库。
uuid: 5f7fbd14-cb9d-4749-8708-7efe49df89d7
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-manager
discoiquuid: 6699e0e7-fd42-41ae-86a2-3b940d905111
role: Administrator
exl-id: 5b7b9816-38c1-4780-b1fc-8184971f3772
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '340'
ht-degree: 0%

---

# 下载XFA或PDF表单模板{#download-an-xfa-or-a-pdf-form-template}

如名称所示，下载操作允许您将表单从存储库导出到本地系统。 与上传操作结合使用，此操作可帮助您将表单从一个存储库迁移到另一个存储库。

在AEM Forms中，以下资产类型支持下载操作：

* 表单模板(XFA Forms)
* PDF forms
* 文档（平面PDF文件）

AEM Forms支持单独或在包含一个或多个受支持表单的文件夹中下载这些表单类型。

除了这些资产之外，如果文件夹中存在`Resource`类型的资产，您还可以下载该资产。 提供此功能后，您可以下载XFA表单引用的资源以及表单。

## 下载一个或多个表单{#download-one-or-more-forms}

1. 登录到位于`https://<server>:<port>/aem/forms.html`的AEM Forms用户界面。

1. 导航到要下载的资产所在的位置。

1. 选择资产。 单击工具栏中的&#x200B;**[!UICONTROL 下载]** ![aem6forms_download](assets/aem6forms_download.png)图标。

   >[!NOTE]
   >
   >您只能选择一个表单进行下载。 如果要下载多个表单，则必须将其下载为文件夹。

1. 在显示的对话框中，单击&#x200B;**[!UICONTROL Download]**。

   AEM Forms会生成包含选定文件或选定文件夹的ZIP文件。

   如果您正在下载文件夹，则文件夹内受支持的资产会按其现有层次结构进行下载。

   ZIP文件会保存到您系统上的`Downloads`文件夹中。

## 上传操作{#related-considerations-for-the-upload-operation}的相关注意事项

* 您可以将ZIP文件上传到同一存储库或其他存储库中的任何其他位置
* 文件夹中资产的层次结构将在上传操作期间保留
* 下载前对下载的资产所做的任何元数据更改都会在上传时反映出来
