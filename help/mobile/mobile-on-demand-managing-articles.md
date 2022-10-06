---
title: 管理文章
seo-title: Managing Articles
description: 可查看本页以了解有关创建和管理文章的信息。
seo-description: Follow this page to learn about creating and managing Articles.
uuid: 72b86cd7-3016-41b6-a001-9dce4084e9db
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: authoring-on-demand-services-app
discoiquuid: b46058f9-4691-4fba-a656-0f8507875a79
exl-id: ea6c8aa3-f86e-4878-8550-fe1662f10696
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '678'
ht-degree: 1%

---

# 管理文章{#managing-articles}

>[!NOTE]
>
>Adobe建议对需要基于单页应用程序框架的客户端渲染（例如React）的项目使用SPA编辑器。 [了解更多](/help/sites-developing/spa-overview.md)。

内容管理操作是帮助在应用程序中创建和管理文章的构建基块。 对应用程序中的文章执行以下操作。

## 文章概述 {#articles-overview}

文章表示基于文本的文本以及传递信息的艺术。

>[!NOTE]
>
>请参阅“联机帮助”中的以下资源，以了解AEM Mobile应用程序中的以下主题：
>
>* [设计注意事项](https://helpx.adobe.com/digital-publishing-solution/help/design-app.html)
>
>* [管理文章](https://helpx.adobe.com/digital-publishing-solution/help/creating-articles.html)
>


## 创建文章 {#creating-an-article}

创建文章的常规工作流如下所示：

1. 选择 **移动设备** 从侧边栏。
1. 在移动设备中，从目录中选择您的移动按需应用程序。
1. 单击 **管理文章** 拼贴。
1. 选择文章模板并单击 **下一个**.
1. 在向导的每个步骤中继续创建新文章。
1. 准备就绪后，单击 **创建**.
1. 您的新文章将显示在 **管理文章** 拼贴。

## 导入新文章 {#importing-a-new-article}

现有的Mobile On-Demand内容可以从Mobile On-Demand下载（导入）到AEM。 这允许编辑和查看本地内容。

>[!NOTE]
>
>导入不包括图像。

导入新文章的工作流

1. 在移动设备中，从目录中选择您的移动按需应用程序。
1. 单击 **管理文章** 拼贴，然后选择“导入文章”。
1. 单击 **导入文章** ，然后单击关闭。
1. 您的Mobile On-Demand文章现在显示在 **管理文章** 拼贴。

>[!CAUTION]
>
>您必须先关联Mobile On-Demand连接。

![chlimage_1-3](assets/chlimage_1-3.gif)

## 编辑文章 {#editing-an-article}

使用AEM中内置的拖放编辑器来添加或更改文章。 可以添加/删除文本和图像等组件。 可以插入DAM资产中的图像。

>[!CAUTION]
>
>只能在编辑器中打开在AEM中创建的文章。

编辑文章的工作流：

1. 在移动设备中，从目录中选择您的移动按需应用程序。
1. 从中选择源于AEM的文章 **管理文章** 拼贴。
1. 从列表视图中单击突出显示的文章以在内容编辑器中打开它。
1. 使用内容编辑器拖动文章内容（手稿、图像、文本等）。

### 查看和编辑文章中的元数据 {#viewing-and-editing-the-metadata-within-an-article}

文章、横幅等内容具有许多属性，如标题、描述、图像。 此操作用于查看和修改此类属性。 （可选）保存后，这些更改可以上传到Mobile On-Demand。

查看/编辑文章的常规工作流：

1. 在移动设备中，从目录中选择您的移动按需应用程序。
1. 从 **管理文章** 拼贴。

1. 选择 **查看属性** 中。
1. 查看该文章的所有可用元数据。
1. 根据需要编辑元数据，然后单击 **保存** 完成时。
1. （可选）立即将更改上传到Mobile On-Demand。

## 上传文章 {#uploading-an-article}

上传操作会复制选定的内容并将其添加到Mobile On-Demand项目。 现有的Mobile On-Demand内容将被新版本替换。

上传文章的常规工作流：

1. 从 **移动设备**，请从目录中选择您的Mobile On-Demand应用程序。
1. 在 **管理文章** 拼贴中，选择要上传到Mobile On-Demand的文章。
1. 根据需要从列表视图添加更多文章。
1. 选择 **上传** 在操作栏中，单击对话框中的上传。
1. 您的文章现已上传到Mobile On-Demand。

![chlimage_1-4](assets/chlimage_1-4.gif)

## 删除文章 {#deleting-an-article}

此操作将从Mobile On-Demand中删除所选内容，并（可选）从本地AEM实例中删除。

删除文章的常规工作流：

1. 在移动设备中，从目录中选择您的移动按需应用程序。
1. 在 **管理文章** 拼贴。
1. 确保在列表中选择了该选件（根据需要选择其他要删除组件）。
1. 单击 **删除** 中。
1. 检查是否要从AEM和Mobile On-Demand中删除。
1. 单击&#x200B;**删除**。
1. 您的文章现已从列表中删除。

![chlimage_1-5](assets/chlimage_1-5.gif)

### 后续步骤 {#the-next-steps}

在您了解如何管理文章时，请参阅

* [管理横幅](/help/mobile/mobile-on-demand-managing-banners.md)
* [管理收藏集](/help/mobile/mobile-on-demand-managing-collections.md)
* [上传共享资源](/help/mobile/mobile-on-demand-shared-resources.md)
* [发布/取消发布内容](/help/mobile/mobile-on-demand-publishing-unpublishing.md)
* [使用预检预览](/help/mobile/aem-mobile-manage-ondemand-services.md)
