---
title: 全景图像
description: 瞭解如何在Dynamic Media中使用全景影像。
uuid: ced3e5bd-93c8-4d5f-a397-1380d4d0a5e7
contentOwner: Rick Brough
topic-tags: dynamic-media
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
content-type: reference
discoiquuid: 632a9074-b747-49a1-a57d-1f42bba1f4e9
docset: aem65
feature: Panoramic Images,Asset Management
role: User, Admin
exl-id: 4d6fbeb1-94db-4154-9e41-b76033fb4398
source-git-commit: 363e5159d290ecfbf4338f6b9793e11b613389a5
workflow-type: tm+mt
source-wordcount: '574'
ht-degree: 0%

---

# 全景影像{#panoramic-images}

本節說明如何使用「全景影像」檢視器來轉譯球面全景影像，以獲得房間、屬性、位置或橫向的360度沈浸式檢視體驗。

另請參閱 [管理檢視器預設集](/help/assets/managing-viewer-presets.md).

![panoramic-image2](assets/panoramic-image2.png)

## 上傳資產以與全景影像檢視器搭配使用 {#uploading-assets-for-use-with-the-panoramic-image-viewer}

若要讓上傳的資產符合您要與全景影像檢視器一起使用的球面全景影像資格，資產必須具備下列其中一項或兩項條件：

* 外觀比例為2。
您可以在下列位置覆寫CRXDE Lite為2的預設外觀比例設定：
   `/conf/global/settings/cloudconfigs/dmscene7/jcr:content`

* 以關鍵字標籤 `equirectangular`，或 `spherical`和 `panorama`，或 `spherical` 和 `panoramic`. 另請參閱 [使用標籤](/help/sites-authoring/tags.md).

外觀比例和關鍵字條件都適用於資產詳細資訊頁面和 `Panoramic Media` wcm元件。

若要上傳資產以與全景影像檢視器搭配使用，請參閱 [上傳資產](/help/assets/manage-assets.md#uploading-assets).

## 設定Dynamic Media Classic {#configuring-dynamic-media-classic-scene}

為了讓「全景影像」檢視器在Adobe Experience Manager中正常運作，請將「全景影像」檢視器預設集與Dynamic Media Classic和Dynamic Media Classic專屬的中繼資料同步，以便在JCR中更新檢視器預設集。 若要完成此同步，請依照以下方式設定Dynamic Media Classic：

1. 開啟 [Dynamic Media Classic案頭應用程式](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started)，然後登入您的帳戶。

1. 在頁面的右上角附近，選取 **[!UICONTROL 設定]** > **[!UICONTROL 應用程式設定]** > **[!UICONTROL 發佈設定]** > **[!UICONTROL 影像伺服器]**.
1. 在「影像伺服器發佈」頁面上，從 **[!UICONTROL 發佈內容]** 頂端附近的下拉式功能表，選取 **[!UICONTROL 影像伺服]**.

1. 在相同「影像伺服器發佈」頁面上，找到標題 **[!UICONTROL 請求屬性]**.
1. 在「請求屬性」標題下，找出 **[!UICONTROL 回覆影像大小限制]**. 然後，在關聯的「寬度」和「高度」欄位中，增加全景影像的最大允許影像大小。

   Dynamic Media Classic有25,000,000畫素的限制。 2:1外觀比例的影像最大允許大小為7000 x 3500。 不過，若是典型的桌上型電腦熒幕，4096 x 2048畫素就足夠了。

   >[!NOTE]
   >
   >僅支援在最大允許影像大小範圍內的影像。 對超過大小限制的影像的請求會產生403回應。

1. 在「請求屬性」標題下，執行下列動作：

   * 將請求模糊化模式設定為 **[!UICONTROL 已停用]**.
   * 將請求鎖定模式設定為 **[!UICONTROL 已停用]**.

   這些設定是使用 `Panoramic Media` WCM元件Experience Manager。

1. 在「影像伺服器發佈」頁面底部，選取左側 **[!UICONTROL 儲存]**.

1. 在右下角，選取 **[!UICONTROL 關閉]**.

### 疑難排解全景媒體WCM元件 {#troubleshooting-the-panoramic-media-wcm-component}

如果您將影像拖放到WCM的全景媒體元件中，且元件預留位置已收合，請疑難排解下列問題：

* 如果您遇到403 Forbidden錯誤，可能是因為要求的影像大小太大。 檢閱 **[!UICONTROL 回覆影像大小限制]** 中的設定 [設定Dynamic Media Classic](/help/assets/panoramic-images.md#configuring-dynamic-media-classic-scene).

* 對於頁面上顯示的「資產鎖定無效」或「剖析錯誤」，請檢查「請求模糊化模式」和「請求鎖定模式」，以確保它們已停用。
* 對於汙染的畫布錯誤，請為影像資產的先前請求設定規則集定義檔案路徑和CTN無效。
* 如果影像請求後大小超過支援的限制時，影像品質變低，請檢查 **[!UICONTROL JPEG編碼屬性>品質]** 設定不是空的。 的典型設定 **[!UICONTROL 品質]** 欄位是 `95`. 您可以在「影像伺服器發佈」頁面上找到設定。 若要存取頁面，請參閱 [設定Dynamic Media Classic](/help/assets/panoramic-images.md#configuring-dynamic-media-classic-scene).

## 預覽全景影像 {#previewing-panoramic-images}

另請參閱 [預覽資產](/help/assets/previewing-assets.md).

## 發佈全景影像 {#publishing-panoramic-images}

另請參閱 [發佈資產](/help/assets/publishing-dynamicmedia-assets.md).
