---
title: 管理收藏集
seo-title: Managing Collections
description: 收藏集表示一个明确定义的存储桶，其中包含适合封面主题的文章或横幅等内容。 关注此页面以了解更多信息。
seo-description: Collections represent a well defined bucket filled with content such as articles or banners that suits the cover's theme. Follow this page to learn more.
uuid: 1d2e9769-d2cc-4d43-a428-e962a51eb5d0
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: authoring-on-demand-services-app
discoiquuid: 64c6d198-983f-4a52-9c83-560206363868
exl-id: 0b4aa1a4-449a-4882-8f7c-3ceea6ac7f83
source-git-commit: 259f257964829b65bb71b5a46583997581a91a4e
workflow-type: tm+mt
source-wordcount: '798'
ht-degree: 0%

---

# 管理收藏集{#managing-collections}

>[!NOTE]
>
>对于需要基于单页应用程序框架的客户端渲染（例如React）的项目，Adobe建议使用SPA编辑器。 [了解详情](/help/sites-developing/spa-overview.md).

内容管理操作是构建块，有助于在应用程序中创建和管理内容。 对应用程序中的内容执行以下操作。

## 收藏集概述 {#collections-overview}

收藏集表示一个明确定义的 *分段* 填入了适合封面主题的文章或横幅等内容。

>[!NOTE]
>
>请参阅联机帮助中的以下资源，了解AEM Mobile应用程序中的以下主题：
>
>* [设计注意事项](https://helpx.adobe.com/digital-publishing-solution/help/design-app.html)
>
>* [管理收藏集](https://helpx.adobe.com/digital-publishing-solution/help/creating-collections.html)
>

## 创建收藏集 {#creating-a-collection}

创建收藏集的常规工作流如下：

1. 选择 **移动设备** 从侧边栏上删除。
1. 从Mobile中，从目录中选择您的Mobile On-Demand应用程序。
1. 单击右上角的向下箭头 **管理收藏集** 图块。
1. 完成向导的每个步骤，以继续创建新文章。
1. 准备就绪后，单击 **创建**.
1. 您的新文章将显示在 **管理收藏集** 图块。

![chlimage_1-1](assets/chlimage_1-1.gif)

## 导入新收藏集 {#importing-a-new-collection}

现有Mobile On-Demand内容可以从Mobile On-Demand下载（导入）到AEM。 这允许编辑和查看本地内容。

>[!NOTE]
>
>导入不包括图像。

用于导入新收藏集的工作流

1. 从Mobile中，从目录中选择您的Mobile On-Demand应用程序。
1. 单击右上角的向下箭头 **管理收藏集** 图块并选择导入收藏集。
1. 单击 **导入收藏集** 在对话框中，然后单击关闭。
1. 您的Mobile On-Demand收藏集现在显示在 **管理收藏集** 图块。

>[!CAUTION]
>
>您必须先关联Mobile On-Demand连接。

## 编辑收藏集 {#editing-a-collection}

使用内置的AEM拖放编辑器添加或更改文章。 可以添加/删除文本和图像等组件。 可以插入DAM资产中的图像。

用于编辑收藏集的工作流：

1. 从Mobile中，从目录中选择您的Mobile On-Demand应用程序。
1. 从中选择AEM源文章 **管理收藏集** 图块。
1. 从列表视图中单击高亮显示的收藏集，以在内容编辑器中打开它。
1. 使用内容编辑器拖动收藏集内容（手稿、图像、文本等）。

### 查看和编辑收藏集中的元数据 {#viewing-and-editing-the-metadata-within-a-collection}

收藏集具有许多属性，例如标题、描述、图像。 此操作用于查看和修改此类属性。 或者，这些更改可以在保存时上传到Mobile On-Demand。

查看/编辑收藏集的常规工作流：

1. 从Mobile中，从目录中选择您的Mobile On-Demand应用程序。
1. 从中选择收藏集 **管理收藏集** 图块。

1. 选择 **属性** 操作栏中的。
1. 查看该文章的所有可用元数据。
1. 编辑元数据（如果需要），然后单击 **保存** 完成时。
1. （可选）立即将更改上传到Mobile On-Demand。

## 上传收藏集 {#uploading-a-collection}

上传操作会复制所选内容并将其添加到Mobile On-Demand项目。 现有的Mobile On-Demand内容将由新版本替换。

上传收藏集的常规工作流：

1. 起始日期 **移动设备**，从目录中选择您的Mobile On-Demand应用程序。
1. 在 **管理收藏集** 磁贴，选择文章以上传到Mobile On-Demand。
1. 如果需要，可从列表视图添加更多收藏集。
1. 选择 **上传** 在操作栏中，单击对话框中的“上传”。
1. 您的收藏集现已上传到Mobile On-Demand。

## 删除收藏集 {#deleting-a-collection}

此操作会从Mobile On-Demand中删除选定的集合，也可以从本地AEM实例中删除（可选）。

用于删除收藏集的常规工作流：

1. 从Mobile中，从目录中选择您的Mobile On-Demand应用程序。
1. 在中选择要删除的文章 **管理收藏集** 图块。
1. 确保在列表中选中它（根据需要选择要删除的其他项）。
1. 单击 **删除** 操作栏中的。
1. 检查是否要从AEM和Mobile On-Demand中删除。
1. 单击&#x200B;**删除**。
1. 您的收藏集现已从列表中删除。

## 将内容添加到收藏集 {#adding-content-to-collections}

收藏集本质上是一类相关内容。 它们将文章、横幅等内容收集到包中，以定义应用程序的导航结构。 可以嵌套收藏集。

>[!NOTE]
>
>必须先将内容上传到Mobile On-Demand，然后才能将其添加到收藏集。

收藏集本质上是一类相关内容：它们会将文章、横幅等内容收集到包中，以定义应用程序的导航结构。 可以嵌套收藏集。

1. 从Mobile中，从目录中选择您的Mobile On-Demand应用程序。
1. 选择之前上传的文章（或横幅/收藏集）
1. 从操作栏中选择“添加到”。
1. 从对话框中选择之前上传的收藏集。
1. 单击 **更新** 以将内容添加到收藏集。

![chlimage_1-2](assets/chlimage_1-2.gif)

### 后续步骤 {#the-next-steps}

有关管理收藏集的信息，请参阅

* [管理横幅](/help/mobile/mobile-on-demand-managing-banners.md)
* [管理文章](/help/mobile/mobile-on-demand-managing-articles.md)
* [上传共享资源](/help/mobile/mobile-on-demand-shared-resources.md)
* [发布/取消发布内容](/help/mobile/mobile-on-demand-publishing-unpublishing.md)
* [使用Preflight预览](/help/mobile/aem-mobile-manage-ondemand-services.md)
