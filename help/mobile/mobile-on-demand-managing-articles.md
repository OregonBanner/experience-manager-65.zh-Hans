---
title: 管理文章
seo-title: 管理文章
description: 可查看本页以了解有关创建和管理文章的信息。
seo-description: 可查看本页以了解有关创建和管理文章的信息。
uuid: 72b86cd7-3016-41b6-a001-9dce4084e9db
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: authoring-on-demand-services-app
discoiquuid: b46058f9-4691-4fba-a656-0f8507875a79
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '690'
ht-degree: 1%

---


# 管理文章{#managing-articles}

>[!NOTE]
>
>Adobe建议对需要基于单页应用程序框架的客户端渲染（例如，React）的项目使用SPA编辑器。 [了解更多](/help/sites-developing/spa-overview.md).

内容管理操作是帮助在应用程序中创建和管理文章的构件。 对应用程序中的文章执行以下操作。

## 文章概述{#articles-overview}

文章表示基于文本和图稿以传递信息。

>[!NOTE]
>
>请参阅“在线帮助”中的以下资源，了解AEM Mobile应用程序中的以下主题：
>
>* [设计注意事项](https://helpx.adobe.com/digital-publishing-solution/help/design-app.html)
   >
   >
* [管理文章](https://helpx.adobe.com/digital-publishing-solution/help/creating-articles.html)

>



## 创建文章{#creating-an-article}

创建文章的常规工作流如下：

1. 从侧边栏中选择&#x200B;**移动**。
1. 从Mobile中，从目录中选择您的Mobile On-Demand应用程序。
1. 单击&#x200B;**管理文章**&#x200B;拼贴右上角的向下箭头。
1. 选择文章模板，然后单击&#x200B;**下一步**。
1. 通过向导的每个步骤继续创建新文章。
1. 准备就绪后，单击&#x200B;**创建**。
1. 您的新文章显示在&#x200B;**管理文章**&#x200B;拼贴中。

## 导入新文章{#importing-a-new-article}

现有移动点播内容可从移动点播下载（导入）到AEM。 这允许编辑和查看本地内容。

>[!NOTE]
>
>导入不包括图像。

导入新文章的工作流

1. 从Mobile中，从目录中选择您的Mobile On-Demand App。
1. 单击&#x200B;**管理文章**&#x200B;拼贴右上角的向下箭头，然后选择“导入文章”。
1. 单击对话框上的&#x200B;**导入文章**，然后单击关闭。
1. 您的Mobile On-Demand文章现在显示在&#x200B;**管理文章**&#x200B;拼贴中。

>[!CAUTION]
>
>必须先关联Mobile On-Demand连接。

![chlimage_1-3](assets/chlimage_1-3.gif)

## 编辑文章{#editing-an-article}

使用内置的AEM拖放编辑器添加或更改文章。 可以添加／删除文本和图像等组件。 可以插入DAM资产中的图像。

>[!CAUTION]
>
>只有在AEM中创建的文章才能在编辑器中打开。

编辑文章的工作流：

1. 从Mobile中，从目录中选择您的Mobile On-Demand应用程序。
1. 从&#x200B;**管理文章**&#x200B;拼贴中选择AEM源文章。
1. 单击列表视图中突出显示的文章以在内容编辑器中打开它。
1. 使用内容编辑器拖动文章内容（手稿、图像、文本等）。

### 查看和编辑文章{#viewing-and-editing-the-metadata-within-an-article}中的元数据

诸如文章、横幅等内容具有许多属性，如标题、描述和图像。 此操作用于视图和修改此类属性。 （可选）这些更改可在保存后上传到Mobile On-Demand。

视图/编辑文章的常规工作流：

1. 从Mobile中，从目录中选择您的Mobile On-Demand应用程序。
1. 从&#x200B;**管理文章**&#x200B;拼贴中选择文章。

1. 从操作栏中选择&#x200B;**视图属性**。
1. 视图该文章的所有可用元数据。
1. 根据需要编辑元数据，完成后单击&#x200B;**保存**。
1. （可选）立即将更改上传到Mobile On-Demand。

## 上传文章{#uploading-an-article}

上传操作会复制选定内容并将其添加到Mobile On-Demand项目。 现有的移动点播内容将被新版本取代。

上传文章的常规工作流：

1. 从&#x200B;**Mobile**&#x200B;中，从目录中选择您的Mobile On-Demand应用程序。
1. 在&#x200B;**管理文章**&#x200B;拼贴中，选择要上传到Mobile On-Demand的文章。
1. 根据需要从列表视图添加更多文章。
1. 从操作栏中选择&#x200B;**上传**，然后在对话框中单击上传。
1. 您的文章现已上传到移动点播。

![chlimage_1-4](assets/chlimage_1-4.gif)

## 删除文章{#deleting-an-article}

此操作将从Mobile On-Demand中删除所选内容，也可以选择从本地AEM实例中删除。

用于删除文章的常规工作流：

1. 从Mobile中，从目录中选择您的Mobile On-Demand应用程序。
1. 在&#x200B;**管理文章**&#x200B;拼贴中选择要删除的文章。
1. 确保在列表中选中它（根据需要选择要删除的其他选项）。
1. 单击操作栏中的&#x200B;**删除**。
1. 检查您是否希望从AEM和Mobile On-Demand中删除。
1. 单击&#x200B;**删除**。
1. 您的文章现在从列表中删除。

![chlimage_1-5](assets/chlimage_1-5.gif)

### 后续步骤 {#the-next-steps}

在您了解管理文章之后，请参阅

* [管理横幅](/help/mobile/mobile-on-demand-managing-banners.md)
* [管理收藏集](/help/mobile/mobile-on-demand-managing-collections.md)
* [上传共享资源](/help/mobile/mobile-on-demand-shared-resources.md)
* [发布／取消发布内容](/help/mobile/mobile-on-demand-publishing-unpublishing.md)
* [使用预检预览](/help/mobile/aem-mobile-manage-ondemand-services.md)
