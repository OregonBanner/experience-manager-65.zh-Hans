---
title: 自訂和擴充 [!DNL Assets]
description: 瞭解您可以自訂和擴充Asset Share和Asset Editor的方式，為使用者提供專門定製的介面和功能集。
contentOwner: AG
role: Developer
feature: Developer Tools
exl-id: 0271c528-23b0-4a3a-b5e8-5baf6cdeecc7
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 0%

---

# 自訂和擴充 [!DNL Assets] {#customizing-and-extending-assets}

Asset Editor是AdobeEnterprise Manager網站的使用者用來尋找、檢視及操控存放庫中數位資產的主要存取點。

作為 [!DNL Experience Manager] 開發人員，您可以透過多種方式自訂和擴充Asset Editor，為使用者提供量身打造的介面和功能集。

可以自訂或增強功能的下列方面：

* [擴充Asset Editor](asseteditorx.md)
* [擴充資產搜尋](searchx.md)
* [使用媒體處理常式和工作流程處理資產](media-handlers.md)
* [將資產與活動資料流整合](extending-activity-stream.md)
* [資產Proxy開發](proxy.md)
* [設定ImageMagick的最佳作法](best-practices-for-imagemagick.md)

## 自訂外觀 {#customizing-the-look-and-feel}

以下是可自訂的Asset Editor外觀與風格：

* 標誌：您可以將自己組織的標誌新增至介面。
* 顏色和字型：您可以變更介面中使用的顏色和字型。
* HTML代碼：如需更徹底的自訂，您可以變更定義介面的基礎HTML代碼。

## 自訂轉譯 {#customizing-renditions}

在 [!DNL Experience Manager Assets] 術語轉譯是資產出現的形式。 一般而言，特定資產可以有多個轉譯。 例如，全色影像可能有一個原始大小的轉譯，另一個是縮小大小轉譯，另一個是縮小並轉換為灰階。

您可以自訂特定資產可用的轉譯，並建立新的轉譯。
