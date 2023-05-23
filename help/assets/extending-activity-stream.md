---
title: 整合 [!DNL Assets] 使用活動資料流
description: 說明的錄製功能 [!DNL Experience Manager] 以及如何設定以記錄特定事件。
contentOwner: AG
role: Developer
feature: Asset Management
exl-id: 2a08a7c1-8be9-42d1-9983-f9c8b12ea4e8
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '267'
ht-degree: 0%

---

# 整合 [!DNL Assets] 使用活動資料流 {#integrating-assets-with-activity-stream}

[!DNL Adobe Experience Manager Assets] 使用者可執行許多動作，例如建立、上傳和刪除資產。 這些動作可以記錄下來，這樣您就可以提供使用者已完成動作的歷史記錄。 本節說明的錄製功能 [!DNL Experience Manager] 以及如何設定 [!DNL Experience Manager] 以記錄特定事件。

## 效能考量事項和預設行為 {#performance-considerations-and-default-behavior}

例如，執行大量匯入時，這項整合可能會耗用CPU和磁碟空間。 基於這些原因， [!DNL Assets] 預設會停用與活動資料流的整合。

## 支援的動作事件 {#supported-action-events}

可以將下列事件設定為記錄：

* 授權已接受（已接受）
* 已建立的資產(ASSET_CREATED)
* 資產已移動(ASSET_MOVED)
* 資產已移除(ASSET_REMOVED)
* 授權已拒絕（已拒絕）
* 資產已下載（已下載）
* 資產版本設定（版本設定）
* 資產版本已還原（已還原）
* 資產中繼資料(METADATA_UPDATED)
* 資產已發佈至外部系統(PUBLISHED_EXTERNAL)
* 資產的原始更新(ORIGINAL_UPDATED)
* 資產轉譯已更新(RENDITION_UPDATED)
* 資產轉譯已移除(RENDITION_REMOVED)
* 子資產已更新(SUBASSET_UPDATED)
* 子資產已移除(SUBASSET_REMOVED)

## 設定 [!DNL Assets] 事件記錄 {#configuring-aem-assets-events-recording}

此 [網頁主控台](/help/sites-deploying/configuring-osgi.md) 提供「資產事件記錄器」調整的存取權。 若要設定「資產事件記錄器」，請依照下列步驟進行：

1. 導覽至 **[!UICONTROL 網頁主控台]**

1. 按一下 **[!UICONTROL 設定]**.

1. 按兩下 **[!UICONTROL Day CQ DAM事件記錄器]**.

1. Check **[!UICONTROL 啟用此服務]**.

1. 檢查哪一個 **[!UICONTROL 事件型別]** 您想要記錄在使用者活動資料流中。

1. 单击“**[!UICONTROL 保存]**”。

## 讀取記錄的事件 {#reading-recorded-events}

記錄的事件會儲存為活動。 您可以使用以下程式設計方式閱讀這些檔案： [ActivityManager API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/activitystreams/ActivityManager.html).
