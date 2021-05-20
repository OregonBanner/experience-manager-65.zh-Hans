---
title: 管理收藏集
seo-title: 管理收藏集
description: 收藏集代表一个定义良好的存储段，其中填充了适合封面主题的文章或横幅等内容。 请阅读本页以了解更多信息。
seo-description: 收藏集代表一个定义良好的存储段，其中填充了适合封面主题的文章或横幅等内容。 请阅读本页以了解更多信息。
uuid: 1d2e9769-d2cc-4d43-a428-e962a51eb5d0
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: authoring-on-demand-services-app
discoiquuid: 64c6d198-983f-4a52-9c83-560206363868
exl-id: 0b4aa1a4-449a-4882-8f7c-3ceea6ac7f83
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '824'
ht-degree: 2%

---

# 管理收藏集{#managing-collections}

>[!NOTE]
>
>Adobe建议对需要基于单页应用程序框架的客户端渲染（例如React）的项目使用SPA编辑器。 [了解更多](/help/sites-developing/spa-overview.md)。

内容管理操作是帮助在应用程序中创建和管理内容的构建基块。 将对应用程序内的内容执行以下操作。

## 收藏集概述{#collections-overview}

收藏集代表一个定义良好的&#x200B;*存储段*，其中填充了适合封面主题的文章或横幅等内容。

>[!NOTE]
>
>请参阅“联机帮助”中的以下资源，以了解AEM Mobile应用程序中的以下主题：
>
>* [设计注意事项](https://helpx.adobe.com/digital-publishing-solution/help/design-app.html)
   >
   >
* [管理收藏集](https://helpx.adobe.com/digital-publishing-solution/help/creating-collections.html)

>



## 创建收藏集 {#creating-a-collection}

创建收藏集的常规工作流如下所示：

1. 从侧边栏中选择&#x200B;**Mobile**。
1. 在移动设备中，从目录中选择您的移动按需应用程序。
1. 单击&#x200B;**管理收藏集**&#x200B;拼贴右上角的向下箭头。
1. 在向导的每个步骤中继续创建新文章。
1. 准备就绪后，单击&#x200B;**创建**。
1. 您的新文章将显示在&#x200B;**管理收藏集**&#x200B;拼贴中。

![chlimage_1-1](assets/chlimage_1-1.gif)

## 导入新集合{#importing-a-new-collection}

现有的Mobile On-Demand内容可以从Mobile On-Demand下载（导入）到AEM。 这允许编辑和查看本地内容。

>[!NOTE]
>
>导入不包括图像。

导入新收藏集的工作流

1. 在移动设备中，从目录中选择您的移动按需应用程序。
1. 单击&#x200B;**管理收藏集**&#x200B;拼贴右上角的向下箭头，然后选择“导入收藏集”。
1. 单击对话框中的&#x200B;**导入收藏集** ，然后单击关闭。
1. 您的Mobile On-Demand收藏集现在显示在&#x200B;**管理收藏集**&#x200B;拼贴中。

>[!CAUTION]
>
>您必须先关联Mobile On-Demand连接。

## 编辑集合{#editing-a-collection}

使用AEM中内置的拖放编辑器来添加或更改文章。 可以添加/删除文本和图像等组件。 可以插入DAM资产中的图像。

编辑收藏集的工作流：

1. 在移动设备中，从目录中选择您的移动按需应用程序。
1. 从&#x200B;**管理收藏集**&#x200B;拼贴中选择源于AEM的文章。
1. 从列表视图中单击突出显示的收藏集，以在内容编辑器中将其打开。
1. 使用内容编辑器拖动收藏内容（手稿、图像、文本等）。

### 查看和编辑集合{#viewing-and-editing-the-metadata-within-a-collection}中的元数据

收藏集具有许多属性，如标题、描述、图像。 此操作用于查看和修改此类属性。 （可选）保存后，这些更改可以上传到Mobile On-Demand。

查看/编辑收藏集的常规工作流：

1. 在移动设备中，从目录中选择您的移动按需应用程序。
1. 从&#x200B;**管理收藏集**&#x200B;拼贴中选择一个收藏集。

1. 从操作栏中选择&#x200B;**属性**。
1. 查看该文章的所有可用元数据。
1. 根据需要编辑元数据，完成后单击&#x200B;**保存**。
1. （可选）立即将更改上传到Mobile On-Demand。

## 上传集合{#uploading-a-collection}

上传操作会复制选定的内容并将其添加到Mobile On-Demand项目。 现有的Mobile On-Demand内容将被新版本替换。

上传收藏集的常规工作流：

1. 从&#x200B;**Mobile**&#x200B;中，从目录中选择您的Mobile On-Demand应用程序。
1. 在&#x200B;**管理收藏集**&#x200B;拼贴中，选择要上传到Mobile On-Demand的文章。
1. 根据需要从列表视图添加更多收藏集。
1. 从操作栏中选择&#x200B;**Upload** ，然后在对话框中单击Upload。
1. 您的收藏集现已上传到Mobile On-Demand。

## 删除收藏集 {#deleting-a-collection}

此操作将从Mobile On-Demand中删除所选集合，并（可选）从本地AEM实例中删除。

删除收藏集的常规工作流：

1. 在移动设备中，从目录中选择您的移动按需应用程序。
1. 在&#x200B;**管理收藏集**&#x200B;拼贴中选择要删除的文章。
1. 确保在列表中选择了该选件（根据需要选择其他要删除组件）。
1. 单击操作栏中的&#x200B;**删除**。
1. 检查是否要从AEM和Mobile On-Demand中删除。
1. 单击&#x200B;**删除**。
1. 您的收藏集现已从列表中删除。

## 向收藏集添加内容{#adding-content-to-collections}

收藏集本质上是相关内容的一类。 它们将文章、横幅等内容收集到用于定义应用程序导航结构的包中。 可以嵌套收藏集。

>[!NOTE]
>
>内容必须先上传到Mobile On-Demand，然后才能添加到收藏集。

收藏集本质上是一类相关内容：它们将文章、横幅等内容收集到用于定义应用程序导航结构的包中。 可以嵌套收藏集。

1. 在移动设备中，从目录中选择您的移动按需应用程序。
1. 选择之前上传的文章（或横幅/收藏集）
1. 从操作栏中选择添加到。
1. 从对话框中选择之前上传的收藏集。
1. 单击&#x200B;**Update**&#x200B;以向集合添加内容。

![chlimage_1-2](assets/chlimage_1-2.gif)

### 后续步骤 {#the-next-steps}

在您了解如何管理收藏集时，请参阅

* [管理横幅](/help/mobile/mobile-on-demand-managing-banners.md)
* [管理文章](/help/mobile/mobile-on-demand-managing-articles.md)
* [上传共享资源](/help/mobile/mobile-on-demand-shared-resources.md)
* [发布/取消发布内容](/help/mobile/mobile-on-demand-publishing-unpublishing.md)
* [使用预检预览](/help/mobile/aem-mobile-manage-ondemand-services.md)
