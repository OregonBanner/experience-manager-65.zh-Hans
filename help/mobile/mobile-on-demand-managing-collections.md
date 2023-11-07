---
title: 管理收藏集
description: 收藏表示一个定义良好的存储段，其中填充了适合封面主题的文章或横幅等内容。 关注此页面以了解更多信息。
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: authoring-on-demand-services-app
exl-id: 0b4aa1a4-449a-4882-8f7c-3ceea6ac7f83
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '796'
ht-degree: 0%

---

# 管理收藏集{#managing-collections}

>[!NOTE]
>
>Adobe建议对需要基于单页应用程序框架的客户端渲染（例如React）的项目使用SPA编辑器。 [了解详情](/help/sites-developing/spa-overview.md)。

内容管理操作是构建块，有助于在应用程序中创建和管理内容。 对应用程序中的内容执行以下操作。

## 收藏集概述 {#collections-overview}

收藏集代表明确定义的 *分段* 填充适合封面主题的文章或横幅等内容。

>[!NOTE]
>
>请参阅联机帮助中的以下资源，以了解AEM Mobile应用程序中的以下主题：
>
>* [设计注意事项](https://helpx.adobe.com/digital-publishing-solution/help/design-app.html)
>
>* [管理收藏集](https://helpx.adobe.com/digital-publishing-solution/help/creating-collections.html)
>

## 创建收藏集 {#creating-a-collection}

创建收藏集的常规工作流如下所示：

1. 选择 **移动设备** 从侧边栏移出。
1. 在Mobile中，从目录中选择您的Mobile On-Demand应用程序。
1. 单击右上角的向下箭头 **管理收藏集** 磁贴。
1. 完成向导的每个步骤以继续创建新文章。
1. 准备就绪后，单击 **创建**.
1. 您的新文章将显示在 **管理收藏集** 磁贴。

![chlimage_1-1](assets/chlimage_1-1.gif)

## 导入新收藏集 {#importing-a-new-collection}

现有Mobile On-Demand内容可以从Mobile On-Demand下载（导入）到AEM。 这允许编辑和查看本地内容。

>[!NOTE]
>
>导入不包括图像。

用于导入新收藏集的工作流

1. 在Mobile中，从目录中选择您的Mobile On-Demand应用程序。
1. 单击右上角的向下箭头 **管理收藏集** 平铺并选择导入收藏集。
1. 单击 **导入收藏集** 在对话框中，然后单击“关闭”。
1. 您的Mobile On-Demand收藏集现在显示在 **管理收藏集** 磁贴。

>[!CAUTION]
>
>您必须先关联Mobile On-Demand连接。

## 编辑收藏集 {#editing-a-collection}

使用内置的AEM拖放编辑器添加或更改文章。 可以添加/删除文本和图像等组件。 可以插入DAM资产中的图像。

用于编辑收藏集的工作流：

1. 在Mobile中，从目录中选择您的Mobile On-Demand应用程序。
1. 从中选择源自AEM的文章 **管理收藏集** 磁贴。
1. 从列表视图中单击高亮显示的收藏集，以在内容编辑器中打开它。
1. 使用内容编辑器拖动收藏集内容（手稿、图像、文本等）。

### 查看和编辑收藏集中的元数据 {#viewing-and-editing-the-metadata-within-a-collection}

收藏集具有许多属性，例如标题、描述和图像。 此操作用于查看和修改此类属性。 或者，这些更改可以在保存时上传到Mobile On-Demand。

查看/编辑收藏集的常规工作流：

1. 在Mobile中，从目录中选择您的Mobile On-Demand应用程序。
1. 从中选择收藏集 **管理收藏集** 磁贴。

1. 选择 **属性** 从操作栏中。
1. 查看该文章的所有可用元数据。
1. 根据需要编辑元数据并单击 **保存** 完成时。
1. （可选）将更改立即上载到Mobile On-Demand。

## 上传收藏集 {#uploading-a-collection}

上传操作会复制所选内容并将其添加到Mobile On-Demand项目。 现有的Mobile On-Demand内容将由新版本替换。

上传收藏集的常规工作流：

1. 从 **移动设备**，从目录中选择您的Mobile On-Demand应用程序。
1. 在 **管理收藏集** 磁贴，选择要上传到Mobile On-Demand的文章。
1. 如果需要，可从列表视图添加更多收藏集。
1. 选择 **上传** 在操作栏中，单击对话框中的上传。
1. 您的收藏集现已上传至Mobile On-Demand。

## 删除收藏集 {#deleting-a-collection}

此操作会从Mobile On-Demand和（可选）本地AEM实例中删除所选集合。

用于删除收藏集的常规工作流：

1. 在Mobile中，从目录中选择您的Mobile On-Demand应用程序。
1. 在中选择要删除的文章 **管理收藏集** 磁贴。
1. 确保在列表中选中它（根据需要选择要删除的其他项）。
1. 单击 **删除** 从操作栏中。
1. 检查是否要从AEM和Mobile On-Demand中删除。
1. 单击&#x200B;**删除**。
1. 您的收藏集现已从列表中删除。

## 将内容添加到收藏集 {#adding-content-to-collections}

收藏集本质上是一类相关内容。 它们将文章、横幅等内容收集到定义应用程序导航结构的包中。 收藏集可嵌套。

>[!NOTE]
>
>在将内容添加到收藏集之前，必须将其上传到Mobile On-Demand。

收藏集本质上是一类相关内容：它们将文章、横幅等内容收集到一起，成为定义应用程序导航结构的包。 收藏集可嵌套。

1. 在Mobile中，从目录中选择您的Mobile On-Demand应用程序。
1. 选择之前上传的文章（或横幅/收藏集）
1. 从操作栏中选择“添加到”。
1. 从对话框中选择之前上传的收藏集。
1. 单击 **更新** 以向收藏集添加内容。

![chlimage_1-2](assets/chlimage_1-2.gif)

### 后续步骤 {#the-next-steps}

有关管理收藏集的详情，请参阅

* [管理横幅](/help/mobile/mobile-on-demand-managing-banners.md)
* [管理文章](/help/mobile/mobile-on-demand-managing-articles.md)
* [上传共享资源](/help/mobile/mobile-on-demand-shared-resources.md)
* [发布/取消发布内容](/help/mobile/mobile-on-demand-publishing-unpublishing.md)
* [使用Preflight预览](/help/mobile/aem-mobile-manage-ondemand-services.md)
