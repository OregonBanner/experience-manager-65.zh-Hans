---
title: 搭配使用者端裝置畫素比使用智慧型影像
description: 瞭解如何透過Dynamic Media在Adobe Experience Manager as a Cloud Service中將使用者端裝置畫素比與智慧型影像搭配使用。
role: Admin,User
exl-id: e38f522a-242a-4ea9-a866-d8d129950831
source-git-commit: c8682118f15132063073df5cdc2b576b6e62a0c8
workflow-type: tm+mt
source-wordcount: '323'
ht-degree: 0%

---

# 關於使用使用者端裝置畫素比(DPR)的智慧型影像 {#client-side-dpr}

目前的智慧型影像解決方案是使用使用者代理字串來判斷所使用的裝置型別（桌上型電腦、平板電腦、行動裝置等）。

裝置偵測功能（以使用者代理字串為基礎的DPR）通常不準確，尤其是對Apple裝置而言。 此外，每當新裝置啟動時，都必須驗證該裝置。

使用者端DPR可為您提供100%正確的值，且適用於任何裝置，不論是Apple或任何其他啟動的新裝置。

## 使用使用者端DPR代碼

**伺服器端轉譯的應用程式**

1. 載入服務背景工作程式初始(`srvinit.js`)在HTML頁面的標頭區段中加入下列指令碼：

   ```javascript
   <script type="text/javascript" src="srvinit.js"></script>
   ```

   Adobe建議您載入此指令碼 _早於_ 任何其他指令碼，以便service worker立即開始初始化。

1. 在HTML頁面內文區段的頂端加入下列DPR影像標籤程式碼：

   ```html
   <img src="aem_dm_dpr_1x.jpg" style="width:1px;height:1px;display:none"
       srcset="aem_dm_dpr_1x.jpg 1x, aem_dm_dpr_1.1x.jpg 1.1x, aem_dm_dpr_1.2x.jpg 1.2x, aem_dm_dpr_1.3x.jpg 1.3x, aem_dm_dpr_1.4x.jpg 1.4x, aem_dm_dpr_1.5x.jpg 1.5x, aem_dm_dpr_1.6x.jpg 1.6x,          aem_dm_dpr_1.7x.jpg 1.7x, aem_dm_dpr_1.8x.jpg 1.8x, aem_dm_dpr_1.9x.jpg 1.9x,
       aem_dm_dpr_2x.jpg 2x, aem_dm_dpr_2.1x.jpg 2.1x, aem_dm_dpr_2.2x.jpg 2.2x, aem_dm_dpr_2.3x.jpg 2.3x, aem_dm_dpr_2.4x.jpg 2.4x, aem_dm_dpr_2.5x.jpg 2.5x, aem_dm_dpr_2.6x.jpg 2.6x, aem_dm_dpr_2.7x.jpg 2.7x, aem_dm_dpr_2.8x.jpg 2.8x, aem_dm_dpr_2.9x.jpg 2.9x,
       aem_dm_dpr_3x.jpg 3x, aem_dm_dpr_3.1x.jpg 3.1x, aem_dm_dpr_3.2x.jpg 3.2x, aem_dm_dpr_3.3x.jpg 3.3x, aem_dm_dpr_3.4x.jpg 3.4x, aem_dm_dpr_3.5x.jpg 3.5x, aem_dm_dpr_3.6x.jpg 3.6x, aem_dm_dpr_3.7x.jpg 3.7x, aem_dm_dpr_3.8x.jpg 3.8x, aem_dm_dpr_3.9x.jpg 3.9x,
       aem_dm_dpr_4x.jpg 4x, aem_dm_dpr_4.1x.jpg 4.1x, aem_dm_dpr_4.2x.jpg 4.2x, aem_dm_dpr_4.3x.jpg 4.3x, aem_dm_dpr_4.4x.jpg 4.4x, aem_dm_dpr_4.5x.jpg 4.5x, aem_dm_dpr_4.6x.jpg 4.6x, aem_dm_dpr_4.7x.jpg 4.7x, aem_dm_dpr_4.8x.jpg 4.8x, aem_dm_dpr_4.9x.jpg 4.9x,
       aem_dm_dpr_5x.jpg 5x">
   ```

   您必須包含此DPR影像標籤代碼 _早於_ HTML頁面中的所有靜態影像。

**使用者端轉譯的應用程式**

1. 在HTML頁面的標頭區段中加入下列DPR指令碼：

   ```javascript
   <script type="text/javascript" src="srvinit.js"></script>
   <script type="text/javascript" src="dprImageInjection.js"></script>
   ```

   您可以將兩個DPR指令碼合併為一個，以避免多個網路請求。

   Adobe建議您載入這些指令碼 _早於_ HTML頁面中的任何其他指令碼。
Adobe也建議您將應用程式Bootstrap在diffHTML標籤下，而不是在body元素下。 原因在於 `dprImageInjection.js` 動態插入HTML頁面內文區段頂端的影像標籤。

## JavaScript檔案下載 {#client-side-dpr-script}

下載中的下列JavaScript檔案僅供範例參考之用。 如果您打算在HTML頁面中使用這些檔案，請務必編輯每個檔案的程式碼，以符合您自己的需求。

* `dprImageInjection.js`
* `srvinit.js`
* `srvwrk.js`

[JavaScript檔案下載](/help/assets/assets-dm/aem-dynamicmedia-smartimaging-dpr.zip)

>[!MORELIKETHIS]
>
>* [智能图像处理](/help/assets/imaging-faq.md)

