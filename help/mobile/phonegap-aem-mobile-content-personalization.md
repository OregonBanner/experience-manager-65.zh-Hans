---
title: AEM Mobile內容個人化
seo-title: AEM Mobile content personalization
description: 請詳閱本頁，瞭解AEM Mobile內容個人化功能，此功能可讓AEM作者運用Adobe Target個人化行動應用程式內容。
seo-description: Follow this page to learn about AEM Mobile content personalization feature that allows AEM authors to personalize mobile app content by leveraging Adobe Target.
uuid: 9078edd1-8399-485f-8a63-a07e766f7ef9
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: c9c818dc-c5c4-4a96-94fe-9dc9fe75705b
exl-id: 70d7ee0d-2f6d-4f97-a6e2-b02d84a0ca42
source-git-commit: ed11891c27910154df1bfec6225aecd8a9245bff
workflow-type: tm+mt
source-wordcount: '2673'
ht-degree: 0%

---

# AEM Mobile內容個人化{#aem-mobile-content-personalization}

>[!NOTE]
>
>Adobe建議針對需要以單頁應用程式框架為基礎的使用者端轉譯（例如React）專案使用SPA編輯器。 [了解详情](/help/sites-developing/spa-overview.md).

>[!NOTE]
>
>本檔案屬於 [AEM Mobile快速入門](/help/mobile/getting-started-aem-mobile.md) 指南，AEM Mobile參考的建議起點。

AEM Mobile內容個人化功能允許 [AEM作者](#author) 運用個人化行動應用程式內容 [Adobe Target](https://www.adobe.com/ca/marketing-cloud/testing-targeting.html). 這可讓您將目標選件傳送給行動應用程式使用者。 Adobe Experience Manager Mobile能夠建立、鎖定和傳送內容，為使用者提供適合其個人口味的內容。

和AEM中的情況一樣，為了讓作者開始建立此內容，管理員和開發人員需要先準備環境。

[AEM管理員](#administrator) 在AEM Mobile和Adobe TargetCloud Service之間建立連線時需要使用。

同時，AEM Mobile [開發人員](#developer) 需要修改其現有指令碼，以利製作目標內容。

## 適用於管理員 {#for-administrators}

必須先完成許多步驟，內容作者才能開始為行動應用程式產生目標式內容：取得使用者和群組的正確許可權集、建立雲端服務、為活動設定應用程式，以及最終產生內容。

本文將引導您完成用來設定 [AEM Mobile混合參考應用程式](https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference) 目標定位。

我們日後會假設AEM Mobile混合參考應用程式已成功部署並可透過AEM Mobile儀表板存取。

在作者可以在應用程式中產生目標內容之前，您的AEM例項必須 [以Adobe TargetCloud Service設定。](/help/mobile/aem-mobile-configuring-cloud-service.md)

### 权限 {#permissions}

需要存取個人化主控台的使用者必須屬於 `target-activity-authors` 群組。

建議將target-activity-group新增至apps-admins群組，作為使用者和群組設定的一部分。 新增target-activity-authors群組後，使用者就能檢視「個人化」導覽功能表專案。

>[!NOTE]
>
>忘記將您想要存取個人化Admin Console的使用者或群組新增至Target活動作者群組，會讓使用者無法看到個人化主控台。

### Cloud Service {#cloud-services}

若要讓目標內容適用於行動應用程式，有兩個服務需要設定： Adobe Target服務和Adobe行動服務服務。 Adobe Target服務提供處理使用者端請求和傳回個人化內容的引擎。 AdobeMobile Services服務會透過AMS Cordova外掛程式使用的ADBMobileConfig.json檔案，提供Adobe服務與行動應用程式之間的連線。 您可以從AEM Mobile Dashboard新增兩項服務，以設定應用程式。

在AEM Mobile控制面板中，找出管理Cloud Services，然後按一下+按鈕。

![chlimage_1-38](assets/chlimage_1-38.png)

從「新增Cloud Service」精靈中選取「Adobe Target」雲端服務卡，然後按一下「下一步」。

![chlimage_1-39](assets/chlimage_1-39.png)

從選取組態下拉式清單中，您可以建立新組態或從現有組態中選取。 若要建立新設定，請從下拉式清單中選取「建立設定」。 輸入Target設定的標題。 輸入與您的Target帳戶相關聯的使用者端代碼、電子郵件和密碼。 如果您不知道這些欄位的值，請聯絡Adobe Target支援。 按一下「驗證」按鈕以驗證認證。 驗證後，按一下提交按鈕以建立雲端服務。

>[!NOTE]
>
>系統會透過精靈，自動將所建立的雲端服務與行動應用程式建立關聯。 在應用程式群組節點的jcr：content節點上設定cq：cloudserviceconfigs屬性值。 對於混合式應用程式範例，其設定於/content/mobileapps/hybrid-reference-app/jcr：content，且值指向位於/etc/cloudservices/testandtarget/adobe-target—aem-apps/framework的自動產生架構節點。 框架節點預設會設定兩個屬性：性別和年齡。 此架構僅供AEM預覽使用，對裝置沒有任何影響。

完成精靈後，「管理Cloud Service」表徵圖將包含Target雲端服務，但包含有關遺失Adobe行動服務帳戶的警告。

![chlimage_1-40](assets/chlimage_1-40.png)

### Adobe Mobile Services {#adobe-mobile-services}

此外，還必須將Adobe Mobile Services (AMS)帳戶連結至應用程式，AMS服務提供必要的ADBMobileConfig.json檔案（其中包含Target使用者端程式碼資訊）。 在建立與AMS帳戶的關聯之前，AMS帳戶需要由擁有AMS許可權的使用者修改。

### 客户代码 {#client-code}

若要登入AMS服務，請造訪 [https://mobilemarketing.adobe.com](https://mobilemarketing.adobe.com/)，選取行動應用程式並按一下設定。 找出「SDK目標選項」欄位，並將使用者端代碼放入欄位中，然後按一下「儲存」。

![chlimage_1-41](assets/chlimage_1-41.png)

現在，使用者端代碼已與行動應用程式相關聯，當透過Adobe行動儀表板設定AMS雲端服務時，服務設定的設定將透過ADBMobileConfig.json檔案傳送。

### Adobe行動服務Cloud Service {#adobe-mobile-service-cloud-service}

現在已設定AMS，是時候在Adobe行動儀表板中關聯行動應用程式了。 在AEM Mobile控制面板中，找出管理Cloud Services，然後按一下+按鈕。

![chlimage_1-42](assets/chlimage_1-42.png)

選取AdobeMobile Services卡片，然後按下一步。

![chlimage_1-43](assets/chlimage_1-43.png)

從建立或選取精靈步驟中選取行動服務下拉式清單，然後選取建立設定專案。 提供標題、公司、使用者名稱、密碼並選取適當的資料中心。 如果您不知道這些值，請聯絡您的Adobe行動服務管理員以取得這些值。 填寫完所有欄位後，按一下驗證按鈕。 驗證程式會移至AMS並驗證帳戶的認證，在成功驗證後，行動應用程式清單將會填入，您可在其中從下拉式清單中選取關聯的行動應用程式。 按一下送出按鈕以完成精靈。 此程式可能需要一點時間才能取得設定資料及與應用程式關聯的任何分析。 程式完成後，按一下強制回應視窗中的「完成」按鈕，返回Adobe行動儀表板。

返回行動儀表板「管理Cloud Services」表徵圖將包含AMS雲端服務。 您也會注意到，「分析量度」表徵圖中將填入生命週期報表。

![chlimage_1-44](assets/chlimage_1-44.png)

## 作者專用 {#for-authors}

**先決條件：** 如上所述，管理員必須先設定與Adobe Target服務的連線，作者才能產生新的目標內容。

在管理員設定兩個雲端服務，且開發人員設定mobileappoffers處理常式後，內容作者現在可以開始產生鎖定目標的體驗。

在AEM Mobile應用程式中編寫目標內容時，會遵循與編寫AEM Sites類似的程式：

如需的完整概述，請參閱此處 [在AEM中製作目標內容](/help/sites-authoring/personalization.md)

## 適用於開發人員 {#for-developers}

建立行動應用程式的AEM開發人員在開發元件時，應該繼續遵循AEM中常用的模式。 在此，我們將逐步引導您完成必要步驟，讓內容作者建立目標內容：

### Adobe Target ContentSync處理常式 {#adobe-target-contentsync-handlers}

若要將內容傳送至使用者的裝置內容，則會透過轉譯AEM內容作者建立的選件來產生。 若要處理目標選件的轉譯，可使用新的內容同步處理常式來處理選件。 使用混合參考應用程式作為範例，en （英文）內容套件包含的ContentSyncConfig具有 [mobileappoffers](https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference/blob/master/aem-package/content-author/src/main/content/jcr_root/content/mobileapps/hybrid-reference-app/en/_jcr_content/pge-app/app-config-dev/targetOffers/.content.xml) 處理常式。 下一步是將選件轉譯至裝置時十分重要。 mobileappoffers處理常式具有路徑屬性，可識別用於應用程式的個人化活動路徑。

例如，如果活動位於 */content/campaigns/hybridref* 複製此路徑，並將其當做值貼到 *路徑* mobileappoffers處理常式的屬性。

>[!NOTE]
>
>對於Hybrid Reference Application，有兩種Mobileappoffer處理常式，一個用於開發，一個用於生產。

在mobileappoffers處理常式的path屬性中設定活動路徑後，請儲存處理常式。 處理常式現在可以開始呈現行動裝置的選件。

### 演算模式 {#render-mode}

Mobileappoffers處理常式的設定方式不同，適用於發佈和開發設定。 對於發佈設定，有一個稱為的屬性 *轉譯模式* 具有值 *發佈* 在cq：ContentSyncConfig節點上設定。 mobileappoffers處理常式會參照renderMode，且如果設為publish，會修改所建立的mbox id。 根據預設，AEM建立的mbox會將 — author值附加至mbox id。 這會識別活動尚未發佈，且應使用未發佈的行銷活動來解析優惠方案。

透過Adobe行動儀表板將內容分段時，分段內容會被視為生產就緒內容，並透過非開發內容同步設定進行轉譯。 以這種方式呈現將會導致 — author從所有mbox id中移除，並預期Target伺服器上會有已發佈的活動。 在測試分階段內容之前，請確定活動已發佈。

### 個人化應用程式開發 {#personalization-app-development}

#### 组件 {#components}

任何內容的基礎通常是頁面元件，它會延伸其中一個基本AEM頁面元件wcm/foundation/components/page或foundation/components/page （視您使用的是HTL或JSP而定）。 這些步驟的持續時間將著重於使用wcm/foundation/components/page元件。 頁面元件的基本結構會細分為多個指令碼，每個指令碼提供特定用途，讓開發人員可視需要整理及覆寫其程式碼。 個人化感興趣的兩個指令碼是head.html和body.html。 這兩個指令碼提供一個區域，可以插入程式碼以支援Context Hub、Cloud Services和行動編寫。

以下為啟用內容鎖定目標之兩個主要指令碼的概觀。

#### head.html {#head-html}

為了讓作者能夠鎖定其內容，需要將目標功能表新增至頁面，讓作者可以將內容從編輯模式變更為鎖定目標模式。 若要啟用此功能，開發人員應修改head.html指令碼，在靠近head.html頂端或靠近 &lt;title>&lt;/title> 元素。

```xml
<meta data-sly-test="${!wcmmode.disabled}">
    <div data-sly-call="${clientLib.all @ categories='personalization.kernel'}" data-sly-unwrap></div>
    <div data-sly-resource="${'config' @ resourceType='cq/personalization/components/clientcontext_optimized/config'}" data-sly-unwrap></div>
    <div data-sly-resource="${'contexthub' @ resourceType='granite/contexthub/components/contexthub'}" data-sly-unwrap></div>
</meta>
```

>[!NOTE]
>
>請注意，只有在尚未停用WCM模式，以致停用WCM模式時（如需詳細資訊，請參閱ContentSync處理常式一節），才應該將指令碼包含在最終應用程式程式碼中。

為了讓作者能夠預覽目標內容，編輯器必須能夠找到Adobe Target雲端服務的設定。 下列程式碼區塊新增兩個重要指令碼。 首次新增頁面功能，以找出關聯的Target雲端服務，並向Adobe Target發出呼叫。 第二個是新增cq.apps.targeting類別。

此 **cq.apps.targeting** 類別會覆寫預設的cq/personalization/component/target元件，並使用可針對行動應用程式使用量呈現特定選件的mobileapps/components/target元件。 有關詳細資訊，請參閱目標元件區段。

程式碼應新增至head.html中，並放置在的結尾之前 &lt;/head> 元素。

```xml
<div data-sly-test="${!wcmmode.disabled}">
    <div data-sly-include="/libs/cq/cloudserviceconfigs/components/servicelibs/servicelibs.jsp" data-sly-unwrap></div>
    <meta data-sly-call="${clientLib.all @ categories='cq.apps.targeting'}" data-sly-unwrap></meta>
</div>
```

>[!NOTE]
>
>請注意，程式碼區塊包裝在WCM模式中時不會停用，因此只有在內容作者正在建立內容時才會發揮作用。 雲端服務指令碼不會新增至產生的行動執行階段程式碼。

#### body.html {#body-html}

若要讓內容作者能夠測試不同角色的body.html指令碼，必須包括下列程式碼區塊作為body元素的第一個子項。

```xml
<div data-sly-test="${!wcmmode.disabled}">
    <div data-sly-resource="${'clientcontext' @ resourceType='cq/personalization/components/clientcontext_optimized'}" data-sly-unwrap></div>
</div>
```

需要的最後一個位元程式碼位於body.html的最底部。 此位元程式碼會尋找關聯的雲端服務，並注入適當的目標定位引擎程式碼。

```xml
<div data-sly-test="${!wcmmode.disabled}">
    <div data-sly-resource="${'cloudservices' @ resourceType='cq/cloudserviceconfigs/components/servicecomponents'}" data-sly-unwrap></div>
</div>
```

### 參考應用程式 {#reference-application}

head.html和body.html的範例可在以下網址找到： [AEM Mobile混合參考應用程式](https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference) 顯示開發人員在兩個指令碼中放置指令碼區塊的位置。

### 內容同步處理常式 {#content-sync-handlers}

內容作者完成建立行動應用程式的內容後，下一步就是下載來源並建置應用程式，或暫存要發佈的內容。 開發人員需完成許多步驟，才能達成此目的。 為協助轉譯內容，AEM Mobile使用內容同步處理常式來轉譯及封裝內容。 已為Personalization使用案例引入新的內容同步處理常式，以便呈現目標內容。 「mobileappoffers」處理常式知道如何呈現內容作者建立的關聯目標選件。 mobileappoffers處理常式會擴充抽象頁面更新處理常式，因此許多屬性都類似。 mobileappoffers處理常式的詳細資訊具有以下屬性。

<table>
 <tbody>
  <tr>
   <td><strong>属性</strong></td>
   <td><strong>价值</strong></td>
   <td><strong>描述</strong></td>
  </tr>
  <tr>
   <td>重寫</td>
   <td>+相對父路徑<p> - "/"</p> </td>
   <td>rewrite屬性可識別應如何重寫內容中的路徑。</td>
  </tr>
  <tr>
   <td>includedPageTypes</td>
   <td><p>"cq/personalization/components/teaserpage",</p> <p>"cq/personalization/components/offerproxy"</p> </td>
   <td>includePageTypes屬性是選用屬性，預設為具有cq/personalization/components/teaserpage和cq/personalization/components/offerproxy資源型別的頁面。 這兩種資源型別是目標內容時使用的預設資源型別。 如果需要支援其他資源型別，則應將其新增至includePageTypes清單。</td>
  </tr>
  <tr>
   <td>locationRoot</td>
   <td>/content/mobileapps/&lt;app&gt;</td>
   <td>應用程式的位置。</td>
  </tr>
  <tr>
   <td>类型</td>
   <td>mobileappoffers</td>
   <td>作為mobileappoffers的處理常式名稱。</td>
  </tr>
  <tr>
   <td>選擇器</td>
   <td>tandt</td>
   <td>tandt選擇器可用來轉譯目標內容。 </td>
  </tr>
  <tr>
   <td>targetRootDirectory</td>
   <td>www</td>
   <td>要保留演算內容的根目錄。</td>
  </tr>
  <tr>
   <td>includeImage</td>
   <td>true | false</td>
   <td>如果為true，則會轉譯選件中包含的任何影像。 如果略過false影像。</td>
  </tr>
  <tr>
   <td>includeVideo</td>
   <td>true | false</td>
   <td>如果為True，則會轉譯選件中包含的任何影片。 如果影片錯誤，則會略過。</td>
  </tr>
  <tr>
   <td>路径</td>
   <td>/content/campaigns/&lt;brand&gt;</td>
   <td>指向優惠方案參與的行銷活動品牌。 目前所有優惠方案都必須來自相同行銷活動。</td>
  </tr>
  <tr>
   <td>深</td>
   <td>true | false</td>
   <td>如果true會遞迴轉譯所有子頁面，如果false則不會遞回。 </td>
  </tr>
  <tr>
   <td>擴充功能</td>
   <td>html</td>
   <td>設定正在轉譯之資源的擴充功能。 設定為html，讓頁面的副檔名為.html。</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>此 [AEM Mobile混合參考應用程式](https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference) 具有預設的mobileappoffer處理常式設定。 範例中的路徑屬性是空的，因為它取決於行銷活動位置。 Campaign作者建立Campaign後，應用程式管理員應指定指向Campaign的路徑屬性，將Campaign與處理常式建立關聯。

### 目標元件 {#target-component}

為協助轉譯專門用於行動應用程式的內容，AEM Mobile使用mobileapps/components/target元件。 行動目標元件會擴充cq/personalization/components/target元件，並覆寫engine_tnt.jsp指令碼。 透過覆寫engine_tnt.jsp，這可讓AEM Mobile控制為行動應用程式使用案例產生的HTML。 對於內容作者鎖定的每個元件，都會由engine_tnt.jsp建立關聯的mbox。

每個mbox的屬性為 **cq目標定位** 新增功能，讓應用程式開發人員可撰寫自訂程式碼，以隨意使用和使用。 此 [AEM Mobile混合參考應用程式](https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference) 有一個使用cq-targeting屬性的Angular指示詞範例。 至於何時及如何取代內容，完全由行動應用程式開發人員決定。 有一個透過AEM /etc/clientlibs/mobileapps/js/mobileapps.js傳遞的Mobile SDK，其提供呼叫Adobe鎖定目標服務的API。 應用程式開發人員可自行指定何時應根據其應用程式的設計進行該呼叫。

## 后续内容? {#what-s-next}

1. [開始我的AEM Mobile應用程式體驗](/help/mobile/starting-aem-phonegap-app.md)
1. [管理我的應用程式內容](/help/mobile/phonegap-manage-app-content.md)
1. [建置我的應用程式](/help/mobile/building-app-mobile-phonegap.md)
1. [透過AdobeMobile Analytics追蹤我的應用程式效能](/help/mobile/phonegap-intro-to-app-analytics.md)
1. [使用Adobe Target提供個人化的應用程式體驗](/help/mobile/phonegap-aem-mobile-content-personalization.md)
1. [傳送重要訊息給我的使用者](/help/mobile/phonegap-push-notifications.md)
