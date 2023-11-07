---
title: 管理横幅
seo-title: Managing Banners
description: 横幅代表典型的图形促销链接。 关注此页面以了解更多信息。
seo-description: Banners represent typically graphical promotional links. Follow this page to learn more.
uuid: 593fe2ef-84df-42e2-8a03-897fb67a896d
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: authoring-on-demand-services-app
discoiquuid: fb1abaa0-9c02-4f20-aa7c-073def067452
exl-id: c65a24e6-3041-4774-aeed-8e188ea19b78
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '661'
ht-degree: 1%

---

# 管理横幅{#managing-banners}

>[!NOTE]
>
>Adobe建议对需要基于单页应用程序框架的客户端渲染（例如React）的项目使用SPA编辑器。 [了解详情](/help/sites-developing/spa-overview.md)。

内容管理操作是构建块，有助于在应用程序中创建和管理内容。 对应用程序中的内容执行以下操作。

## 横幅概述 {#banners-overview}

横幅代表典型的图形促销链接。

>[!NOTE]
>
>请参阅联机帮助中的以下资源，以了解AEM Mobile应用程序中的以下主题：
>
>* [设计注意事项](https://helpx.adobe.com/digital-publishing-solution/help/design-app.html)
>
>* [创建横幅](https://helpx.adobe.com/digital-publishing-solution/help/creating-banners.html)
>

## 创建横幅 {#creating-a-banner}

创建文章的常规工作流如下所示：

1. 选择 **移动设备** 从侧边栏移出。
1. 在Mobile中，从目录中选择您的Mobile On-Demand应用程序。
1. 单击右上角的向下箭头 **管理横幅** 磁贴。
1. 完成向导的每个步骤，以继续创建新横幅。
1. 准备就绪后，单击 **创建**.
1. 您的新横幅将显示在 **管理横幅** 磁贴。

![chlimage_1-6](assets/chlimage_1-6.gif)

## 导入新横幅 {#importing-a-new-banner}

现有Mobile On-Demand内容可以从Mobile On-Demand下载（导入）到AEM。 这允许编辑和查看本地内容。

>[!NOTE]
>
>导入不包括图像。

用于导入新文章的工作流

1. 在Mobile中，从目录中选择您的Mobile On-Demand应用程序。
1. 单击右上角的向下箭头 **管理横幅** 平铺并选择导入横幅。
1. 单击 **导入横幅** 在对话框中，然后单击“关闭”。
1. 您的Mobile On-Demand文章现在显示在 **管理横幅** 磁贴。

>[!CAUTION]
>
>您必须先关联Mobile On-Demand连接。

## 编辑横幅 {#editing-a-banner}

使用内置的AEM拖放编辑器添加或更改文章。 可以添加/删除文本和图像等组件。 可以插入DAM资产中的图像。

>[!CAUTION]
>
>只有在AEM中创建的横幅才能在编辑器中打开。

用于编辑文章的工作流：

1. 在Mobile中，从目录中选择您的Mobile On-Demand应用程序。
1. 从**管理横幅**图块中选择一个源自AEM的横幅。
1. 从列表视图中单击高亮显示的横幅以在内容编辑器中打开它。
1. 使用内容编辑器拖动横幅内容（手稿、图像、文本等）。

### 查看和编辑横幅中的元数据 {#viewing-and-editing-the-metadata-within-a-banner}

横幅具有许多属性，如标题、描述和图像。 此操作用于查看和修改此类属性。 或者，这些更改可以在保存时上传到Mobile On-Demand。

查看/编辑文章的常规工作流：

1. 在Mobile中，从目录中选择您的Mobile On-Demand应用程序。
1. 从中选择横幅 **管理横幅** 磁贴。

1. 选择 **属性** 从操作栏中。
1. 查看该文章的所有可用元数据。
1. 根据需要编辑元数据并单击 **保存** 完成时。
1. （可选）将更改立即上载到Mobile On-Demand。

## 上传横幅 {#uploading-a-banner}

上传操作会复制所选内容并将其添加到Mobile On-Demand项目。 现有的Mobile On-Demand内容将由新版本替换。

用于上传横幅的常规工作流：

1. 从 **移动设备**，从目录中选择您的Mobile On-Demand应用程序。
1. 在 **管理横幅** 图块，选择要上传到Mobile On-Demand的横幅。
1. 如果需要，可从列表视图添加更多横幅。
1. 选择 **上传** 在操作栏中，单击对话框中的上传。
1. 您的横幅现已上传至Mobile On-Demand。

![chlimage_1-7](assets/chlimage_1-7.gif)

## 删除横幅 {#deleting-a-banner}

此操作会从Mobile On-Demand和（可选）本地AEM实例中删除所选横幅。

用于删除横幅的常规工作流：

1. 在Mobile中，从目录中选择您的Mobile On-Demand应用程序。
1. 选择要删除的横幅 **管理横幅** 磁贴。
1. 确保在列表中选中它（根据需要选择要删除的其他项）。
1. 单击 **删除** 从操作栏中。
1. 检查是否要从AEM和Mobile On-Demand中删除。
1. 单击&#x200B;**删除**。
1. 您的横幅现已从列表中删除。

### 后续步骤 {#the-next-steps}

如果您了解如何管理横幅，请参阅

* [管理文章](/help/mobile/mobile-on-demand-managing-articles.md)
* [管理收藏集](/help/mobile/mobile-on-demand-managing-collections.md)
* [上传共享资源](/help/mobile/mobile-on-demand-shared-resources.md)
* [发布/取消发布内容](/help/mobile/mobile-on-demand-publishing-unpublishing.md)
* [使用Preflight预览](/help/mobile/aem-mobile-manage-ondemand-services.md)
