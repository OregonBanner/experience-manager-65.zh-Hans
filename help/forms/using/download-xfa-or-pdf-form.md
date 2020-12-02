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
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '340'
ht-degree: 0%

---


# 下载XFA或PDF表单模板{#download-an-xfa-or-a-pdf-form-template}

下载操作（如名称所示）允许您将表单从存储库导出到本地系统。 与上传操作相结合，此操作可帮助您将表单从一个存储库迁移到另一个存储库。

在AEM Forms，下列资产类型支持下载操作：

* 表单模板(XFAForms)
* PDF forms
* 文档（平面PDF文件）

AEM Forms支持单独下载这些表单类型或在包含一个或多个支持表单的文件夹中下载这些表单类型。

除了这些资产外，如果资产位于文件夹中，您还可以下载`Resource`类型的资产。 此功能允许您下载XFA表单所引用的资源以及表单。

## 下载一个或多个表单{#download-one-or-more-forms}

1. 登录到位于`https://<server>:<port>/aem/forms.html`的AEM Forms用户界面。

1. 导航到要下载的资产所在的位置。

1. 选择资产。 单击工具栏中的&#x200B;**[!UICONTROL 下载]** ![ aem6forms_download](assets/aem6forms_download.png)图标。

   >[!NOTE]
   >
   >只能选择一个表单进行下载。 如果要下载多个表单，则必须将其作为文件夹下载。

1. 在显示的对话框中，单击&#x200B;**[!UICONTROL 下载]**。

   AEM Forms会生成包含选定文件或选定文件夹的ZIP文件。

   如果您正在下载文件夹，则文件夹内受支持的资产会下载到其现有层次结构中。

   ZIP文件将保存到系统上的`Downloads`文件夹。

## 上传操作{#related-considerations-for-the-upload-operation}的相关注意事项

* 您可以将ZIP文件上传到同一存储库或其他存储库中的任何其他位置
* 在上传操作过程中，将保留文件夹中资产的层次结构
* 下载前对下载的资产所做的任何元数据更改均会在上传时反映出来

