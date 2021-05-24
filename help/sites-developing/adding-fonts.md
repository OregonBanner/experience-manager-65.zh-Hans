---
title: 添加用于图形渲染的字体
seo-title: 添加用于图形渲染的字体
description: AEM允许您生成图形，其中包含从内容中动态提取的文本
seo-description: AEM允许您生成图形，其中包含从内容中动态提取的文本
uuid: 67d9b10f-e986-4d29-bde2-10e08075fe17
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 6af48ef5-75e6-4b66-bc0d-ecf254b1c4ef
exl-id: 725c81d0-0258-4118-8b01-29fd7bcaf9b3
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '200'
ht-degree: 1%

---

# 为图形渲染添加字体{#adding-fonts-for-graphic-rendering}

AEM允许您生成图形，其中包含从内容中动态提取的文本。

为此，您还可以加载和使用您自己的字体。

目前，所有Java平台实施都支持[TrueType](https://en.wikipedia.org/wiki/Truetype)字体。

1. 打开CRXDE Lite并导航到您的项目应用程序文件夹：

   `/apps/<your-project>/`

1. 在`/apps/<your-project>/`下创建新节点：

   * **名称**: `fonts`
   * **类型**: `sling:Folder`

   保存所有更改。

1. 将字体文件复制到该文件夹中；例如，使用WebDAV。

   >[!NOTE]
   >
   >存储库中的字体文件必须具有后缀`*.ttf`或`*.TTF`。

1. 更新[](/help/sites-deploying/configuring-osgi.md)[Day Commons GFX Font Helper](/help/sites-deploying/osgi-configuration-settings.md)的OSGi配置。 添加字体文件夹的路径；例如`/apps/<your-project>/fonts`。

1. 返回CRXDE Lite。 现在，您应会在文件夹中看到一个`.fontlist`节点，其中包含导入字体的名称。

   这些字体现在可以在Java API中使用。

有关如何将字体与Java API结合使用的完整详细信息，请参阅[有关Java API](https://download.oracle.com/javase/6/docs/api/java/awt/Font.html)字体类的文档。
