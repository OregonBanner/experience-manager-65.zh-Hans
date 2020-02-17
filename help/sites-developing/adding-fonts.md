---
title: 为图形渲染添加字体
seo-title: 为图形渲染添加字体
description: AEM允许您生成包含从内容动态获取的文本的图形
seo-description: AEM允许您生成包含从内容动态获取的文本的图形
uuid: 67d9b10f-e986-4d29-bde2-10e08075fe17
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 6af48ef5-75e6-4b66-bc0d-ecf254b1c4ef
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 为图形渲染添加字体{#adding-fonts-for-graphic-rendering}

AEM允许您生成包含从内容动态获取的文本的图形。

为此，您还可以加载和使用您自己的字体。

目前，所有Java平台实现都支持 [TrueType字体](https://en.wikipedia.org/wiki/Truetype) 。

1. 打开CRXDE lite并导航到您的项目应用程序文件夹：

   `/apps/<your-project>/`

1. 在“ `/apps/<your-project>/` 创建新节点”下：

   * **名称**: `fonts`
   * **类型**: `sling:Folder`
   保存所有更改。

1. 将字体文件复制到该文件夹中；例如，使用WebDAV。

   >[!NOTE]
   >
   >存储库中的字体文件必须具有后缀 `*.ttf` 或 `*.TTF`。

1. 更新 [Day Commons](/help/sites-deploying/configuring-osgi.md) GFX [Font Helper的OSGi配置](/help/sites-deploying/osgi-configuration-settings.md)。 添加字体文件夹的路径；即 `/apps/<your-project>/fonts`.

1. 返回CRXDE Lite。 您现在应该会在您 `.fontlist` 的文件夹中看到一个包含导入字体名称的节点。

   这些字体现在可以在Java API中使用。

有关如何将字体与Java API一起使用的完整详细信息，请参 [阅Java API的Font类的文档](https://download.oracle.com/javase/6/docs/api/java/awt/Font.html)。

