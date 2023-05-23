---
title: 延伸 [!DNL Adobe Experience Manager] 6.5使用Adobe Developer App Builder。
description: 延伸 [!DNL Adobe Experience Manager] 6.5使用Adobe Developer App Builder。
exl-id: 8221c2db-82d4-43df-ad38-e8e7831541ac
source-git-commit: cc1b86a15eb7ef45616bc9ea4f8aab4a28e74add
workflow-type: tm+mt
source-wordcount: '550'
ht-degree: 0%

---

# 延伸 [!DNL Adobe Experience Manager] 使用Adobe Developer App Builder {#extend-using-app-builder}

## 什麼是App Builder for AEM {#project-appbuilder}

新的Adobe Developer App Builder為開發人員提供擴充性架構，以便輕鬆擴充AEM功能。

App Builder提供統一的第三方擴充功能架構，可整合及建立可擴充Adobe Experience Manager的自訂體驗。 透過這個以Adobe基礎架構為基礎的完整擴充性架構，開發人員可以建立自訂微服務、擴充及整合跨Adobe解決方案和IT棧疊其他部分的Adobe Experience Manager。

App Builder讓客戶能在各種使用案例中輕鬆擴充Adobe Experience Manager：

* 中介軟體擴充性 — 將外部系統與建置自訂聯結器的Adobe應用程式連線，或利用預先建立的整合套件。
* 核心服務擴充性 — 透過自訂功能和商業邏輯擴充預設行為，進而擴充核心應用程式功能。
* 使用者體驗擴充性 — 擴充核心體驗以支援業務需求，或建立客戶專屬的數位財產、店面和後台應用程式。

自2020年夏季起，企業客戶和合作夥伴即可透過我們的開發人員預覽版使用App Builder。 App Builder正式發行(GA)日期排定於2021年12月。 我們歡迎開發人員透過我們的 [試用方案](https://adobe.ly/appbuilder-trial).

>[!NOTE]
>
>對於想要運用App Builder的AEMas a Cloud Service客戶，請前往 [使用Adobe Developer App Builder延伸Adobe Experience Manager as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/configuring-and-extending/app-builder.html).

## 架构 {#architecture}

Adobe Developer App Builder不是現成可用的解決方案，而是提供通用、一致、標準化的開發平台，用於擴充Adobe雲端解決方案(例如AEM)，包括：

* Adobe Developer Console — 適用於自訂微服務和擴充功能開發，可讓開發人員在存取建立外掛程式和整合所需的所有工具和API時，建立和管理專案。
* 開發人員工具 — 開放原始碼工具、SDK和程式庫，讓開發人員可輕鬆建立自訂擴充功能和整合。 使用React Spectrum (Adobe的UI工具組)，讓所有Adobe應用程式擁有一個通用UI。
* 服務 — 用於在我們的無伺服器平台上託管基礎結構的I/O執行階段，以及用於事件式整合的I/O事件。 我們也提供立即可用的資料與檔案儲存支援。
* Adobe Experience Cloud — 開發人員可以提交擴充功能和整合內容，以便在其Experience Cloud組織中發佈。接著，系統管理員可以檢閱、管理和核准這些擴充功能。 發佈後，您的自訂App Builder擴充功能和工具可與其他Adobe Experience Cloud應用程式一併找到。

下圖說明在App Builder上建置的標準應用程式如何運用這些功能：

![架构](assets/appbuilder-architecture.jpg)

如需App Builder架構的詳細資訊，請參閱 [架構概述](https://www.adobe.io/app-builder/docs/guides/).

## 開始使用App Builder {#additional-resources}

為協助您開始使用App Builder，我們建立了一系列檔案來協助您開始使用：

* [App Builder入門](https://www.adobe.io/app-builder/docs/getting_started/)

## 繼續學習使用檔案 {#appbuilder-documentation}

App Builder為開發人員提供影片和檔案，包括指南，以及參考檔案，以協助您開始開發自己的自訂應用程式：

* [App Builder檔案](https://www.adobe.io/app-builder/docs/overview/)
* [App Builder影片](https://www.youtube.com/playlist?list=PLcVEYUqU7VRfDij-Jbjyw8S8EzW073F_o)

## 嘗試其中一個範例應用程式 {#appbuilder-codesamples}

準備好開始開發了嗎？ 我們提供許多範例應用程式，協助您快速上手：

* [Adobe Developer網站上的App Builder程式碼實驗室](https://www.adobe.io/app-builder/docs/resources/)

