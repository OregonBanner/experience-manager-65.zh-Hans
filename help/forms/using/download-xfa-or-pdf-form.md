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

---


# 下载XFA或PDF表单模板 {#download-an-xfa-or-a-pdf-form-template}

根据名称含义，下载操作允许您将表单从存储库导出到本地系统。 结合上传操作，此操作可帮助您将表单从一个存储库迁移到另一个存储库。

在AEM Forms中，以下资产类型支持下载操作：

* 表单模板（XFA表单）
* PDF表单
* 文档（平面PDF文件）

AEM Forms支持单独下载这些表单类型，或下载到包含一个或多个受支持表单的文件夹中。

除了这些资产外，如果资 `Resource` 产类型在文件夹中，您还可以下载它。 提供此功能后，您可以下载XFA表单所引用的资源以及表单。

## 下载一个或多个表单 {#download-one-or-more-forms}

1. 登录到AEM Forms用户界面（位于） `https://<server>:<port>/aem/forms.html`。

1. 导航到要下载的资产所在的位置。

1. 选择资产。 单击工 **[!UICONTROL 具]** 栏中的 ![“下载](assets/aem6forms_download.png) aem6forms_download”图标。

   >[!NOTE]
   >
   >只能选择一个表单进行下载。 如果要下载多个表单，则必须将其下载为文件夹。

1. 在出现的对话框中，单击“下 **[!UICONTROL 载”]**。

   AEM Forms会生成一个ZIP文件，其中包含所选文件或所选文件夹。

   如果您正在下载文件夹，则文件夹内受支持的资产将下载到其现有层次结构中。

   ZIP文件将保存到系统 `Downloads` 上的文件夹中。

## 上传操作的相关注意事项 {#related-considerations-for-the-upload-operation}

* 您可以将ZIP文件上传到同一存储库或另一个存储库中的任何其他位置
* 在上传操作过程中，文件夹中资产的层次结构将保留
* 下载前对下载的资产所做的任何元数据更改都会在上传时反映出来

