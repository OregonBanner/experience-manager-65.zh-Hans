---
title: 管理收藏集
seo-title: 管理收藏集
description: 集合代表一个定义良好的存储桶，其中填充了适合封面主题的文章或横幅等内容。 可查看本页以了解更多信息。
seo-description: 集合代表一个定义良好的存储桶，其中填充了适合封面主题的文章或横幅等内容。 可查看本页以了解更多信息。
uuid: 1d2e9769-d2cc-4d43-a428-e962a51eb5d0
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: authoring-on-demand-services-app
discoiquuid: 64c6d198-983f-4a52-9c83-560206363868
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '824'
ht-degree: 2%

---


# 管理收藏集{#managing-collections}

>[!NOTE]
>
>Adobe建议对需要基于单页应用程序框架的客户端渲染（例如，React）的项目使用SPA编辑器。 [了解更多](/help/sites-developing/spa-overview.md).

内容管理操作是帮助在应用程序中创建和管理内容的构件。 对应用程序中的内容执行以下操作。

## 集合概述{#collections-overview}

集合表示定义良好的&#x200B;*存储桶*，其中填充了适合封面主题的文章或横幅等内容。

>[!NOTE]
>
>请参阅“在线帮助”中的以下资源，了解AEM Mobile应用程序中的以下主题：
>
>* [设计注意事项](https://helpx.adobe.com/digital-publishing-solution/help/design-app.html)
   >
   >
* [管理收藏集](https://helpx.adobe.com/digital-publishing-solution/help/creating-collections.html)

>



## 创建收藏集 {#creating-a-collection}

用于创建集合的常规工作流如下：

1. 从侧边栏中选择&#x200B;**移动**。
1. 从Mobile中，从目录中选择您的Mobile On-Demand应用程序。
1. 单击&#x200B;**管理集合**&#x200B;拼贴右上角的向下箭头。
1. 通过向导的每个步骤继续创建新文章。
1. 准备就绪后，单击&#x200B;**创建**。
1. 您的新文章显示在&#x200B;**管理集合**&#x200B;拼贴中。

![chlimage_1-1](assets/chlimage_1-1.gif)

## 导入新集合{#importing-a-new-collection}

现有移动点播内容可从移动点播下载（导入）到AEM。 这允许编辑和查看本地内容。

>[!NOTE]
>
>导入不包括图像。

导入新集合的工作流

1. 从Mobile中，从目录中选择您的Mobile On-Demand App。
1. 单击&#x200B;**管理集合**&#x200B;拼贴右上角的向下箭头，然后选择“导入集合”。
1. 单击对话框中的&#x200B;**导入集合**，然后单击关闭。
1. 您的Mobile On-Demand集合现在显示在&#x200B;**管理集合**&#x200B;拼贴中。

>[!CAUTION]
>
>必须先关联Mobile On-Demand连接。

## 编辑集合{#editing-a-collection}

使用内置的AEM拖放编辑器添加或更改文章。 可以添加／删除文本和图像等组件。 可以插入DAM资产中的图像。

编辑集合的工作流：

1. 从Mobile中，从目录中选择您的Mobile On-Demand应用程序。
1. 从&#x200B;**管理集合**&#x200B;拼贴中选择AEM源文章。
1. 单击列表视图中突出显示的集合以在内容编辑器中将其打开。
1. 使用内容编辑器拖动集合内容（手稿、图像、文本等）。

### 查看和编辑集合{#viewing-and-editing-the-metadata-within-a-collection}中的元数据

集合具有许多属性，如标题、说明和图像。 此操作用于视图和修改此类属性。 （可选）这些更改可在保存后上传到Mobile On-Demand。

视图/编辑集合的常规工作流：

1. 从Mobile中，从目录中选择您的Mobile On-Demand应用程序。
1. 从&#x200B;**管理集合**&#x200B;拼贴中选择集合。

1. 从操作栏中选择&#x200B;**属性**。
1. 视图该文章的所有可用元数据。
1. 根据需要编辑元数据，完成后单击&#x200B;**保存**。
1. （可选）立即将更改上传到Mobile On-Demand。

## 上传集合{#uploading-a-collection}

上传操作会复制选定内容并将其添加到Mobile On-Demand项目。 现有的移动点播内容将被新版本取代。

上传集合的常规工作流：

1. 从&#x200B;**Mobile**&#x200B;中，从目录中选择您的Mobile On-Demand应用程序。
1. 在&#x200B;**管理集合**&#x200B;拼贴中，选择要上传到Mobile On-Demand的文章。
1. 根据需要从列表视图添加更多集合。
1. 从操作栏中选择&#x200B;**上传**，然后在对话框中单击上传。
1. 您的集合现已上传到移动点播。

## 删除收藏集 {#deleting-a-collection}

此操作将从Mobile On-Demand中删除所选集合，也可以选择从本地AEM实例中删除。

用于删除集合的常规工作流：

1. 从Mobile中，从目录中选择您的Mobile On-Demand应用程序。
1. 在&#x200B;**管理集合**&#x200B;拼贴中选择要删除的文章。
1. 确保在列表中选中它（根据需要选择要删除的其他选项）。
1. 单击操作栏中的&#x200B;**删除**。
1. 检查您是否希望从AEM和Mobile On-Demand中删除。
1. 单击&#x200B;**删除**。
1. 您的集合现已从列表中删除。

## 将内容添加到集合{#adding-content-to-collections}

集合本质上是相关内容的类别。 他们将文章、横幅等内容收集到定义应用程序导航结构的包中。 集合可以嵌套。

>[!NOTE]
>
>内容必须先上传到Mobile On-Demand，然后才能添加到集合。

集合本质上是相关内容的类别:他们将文章、横幅等内容收集到定义应用程序导航结构的包中。 集合可以嵌套。

1. 从Mobile中，从目录中选择您的Mobile On-Demand应用程序。
1. 选择之前上传的文章（或横幅／集合）
1. 从操作栏中选择添加到。
1. 从对话框中选择以前上传的集合。
1. 单击&#x200B;**更新**&#x200B;以向集合添加内容。

![chlimage_1-2](assets/chlimage_1-2.gif)

### 后续步骤 {#the-next-steps}

在您了解管理集合时，请参阅

* [管理横幅](/help/mobile/mobile-on-demand-managing-banners.md)
* [管理文章](/help/mobile/mobile-on-demand-managing-articles.md)
* [上传共享资源](/help/mobile/mobile-on-demand-shared-resources.md)
* [发布／取消发布内容](/help/mobile/mobile-on-demand-publishing-unpublishing.md)
* [使用预检预览](/help/mobile/aem-mobile-manage-ondemand-services.md)
