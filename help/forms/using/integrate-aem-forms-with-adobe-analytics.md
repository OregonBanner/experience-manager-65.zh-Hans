---
title: 如何將AEM Forms與Adobe Analytics整合？
description: AEM Forms與Adobe Analytics整合，以擷取和追蹤您發佈之表單的績效量度。
docset: aem65
exl-id: 030fe9f2-cd41-4290-b8a6-2f9ade6b5789
source-git-commit: 45ca98ffb68e1e31e2f45f352e86f5aa1b6f0f00
workflow-type: tm+mt
source-wordcount: '1806'
ht-degree: 0%

---

# 分析使用 [!DNL Adobe Launch] {#analyticsusingadobelaunch}

AEM Forms整合 [Adobe Analytics](https://experienceleague.adobe.com/docs/analytics-learn/tutorials/overview.html?lang=en) 可讓您擷取及追蹤已發佈表單的績效量度。 分析這些量度是為了讓業務使用者深入瞭解一般使用者行為，並最佳化資料擷取體驗。 您可以透過Adobe Analytics for Adaptive Forms擷取及追蹤已登入和未登入（匿名）使用者的行為。

您也可以使用Cloud Service框架執行分析。 如需如何將AEM Forms與Cloud Service架構整合的詳細資訊，請參閱 [使用Cloud Service架構的Analytics](/help/forms/using/configure-analytics-forms-documents.md). 使用Analytics Launch勝過Analytics使用AdobeCloud Service架構的主要優點在於，除了這些現成可用的事件外，您還可以定義自訂事件。 自訂事件是使用規則編輯器或客戶clientlibs定義，並對應至中的事件 [!DNL Adobe Analytics].

執行本文所述的動作後，您可以在中設定和檢視報表 [!DNL Adobe Analytics]，如下列影片所示：

>[!VIDEO](https://video.tv.adobe.com/v/337262)

您可以使用 [!DNL Adobe Analytics] 探索使用者在使用最適化表單時遇到的互動模式和問題。 開箱即用 [!DNL Adobe Analytics] 追蹤並儲存下列事件的相關資訊：

* **演算**：表單開啟次數。

* **提交**：表單提交次數。

* **放棄**：使用者未完成表單而離開的次數。

* **錯誤**：在面板和面板欄位上遇到的錯誤數。

* **說明**：使用者開啟面板說明及面板欄位的次數。

* **現場造訪**：使用者造訪表單中欄位的次數。

* **儲存**：使用者將表單儲存至Forms入口網站的次數。

除了這些現成可用的事件以外，您也可以定義自訂事件。

下圖說明在中檢視報表之前需要執行的動作 [!DNL Adobe Analytics]：

![Analytics概觀](/help/forms/using/assets/analyticsworkflow.png)

## 1.設定 [!DNL Adobe Analytics] {#Configure-adobe-analytics}

設定前 [!DNL Adobe Analytics]，建立：

* 要登入的Adobe ID [Adobe Experience Cloud](https://experience.adobe.com/#/home).
* A [報告套裝](https://experienceleague.adobe.com/docs/analytics/admin/manage-report-suites/new-report-suite/t-create-a-report-suite.html).


### 安裝AEM Forms和 [!DNL Adobe Analytics] 擴充功能 {#install-extensions}

執行以下步驟來設定AEM Forms和 [Adobe Analytics](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/analytics/overview.html) 擴充功能：

1. 登入Adobe Experience Cloud並為公司選取適當的名稱。

1. 點選 **[!UICONTROL 啟動/資料收集]** 並點選 **[!UICONTROL 前往啟動/資料收集]**.

1. 點選 **[!UICONTROL 新增屬性]** 並指定設定的名稱。

1. 指定網域名稱並點選 **[!UICONTROL 儲存]** 以儲存屬性。

1. 點選「標籤屬性」清單中可用的設定名稱。

1. 在 **[!UICONTROL 製作]** 區段，點選 **[!UICONTROL 擴充功能]**.

1. 點選 **[!UICONTROL 目錄]** 並點選 **[!UICONTROL 安裝]** 的 **[!UICONTROL Adobe Experience Manager Forms]** 副檔名。 **[!UICONTROL Adobe Experience Manager Forms]** 會顯示在中提供的已安裝擴充功能清單中 **已安裝** 標籤。

1. 點選 **[!UICONTROL 安裝]** 的 **[!UICONTROL Adobe Analytics]** 副檔名。
1. 在中選取報表套裝名稱 **[!UICONTROL 開發報表套裝]**， **[!UICONTROL 中繼報表套裝]**、和 **[!UICONTROL 產品報表套裝]** 下拉式清單並點選 **[!UICONTROL 儲存]** 以儲存擴充功能。

### 設定資料元素 {#configure-data-elements}

您可以在為事件建立的規則中，選取任何已設定的資料元素。 當最適化表單上發生事件時，AEM Forms會將這些資料元素傳送至 [!DNL Adobe Analytics].

安裝後 **[!UICONTROL Adobe Experience Manager Forms]** 擴充功能上，您可以建立下列資料元素：

<table>
 <tbody>
  <tr>
   <td>欄位名稱</th>
   <td>欄位標題</th>
   <td>FormInstance</th>
  </tr>
  <tr>
   <td>FormName<br /> </td>
   <td>表單標題<br /> </td>
   <td>頁面名稱</td>
  </tr>
  <tr>
   <td>PageURL<br /> </td>
   <td>面板標題<br /> </td>
   <td>逗留時間</td>
  </tr>
 </tbody>
</table>

執行以下步驟來設定資料元素：

1. 在 **[!UICONTROL 製作]** 區段，點選 **[!UICONTROL 資料元素]**.

1. 點選 **[!UICONTROL 建立新資料元素]**.

1. 指定資料元素的名稱。 例如，FormTitle資料元素型別的表單標題。

1. 指定 **[!UICONTROL Adobe Experience Manager Forms]** 作為擴充功能名稱。

1. 選取 **[!UICONTROL 資料元素型別]**.

1. 點選 **[!UICONTROL 儲存]** 以儲存資料元素。

   >[!VIDEO](https://video.tv.adobe.com/v/337472)

### 設定規則 {#configure-rules}

執行以下步驟，根據下列專案建立規則： **[!UICONTROL Adobe Experience Manager Forms]** 副檔名：

1. 在 **[!UICONTROL 製作]** 區段，點選 **[!UICONTROL 規則]**.

1. 點選 **[!UICONTROL 建立新規則]**.

1. 指定「規則」的名稱。 例如，表單提交可記錄表單提交。

1. 在 **[!UICONTROL 事件]** 區段，點選 **[!UICONTROL 新增]**.

1. 指定 **[!UICONTROL Adobe Experience Manager Forms]** 作為擴充功能名稱。

1. 選取事件型別。 的輸入 **[!UICONTROL 名稱]** 欄位會自動根據選取的事件型別填入。

1. 點選 **[!UICONTROL 保留變更]** 以儲存事件。

1. 在 **[!UICONTROL 動作]** 區段，點選 **[!UICONTROL 新增]**.

1. 指定 **[!UICONTROL Adobe Analytics]** 作為擴充功能名稱。

1. 選取 **[!UICONTROL 設定變數]** 作為「動作型別」。 下拉式清單中可用的選項包括：

   * **[!UICONTROL 設定變數]**：使用此動作型別可定義從AEM Forms將所選資料元素傳送至的事件型別 [!DNL Adobe Analytics].

   * **[!UICONTROL 傳送信標]**：使用此動作型別將資料從AEM Forms傳送至 [!DNL Adobe Analytics].

   * **[!UICONTROL 清除變數]**：使用此動作型別可清除資料追蹤，讓事件在中只註冊一次 [!DNL Adobe Analytics].

      建議方法是使用 **[!UICONTROL 設定變數]** 動作型別以設定事件和資料元素，然後使用 **[!UICONTROL 傳送信標]** 以傳送資料，然後使用 **[!UICONTROL 清除變數]** 以清除資料軌跡。

1. 在 **[!UICONTROL Prop]** 區段，將下拉式清單中可用的報表套裝選項，與使用定義的資料元素對應 [設定資料元素](#configure-data-elements).

   例如，若要傳送 **表單標題** 資料元素從AEM Forms移至 [!DNL Adobe Analytics] 當您提交表單時：
   1. 在 **[!UICONTROL Prop]** 區段，選取報表套裝中可用表單標題的prop，然後點選 ![資料庫圖示](/help/forms/using/assets/database-icon.svg) 以將其對應至在中建立的表單標題 [設定資料元素](#configure-data-elements).

      ![define-props](/help/forms/using/assets/define-props.png)

   1. 點選 **[!UICONTROL 新增其他]** 以新增更多資料元素至清單。

1. 在 **[!UICONTROL 事件]** 區段中，從報表套裝中可用的選項中選取事件，然後點選 **[!UICONTROL 保留變更]**.

1. 在 **[!UICONTROL 動作]** 區段，點選+並指定 **[!UICONTROL Adobe Analytics]** 作為擴充功能名稱。

1. 選取 **[!UICONTROL 傳送信標]** 作為「動作型別」。 在右窗格中，選取 **[!UICONTROL s.t()]** 將資料傳送至 [!DNL Adobe Analytics] 並將其視為頁面檢視或 **[!UICONTROL s.tl()]** 將資料傳送至 [!DNL Adobe Analytics] 且不要將其視為頁面檢視。 點選 **[!UICONTROL 保留變更]**.

1. 在 **[!UICONTROL 動作]** 區段，點選+並指定 **[!UICONTROL Adobe Analytics]** 作為擴充功能名稱。

1. 選取 **[!UICONTROL 清除變數]** 作為「動作型別」。 點選 **[!UICONTROL 保留變更]**. 執行這些步驟後， **[!UICONTROL 動作]** 區段顯示為：
   ![動作設定](/help/forms/using/assets/actions-config.png)

   自訂 **[!UICONTROL 動作]** 區段。 例如，您可以定義兩個 **傳送信標** 傳送資料的目標動作流程步驟 [!DNL Adobe Analytics] 並將其視為一個步驟中的頁面檢視，並將資料傳送至 [!DNL Adobe Analytics] 且請勿將其視為第二個步驟中的頁面檢視。

   ![動作設定](/help/forms/using/assets/actions-config-2.png)

1. 點選 **[!UICONTROL 儲存]** 以儲存規則。

   您可以為所有事件型別建立規則，例如「放棄」、「錯誤」、「欄位瀏覽」、「說明」、「呈現」、「儲存」和「提交」。

   >[!VIDEO](https://video.tv.adobe.com/v/337425)


### 發佈流程 {#publish-flow}

建立資料元素並在規則中使用它們後，發佈設定以在中收集表單資料 [!DNL Adobe Analytics].

執行以下步驟以發佈設定：

1. 在 **[!UICONTROL 發佈]** 區段，點選 **[!UICONTROL 發佈流程]**.

1. 點選 **[!UICONTROL 新增程式庫]** 和指定名稱，並選取程式庫的環境。

1. 點選 **[!UICONTROL 新增所有變更的資源]** 然後點選 **[!UICONTROL 儲存並建置到開發環境]**.

1. 在 **[!UICONTROL 開發]** 區段，點選 ![更多選項](/help/forms/using/assets/more-options-icon.svg) 然後點選 **[!UICONTROL 核准並發佈至生產環境]**.

1. 確認變更，發佈流程即會顯示在 **[!UICONTROL 已發佈]** 區段。

![發佈流程](/help/forms/using/assets/publish-flow.png)

## 2.設定AEM Forms {#configure-aem-forms}

建立Adobe Launch設定之前，請先建立 [使用Adobe Launch作為雲端解決方案的Adobe IMS設定](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/integrations/experience-platform-launch/connect-aem-launch-adobe-io.html).

### 创建 Adobe Launch 配置 {#create-adobe-launch-configuration}

執行以下步驟來建立Adobe Launch設定：

1. 在AEM Forms作者執行個體上，導覽至 **[!UICONTROL 工具]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL AdobeLaunch設定]**.

1. 選取資料夾以建立設定並點選 **[!UICONTROL 建立]**.

1. 在中指定設定的標題 **[!UICONTROL 標題]** 欄位。

1. 選取 [關聯的Adobe IMS設定](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/integrations/experience-platform-launch/connect-aem-launch-adobe-io.html).

1. 選取當時使用的公司名稱 [設定Adobe Analytics](#Configure-adobe-analytics).

1. 選取建立時建立的屬性名稱。 [設定Adobe Analytics](#install-extensions).

1. 點選 **[!UICONTROL 儲存並關閉]**.

1. 發佈設定。

### 啟用 [!DNL Adobe Analytics] 最適化表單 {#enable-analytics-adaptive-form}

使用 [!DNL Adobe Launch] 現有最適化表單中的設定：

1. 在AEM Forms作者執行個體上，導覽至 **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms與檔案]**.
1. 選取最適化表單並點選 **[!UICONTROL 屬性]**.
1. 在 **[!UICONTROL 基本]** 索引標籤中，選取 [設定容器](#create-adobe-launch-configuration) 用於建立Adobe Launch設定。
1. 點選 **[!UICONTROL 儲存並關閉]**. 已針對以下專案啟用最適化表單 [!DNL Adobe Analytics].
1. 發佈表單。

在您啟用之後 [!DNL Adobe Analytics] 對於最適化表單，您可以 [驗證](https://experienceleague.adobe.com/docs/launch-learn/implementing-in-websites-with-launch/implement-solutions/analytics.html?lang=en#validate-the-page-view-beacon) 如果AEM Forms和之間有適當的資料事件流程 [!DNL Adobe Analytics]. AEM Forms與Adobe Analytics的整合已完成。 您現在可以 [在Adobe Analytics中設定和檢視報表](#view-reports-adobe-analytics).

>[!NOTE]
>如果兩者皆有 [使用Cloud Service架構的Analytics](/help/forms/using/configure-analytics-forms-documents.md) 和 **使用Adobe啟動的Analytics** 功能會同時啟用， **使用Adobe啟動的Analytics** 將取得優先權。

### 建立規則以擷取自訂事件（選用） {#capture-custom-events}

使用規則編輯器在最適化表單的特定欄位上建立規則，以將Analytics資料從最適化表單傳送至 [!DNL Adobe Analytics].

在兩階段程式中，您會在最適化表單的欄位上定義規則。 規則會傳送事件。 事件名稱會對應至Adobe Launch中的自訂擷取事件。

若要在最適化表單中使用規則編輯器建立規則：

1. 點選欄位並選取 ![規則編輯器](/help/forms/using/assets/rule-editor-icon.svg) 以開啟規則編輯器頁面。
1. 在中定義條件 [!UICONTROL 時間] 區段。
1. 在 [!UICONTROL 則] 區段，選取 **[!UICONTROL 分派事件]** 從 **[!UICONTROL 選取動作]** 下拉式清單。
1. 在中指定事件的名稱 **[!UICONTROL 輸入事件名稱]** 欄位。

例如，如果出生日期在某個日期之前，AEM Forms會傳送 **安全性** 事件。

![分派事件](/help/forms/using/assets/security-event.png)

若要將事件對應至中的自訂擷取事件 [!DNL Adobe Analytics]：

1. [创建规则](#configure-rules).

1. 在 **[!UICONTROL 事件]** 區段，點選 **[!UICONTROL 新增]**.

1. 指定 **[!UICONTROL Adobe Experience Manager Forms]** 作為擴充功能名稱。

1. 選取 **[!UICONTROL 擷取自訂事件]** 從 **[!UICONTROL 事件型別]** 下拉式清單。

1. 使用規則編輯器建立規則時，指定您在步驟4中指定的事件名稱。

1. 點選 **保留變更** 並執行中指定的其餘動作 [設定規則](#configure-rules).

## 3.設定並檢視報表，於 [!DNL Adobe Analytics] {#view-reports-adobe-analytics}

設定最適化表單以傳送事件資料至後 [!DNL Adobe Analytics]，您就可以開始在中檢視報表 [!DNL Adobe Analytics]：

1. 點選 ![選取產品](/help/forms/using/assets/select-analytics.png) 並選取 **[!UICONTROL 分析]**.

1. 點選 **[!UICONTROL 建立專案]** 並選取 **[!UICONTROL 空白專案]**.

1. 從自由表格右上角的下拉式清單中選取報表套裝名稱。

1. 指定 **表單標題** 在 **[!UICONTROL 搜尋維度專案]** 文字以檢視所有表單標題。

1. 將最適化表單標題拖放至 **[!UICONTROL 將區段拖放到這裡（或任何其他元件）]** 文字方塊。

1. 從 **[!UICONTROL 量度]** 區段，放置要追蹤的事件 **[!UICONTROL 將量度拖放到這裡（或任何其他元件）]** 文字方塊。

1. 點選 ![視覺效果](/help/forms/using/assets/visualization-icon.svg) 並將圖表型別拖放至「自由格式」區段。 同樣地，您可以將多個圖表型別新增至自由格式區段。

1. 點選Ctrl + S鍵並指定名稱以儲存專案。

如需檢視表單分析報表的詳細資訊，請參閱 [檢視和瞭解AEM Forms Analytics報表](../../forms/using/view-understand-aem-forms-analytics-reports.md).
