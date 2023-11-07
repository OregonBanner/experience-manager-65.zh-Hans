---
title: 添加用于图形渲染的字体
seo-title: Adding Fonts for Graphic-Rendering
description: AEM允许您生成包含从内容中动态获取的文本的图形
seo-description: AEM lets you generate graphics incorporating text dynamically taken from your content
uuid: 67d9b10f-e986-4d29-bde2-10e08075fe17
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 6af48ef5-75e6-4b66-bc0d-ecf254b1c4ef
exl-id: 725c81d0-0258-4118-8b01-29fd7bcaf9b3
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 1%

---

# 添加用于图形渲染的字体{#adding-fonts-for-graphic-rendering}

AEM允许您生成包含从内容中动态获取的文本的图形。

为此，您还可以加载和使用自己的字体。

当前所有实施的Java平台支持 [TrueType](https://en.wikipedia.org/wiki/Truetype) 字体。

1. 打开CRXDE Lite并导航到您的项目应用程序文件夹：

   `/apps/<your-project>/`

1. 下 `/apps/<your-project>/` 创建节点：

   * **名称**：`fonts`
   * **类型**：`sling:Folder`

   保存所有更改。

1. 将字体文件复制到此文件夹中；例如，使用WebDAV。

   >[!NOTE]
   >
   >存储库中的字体文件必须具有后缀 `*.ttf` 或 `*.TTF`.

1. 更新 [OSGi配置](/help/sites-deploying/configuring-osgi.md) 之 [Day Commons GFX字体帮助程序](/help/sites-deploying/osgi-configuration-settings.md). 将路径添加到您的fonts文件夹；即 `/apps/<your-project>/fonts`.

1. 返回CRXDE Lite。 您现在应会看到 `.fontlist` 文件夹中包含导入字体的名称的节点。

   这些字体现在可以在Java API中使用。

有关如何在Java API中使用字体的完整详细信息，请参阅 [Java API的Font类的文档](https://download.oracle.com/javase/6/docs/api/java/awt/Font.html).
