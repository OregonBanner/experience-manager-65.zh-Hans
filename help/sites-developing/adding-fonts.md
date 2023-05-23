---
title: 新增用於圖形演算的字型
seo-title: Adding Fonts for Graphic-Rendering
description: AEM可讓您產生結合動態擷取自內容之文字的圖形
seo-description: AEM allows you to generate graphics incorporating text dynamically taken from your content
uuid: 67d9b10f-e986-4d29-bde2-10e08075fe17
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 6af48ef5-75e6-4b66-bc0d-ecf254b1c4ef
exl-id: 725c81d0-0258-4118-8b01-29fd7bcaf9b3
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '183'
ht-degree: 1%

---

# 新增用於圖形演算的字型{#adding-fonts-for-graphic-rendering}

AEM可讓您產生結合動態擷取自內容的文字的圖形。

要執行此操作，您也可以載入並使用您自己的字型。

目前所有Java平台支援的實作 [TrueType](https://en.wikipedia.org/wiki/Truetype) 字型。

1. 開啟CRXDE Lite並導覽至您的專案應用程式資料夾：

   `/apps/<your-project>/`

1. 下 `/apps/<your-project>/` 建立新節點：

   * **名称**: `fonts`
   * **类型**: `sling:Folder`

   儲存所有變更。

1. 將字型檔案複製到此資料夾；例如，使用WebDAV。

   >[!NOTE]
   >
   >存放庫中的字型檔案必須具有字尾 `*.ttf` 或 `*.TTF`.

1. 更新 [OSGi設定](/help/sites-deploying/configuring-osgi.md) 之 [Day Commons GFX Font Helper](/help/sites-deploying/osgi-configuration-settings.md). 將路徑新增至字型資料夾；即 `/apps/<your-project>/fonts`.

1. 返回CRXDE Lite。 您現在應該會看到 `.fontlist` 節點（包含匯入字型名稱）。

   這些字型現已可在Java API中使用。

如需如何搭配Java API使用字型的完整詳細資訊，請參閱 [Java API的字型類別檔案](https://download.oracle.com/javase/6/docs/api/java/awt/Font.html).
