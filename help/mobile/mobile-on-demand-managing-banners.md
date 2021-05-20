---
title: 管理横幅
seo-title: 管理横幅
description: 横幅通常表示图形促销链接。 请阅读本页以了解更多信息。
seo-description: 横幅通常表示图形促销链接。 请阅读本页以了解更多信息。
uuid: 593fe2ef-84df-42e2-8a03-897fb67a896d
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: authoring-on-demand-services-app
discoiquuid: fb1abaa0-9c02-4f20-aa7c-073def067452
exl-id: c65a24e6-3041-4774-aeed-8e188ea19b78
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '676'
ht-degree: 1%

---

# 管理横幅{#managing-banners}

>[!NOTE]
>
>Adobe建议对需要基于单页应用程序框架的客户端渲染（例如React）的项目使用SPA编辑器。 [了解更多](/help/sites-developing/spa-overview.md)。

内容管理操作是帮助在应用程序中创建和管理内容的构建基块。 将对应用程序内的内容执行以下操作。

## 横幅概述{#banners-overview}

横幅通常表示图形促销链接。

>[!NOTE]
>
>请参阅“联机帮助”中的以下资源，以了解AEM Mobile应用程序中的以下主题：
>
>* [设计注意事项](https://helpx.adobe.com/digital-publishing-solution/help/design-app.html)
   >
   >
* [创建横幅](https://helpx.adobe.com/digital-publishing-solution/help/creating-banners.html)

>



## 创建横幅{#creating-a-banner}

创建文章的常规工作流如下所示：

1. 从侧边栏中选择&#x200B;**Mobile**。
1. 在移动设备中，从目录中选择您的移动按需应用程序。
1. 单击&#x200B;**管理横幅**&#x200B;图块右上角的向下箭头。
1. 在向导的每个步骤中继续创建新横幅。
1. 准备就绪后，单击&#x200B;**创建**。
1. 您的新横幅将显示在&#x200B;**管理横幅**&#x200B;拼贴中。

![chlimage_1-6](assets/chlimage_1-6.gif)

## 导入新横幅{#importing-a-new-banner}

现有的Mobile On-Demand内容可以从Mobile On-Demand下载（导入）到AEM。 这允许编辑和查看本地内容。

>[!NOTE]
>
>导入不包括图像。

导入新文章的工作流

1. 在移动设备中，从目录中选择您的移动按需应用程序。
1. 单击&#x200B;**管理横幅**&#x200B;图块右上角的向下箭头，然后选择“导入横幅”。
1. 单击对话框中的&#x200B;**导入横幅** ，然后单击关闭。
1. 您的Mobile On-Demand文章现在显示在&#x200B;**管理横幅**&#x200B;拼贴中。

>[!CAUTION]
>
>您必须先关联Mobile On-Demand连接。

## 编辑横幅{#editing-a-banner}

使用AEM中内置的拖放编辑器来添加或更改文章。 可以添加/删除文本和图像等组件。 可以插入DAM资产中的图像。

>[!CAUTION]
>
>只有在AEM中创建的横幅才能在编辑器中打开。

编辑文章的工作流：

1. 在移动设备中，从目录中选择您的移动按需应用程序。
1. 从**管理横幅**拼贴中选择源于AEM的横幅。
1. 从列表视图中单击突出显示的横幅，以在内容编辑器中将其打开。
1. 使用内容编辑器拖动横幅内容（手稿、图像、文本等）。

### 查看和编辑横幅{#viewing-and-editing-the-metadata-within-a-banner}中的元数据

横幅具有许多属性，如标题、描述、图像。 此操作用于查看和修改此类属性。 （可选）保存后，这些更改可以上传到Mobile On-Demand。

查看/编辑文章的常规工作流：

1. 在移动设备中，从目录中选择您的移动按需应用程序。
1. 从&#x200B;**管理横幅**&#x200B;拼贴中选择一个横幅。

1. 从操作栏中选择&#x200B;**属性**。
1. 查看该文章的所有可用元数据。
1. 根据需要编辑元数据，完成后单击&#x200B;**保存**。
1. （可选）立即将更改上传到Mobile On-Demand。

## 上传横幅{#uploading-a-banner}

上传操作会复制选定的内容并将其添加到Mobile On-Demand项目。 现有的Mobile On-Demand内容将被新版本替换。

上传横幅的常规工作流：

1. 从&#x200B;**Mobile**&#x200B;中，从目录中选择您的Mobile On-Demand应用程序。
1. 在&#x200B;**管理横幅**&#x200B;拼贴中，选择要上传到Mobile On-Demand的横幅。
1. 根据需要从列表视图添加更多横幅。
1. 从操作栏中选择&#x200B;**Upload** ，然后在对话框中单击Upload。
1. 您的横幅现已上传到Mobile On-Demand。

![chlimage_1-7](assets/chlimage_1-7.gif)

## 删除横幅{#deleting-a-banner}

此操作将从Mobile On-Demand中删除所选横幅，并（可选）从本地AEM实例中删除。

删除横幅的常规工作流：

1. 在移动设备中，从目录中选择您的移动按需应用程序。
1. 在&#x200B;**管理横幅**&#x200B;拼贴中选择要删除的横幅。
1. 确保在列表中选择了该选件（根据需要选择其他要删除的选件）。
1. 单击操作栏中的&#x200B;**删除**。
1. 检查是否要从AEM和Mobile On-Demand中删除。
1. 单击&#x200B;**删除**。
1. 您的横幅现已从列表中删除。

### 后续步骤 {#the-next-steps}

如果您了解如何管理横幅，请参阅

* [管理文章](/help/mobile/mobile-on-demand-managing-articles.md)
* [管理收藏集](/help/mobile/mobile-on-demand-managing-collections.md)
* [上传共享资源](/help/mobile/mobile-on-demand-shared-resources.md)
* [发布/取消发布内容](/help/mobile/mobile-on-demand-publishing-unpublishing.md)
* [使用预检预览](/help/mobile/aem-mobile-manage-ondemand-services.md)
