---
title: 匯入和匯出全域設定
seo-title: Importing and exporting global settings
description: 您可以匯入和匯出Workspace的搜尋範本定義和全域設定。
seo-description: You can import and export search template definitions and global settings for Workspace.
uuid: 8f1f210d-e850-4b2c-bb5a-942fa8299791
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_workspace
products: SG_EXPERIENCEMANAGER/6.4/FORMS
discoiquuid: 72fe5749-2fa2-442f-b679-7889faeafcac
exl-id: cdb7ff54-7891-45b1-a921-10b01ef5188d
source-git-commit: 0c7dba43dad8608b4a5de271e1e44942c950fb16
workflow-type: tm+mt
source-wordcount: '1245'
ht-degree: 0%

---

# 匯入和匯出全域設定 {#importing-and-exporting-global-settings}

您可以匯入和匯出Workspace的搜尋範本定義和全域設定。

>[!NOTE]
>
>AEM Forms版本已棄用Flex Workspace。

例如，您可以從開發環境移至生產環境，方法是從某個環境匯出搜尋範本定義和全域設定，然後將其匯入另一個環境。

匯出全域設定檔案後，您可以在XML或文字編輯器中修改設定。 不過，您唯一需要編輯的設定是JChannelConnectionProperties、formViewOnly和specialRoutes設定。 如需詳細資訊，請參閱 [工作區全域設定](importing-exporting-global-settings.md#workspace-global-settings).


>[!NOTE]
>
>如果您變更全域設定檔案中的事件屬性，則必須重新啟動伺服器。

## 匯入搜尋範本定義 {#import-a-search-template-definition}

1. 在管理控制檯中，按一下「服務>工作區>全域管理」。
1. 在「匯入搜尋範本定義」方塊下，按一下「選擇檔案」並選取搜尋範本。 您只能匯入原本從Workspace例項匯出的搜尋範本定義。
1. 按一下「匯入」。

## 匯出搜尋範本定義 {#export-a-search-template-definition}

1. 在「全域管理」頁面的「匯出搜尋範本定義」下，按一下「列出全部」。
1. 在搜尋範本清單中，選取要匯出的範本。

   >[!NOTE]
   >
   >您可以選取多個範本，但只會匯出最後選取的範本。

1. 按一下「匯出」 ，然後將檔案儲存在電腦上。

## 匯入全域設定 {#import-global-settings}

1. 在「全域管理」頁面的「匯入全域設定」下，按一下「選擇檔案」並選取全域設定檔案。 全域設定檔案必須是XML格式。
1. 按一下「匯入」。

## 匯出全域設定 {#export-global-settings}

1. 在「全域管理」頁面的「匯出全域設定」下，按一下「匯出」。
1. 將檔案儲存在電腦上。

## 工作區全域設定 {#workspace-global-settings}

您可以修改全域設定檔案；不過，您唯一想要編輯的設定是JChannelConnectionProperties、formViewOnly和specialRoutes設定。

>[!NOTE]
>
>AEM Forms版本已棄用Flex Workspace。

工作區全域設定檔案包含下列設定：

### specialRoutes設定 {#specialroutes-settings}

此 *specialRoutes* 設定在Workspace中指定特殊路由（核准和拒絕）的屬性。 在某些情況下，這些路由的按鈕會出現在Workspace的工作卡上，使用者可以在不開啟表單的情況下選取它們。 您可以修改全域設定檔案中的specialRoutes設定，以新增自訂名稱來核准和拒絕或建立其他路由。

**client_specialRoutes_routes_approve_style：** 位於工作區主題中的樣式名稱，可識別核准按鈕圖示。 樣式必須包含啟用圖示和停用圖示的值。 若要定義自訂按鈕的樣式，您必須使用下列範本：
` .buttonApprove {  icon: Embed('images/LC_DirectApprove_Sm_N.png');  disabledIcon: Embed('images/LC_DirectApprove_Sm_D.png');  paddingLeft: 5;  }` Workspace CSS檔案內嵌於workspace-theme.swf檔案中，該檔案位於adobe-workspace-client.ear > adobe-workspace-client.war檔案中。 若要變更Workspace的外觀，您必須重新編譯workspace-theme.swf檔案。

**client_specialRoutes_routes_deny_names：** Workbench使用者可用來解譯為「拒絕」的各種字串。 字串區分大小寫。 例如，預設值為deny。 如果Workbench使用者在處理序中使用了「拒絕」一詞，則無法辨識該字。 必須將「拒絕」一詞新增至此設定，才能自訂路由按鈕並套用樣式。

**client_specialRoutes_routes_deny_style：** 位於Workspace主題檔案中的樣式名稱，可識別拒絕按鈕圖示。 樣式必須包含啟用圖示和停用圖示的值。 若要定義自訂按鈕的樣式，您必須使用下列範本：
`  .buttonDeny {   icon: Embed('images/LC_DirectDeny_Sm_N.png');   disabledIcon: Embed('images/LC_DirectDeny_Sm_D.png');   paddingLeft: 0;   }` **client_specialRoutes_routes_approve_names：** Workbench使用者可用來解譯為「核准」的各種字串。 字串區分大小寫。 例如，預設值為approve。 如果Workbench使用者在流程中使用了「核准」一詞，則無法辨識該字。 必須將「核准」一詞新增至此設定，才能自訂路由按鈕並套用樣式。

**client_specialRoutes_names：** 用來從資源檔案中找出自訂字串值的金鑰。 此設定中的每個專案都必須包含名稱和樣式的值。

### 群組設定 {#jgroup-settings}

這些設定僅在您從AdobeLiveCycleES 2.5或更早版本升級時顯示。

**server_remoteevents_ClientTimeoutMilliseconds：** JGroup等待事件訊息的最長時間。 此設定不應變更。

**server_remoteevents_ServerTimeoutMilliseconds：** 在伺服器上接收JGroup訊息的逾時。 此選項會設定從伺服器傳送訊息至使用者端的延遲。

**server_remoteevents_JChannelConnectionProperties：** 用來在伺服器（RemoteEvent服務處理服務事件）與工作區所有執行個體之間通訊的JGroup連線屬性。

您可能需要變更多點傳送IP位址(mcast_addr)、多點傳送IP連線埠(mcast_port)和多點傳送封包(ip_ttl)的UDP值。 預設情況下，多點傳送IP位址和連線埠值是隨機產生的，通常不需要變更值。 但是，如果貴公司對於多點傳送IP位址的特定多點傳送範圍有任何網路原則，您可能需要變更值。

>[!NOTE]
>
>TTL必須大於叢集中伺服器之間的網路交換器數目；但是，如果該值設定得太高，可能會造成多點傳送封包傳送到子網路，並在子網路中捨棄。

此設定中的其餘屬性不應變更。

**server_remoteevents_JGroupName：** 用於遠端事件通訊的JGroup名稱。 此值是隨機產生的，以避免叢集中的衝突。 此值不應變更。

<!--

For additional information on JGroups and Workspace, see [JGroups and AEM forms Workspace - Explained](https://blogs.adobe.com/livecycle/2011/03/jgroups-and-livecycle-workspace-explained.html).

-->

### formView設定 {#formview-settings}

**client_formView_openFormInFullScreen：** 若要以全熒幕模式在Workspace中顯示所有表單，請將此選項設定為true。 依預設，此選項會設為false，且表單不會以全熒幕模式顯示。 請注意，使用者服務包含以全熒幕模式開啟與任務相關聯之檔案的選項。 這可讓您根據每個處理序來控制顯示。

**client_routes_formViewOnly：** 設定為True時，路由不會顯示在工作區中的卡片檢視或清單檢視中。 預設值為False，表示路由會顯示在卡片檢視和清單檢視中。

### 其他設定 {#other-settings}

**client_mimeTypes_openOutsideBrowser：** 將在工作區瀏覽器例項外部開啟的MIME檔案型別。 如果貴組織的流程需要其他MIME型別，請在此處指定。 預設值為：

* `application/msword`
* `application/msexcel`
* `application/ms-powerpoint`

**client_customUI_caching：** 快取自訂任務使用者介面。

**server_debugLevel：** 請勿變更此設定。

**client_pollingInterval：** 設定用於(JEE上已棄用的AEM表單) Flex Workspace的輪詢間隔（以秒為單位），以偵測新的和修改的工作。 預設值為3秒。 這在AEM Forms Workspace中無法運作。

**client_systemContext_name：** 為AEM Forms Workspace中工作的附件指定要顯示在「新增者」欄位（「附件」標籤中）的自訂名稱（例如「公民」）。

若要定義自訂名稱：

`<client_systemContext_name>[custom name to display]</client_systemContext_name>`

>[!NOTE]
>
>對於示範應用程式，預設顯示名稱為 **公民**. 對於您建立的自訂應用程式，預設顯示名稱為 **系統內容帳戶**.
>
>**client_idleTimeout：** 當使用者在特定時間內保持非使用中時，AEM Forms Workspace工作階段會過期。 若要啟用此功能，請在[全域設定]中新增專案 &lt;client_idletimeout>*IDLE_TIMEOUT_IN_SECONDS*&lt;/client_idletimeout>. 您可以指定值0來停用閒置逾時。 時間長度以秒為單位。
