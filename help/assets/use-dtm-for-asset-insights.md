---
title: 透過DTM啟用資產分析
description: 瞭解如何使用Adobe動態Tag Management (DTM)來啟用Assets Insights。
contentOwner: AG
role: User, Admin
feature: Asset Insights,Asset Reports
exl-id: 80e8f84e-3235-4212-9dcd-6acdb9067893
source-git-commit: afc72fb6b324cf2e0ad8168f783d9c1a6f96c614
workflow-type: tm+mt
source-wordcount: '647'
ht-degree: 1%

---

# 透過DTM啟用資產分析 {#enable-asset-insights-through-dtm}

Adobe Dynamic Tag Management是可啟用數位行銷工具的工具。 Adobe Analytics客戶可免費使用。 您可以自訂追蹤程式碼，讓協力廠商CMS解決方案能夠使用Assets Insights，也可以使用DTM插入Assets Insights標籤。 僅支援並為影像提供深入分析。

>[!CAUTION]
>
>AdobeDTM已過時，改用 [!DNL Adobe Experience Platform] 很快就會到達 [生命週期結束](https://medium.com/launch-by-adobe/dtm-plans-for-a-sunset-3c6aab003a6f). Adobe建議您 [use [!DNL Adobe Experience Platform] 用於資產分析](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/advanced/asset-insights-launch-tutorial.html).

執行這些步驟，透過DTM啟用Assets Insights。

1. 按一下Experience Manager標誌，然後前往 **[!UICONTROL 工具]** > **[!UICONTROL 資產]** > **[!UICONTROL Insights設定]**.
1. [使用DTMCloud Service設定Experience Manager部署](/help/sites-administering/dtm.md)

   API權杖應在您登入後提供 [https://dtm.adobe.com](https://dtm.adobe.com/) 和造訪 **[!UICONTROL 帳戶設定]** 在使用者設定檔中。 從Assets Insights的角度來看，不需要執行此步驟，因為Experience Manager Sites與Assets Insights的整合仍在進行中。

1. 登入 [https://dtm.adobe.com](https://dtm.adobe.com/)，並視需要選取公司。
1. 建立或開啟現有的Web屬性

   * 選取 **[!UICONTROL Web屬性]** 標籤，然後按一下 **[!UICONTROL 新增屬性]**.

   * 視需要更新欄位，然後按一下 **[!UICONTROL 建立屬性]**. 另請參閱 [檔案](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html?lang=zh-Hans).

   ![建立編輯Web屬性](assets/Create-edit-web-property.png)

1. 在 **[!UICONTROL 規則]** 索引標籤，選取 **[!UICONTROL 頁面載入規則]** ，然後按一下 **[!UICONTROL 建立新規則]**.

   ![chlimage_1-58](assets/chlimage_1-194.png)

1. 展開 **[!UICONTROL JavaScript /第三方標籤]**. 然後按一下 **[!UICONTROL 新增指令碼]** 在 **[!UICONTROL 順序HTML]** 標籤以開啟Script對話方塊。

   ![chlimage_1-59](assets/chlimage_1-195.png)

1. 按一下Experience Manager標誌，然後前往 **[!UICONTROL 工具]** > **[!UICONTROL 資產]**.
1. 按一下 **[!UICONTROL 前瞻分析頁面追蹤器]**，複製追蹤器程式碼，然後貼到您在步驟6開啟的指令碼對話方塊中。 保存更改。

   >[!NOTE]
   >
   >* `AppMeasurement.js` 「 」已移除。 應透過DTM的Adobe Analytics工具提供。
   >* 對的呼叫 `assetAnalytics.dispatcher.init()` 「 」已移除。 DTM的Adobe Analytics工具載入完成後，應該就會呼叫函式。
   >* 根據託管Assets Insights頁面追蹤器的位置(例如Experience Manager、CDN等)，指令碼來源的來源可能需要變更。
   >* 對於Experience Manager託管的頁面追蹤器，來源應該指向使用Dispatcher執行個體主機名稱的發佈執行個體。


1. 访问 `https://dtm.adobe.com`. 按一下 **[!UICONTROL 概觀]** 在web屬性中並按一下 **[!UICONTROL 新增工具]** 或開啟現有的Adobe Analytics工具。 建立工具時，您可以設定 **[!UICONTROL 設定方法]** 至 **[!UICONTROL 自動]**.

   ![新增Adobe Analytics工具](assets/Add-Adobe-Analytics-Tool.png)

   視情況選取測試/生產報表套裝。

1. 展開 **[!UICONTROL 程式庫管理]**，並確保 **[!UICONTROL 載入程式庫於]** 設為 **[!UICONTROL 頁面頂端]**.

   ![chlimage_1-61](assets/chlimage_1-197.png)

1. 展開 **[!UICONTROL 自訂頁面程式碼]**，然後按一下 **[!UICONTROL 開啟編輯器]**.

   ![chlimage_1-62](assets/chlimage_1-198.png)

1. 在視窗中貼上下列程式碼：

   ```Java
   var sObj;
   
   if (arguments.length > 0) {
     sObj = arguments[0];
   } else {
     sObj = _satellite.getToolsByType('sc')[0].getS();
   }
   _satellite.notify('in assetAnalytics customInit');
   (function initializeAssetAnalytics() {
     if ((!!window.assetAnalytics) && (!!assetAnalytics.dispatcher)) {
       _satellite.notify('assetAnalytics ready');
       /** NOTE:
           Copy over the call to 'assetAnalytics.dispatcher.init()' from Assets Pagetracker
           Be mindful about changing the AppMeasurement object as retrieved above.
       */
       assetAnalytics.dispatcher.init(
             "",  /** RSID to send tracking-call to */
             "",  /** Tracking Server to send tracking-call to */
             "",  /** Visitor Namespace to send tracking-call to */
             "",  /** listVar to put comma-separated-list of Asset IDs for Asset Impression Events in tracking-call, e.g. 'listVar1' */
             "",  /** eVar to put Asset ID for Asset Click Events in, e.g. 'eVar3' */
             "",  /** event to include in tracking-calls for Asset Impression Events, e.g. 'event8' */
             "",  /** event to include in tracking-calls for Asset Click Events, e.g. 'event7' */
             sObj  /** [OPTIONAL] if the webpage already has an AppMeasurement object, include the object here. If unspecified, Pagetracker Core shall create its own AppMeasurement object */
             );
       sObj.usePlugins = true;
       sObj.doPlugins = assetAnalytics.core.updateContextData;
       assetAnalytics.core.optimizedAssetInsights();
     }
     else {
       _satellite.notify('assetAnalytics not available. Consider updating the Custom Page Code', 4);
     }
   })();
   ```

   * DTM中的頁面載入規則僅包含 `pagetracker.js` 程式碼。 任何 `assetAnalytics` 會將欄位視為預設值的覆寫。 預設不需要。
   * 程式碼呼叫 `assetAnalytics.dispatcher.init()` 確認之後 `_satellite.getToolsByType('sc')[0].getS()` 已初始化且 `assetAnalytics,dispatcher.init` 可用。 因此，您可以略過在步驟11中新增。
   * 如前瞻分析頁面追蹤器程式碼內的註解所示(**[!UICONTROL 「工具>資產>前瞻分析頁面追蹤器」]**)，則頁面追蹤器不會建立 `AppMeasurement` 物件、前三個引數（RSID、追蹤伺服器和訪客名稱空間）無關。 傳遞空字串以反白標示此內容。\
      其餘引數對應至「見解設定」頁面中已設定的專案(**[!UICONTROL 「工具>資產>前瞻分析設定」]**)。
   * 透過查詢來擷取AppMeasurement物件 `satelliteLib` 用於所有可用的SiteCatalyst引擎。 如果已設定多個標籤，請適當地變更陣列選擇器的索引。 陣列中的專案會根據DTM介面中可用的SiteCatalyst工具排序。

1. 儲存並關閉程式碼編輯器視窗，然後將變更儲存在工具設定中。
1. 在 **[!UICONTROL 核准]** 索引標籤中，核准兩個擱置的核准。 DTM標籤已準備好插入您的網頁。
