---
title: 設定Dynamic Media — 混合模式
description: 瞭解如何設定Dynamic Media — 混合模式。
mini-toc-levels: 3
uuid: 39ad7d83-d310-4baf-9d85-5532c2f201f3
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: 7d8e7273-29f3-4a45-ae94-aad660d2c71d
docset: aem65
legacypath: /content/docs/en/aem/6-0/administer/integration/dynamic-media/config-dynamic
role: User, Admin
exl-id: 5719d32c-4f19-47c1-bea9-8fd0bc8439ed
feature: Configuration,Hybrid Mode
source-git-commit: 05af34f8be6a4e32c3488ec05bc0133154caff7f
workflow-type: tm+mt
source-wordcount: '7792'
ht-degree: 2%

---

# 設定Dynamic Media — 混合模式 {#configuring-dynamic-media-hybrid-mode}

必須啟用並設定Dynamic Media-Hybrid才能使用。 根據您的使用案例，Dynamic Media提供數種 [支援的設定](#supported-dynamic-media-configurations).

>[!NOTE]
>
>如果您想在Scene7執行模式下設定和執行Dynamic Media，請參閱 [設定Dynamic Media - Scene7模式](/help/assets/config-dms7.md).
>
>如果您打算在混合執行模式中設定並執行Dynamic Media，請依照本頁面上的指示操作。

進一步瞭解使用 [視訊](/help/assets/video.md) 在Dynamic Media中。

>[!NOTE]
>
>如果您針對不同環境使用Adobe Experience Manager設定（例如用於開發、測試和即時生產的環境），請為每個環境設定Dynamic MediaCloud Services。

>[!NOTE]
>
>如果您的Dynamic Media設定發生問題，請檢視Dynamic Media專屬的記錄檔。 當您啟用Dynamic Media時，這些檔案會自動安裝：
>
>* `s7access.log`
>* `ImageServing.log`
>
>記錄於 [監控及維護您的Experience Manager執行個體](/help/sites-deploying/monitoring-and-maintaining.md).

混合式發佈和傳送是Adobe Experience Manager以外的Dynamic Media核心功能。 混合發佈可讓您從雲端而不是Experience Manager發佈節點傳送Dynamic Media資產，例如影像、集合和視訊。

Dynamic Media檢視器、網站頁面和靜態內容等其他內容會繼續從Experience Manager發佈節點提供。

如果您是Dynamic Media的客戶，則必須使用混合式傳送作為所有Dynamic Media內容的傳送機制。

## 視訊的混合式發佈架構 {#hybrid-publishing-architecture-for-videos}

![chlimage_1-506](assets/chlimage_1-428.png)

## 影像的混合式發佈架構 {#hybrid-publishing-architecture-for-images}

![chlimage_1-507](assets/chlimage_1-507.png)

## 支援的Dynamic Media設定 {#supported-dynamic-media-configurations}

後續的設定任務會參考以下術語：

| **术语** | **Dynamic Media已啟用** | **描述** |
|---|---|---|
| Experience Manager作者節點 | 綠色圓圈中的白色勾號 | 您部署至內部部署或透過Managed Services的作者節點。 |
| Experience Manager發佈節點 | 紅色正方形中的白色「X」。 | 您部署至內部部署或透過Managed Services的發佈節點。 |
| 影像服務發佈節點 | 綠色圓圈中的白色勾號。 | 您在由Adobe管理的資料中心上執行的發佈節點。 參考影像服務URL。 |

您可以選擇僅針對影像實作Dynamic Media （僅適用於視訊），或同時針對影像和視訊實作。 若要判斷針對特定案例設定Dynamic Media的步驟，請參閱下表。

<table>
 <tbody>
  <tr>
   <td><strong>情境</strong></td>
   <td ><strong>運作方式</strong></td>
   <td><strong>設定步驟</strong></td>
  </tr>
  <tr>
   <td>在生產環境中僅傳遞影像</td>
   <td>影像是透過Adobe全球資料中心的伺服器提供，然後由CDN快取，以提供可擴充的效能及全球影響力。</td>
   <td>
    <ol>
     <li>在Experience Manager上 <strong>作者</strong> 節點， <a href="#enabling-dynamic-media">啟用Dynamic Media</a>.</li>
     <li>在中設定影像 <a href="#configuring-dynamic-media-cloud-services">Dynamic MediaCloud Services</a>.</li>
     <li><a href="#configuring-image-replication">設定影像復寫</a>.</li>
     <li><a href="#replicating-catalog-settings">復寫目錄設定</a>.</li>
     <li><a href="#replicating-viewer-presets">複製檢視器預設集</a>.</li>
     <li><a href="#using-default-asset-filters-for-replication">使用預設的資產篩選器進行復寫</a>.</li>
     <li><a href="#configuring-dynamic-media-image-server-settings">設定Dynamic Media影像伺服器設定</a>.</li>
     <li><a href="#delivering-assets">傳遞資產</a>.</li>
    </ol> </td>
  </tr>
  <tr>
   <td>只會在生產前提供影像（開發、QE、階段等）。</td>
   <td>影像會透過Experience Manager發佈節點傳遞。 在此案例中，由於流量極少，因此不需要將影像傳送至Adobe的資料中心。 而且可在生產啟動前安全地預覽內容。</td>
   <td>
    <ol>
     <li>在Experience Manager上 <strong>作者</strong> 節點， <a href="#enabling-dynamic-media">啟用Dynamic Media</a>.</li>
     <li>在Experience Manager上 <strong>發佈</strong> 節點， <a href="#enabling-dynamic-media">啟用Dynamic Media</a>.</li>
     <li><a href="#replicating-viewer-presets">複製檢視器預設集</a>.</li>
     <li>設定 <a href="#setting-up-asset-filters-for-imaging-in-non-production-deployments">非生產影像的資產篩選器</a>.</li>
     <li><a href="#configuring-dynamic-media-image-server-settings">設定Dynamic Media影像伺服器設定。</a></li>
     <li><a href="#delivering-assets">傳遞資產。</a></li>
    </ol> </td>
  </tr>
  <tr>
   <td>只在任何環境中傳送視訊（生產、開發、QE、舞台等）</td>
   <td>影片會由CDN傳送和快取，以提供可擴充的效能和全球範圍。 視訊海報影像（在開始播放前顯示的視訊縮圖）由Experience Manager發佈執行個體傳遞。</td>
   <td>
    <ol>
     <li>在Experience Manager上 <strong>作者</strong> 節點， <a href="#enabling-dynamic-media">啟用Dynamic Media</a>.</li>
     <li>在Experience Manager上 <strong>發佈</strong> 節點， <a href="#enabling-dynamic-media">啟用Dynamic Media</a> （發佈例項會提供視訊海報影像，並提供視訊播放的中繼資料）。</li>
     <li>在中設定視訊 <a href="#configuring-dynamic-media-cloud-services">Dynamic MediaCloud Services。</a></li>
     <li><a href="#replicating-viewer-presets">複製檢視器預設集</a>.</li>
     <li>設定 <a href="#setting-up-asset-filters-for-video-only-deployments">僅限視訊的資產篩選器</a>.</li>
     <li><a href="#delivering-assets">傳遞資產。</a></li>
    </ol> </td>
  </tr>
  <tr>
   <td>在生產環境中同時傳送影像和視訊</td>
   <td><p>影片會由CDN傳送和快取，以提供可擴充的效能和全球範圍。 影像和視訊海報影像會透過Adobe全球資料中心的伺服器提供，然後由CDN快取，以發揮可擴充的效能並延伸至全球。</p> <p>請參閱先前章節，以在預先製作中設定影像或影片。 </p> </td>
   <td>
    <ol>
     <li>在Experience Manager上 <strong>作者</strong> 節點， <a href="#enabling-dynamic-media">啟用Dynamic Media</a>.</li>
     <li>在中設定視訊 <a href="#configuring-dynamic-media-cloud-services">Dynamic MediaCloud Services。</a></li>
     <li>在中設定影像 <a href="#configuring-dynamic-media-cloud-services">Dynamic MediaCloud Services。</a></li>
     <li><a href="#configuring-image-replication">設定影像復寫</a>.</li>
     <li><a href="#replicating-catalog-settings">復寫目錄設定</a>.</li>
     <li><a href="#replicating-viewer-presets">複製檢視器預設集</a>.</li>
     <li><a href="#using-default-asset-filters-for-replication">使用預設的資產篩選器進行復寫。</a></li>
     <li><a href="#configuring-dynamic-media-image-server-settings">設定Dynamic Media影像伺服器設定。</a></li>
     <li><a href="#delivering-assets">傳遞資產。</a></li>
    </ol> </td>
  </tr>
 </tbody>
</table>

## 啟用Dynamic Media {#enabling-dynamic-media}

[Dynamic Media](https://business.adobe.com/products/experience-manager/assets/dynamic-media.html) 預設為停用。 若要利用Dynamic MediaDynamic Media功能，您必須使用 `dynamicmedia` 執行模式，例如， `publish` 執行模式。 在啟用之前，請務必檢閱 [技術需求](/help/sites-deploying/technical-requirements.md#requirements-for-aem-dynamic-media-add-on).

>[!NOTE]
>
>透過執行模式啟用Dynamic Media會取代Experience Manager6.1和Experience ManagerDynamic Media 6.0中的功能，而您透過設定 `dynamicMediaEnabled` 標幟到 **[!UICONTROL true]**. 此標幟在Experience Manager6.2和更新版本中沒有任何功能。 此外，您不需要重新啟動快速入門即可啟用Dynamic Media。

啟用Dynamic Media後，UI即可使用Dynamic Media功能，而每個上傳的影像資產都會收到 *cqdam.pyramid.tiff* 用於快速傳送動態影像轉譯的轉譯。 這些PTIFF具有下列顯著優點：

* 僅能管理單一主要來源影像，且無需額外儲存空間即可即時產生無限轉譯。
* 能夠使用互動式視覺效果，例如縮放、平移和迴轉。

如果您想要在Experience ManagerDynamic Media中使用Dynamic Media Classic，除非您使用 [特定案例](/help/sites-administering/scene7.md#aem-scene-integration-versus-dynamic-media). 除非您透過執行模式啟用Dynamic Media，否則會停用Dynamic Media。

若要啟用Dynamic Media，您必須從命令列或快速入門檔案名稱啟用Dynamic Media執行模式。

**若要啟用Dynamic Media：**

1. 在命令列上，啟動快速入門時，請執行下列動作：

   * 新增 `-r dynamicmedia` 啟動jar檔案時到達命令列的結尾。

   ```shellsession {.line-numbers}
   java -Xmx4096m -Doak.queryLimitInMemory=500000 -Doak.queryLimitReads=500000 -jar cq-quickstart-6.5.0.jar -r dynamicmedia
   ```

   如果您要發佈至s7delivery，您還必須包含下列trustStore引數：

   ```shellsession {.line-numbers}
   -Djavax.net.ssl.trustStore=<absoluteFilePath>/customerTrustStoreFileName>
   
    -Djavax.net.ssl.trustStorePassword=<passwordForTrustStoreFile>
   ```

1. 請求 `https://localhost:4502/is/image` 並確保影像伺服器正在執行。

   >[!NOTE]
   >
   >若要針對Dynamic Media問題進行疑難排解，請參閱以下記錄檔： `crx-quickstart/logs/` 目錄：
   >
   >* 影像伺服器 — &lt;portid>-&lt;yyyy>&lt;mm>&lt;dd>.log - ImageServer記錄提供用於分析內部ImageServer處理序行為的統計資料和分析資訊。

   影像伺服器記錄檔名稱的範例： `ImageServer-57346-2020-07-25.log`
   * s7access-&lt;yyyy>&lt;mm>&lt;dd>.log - s7access記錄會記錄透過向Dynamic Media提出的每個請求 `/is/image` 和 `/is/content`.

   這些記錄檔僅在啟用Dynamic Media時使用。 這些屬性不會包含在 **下載完整部分** 從產生的套件 `system/console/status-Bundlelist` 頁面；如果您有Dynamic Media問題，在呼叫客戶支援時，將這兩個記錄附加至問題。

### 如果您將Experience Manager安裝至其他連線埠或內容路徑…… {#if-you-installed-aem-to-a-different-port-or-context-path}

如果您要部署 [應用程式伺服器的Experience Manager](/help/sites-deploying/application-server-install.md) 並啟用Dynamic Media，您必須設定 **自我網域** 在Externalizer中。 否則，資產的縮圖產生功能無法正常用於Dynamic Media資產。

此外，如果您在不同的連線埠或內容路徑上執行快速入門，也必須變更 **自我網域**.

啟用Dynamic Media時，會使用Dynamic Media產生影像資產的靜態縮圖轉譯。 為了讓Dynamic Media的縮圖產生功能正常運作，Experience Manager必須對其本身執行URL要求，而且必須知道連線埠號碼和內容路徑。

Experience Manager：

* 此 **自我網域** 在 [Externalizer](/help/sites-developing/externalizer.md) 用於擷取連線埠號碼和內容路徑。
* 若否 **自我網域** 設定，從Jetty HTTP服務擷取連線埠號碼和內容路徑。

在Experience ManagerQuickStart WAR部署中，無法衍生連線埠號碼和內容路徑，因此您必須設定 **自我網域**. 另請參閱 [Externalizer檔案](/help/sites-developing/externalizer.md) 如何設定 **自我網域**.

>[!NOTE]
在 [Experience Manager Quickstart獨立部署](/help/sites-deploying/deploy.md)， a **自我網域** 通常不需要設定，因為連線埠號碼和內容路徑可以自動設定。 不過，如果所有的網路介面都已關閉，您必須設定 **自我網域**.

## 停用Dynamic Media  {#disabling-dynamic-media}

Dynamic Media預設為未啟用。 不過，如果您先前曾啟用Dynamic Media，稍後可以將其關閉。

若要在啟用Dynamic Media後將其停用，請移除 `-r dynamicmedia` 執行模式旗標。

**若要停用Dynamic Media：**

1. 在命令列上，啟動快速入門時，您可以執行下列任一項作業：

   * 不要新增 `-r dynamicmedia` 啟動jar檔案時至命令列。

   ```shellsession {.line-numbers}
   java -Xmx4096m -Doak.queryLimitInMemory=500000 -Doak.queryLimitReads=500000 -jar cq-quickstart-6.5.0.jar
   ```

1. 請求 `https://localhost:4502/is/image`. 您會收到Dynamic Media已停用的訊息。

   >[!NOTE]
   停用Dynamic Media執行模式後，會產生 `cqdam.pyramid.tiff` 會自動略過轉譯。 它也會停用動態轉譯支援和其他Dynamic Media功能。
   另請注意，設定Experience Manager伺服器後停用Dynamic Media執行模式時，所有在該執行模式下上傳的資產現在都無效。

## （可選）將Dynamic Media預設集和設定從6.3移轉至6.5 （零停機時間） {#optional-migrating-dynamic-media-presets-and-configurations-from-to-zero-downtime}

如果您要將Experience Manager- Dynamic Media從6.3升級至6.5 （現在包含零停機部署功能），您必須執行以下curl命令。 該命令會從移轉您的所有預設集和設定 `/etc` 至 `/conf` 在CRXDE Lite中。

>[!NOTE]
如果您以相容性模式執行Experience Manager執行個體（即已安裝相容性套件），則不需要執行這些命令。

對於所有升級（無論是否包含相容性套件），您可以執行下列Linux® curl命令，複製最初隨Dynamic Media提供的預設現成檢視器預設集：

`curl -u admin:admin -X POST https://<server_address>:<server_port>/libs/settings/dam/dm/presets/viewer.pushviewerpresets.json`

移轉您建立的任何自訂檢視器預設集和設定 `/etc` 至 `/conf`，執行下列Linux® curl命令：

`curl -u admin:admin -X POST https://<server_address>:<server_port>/libs/settings/dam/dm/presets.migratedmcontent.json`

## 設定影像復寫 {#configuring-image-replication}

Dynamic Media影像傳送的運作方式是從Experience Manager Author發佈影像資產（包括視訊縮圖），並將其復寫至Adobe的隨選復寫服務（復寫服務URL）。 然後透過隨選影像傳送服務（影像服務URL）傳送資產。

执行以下操作：

1. [設定驗證](#setting-up-authentication).
1. [設定復寫代理程式](#configuring-the-replication-agent).

復寫代理程式會發佈Dynamic Media資產（例如影像、視訊中繼資料），並將設定為Adobe託管的影像服務。 復寫代理程式預設為未啟用。

設定復寫代理程式後，您必須 [驗證並測試它是否已成功設定](#validating-the-replication-agent-for-dynamic-media). 本節說明這些程式。

>[!NOTE]
在所有工作流程中，建立PTIFF的預設記憶體限製為3 GB。 例如，您可以處理一個需要3 GB記憶體的影像，同時暫停其他工作流程，或者您可以並行處理10個影像，每個影像需要300 MB的記憶體。
記憶體限制是可設定的，且符合系統資源可用性以及正在處理的影像內容型別。 如果您有許多大型資產，而且系統上有足夠的記憶體，您可以提高此限制，以確保同時處理影像。
需要超過最大記憶體限制的影像會遭到拒絕。
若要變更PTIFF建立的記憶體限制，請瀏覽至 **[!UICONTROL 工具]** > **[!UICONTROL 作業]** > **[!UICONTROL 網頁主控台]** > **[!UICONTROL Adobe CQ Scene7 PtiffManager]** 並變更 **[!UICONTROL 最大記憶體]** 值。

### 設定驗證 {#setting-up-authentication}

在作者上設定復寫驗證，以便您可以將影像復寫至Dynamic Media影像傳遞服務。 您先取得KeyStore，然後將其儲存在 **[!UICONTROL dynamic-media-replication]** 使用並進行設定。 在布建程式進行期間，您的公司管理員收到一封歡迎電子郵件，其中包含KeyStore檔案和必要的認證。 如果您沒有收到此資訊，請聯絡Adobe客戶支援。

**若要設定驗證：**

1. 如果您還沒有檔案和密碼，請連絡Adobe客戶支援以取得您的KeyStore檔案和密碼。 此資訊是布建的必要部分。 會將金鑰與您的帳戶建立關聯。

1. 在Experience Manager中，選取Experience Manager標誌以存取全域導覽主控台，然後導覽至 **[!UICONTROL 工具]** > **[!UICONTROL 安全性]** > **[!UICONTROL 使用者]**.

1. 在「使用者管理」頁面上，導覽至 **[!UICONTROL dynamic-media-replication]** 使用者，然後選取以開啟。

   ![dm-replication](assets/dm-replication.png)

1. 在「編輯動態媒體複製的使用者設定值」頁面中，選取 **[!UICONTROL 金鑰存放區]** 索引標籤，然後選取 **[!UICONTROL 建立KeyStore]**.

   ![dm-replication-keystore](assets/dm-replication-keystore.png)

1. 輸入密碼，然後在 **[!UICONTROL 設定KeyStore存取密碼]** 對話方塊。

   >[!NOTE]
   請記住密碼，因為當您稍後設定「復寫代理程式」時，必須再次輸入密碼。

   ![chlimage_1-508](assets/chlimage_1-508.png)

1. 於 **[!UICONTROL 編輯Dynamic-media-replication的使用者設定]** 頁面，展開 **從KeyStore檔案新增私密金鑰** 區域並新增下列專案（請參閱下列影像）：

   * 在 **[!UICONTROL 新增別名]** 欄位，輸入您稍後要在複製組態中使用的別名名稱。 例如，您可以使用 `replication` 作為別名。
   * 選取 **[!UICONTROL KeyStore檔案]**. 導覽至按Adobe提供給您的KeyStore檔案，選取該檔案，然後選取 **[!UICONTROL 開啟]**.
   * 在 **[!UICONTROL KeyStore檔案密碼]** 欄位，輸入KeyStore檔案密碼。 此密碼為 **not** 您在步驟5中建立的KeyStore密碼，但在布建期間傳送給您的「歡迎」電子郵件中會提供KeyStore檔案密碼Adobe。 如果您沒有收到KeyStore檔案密碼，請聯絡Adobe客戶支援。
   * 在 **[!UICONTROL 私密金鑰密碼]** 欄位，輸入私密金鑰密碼（可以是上一步驟中提供的相同私密金鑰密碼）。 Adobe會在布建期間傳送給您的歡迎電子郵件中提供私密金鑰密碼。 如果您沒有收到私密金鑰密碼，請聯絡Adobe客戶支援。
   * 在 **[!UICONTROL 私密金鑰別名]** 欄位，輸入私密金鑰別名。 例如， `*companyname*-alias`. Adobe會在布建期間傳送給您的歡迎電子郵件中提供私密金鑰別名。 如果您沒有收到私密金鑰別名，請聯絡Adobe客戶支援。

   ![edit_settings_fordynamic-media-replication2](assets/edit_settings_fordynamic-media-replication2.png)

1. 選取 **[!UICONTROL 儲存並關閉]** 以儲存您對此使用者的變更。

   接下來，您必須 [設定復寫代理](#configuring-the-replication-agent).

### 設定復寫代理程式 {#configuring-the-replication-agent}

1. 在Experience Manager中，選取Experience Manager標誌以存取全域導覽主控台，然後導覽至 **[!UICONTROL 工具]** > **[!UICONTROL 部署]** > **[!UICONTROL 復寫]** > **[!UICONTROL 作者上的代理]**.
1. 在「作者上的代理程式」頁面上，選取 **[!UICONTROL Dynamic Media混合影像復寫(s7delivery)]**.
1. 选择&#x200B;**[!UICONTROL 编辑]**。
1. 選取 **[!UICONTROL 設定]** 標籤，然後輸入下列內容：

   * **[!UICONTROL 已啟用]**  — 選取此核取方塊以啟用復寫代理。
   * **[!UICONTROL 地區]**  — 設定為適當的區域：北美洲、歐洲或亞洲
   * **[!UICONTROL 租使用者ID]**  — 此值是您要發佈至復寫服務的公司/租使用者的名稱。 此值是Adobe在布建期間傳送給您的歡迎電子郵件中提供的租使用者ID。 如果您沒有收到此資訊，請聯絡Adobe客戶支援。
   * **[!UICONTROL 金鑰存放區別名]**  — 此值與 **新增別名** 在中產生索引鍵時設定的值 [設定驗證](#setting-up-authentication)；例如， `replication`. （請參閱中的步驟7） [設定驗證](#setting-up-authentication).)
   * **[!UICONTROL 金鑰庫密碼]**  — 您點選時建立的KeyStore密碼 **[!UICONTROL 建立KeyStore]**. Adobe未提供此密碼。 請參閱步驟5 / [設定驗證](#setting-up-authentication).

   下圖顯示具有範例資料的復寫代理程式：

   ![chlimage_1-509](assets/chlimage_1-509.png)

1. 選取 **[!UICONTROL 確定]**.

### 驗證Dynamic Media的復寫代理程式 {#validating-the-replication-agent-for-dynamic-media}

若要驗證Dynamic Media的復寫代理程式，請執行下列動作：

選取 **[!UICONTROL 測試連線]**. 範例輸出如下：

```shell
11.03.2016 10:57:55 - Transferring content for ReplicationAction{type=TEST, path[0]='/content/dam', time=1457722675402, userId='admin', revision='null'}
11.03.2016 10:57:55 - * Auth User: replication-receiver
11.03.2016 10:57:55 - * HTTP Version: 1.1
11.03.2016 10:57:55 - * Using OAuth 2.0 Authorization Grants
11.03.2016 10:57:55 - * OAuth 2.0 User: dynamic-media-replication
11.03.2016 10:57:55 - * OAuth 2.0 Token: '*****' initialized
11.03.2016 10:57:55 - Publishing: POST[https://replicate-na.assetsadobe.com:8580/is-publish/publish-receiver?Cmd=Test&RootId=xfpuu-6613]
11.03.2016 10:57:55 - Publish response: OK[]
11.03.2016 10:57:55 - Transfer succeeded in 141 ms for ReplicationAction{type=TEST, path[0]='/content/dam', time=1457722675402, userId='admin', revision='null'}
-------------------------------------------------------------------------------------------------------------------------------
Replication test succeeded
```

>[!NOTE]
您也可以執行下列任一項作業來檢查：
* 檢查復寫記錄檔，確認資產已復寫。
* 發佈影像。 選取影像並選取 **[!UICONTROL 檢視者]** 在下拉式功能表中，選取檢視器預設集。 選取 **[!UICONTROL URL]**. 若要確認您能看到影像，請複製並在瀏覽器中貼上URL路徑。
>


### 疑難排解驗證 {#troubleshooting-authentication}

設定驗證時，您可能會在其解決方案中遇到以下問題。 在檢查這些問題之前，請確定您已設定復寫。

#### 問題：HTTP狀態碼401及訊息 — 需要授權 {#problem-http-status-code-with-message-authorization-required}

此問題可能是由於無法設定的KeyStore `dynamic-media-replication` 使用者。

```shell
Replication test to s7delivery:https://s7bern.macromedia.com:8580/is-publish/
17.06.2016 18:54:43 - Transferring content for ReplicationAction{type=TEST, path[0]='/content/dam', time=1466214883309, userId='admin', revision='null'}
17.06.2016 18:54:43 - * Auth User: replication-receiver
17.06.2016 18:54:43 - * HTTP Version: 1.1
17.06.2016 18:54:43 - * Using OAuth 2.0 Authorization Grants
17.06.2016 18:54:43 - * OAuth 2.0 User: dynamic-media-replication
17.06.2016 18:54:43 - No OAuth token available. OAuth not initialized
17.06.2016 18:54:43 - * Using Client Auth SSL alias - replication-alias *
17.06.2016 18:54:43 - Publishing: POST[https://<localhost>:8580/is-publish//publish-receiver?Cmd=Test&RootId=brough]
17.06.2016 18:54:43 - Transfer failed for ReplicationAction{type=TEST, path[0]='/content/dam', time=1466214883309, userId='admin', revision='null'}. java.io.IOException: Failed to execute request
'https://<localhost>:8580/is-publish//publish-receiver?Cmd=Test&RootId=brough':
 Server returned status code 401 with message: Authorization required.
17.06.2016 18:54:43 - Error while replicating: com.day.cq.replication.ReplicationException: Transfer failed for ReplicationAction{type=TEST, path[0]='/content/dam', time=1466214883309,
 userId='admin', revision='null'}. java.io.IOException: Failed to execute request
'https://<localhost>:8580/is-publish//publish-receiver?Cmd=Test&RootId=brough':
 Server returned status code 401 with message: Authorization required.
```

**解決方案：**
檢查 `KeyStore` 已儲存至 **dynamic-media-replication** 使用者及已提供正確的密碼。

#### 問題：無法解密金鑰 — 無法解密資料 {#problem-could-not-decrypt-key-could-not-decrypt-data}

```xml
Replication test to s7delivery:https://<localhost>:8580/is-publish/
17.06.2016 19:00:16 - Transferring content for ReplicationAction{type=TEST, path[0]='/content/dam', time=1466215216662, userId='admin', revision='null'}
17.06.2016 19:00:16 - * Auth User: replication-receiver
17.06.2016 19:00:16 - * HTTP Version: 1.1
17.06.2016 19:00:16 - * Using OAuth 2.0 Authorization Grants
17.06.2016 19:00:16 - * OAuth 2.0 User: dynamic-media-replication
17.06.2016 19:00:16 - No OAuth token available. OAuth not initialized
17.06.2016 19:00:16 - * Using Client Auth SSL alias - replication-alias *
17.06.2016 19:00:16 - Transfer failed for ReplicationAction{type=TEST, path[0]='/content/dam', time=1466215216662, userId='admin', revision='null'}. java.lang.SecurityException: java.security.UnrecoverableKeyException: Could not decrypt key: Could not decrypt data.
```

**解決方案：**
檢查密碼。 儲存在復寫代理程式中的密碼與用來建立金鑰存放區的密碼不同。

#### 問題： InvalidAlgorithmParameterException {#problem-invalidalgorithmparameterexception}

此問題是由於Experience Manager編寫執行個體中的設定錯誤所導致。 作者的Java™程式不正確 `javax.net.ssl.trustStore`. 您在復寫記錄中看到此錯誤：

```shell
14.04.2016 09:37:43 - Transfer failed for ReplicationAction{type=TEST, path[0]='/content/dam', time=1460651862089, userId='admin', revision='null'}. java.io.IOException: Failed to execute request 'https://<localhost>:8580/is-publish/publish-receiver?Cmd=Test&RootId=rbrough-osx2': java.lang.RuntimeException: Unexpected error: java.security.InvalidAlgorithmParameterException: the trustAnchors parameter must be non-empty
14.04.2016 09:37:43 - Error while replicating: com.day.cq.replication.ReplicationException: Transfer failed for ReplicationAction{type=TEST, path[0]='/content/dam', time=1460651862089, userId='admin', revision='null'}. java.io.IOException: Failed to execute request 'https://<localhost>:8580/is-publish/publish-receiver?Cmd=Test&RootId=rbrough-osx2': java.lang.RuntimeException: Unexpected error: java.security.InvalidAlgorithmParameterException: the trustAnchors parameter must be non-empty
```

或錯誤記錄：

```shell
07.25.2019 12:00:59.893 *ERROR* [sling-threadpool-db2763bb-bc50-4bb5-bb64-10a09f432712-(apache-sling-job-thread-pool)-90-com_day_cq_replication_job_s7delivery(com/day/cq/replication/job/s7delivery)] com.day.cq.replication.Agent.s7delivery.queue Error during processing of replication.

java.io.IOException: Failed to execute request 'https://replicate-na.assetsadobe.com:8580/is-publish/publish-receiver?Cmd=Test&RootId=rbrough-osx': java.lang.RuntimeException: Unexpected error: java.security.InvalidAlgorithmParameterException: the trustAnchors parameter must be non-empty
        at com.scene7.is.catalog.service.publish.atomic.PublishingServiceHttp.executePost(PublishingServiceHttp.scala:195)
```

**解決方案：**
請確定Experience Manager作者上的Java™程式具有system屬性 `-Djavax.net.ssl.trustStore=` 設定為有效的truststore。

#### 問題： KeyStore未設定或未初始化 {#problem-keystore-is-either-not-set-up-or-it-is-not-initialized}

此問題可能是因為Hot Fix或Feature Pack覆寫Dynamic-Media-User或Keystore節點所造成。

復寫記錄範例：

```shell
Replication test to s7delivery:https://replicate-na.assetsadobe.com/is-publish
02.08.2016 14:37:44 - Transferring content for ReplicationAction{type=TEST, path[0]='/content/dam', time=1470173864834, userId='admin', revision='null'}
02.08.2016 14:37:44 - * Auth User: replication-receiver
02.08.2016 14:37:44 - * HTTP Version: 1.1
02.08.2016 14:37:44 - * Using OAuth 2.0 Authorization Grants
02.08.2016 14:37:44 - * OAuth 2.0 User: dynamic-media-replication
02.08.2016 14:37:44 - Transfer failed for ReplicationAction{type=TEST, path[0]='/content/dam', time=1470173864834, userId='admin', revision='null'}. com.adobe.granite.keystore.KeyStoreNotInitialisedException: Uninitialised key store for user dynamic-media-replication
```

**解决方案:**

1. 導覽至「使用者管理」頁面：
   `localhost:4502/libs/granite/security/content/useradmin.html`
1. 在「使用者管理」頁面上，導覽至 `dynamic-media-replication` 使用者，然後選取以開啟。
1. 選取 **[!UICONTROL 金鑰存放區]** 標籤。 如果 **[!UICONTROL 建立KeyStore]** 按鈕顯示，您必須重做底下的步驟 [設定驗證](#setting-up-authentication) 較早。
1. 如果您必須重做KeyStore設定，您必須執行 [設定復寫代理程式](/help/assets/config-dynamic.md#configuring-the-replication-agent) 同樣地。

   重新設定s7delivery Replication Agent。
   `localhost:4502/etc/replication/agents.author/s7delivery.html`

1. 選取 **[!UICONTROL 測試連線]** 以確認設定是否有效。

#### 問題：發佈代理程式正在使用SSL而不是OAuth {#problem-publish-agent-is-using-ssl-instead-of-oauth}

此問題可能是因為Hot Fix或Feature Pack未正確安裝或覆寫設定所造成。

復寫記錄範例：

```shell
01.08.2016 18:42:59 - Transferring content for ReplicationAction{type=TEST, path[0]='/content/dam', time=1470073379634, userId='admin', revision='null'}
01.08.2016 18:42:59 - * Auth User: replication-receiver
01.08.2016 18:42:59 - * HTTP Version: 1.1
01.08.2016 18:42:59 - * Using Client Auth SSL alias - replication-receiver *
01.08.2016 18:42:59 - Publishing: POST[https://replicate-eu.assetsadobe2.com:443/is-publish/publish-receiver?Cmd=Test&RootId=altayerstaging]
01.08.2016 18:42:59 - Transfer failed for ReplicationAction{type=TEST, path[0]='/content/dam', time=1470073379634, userId='admin', revision='null'}. java.io.IOException: Failed to execute request 'https://replicate-eu.assetsadobe2.com:443/is-publish/publish-receiver?Cmd=Test&RootId=rbroughstaging': Server returned status code 401 with message: Authorization required.
01.08.2016 18:42:59 - Error while replicating: com.day.cq.replication.ReplicationException: Transfer failed for ReplicationAction{type=TEST, path[0]='/content/dam', time=1470073379634, userId='admin', revision='null'}. java.io.IOException: Failed to execute request 'https://replicate-eu.assetsadobe2.com:443/is-publish/publish-receiver?Cmd=Test&RootId=rbroughstaging': Server returned status code 401 with message: Authorization required.
```

**解决方案:**

1. 在Experience Manager中，導覽至 **[!UICONTROL 工具]** > **[!UICONTROL 一般]** > **[!UICONTROL CRXDE Lite]**.

   `localhost:4502/crx/de/index.jsp`

1. 導覽至s7delivery Replication Agent節點。
   `localhost:4502/crx/de/index.jsp#/etc/replication/agents.author/s7delivery/jcr:content`

1. 將此設定新增至復寫代理程式(布林值，其值設定為 **[!UICONTROL True]**)：

   `enableOauth=true`

1. 在頁面的左上角附近，選取 **[!UICONTROL 全部儲存]**.

### 測試您的設定 {#testing-your-configuration}

Adobe建議您執行設定的端對端測試。

在開始此測試之前，請確定您已完成下列操作：

* 新增影像預設集。
* 設定 **[!UICONTROL Dynamic Media設定（6.3以前版本）]** 在「Cloud Services」底下。 此測試需要影像服務URL

**若要測試您的設定：**

1. 上傳影像資產。 (在「資產」中，導覽至 **[!UICONTROL 建立]** > **[!UICONTROL 檔案]** 並選取檔案。)
1. 等待工作流程完成。
1. 發佈影像資產。 (選取資產並選取 **[!UICONTROL 快速發佈]**.)
1. 透過開啟影像並點選，導覽至該影像的轉譯 **[!UICONTROL 轉譯]**.

   ![chlimage_1-510](assets/chlimage_1-510.png)

1. 選取任何動態轉譯。
1. 若要取得此資產的URL，請選取 **[!UICONTROL URL]**.
1. 導覽至選取的URL，並檢查影像是否如預期般運作。

測試您的資產是否已傳遞的另一種方法是，將req=exists附加至您的URL。

## 設定Dynamic MediaCloud Services {#configuring-dynamic-media-cloud-services}

Dynamic MediaCloud Service支援影像和視訊、視訊分析和視訊編碼等的混合式發佈和傳送。

在設定過程中，您必須輸入註冊ID、視訊服務URL、影像服務URL、復寫服務URL，並設定驗證。 此資訊是透過電子郵件傳送給您，作為帳戶布建程式的一部分。 如果您沒有收到此資訊，請聯絡Adobe Experience Manager管理員或Adobe客戶支援以取得資訊。

>[!NOTE]
設定Dynamic Media Cloud Services之前，請務必先設定您的發佈執行個體。 在設定Dynamic MediaCloud Services之前，您也必須設定復寫。

**若要設定Dynamic MediaCloud Services：**

1. 在Experience Manager中，選取Experience Manager標誌以存取全域導覽主控台，然後導覽至 **[!UICONTROL 工具]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Dynamic Media設定（6.3以前版本）]**.
1. 在Dynamic Media設定瀏覽器頁面的左側窗格中，選取 **[!UICONTROL 全域]**，然後選取 **[!UICONTROL 建立]**.
1. 在 **[!UICONTROL 建立Dynamic Media設定]** 對話方塊中，在「標題」欄位中輸入標題。
1. 如果您要設定Dynamic Media的視訊，

   * 在 **[!UICONTROL 註冊ID]** 欄位，輸入您的註冊ID。
   * 在 **[!UICONTROL 視訊服務URL]** 欄位中，輸入Dynamic Media閘道的視訊服務URL。

1. 如果您要設定Dynamic Media以進行影像處理，請在 **[!UICONTROL 影像服務URL]** 欄位中，輸入Dynamic Media閘道的影像服務URL。
1. 選取 **[!UICONTROL 儲存]** 返回Dynamic Media設定瀏覽器頁面。
1. 若要存取全域導覽主控台，請選取Experience Manager標誌。

## 設定視訊報告 {#configuring-video-reporting}

您可以使用Dynamic Media Hybrid在Experience Manager的多個安裝間設定視訊報表。

**何時使用：** 當您設定Dynamic Media設定（6.3以前版本）時，多項功能即會啟動，包括視訊報告功能。 此設定會在地區性Analytics公司中建立報表套裝。 如果您設定多個作者節點，需為每個節點建立個別的報表套裝。 因此，不同安裝之間的報表資料不一致。 此外，如果每個作者節點參考相同的混合式發佈伺服器，則上次的作者安裝會變更所有視訊報表的目標報表套裝。 此問題會讓Analytics系統超載，造成太多報表套裝。

**開始使用：** 完成下列三個工作來設定視訊報表。

1. 在第一個作者節點上設定Dynamic Media設定（6.3以前版本）後，請建立Video Analytics預設集套件。 此初始工作很重要，因為它可讓新設定繼續使用相同的報表套裝。
1. 將Video Analytics預設集套件安裝至任何 ***新*** 作者節點 ***早於*** 您可以設定Dynamic Media設定（6.3以前版本）。
1. 驗證及偵錯套件安裝。

### 設定第一個「作者」節點後，建立Video Analytics預設集套件 {#creating-a-video-analytics-preset-package-after-configuring-the-first-author-node}

完成此工作後，您會有包含Video Analytics預設集的套件檔案。 這些預設集包含報表套裝、追蹤伺服器、追蹤名稱空間及Experience Cloud組織ID （若有）。

1. 如果您尚未這樣做，請設定Dynamic Media設定（6.3以前版本）。
1. （選用）檢視和複製報表套裝ID （您必須擁有JCR的存取權）。 雖然不需要報表套裝ID，但可讓驗證更輕鬆。
1. 使用「封裝管理員」建立封裝。
1. 編輯套件以包含篩選器。

   Experience Manager： `/conf/global/settings/dam/dm/presets/analytics/jcr:content/userdata`

1. 构建包。
1. 下載或分享Video Analytics預設集套件，以便與後續的新作者節點分享。

### 在設定更多作者節點之前，請先安裝Video Analytics預設集套件 {#installing-the-video-analytics-preset-package-before-you-configure-additional-author-nodes}

請確定您已完成此工作 ***早於*** 您可以設定Dynamic Media設定（6.3以前版本）。 若未這麼做，則會建立另一個未使用的報表套裝。 此外，即使視訊報表繼續正常運作，但資料收集並未最佳化。

請確定第一個作者節點的Video Analytics預設集套件可在新的作者節點上存取。

1. 將您先前建立的Video Analytics預設集套件上傳至封裝管理員。
1. 安裝Video Analytics預設集套件。
1. 設定Dynamic Media設定（6.3以前版本）。

### 驗證及偵錯套件安裝 {#verifying-and-debugging-the-package-installation}

1. 執行下列任一項作業，驗證套件安裝，並視需要偵錯套件安裝：

   * **透過JCR檢查視訊分析預設集**
若要透過JCR檢查Video Analytics預設集，您必須擁有CRXDE Lite存取權。

      Experience Manager — 在CRXDE Lite中，導覽至 `/conf/global/settings/dam/dm/presets/analytics/jcr:content/userdata`

      如在 `https://localhost:4502/crx/de/index.jsp#/conf/global/settings/dam/dm/presets/analytics/jcr%3Acontent/userdata`

      如果您無權存取Author節點上的CRXDE Lite，您可以透過Publish伺服器檢查預設集。

   * **透過影像伺服器檢查Video Analytics預設集**

      您可以發出影像伺服器req=userdata要求，直接驗證Video Analytics預設集。
例如，若要檢視「作者」節點上的Analytics預設集，您可以提出以下請求：

      `https://localhost:4502/is/image/conf/global/settings/dam/dm/presets/analytics?req=userdata`

      若要在發佈伺服器上驗證預設集，您可以向發佈伺服器提出類似的直接請求。 在「作者」和「發佈」節點上的回應是相同的。 回應看起來類似下列：

      ```
      marketingCloudOrgId=0FC4E86B573F99CC7F000101
       reportSuite=aemaem6397618-2018-05-23
       trackingNamespace=aemvideodal
       trackingServer=aemvideodal.d2.sc.omtrdc.net
      ```

   * **透過Experience Manager中的視訊報告工具檢查視訊分析預設集**
導覽至 **[!UICONTROL 工具]** > **[!UICONTROL 資產]** > **[!UICONTROL 視訊報告]**

      `https://localhost:4502/mnt/overlay/dam/gui/content/s7dam/videoreports/videoreport.html`

      如果您看到下列錯誤訊息，表示報表套裝可供使用，但未填入。 在系統收集任何資料之前，在新安裝中，此錯誤是正確的，也是必要的。
   ![screen_shot_2018-05-23at52254pm](assets/screen_shot_2018-05-23at52254pm.png)

   若要產生報表資料，請上傳並發佈一段影片。 使用 **[!UICONTROL 複製URL]** 並至少執行一次視訊。

   從Video Viewer使用狀況填入報表資料最多可能需要12小時的時間。

   如果出現錯誤，且報表套裝未正確設定，則會顯示以下警報。

   ![screen_shot_2018-05-23at52612pm](assets/screen_shot_2018-05-23at52612pm.png)

   如果您在設定Dynamic Media設定（6.3以前版本）服務之前執行視訊報告，也會顯示此錯誤。

### 疑難排解視訊報表設定 {#troubleshooting-the-video-reporting-configuration}

* 在安裝期間，有時候與Analytics API伺服器的連線會逾時。 安裝會重試連線20次，但還是會失敗。 發生這種情況時，記錄檔會記錄多個錯誤。 搜索 `SiteCatalystReportService`.
* 不先安裝Analytics預設集套件可能會導致建立新的報表套裝。
* 從Experience Manager6.3升級至Experience Manager6.4或Experience Manager6.4.1，接著設定Dynamic Media設定（6.3以前版本），仍會建立報表套裝。 此問題已知且預定會在Experience Manager6.4.2中修正。

### 關於視訊分析預設集 {#about-the-video-analytics-preset}

Video Analytics預設集（有時簡稱為Analytics預設集）儲存在Dynamic Media中的檢視器預設集旁邊。 它基本上與檢視器預設集相同，但含有用來設定AppMeasurement和視訊心率報表的資訊。

預設集的屬性如下：

* `reportSuite`
* `trackingServer`
* `trackingNamespace`
* `marketingCloudOrgId` (在舊版Experience Manager中不存在)

Experience Manager6.4和更新版本將此預設集儲存在 `/conf/global/settings/dam/dm/presets/analytics/jcr:content/userdata`

## 復寫目錄設定 {#replicating-catalog-settings}

在設定程式中透過JCR發佈您自己的預設目錄設定。 若要複製目錄設定：

1. 在「終端機」視窗中，執行下列動作：

   `curl -u admin:admin localhost:4502/libs/settings/dam/dm/presets/viewer.pushviewerpresets`

1. 在Experience Manager中，瀏覽至CRXDE Lite中的以下位置（需要管理員許可權）：

   `https://<*server*>:<*port*>/crx/de/index.jsp#/conf/global/settings/dam/dm/imageserver/`

1. 選取 **[!UICONTROL 復寫]** 標籤。
1. 選取 **[!UICONTROL 復寫]**.

## 複製檢視器預設集 {#replicating-viewer-presets}

要傳遞 *具有檢視器預設集的資產，您必須複製/發佈* 檢視器預設集。 (必須啟用所有檢視器預設集 *和* 復寫以取得資產的URL或內嵌程式碼。
另請參閱 [發佈檢視器預設集](/help/assets/managing-viewer-presets.md#publishing-viewer-presets) 以取得詳細資訊。

>[!NOTE]
依預設，當您選取時，系統會顯示各種轉譯 **[!UICONTROL 轉譯]** 和各種檢視器預設集 **[!UICONTROL 檢視者]** 在資產的詳細資料檢視中。 您可以增加或減少看到的數量。 另請參閱 [增加顯示的影像預設集數目](/help/assets/managing-image-presets.md#increasing-or-decreasing-the-number-of-image-presets-that-display) 或 [增加顯示的檢視器預設集數目](/help/assets/managing-viewer-presets.md#increasing-the-number-of-viewer-presets-that-display).

## 篩選資產以進行復寫 {#filtering-assets-for-replication}

在非Dynamic Media部署中，您需進行復寫 *全部* 資產（包括影像和視訊）從Experience Manager製作環境移至Experience Manager發佈節點。 此工作流程是必要的，因為Experience Manager Publish伺服器也會傳送資產。

不過，在Dynamic Media部署中，由於資產是透過雲端傳送，因此不需要將這些相同的資產復寫至Experience Manager發佈節點。 這種「混合式發佈」工作流程可避免額外的儲存成本及較長的複製資產處理時間。 Dynamic Media檢視器、網站頁面和靜態內容等其他內容會繼續從Experience Manager發佈節點提供。

除了復寫資產外，也會復寫下列非資產：

* Dynamic Media傳遞設定： `/conf/global/settings/dam/dm/imageserver/jcr:content`
* 图像预设: `/conf/global/settings/dam/dm/presets/macros`
* 查看器预设: `/conf/global/settings/dam/dm/presets/viewer`

這些篩選器可讓您 *排除* 資產無法復寫至Experience Manager發佈節點。

### 使用預設的資產篩選器進行復寫 {#using-default-asset-filters-for-replication}

如果您在生產環境中使用Dynamic Media進行(1)影像處理 *或* (2)影像與視訊，然後您可以使用Adobe依現狀提供的預設濾鏡。 下列篩選器預設為作用中：

<table>
 <tbody>
  <tr>
   <td> </td>
   <td><strong>过滤器</strong></td>
   <td><strong>Mime型別</strong></td>
   <td><strong>演绎版</strong></td>
  </tr>
  <tr>
   <td>Dynamic Media影像傳送</td>
   <td><p>filter-images</p> <p>篩選集</p> <p> </p> </td>
   <td><p>開頭為 <strong>image/</strong></p> <p>包含 <strong>應用程式/</strong> 結束於 <strong>set</strong>.</p> </td>
   <td>現成可用的「濾鏡影像」（適用於單一影像資產，包括互動式影像）和「濾鏡集」（適用於迴轉集、影像集、混合媒體集和轉盤集）將：
    <ul>
     <li>包含PTIFF影像和中繼資料以進行復寫(任何開頭為 <strong>cqdam</strong>)。</li>
     <li>從復寫中排除原始影像和靜態影像轉譯。</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Dynamic Media視訊傳送</td>
   <td>濾鏡 — 視訊</td>
   <td>開頭為 <strong>video/</strong></td>
   <td>現成可用的「filter-video」將：
    <ul>
     <li>包含Proxy視訊轉譯、視訊縮圖/海報影像、中繼資料（同時在父視訊和視訊轉譯中）以供復寫(任何開頭為 <strong>cqdam</strong>)。</li>
     <li>從復寫中排除原始視訊和靜態縮圖轉譯。<br /> <br /> <strong>注意：</strong> Proxy視訊轉譯不包含二進位檔案，而是只有節點屬性。 因此，對發佈者存放庫大小沒有影響。</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Dynamic Media Classic (Scene7)整合</td>
   <td><p>filter-images</p> <p>篩選集</p> <p>濾鏡 — 視訊</p> </td>
   <td><p>開頭為 <strong>image/</strong></p> <p>包含 <strong>應用程式/</strong> 結束於 <strong>set</strong>.</p> <p>開頭為 <strong>video/</strong></p> </td>
   <td><p>您可以設定傳輸URI以指向您的Experience Manager發佈伺服器，而不是AdobeDynamic Media雲端復寫服務URL。 設定此篩選器可讓Dynamic Media Classic傳送資產，而非Experience Manager發佈執行個體。</p> <p>現成可用的「filter-images」、「filter-sets」和「filter-video」將：</p>
    <ul>
     <li>包含PTIFF影像、Proxy視訊轉譯以及用於復寫的中繼資料。 但是，由於這些範本不存在於針對執行Experience Manager的JCR中 — Dynamic Media Classic整合 — 它實際上不會執行任何動作。</li>
     <li>從複製中排除原始影像、靜態影像轉譯、原始視訊和靜態縮圖轉譯。 Dynamic Media Classic而是提供影像和視訊資產。</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
篩選器套用至MIME型別，且不能為路徑專用。

### 設定僅視訊部署的資產篩選器 {#setting-up-asset-filters-for-video-only-deployments}

如果您將Dynamic Media用於僅限視訊，請依照下列步驟設定用於復寫的資產篩選器：

1. 在Experience Manager中，選取Experience Manager標誌以存取全域導覽主控台，然後導覽至 **[!UICONTROL 工具]** > **[!UICONTROL 部署]** > **[!UICONTROL 復寫]** > **[!UICONTROL 作者上的代理]**.
1. 在「作者上的代理程式」頁面上，選取 **[!UICONTROL 預設代理程式（發佈）]**.
1. 选择&#x200B;**[!UICONTROL 编辑]**。
1. 在 **[!UICONTROL 代理程式設定]** 對話方塊，在 **[!UICONTROL 設定]** 索引標籤，核取 **[!UICONTROL 已啟用]** 以開啟代理程式。
1. 選取 **[!UICONTROL 確定]**.
1. 在Experience Manager中，導覽至 **[!UICONTROL 工具]** > **[!UICONTROL 一般]** > **[!UICONTROL CRXDE Lite]**.
1. 在左側資料夾樹狀結構中，導覽至 `/etc/replication/agents.author/dynamic_media_replication/jcr:content/damRenditionFilters`
1. 尋找 **[!UICONTROL 濾鏡 — 視訊]**，以滑鼠右鍵按一下該區段，然後選取 **[!UICONTROL 複製]**.
1. 在左側資料夾樹狀結構中，導覽至 `/etc/replication/agents.author/publish`
1. 尋找 `jcr:content`，以滑鼠右鍵按一下該區段，然後選取 **[!UICONTROL 貼上]**.

這些步驟會設定Experience Manager發佈執行個體，在視訊本身由Dynamic MediaCloud Service傳送時，傳送視訊海報影像和播放所需的視訊中繼資料。 此篩選器也會將原始視訊和靜態縮圖轉譯排除在復寫之外，因為發佈執行個體上不需要這些轉譯。

### 設定資產篩選器，以便在非生產部署中成像 {#setting-up-asset-filters-for-imaging-in-non-production-deployments}

如果您使用Dynamic Media在非生產部署中進行影像處理，請依照下列步驟設定用於復寫的資產篩選器：

1. 在Experience Manager中，選取Experience Manager標誌以存取全域導覽主控台，然後導覽至 **[!UICONTROL 工具]** > **[!UICONTROL 部署]** > **[!UICONTROL 復寫]** > **[!UICONTROL 作者上的代理]**.
1. 在「作者上的代理程式」頁面上，選取 **[!UICONTROL 預設代理程式（發佈）]**.
1. 选择&#x200B;**[!UICONTROL 编辑]**。
1. 在 **[!UICONTROL 代理程式設定]** 對話方塊，在 **[!UICONTROL 設定]** 索引標籤，核取 **[!UICONTROL 已啟用]** 以開啟代理程式。
1. 選取 **[!UICONTROL 確定]**.
1. 在Experience Manager中，導覽至 **[!UICONTROL 工具]** > **[!UICONTROL 一般]** > **[!UICONTROL CRXDE Lite]**.
1. 在左側資料夾樹狀結構中，導覽至 `/etc/replication/agents.author/dynamic_media_replication/jcr:content/damRenditionFilters`

   ![image-2018-01-16-10-22-40-410](assets/image-2018-01-16-10-22-40-410.png)

1. 尋找 **[!UICONTROL filter-images]**，以滑鼠右鍵按一下該區段，然後選取 **[!UICONTROL 複製]**.
1. 在左側資料夾樹狀結構中，導覽至 `/etc/replication/agents.author/publish`
1. 尋找 `jcr:content`，以滑鼠右鍵按一下該區段，然後前往 **[!UICONTROL 建立]** > **[!UICONTROL 建立節點]**. 輸入名稱 `damRenditionFilters` 型別 `nt:unstructured`.
1. 尋找 `damRenditionFilters`，以滑鼠右鍵按一下該區段，然後選取 **[!UICONTROL 貼上]**.

這些步驟會設定Experience Manager發佈執行個體，以將影像傳送至您的非生產環境。 此篩選器也會將原始影像和靜態轉譯排除在復寫之外，因為發佈執行個體上不需要這些原始影像和靜態轉譯。

>[!NOTE]
如果作者中有許多不同的篩選器，每個代理程式都需要指派不同的使用者。 Granite程式碼會強制每個使用者一個篩選模型。 每個篩選器設定一律有不同的使用者。
您在伺服器上使用多個篩選器嗎？ 例如，一個篩選器用於復寫至發佈，第二個篩選器用於s7delivery。 若是如此，您必須確定這兩個篩選器有不同的值 **userId** 指派給他們的 `jcr:content` 節點。 請參閱下列影像：

![image-2018-01-16-10-26-28-465](assets/image-2018-01-16-10-26-28-465.png)

### 自訂資產篩選器以進行復寫（選用） {#customizing-asset-filters-for-replication}

1. 在Experience Manager中，選取Experience Manager標誌以存取全域導覽主控台，然後導覽至 **[!UICONTROL 工具]** > **[!UICONTROL 一般]** > **[!UICONTROL CRXDE Lite]**.
1. 在左側資料夾樹狀結構中，導覽至 `/etc/replication/agents.author/dynamic_media_replication/jcr:content/damRenditionFilters` 以檢閱篩選器。

   ![chlimage_1-511](assets/chlimage_1-511.png)

1. 若要定義篩選器的MIME型別，您可以依照以下步驟找到「MIME型別」：

   在左側邊欄中，展開 `content > dam > <locate_your_asset> >  jcr:content > metadata` 然後在表格中，找出 `dc:format`.

   下圖為資產路徑至的範例： `dc:format`.

   ![chlimage_1-512](assets/chlimage_1-512.png)

   請注意 `dc:format` 資產的 `Fiji Red.jpg` 是 `image/jpeg`.

   若要將此篩選套用至所有影像，無論其格式為何，請將此值設為 `image/*` 位置 `*` 是套用至任何格式之所有影像的規則運算式。

   若要讓篩選器僅套用至型別JPEG的影像，請輸入值 `image/jpeg`.

1. 定義您要在復寫中包含或排除的轉譯。

   您可以用來篩選復寫字元的字元包括：

   | 要使用的字元 | 如何篩選資產以進行復寫 |
   | --- | --- |
   | `*` | 通配符 |
   | `+` | 包含用於復寫的資產 |
   | `-` | 從復寫中排除資產 |

   导航到 `content/dam/<locate your asset>/jcr:content/renditions`。

   下圖是資產的轉譯範例。

   ![chlimage_1-513](assets/chlimage_1-4.png)

   根據上述範例，如果您只想複製PTIFF (金字塔TIFF)，則您可以輸入 `+cqdam,*` 包括開頭為的所有轉譯 `cqdam`. 在此範例中，該轉譯為 `cqdam.pyramid.tiff`.

   如果您只想複製原始檔案，您可以輸入 `+original`.

## 正在設定Dynamic Media影像伺服器設定 {#configuring-dynamic-media-image-server-settings}

設定Dynamic Media影像伺服器需要編輯Adobe CQ Scene7 ImageServer套件組合和Adobe CQ Scene7 PlatformServer套件組合。

>[!NOTE]
Dynamic Media現成可用 [啟用後](#enabling-dynamic-media). 不過，您可以選擇設定Dynamic Media Image Server來微調安裝，以符合特定規格或需求。

**先決條件** - *早於* 設定Dynamic Media Image Server時，請確定Windows®的VM包含Microsoft® Visual C++程式庫的安裝。 執行Dynamic Media Image Server時，必須要有程式庫。 您可以 [在此處下載Microsoft® Visual C++ 2010可轉散發套件(x64)](https://www.microsoft.com/en-us/download/details.aspx?id=26999).

若要設定Dynamic Media影像伺服器設定：

1. 在Experience Manager的左上角，選取 **[!UICONTROL Adobe Experience Manager]** 若要存取全域導覽主控台，請導覽至 **[!UICONTROL 工具]** > **[!UICONTROL 作業]** > **[!UICONTROL 網頁主控台]**.
1. 在Adobe Experience Manager Web Console設定頁面上，前往 **[!UICONTROL osgi]** > **[!UICONTROL 設定]** 以列出目前在Experience Manager內執行的所有組合。

   Dynamic Media傳遞伺服器位於清單中的下列名稱下：

   * `Adobe CQ Scene7 ImageServer`
   * `Adobe CQ Scene7 PlatformServer`

1. 在套件清單中，在Adobe CQ Scene7 ImageServer的右側，選取 **[!UICONTROL 編輯]** 圖示。
1. 在Adobe CQ Scene7 ImageServer對話方塊中，設定下列設定值：

   >[!NOTE]
   通常不需要變更預設值。 但是，如果您確實變更了預設值，則必須重新啟動束才能使變更生效。

   | 属性 | 預設值 | 描述 |
   | --- | --- | --- |
   | `TcpPort.name` | *`empty`* | 用來與ImageServer處理序通訊的連線埠號碼。 預設會自動偵測自由連線埠。 |
   | `AllowRemoteAccess.name` | *`empty`* | 允許或不允許遠端存取ImageServer處理序。 如果為false，則影像伺服器只會在localhost上接聽。<br> 指向本機主機的預設Externalizer設定值必須指定特定VM執行處理的實際網域或IP位址。 原因在於localhost指向VM的父系。<br>VM的網域或IP位址必須有主機檔案專案，才能自行解析。 |
   | `MaxRenderRgnPixels` | 160萬畫素 | 已轉譯的大小上限（百萬畫素）。 |
   | `MaxMessageSize` | 16 MB | 傳遞的訊息大小上限（以MB為單位）。 |
   | `RandomAccessUrlTimeout` | 20 | 逾時值：影像伺服器等待JCR回應範圍並排要求的時間（以秒為單位）。 |
   | `WorkerThreads` | 10 | 工作者執行緒數目。 |

1. 选择&#x200B;**[!UICONTROL 保存]**。
1. 在套件組合清單中，在Adobe CQ Scene7 PlatformServer的右側，選取 **[!UICONTROL 編輯]** 圖示。
1. 在Adobe CQ Scene7 PlatformServer對話方塊中，設定下列預設值選項：

   >[!NOTE]
   Dynamic Media Image Server會使用自己的磁碟快取來快取回應。 Experience ManagerHTTP快取和Dispatcher無法用於快取來自Dynamic Media Image Server的回應。

   | 属性 | 預設值 | 描述 |
   |---|---|---|
   | 已啟用快取 | 已选中 | 回應快取是否已啟用 |
   | 快取根目錄 | cache | 回應快取資料夾的一或多個路徑。 相對路徑會針對內部s7影像組合資料夾進行解析。 |
   | 快取大小上限 | 200000000 | 回應快取的大小上限（位元組）。 |
   | 快取最大專案數 | 100000 | 快取中允許的最大專案數。 |

### 預設資訊清單設定 {#default-manifest-settings}

預設資訊清單可讓您設定用來產生Dynamic Media傳送回應的預設值。 您可以微調品質(JPEG品質、解析度、重新取樣模式)、快取（有效期），以及防止轉譯過大(defaultpix、defaultthumbpix、maxpix)的影像。

預設資訊清單設定的位置取自 **[!UICONTROL 目錄根目錄]** 的預設值 **[!UICONTROL Adobe CQ Scene7平台伺服器]** 套件組合。 根據預設，此值位於以下路徑： **[!UICONTROL 工具]** > **[!UICONTROL 一般]** > **[!UICONTROL CRXDE Lite]**

`/conf/global/settings/dam/dm/imageserver/`

![在CRXDE Lite中設定影像伺服器](assets/configimageservercrxdelite.png)

您可以輸入新值來變更屬性的值，如下表所述。

變更完預設資訊清單後，在頁面的左上角，選取 **[!UICONTROL 全部儲存]**.

請務必選取 **[!UICONTROL 存取控制]** 標籤（「屬性」標籤右側），然後將存取控制許可權設定為 `jcr:read` 適用於所有使用者和dynamic-media-replication使用者。

![在CRXDE Lite中設定「影像伺服器」並設定「存取控制」標籤](assets/configimageservercrxdeliteaccesscontroltab.png)

資訊清單設定及其預設值的表格：

| 属性 | 預設值 | 描述 |
| --- | --- | --- |
| `bkgcolor` | `FFFFFF` | 默认背景颜色. 用於填滿不包含實際影像資料之回覆影像任何區域的RGB值。 另請參閱 [BkgColor](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-bkgcolor.html#image-serving-api) 影像伺服API中的。 |
| `defaultpix` | `300,300` | 默认视图大小. 如果要求未使用wid=、hei=或scl=明確指定檢視大小，伺服器會將回覆影像限製為不得大於此寬度與高度。<br>指定為兩個整數，0或更大，以逗號分隔。 寬度和高度（畫素）。 任一或兩個值都可以設定為0，以保持其不受限制。 不適用於巢狀/內嵌請求。<br>另請參閱 [預設畫素](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-defaultpix.html#image-serving-api) 影像伺服API中的。<br>不過，您通常是使用檢視器預設集或影像預設集來傳送資產。 Defaultpix僅適用於未使用檢視器預設集或影像預設集的資產。 |
| `defaultthumbpix` | `100,100` | 默认缩略图大小. 用於縮圖要求(`req=tmb`)。<br>伺服器會將回覆影像限製為不得大於此寬度與高度。 如果縮圖要求(`req=tmb`)不會明確指定大小，也不會明確使用指定檢視大小 `wid=`， `hei=`，或 `scl=`.<br>指定為兩個整數，0或更大，以逗號分隔。 寬度和高度（畫素）。 任一或兩個值都可以設定為0，以保持其不受限制。<br>不適用於巢狀/內嵌請求。<br>另請參閱 [DefaultthumbPix](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-defaultthumbpix.html#image-serving-api) 影像伺服API中的。 |
| `expiration` | `36000000` | 預設使用者端快取存留時間。 提供預設到期時間間隔，以防止特定目錄記錄未包含有效的目錄：：Expiration值。<br>實數，0或更大。 從產生回覆資料到到期為止的毫秒數。 設為0可一律使回覆影像立即過期，以有效停用使用者端快取。 預設情況下，此值會設為10小時，這表示如果發佈新影像，則舊影像需要10小時才能離開使用者的快取。 如果您需要更早清除快取，請聯絡客戶支援。<br>另請參閱 [有效期](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-expiration.html) 影像伺服API中的。 |
| `jpegquality` | `80` | 預設JPEG編碼屬性。 指定JPEG回覆影像的預設屬性。<br>整數與旗標，以逗號分隔。 第一個值在1到100的範圍內，並定義品質。 第二個值可以是0 （代表正常行為），或是1 (代表JPEG編碼器採用的RGB色度縮減取樣)來停用。<br>另請參閱 [JpegQuality](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-jpegquality.html#image-serving-api) 影像伺服API中的。 |
| `maxpix` | `2000,2000` | 回复图像大小限制. 傳回給使用者端的最大回覆影像寬度和高度。<br>如果要求造成回覆影像的寬度或高度大於attribute：：MaxPix，伺服器會傳回錯誤。<br>另請參閱 [MaxPix](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-maxpix.html#image-serving-api) 影像伺服API中的。 |
| `resmode` | `SHARP2` | 默认重新取样模式. 指定用來縮放影像資料的預設重新取樣與內插屬性。<br>使用時機 `resMode=` 請求中未指定。<br>允許的值包括 `BILIN`， `BICUB`，或 `SHARP2`.<br>列舉。 設為2 `bilin`， 3表示 `bicub`，或4個 `sharp2` 內插模式。 使用 `sharp2` 以取得最佳結果。<br>另請參閱 [解析模式](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-is-cat-resmode.html#image-serving-api) 影像伺服API中的。 |
| `resolution` | `72` | 預設物件解析度。 提供預設物件解析度，以防止特定目錄記錄未包含有效的catalog：：Resolution值。<br>大於0的實數。 通常以畫素/英吋表示，但也可用其他單位，例如每米的畫素。<br>另請參閱 [解析度](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-resolution.html#image-serving-api) 影像伺服API中的。 |
| `thumbnailtime` | `1%,11%,21%,31%,41%,51%,61%,71%,81%,91%` | 這些值代表視訊播放時間的快照，並傳遞至 [encoding.com](https://www.encoding.com/). 另請參閱 [關於視訊縮圖](/help/assets/video.md#about-video-thumbnails-in-dynamic-media-hybrid-mode) 以取得詳細資訊。 |

## 設定Dynamic Media色彩管理 {#configuring-dynamic-media-color-management}

Dynamic Media色彩管理可讓您校正資產的色彩，以進行預覽。

透過色彩校正，擷取的資產可保留其色彩空間(RGB、CMYK、灰色)並在產生的金字塔TIFF轉譯中嵌入色彩設定檔。 當您請求動態轉譯時，影像顏色會校正到目標色域中。 您可以在JCR的Dynamic Media發佈設定中設定輸出色彩設定檔。

Adobe的色彩管理使用ICC （國際色彩聯盟）設定檔，這是ICC定義的格式。

您可以設定Dynamic Media色彩管理，並使用CMYK、RGB或灰階輸出來設定影像預設集。 另請參閱 [設定影像預設集](/help/assets/managing-image-presets.md).

進階使用案例可以使用手動設定 `icc=` 修飾元，可明確選取輸出色彩設定檔：

* `icc` - [https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-icc.html](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-icc.html)

* `iccEmbed` - [https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-iccembed.html](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-iccembed.html)

>[!NOTE]
標準Adobe色彩設定檔集僅在您有 [Software Distribution的Feature Pack 12445](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq630/featurepack/cq-6.3.0-featurepack-12445) 已安裝。 所有Feature Pack和Service Pack都可在 [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html). Feature Pack 12445提供Adobe的色彩設定檔。


### 安裝Feature Pack 12445 {#installing-feature-pack}

若要使用Dynamic Media色彩管理功能，請安裝Feature Pack 12445。

**若要安裝Feature Pack 12445：**

1. 導覽至 [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html) 並下載 `cq-6.3.0-featurepack-12445`.

   另請參閱 [如何使用套件](/help/sites-administering/package-manager.md) 有關在中使用套件的詳細資訊 [!DNL Adobe Experience Manager].

1. 安裝功能套件。

### 設定預設色彩設定檔 {#configuring-the-default-color-profiles}

安裝Feature Pack後，請設定適當的預設色彩設定檔，以便在請求RGB或CMYK影像資料時啟用色彩校正。

**若要設定預設色彩設定檔：**

1. 在 **[!UICONTROL 工具]** > **[!UICONTROL 一般]** > **[!UICONTROL CRXDE Lite]**，導覽至 `/conf/global/settings/dam/dm/imageserver/jcr:content` ，其中包含預設的Adobe Color設定檔。

   ![chlimage_1-514](assets/chlimage_1-514.png)

1. 捲動至底端，新增色彩校正屬性。 **[!UICONTROL 屬性]** 標籤。 手動輸入屬性名稱、型別和值，如下表所述。 輸入值後，選取 **[!UICONTROL 新增]** 然後 **[!UICONTROL 全部儲存]** 以儲存您的值。

   色彩校正屬性的說明請參閱 **色彩校正屬性** 表格。 您可以指派給色彩校正屬性的值位於 **色彩設定檔** 表格。

   例如，在 **[!UICONTROL 名稱]**，新增 `iccprofilecmyk`，選取 **[!UICONTROL 型別]** `String`，並新增 `WebCoated` as a **[!UICONTROL 值]**. 然後選取 **[!UICONTROL 新增]** 然後 **[!UICONTROL 全部儲存]** 以儲存您的值。

   ![chlimage_1-515](assets/chlimage_1-515.png)

   **色彩校正屬性表格**

<table>
 <tbody>
  <tr>
   <td><strong>属性</strong></td>
   <td><strong>类型</strong></td>
   <td><strong>默认</strong></td>
   <td><strong>描述</strong></td>
  </tr>
  <tr>
   <td><a href="https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccprofilergb.html">iccprofilergb</a></td>
   <td>字符串</td>
   <td>&lt;empty&gt;</td>
   <td>預設RGB色彩設定檔的名稱。</td>
  </tr>
  <tr>
   <td><a href="https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccprofilecmyk.html">iccprofilecmyk</a></td>
   <td>字符串</td>
   <td>&lt;empty&gt;</td>
   <td>預設CMYK色彩設定檔的名稱。</td>
  </tr>
  <tr>
   <td><a href="https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccprofilegray.html">iccprofilegray</a></td>
   <td>字符串</td>
   <td>&lt;empty&gt;</td>
   <td>預設灰階色彩設定檔的名稱。</td>
  </tr>
  <tr>
   <td><a href="https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccprofilesrcrgb.html">iccprofilesrcrgb</a></td>
   <td>字符串</td>
   <td>&lt;empty&gt;</td>
   <td>用於沒有內嵌色彩設定檔的RGB影像的預設RGB色彩設定檔名稱</td>
  </tr>
  <tr>
   <td><a href="https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccprofilesrccmyk.html">iccprofilesrccmyk</a></td>
   <td>字符串</td>
   <td>&lt;empty&gt;</td>
   <td>用於沒有內嵌色彩設定檔的CMYK影像的預設CMYK色彩設定檔名稱。</td>
  </tr>
  <tr>
   <td><a href="https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccprofilesrcgray.html">iccprofilesrcgray</a></td>
   <td>字符串</td>
   <td>&lt;empty&gt;</td>
   <td>用於沒有內嵌色彩設定檔的CMYK影像的預設灰階色彩設定檔名稱。</td>
  </tr>
  <tr>
   <td><a href="https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccblackpointcompensation.html">iccblackpointcompensation</a></td>
   <td>布尔值</td>
   <td>True</td>
   <td>指定在色彩校正期間是否完成黑點補償。 Adobe建議開啟此設定。</td>
  </tr>
  <tr>
   <td><a href="https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccdither.html">iccdither</a></td>
   <td>布尔值</td>
   <td>False</td>
   <td>指定色彩校正期間是否執行遞色。</td>
  </tr>
  <tr>
   <td><a href="https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccrenderintent.html">iccrenderintent</a></td>
   <td>字符串</td>
   <td>相对</td>
   <td><p>指定演算色彩比對方式。 可接受的值包括： <strong>可感知、相對、飽和度、絕對。 </strong><i></i>Adobe建議 <strong>相對 </strong><i></i>作為預設值。</p> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
屬性名稱會區分大小寫，且必須全部小寫。

**色彩設定檔表格**

已安裝下列色彩設定檔：

<table>
 <tbody>
  <tr>
   <th><p>名称</p> </th>
   <th><p>色彩空間</p> </th>
   <th><p>描述</p> </th>
  </tr>
  <tr>
   <td>Adobe RGB</td>
   <td>RGB</td>
   <td>Adobe RGB (1998)</td>
  </tr>
  <tr>
   <td>AppleRGB</td>
   <td>RGB</td>
   <td>AppleRGB</td>
  </tr>
  <tr>
   <td>CIERGB</td>
   <td>RGB</td>
   <td>CIERGB</td>
  </tr>
  <tr>
   <td>CoatedFogra27</td>
   <td>CMYK</td>
   <td>COATED FOGRA27 (ISO 12647-2:2004)</td>
  </tr>
  <tr>
   <td>CoatedFogra39</td>
   <td>CMYK</td>
   <td>COATED FOGRA39 (ISO 12647-2:2004)</td>
  </tr>
  <tr>
   <td>CoatedGraCol</td>
   <td>CMYK</td>
   <td>鍍膜GRACoL 2006 (ISO 12647-2:2004)</td>
  </tr>
  <tr>
   <td>ColorMatchRGB</td>
   <td>RGB</td>
   <td>ColorMatchRGB</td>
  </tr>
  <tr>
   <td>EuropeISOCoated</td>
   <td>CMYK</td>
   <td>歐洲ISO銅版FOGRA27</td>
  </tr>
  <tr>
   <td>EuroscaleCoated</td>
   <td>CMYK</td>
   <td>Euro scale Coated v2</td>
  </tr>
  <tr>
   <td>EuroscaleUncoated</td>
   <td>CMYK</td>
   <td>Euro scale Uncoated v2</td>
  </tr>
  <tr>
   <td>JapanColorCoated</td>
   <td>CMYK</td>
   <td>Japan Color 2001塗裝</td>
  </tr>
  <tr>
   <td>JapanColorNewspaper</td>
   <td>CMYK</td>
   <td>Japan Color 2002報紙</td>
  </tr>
  <tr>
   <td>JapanColorUncoated</td>
   <td>CMYK</td>
   <td>Japan Color 2001 Uncoated</td>
  </tr>
  <tr>
   <td>JapanColorWebCoated</td>
   <td>CMYK</td>
   <td>Japan Color 2003 Web Coated</td>
  </tr>
  <tr>
   <td>JapanWebCoated</td>
   <td>CMYK</td>
   <td>Japan Web Coated （廣告）</td>
  </tr>
  <tr>
   <td>NewsprintSNAP2007</td>
   <td>CMYK</td>
   <td>美國新聞紙(SNAP 2007)</td>
  </tr>
  <tr>
   <td>NTSC</td>
   <td>RGB</td>
   <td>NTSC (1953)</td>
  </tr>
  <tr>
   <td>PAL</td>
   <td>RGB</td>
   <td>PAL/SECAM</td>
  </tr>
  <tr>
   <td>ProPhoto</td>
   <td>RGB</td>
   <td>ProPhotoRGB</td>
  </tr>
  <tr>
   <td>PS4Default</td>
   <td>CMYK</td>
   <td>Photoshop 4預設CMYK</td>
  </tr>
  <tr>
   <td>PS5Default</td>
   <td>CMYK</td>
   <td>Photoshop 5預設CMYK</td>
  </tr>
  <tr>
   <td>SheetfedCoated</td>
   <td>CMYK</td>
   <td>U.S. Sheetfed Coated v2</td>
  </tr>
  <tr>
   <td>SheetfedUncoated</td>
   <td>CMYK</td>
   <td>U.S. Sheetfed Uncoated v2</td>
  </tr>
  <tr>
   <td>SMPTE</td>
   <td>RGB</td>
   <td>SMPTE-C</td>
  </tr>
  <tr>
   <td>sRGB</td>
   <td>RGB</td>
   <td>sRGB IEC61966-2.1</td>
  </tr>
  <tr>
   <td>UncoatedFogra29</td>
   <td>CMYK</td>
   <td>未塗層的FOGRA29 (ISO 12647-2:2004)</td>
  </tr>
  <tr>
   <td>網頁塗層</td>
   <td>CMYK</td>
   <td>U.S. Web Coated (SWOP) v2</td>
  </tr>
  <tr>
   <td>WebCoatedFogra28</td>
   <td>CMYK</td>
   <td>Web Coated FOGRA28 (ISO 12647-2:2004)</td>
  </tr>
  <tr>
   <td>WebCoatedGrade3</td>
   <td>CMYK</td>
   <td>網頁版SWOP 2006 3級紙張</td>
  </tr>
  <tr>
   <td>WebCoatedGrade5</td>
   <td>CMYK</td>
   <td>網頁版SWOP 2006 5級紙張</td>
  </tr>
  <tr>
   <td>WebUncoated</td>
   <td>CMYK</td>
   <td>U.S. Web Uncoated v2</td>
  </tr>
  <tr>
   <td>WideGamutRGB</td>
   <td>RGB</td>
   <td>寬色域RGB</td>
  </tr>
 </tbody>
</table>

1. 選取 **[!UICONTROL 全部儲存]**.

例如，您可以將 **[!UICONTROL iccprofilergb]** 至 `sRGB`、和 **[!UICONTROL iccprofilecmyk]** 至 **[!UICONTROL 網頁塗層]**.

這麼做會執行下列動作：

* 啟用RGB和CMYK影像的色彩校正。
* 沒有色彩設定檔的RGB影像會假設在 *sRGB* 色域。
* 沒有色彩設定檔的CMYK影像會假設為 *網頁塗層* 色域。
* 傳回RGB輸出的動態轉譯，以*sRGB *色域傳回。
* 傳回CMYK輸出的動態轉譯，在 *網頁塗層* 色域。

## 傳遞資產 {#delivering-assets}

完成上述所有工作後，系統會從影像或視訊服務中提供已啟動的Dynamic Media資產。 在Experience Manager中，此功能會顯示在 **[!UICONTROL 複製影像URL]**， **[!UICONTROL 複製檢視器URL]**， **[!UICONTROL 內嵌檢視器程式碼]**，以及WCM中的。

另請參閱 [傳遞Dynamic Media資產](/help/assets/delivering-dynamic-media-assets.md).

<table>
 <tbody>
  <tr>
   <td><strong>當您……</strong></td>
   <td><strong>结果</strong></td>
  </tr>
  <tr>
   <td>複製影像URL</td>
   <td><p>「複製URL」對話方塊會顯示類似以下的URL （URL僅供示範之用）：</p> <p><code>https://IMAGESERVICEPUBLISHNODE/is/image/content/dam/path/to/Image.jpg?$preset$</code></p> <p>位置 <code>IMAGESERVICEPUBLISHNODE</code> 參考影像服務URL。</p> <p>另請參閱 <a href="/help/assets/delivering-dynamic-media-assets.md">傳遞Dynamic Media資產</a>.</p> </td>
  </tr>
  <tr>
   <td>複製檢視器URL</td>
   <td><p>「複製URL」對話方塊會顯示類似以下的URL （URL僅供示範之用）：</p> <p><code>https://PUBLISHNODE/etc/dam/viewers/s7viewers/html5/BasicZoomViewer.html?asset=/content/dam/path/to/Image.jpg&amp;config=/conf/global/settings/dam/dm/presets/viewer/Zoom_dark&amp;serverUrl=https://IMAGESERVICEPUBLISHNODE/is/image/&amp;contentRoot=%2F</code></p> <p>位置 <code>PUBLISHNODE</code> 是指一般Experience Manager發佈節點和 <code>IMAGESERVICEPUBLISHNODE</code> 參考影像服務URL。</p> <p>另請參閱 <a href="/help/assets/delivering-dynamic-media-assets.md">傳遞Dynamic Media資產</a>.</p> </td>
  </tr>
  <tr>
   <td>複製檢視器的內嵌程式碼</td>
   <td><p>複製內嵌程式碼對話方塊會顯示類似下列的程式碼片段（程式碼範例僅供示範之用）：</p> <p><code class="code">&lt;style type="text/css"&gt;
       #s7basiczoom_div.s7basiczoomviewer{
       width:100%;
       height:auto;
       }
       &lt;/style&gt;
       &lt;script
       type="text/javascript" src="https://PUBLISHNODE/etc/dam/viewers/s7viewers/html5/js/BasicZoomViewer.js"&gt;&lt;/script&gt;
       &lt;div id="s7basiczoom_div"&gt;&lt;/div&gt;
       &lt;script type="text/javascript"&gt;
       var s7basiczoomviewer = new s7viewers.BasicZoomViewer({
       "containerId" : "s7basiczoom_div",
       "params" : {
       "serverurl" : "https://IMAGESERVICEPUBLISHNODE/is/image/",
       "contenturl" : "https://PUBLISHNODE/",
       "config" : "/conf/global/settings/dam/dm/presets/viewer/Zoom_dark",
       "asset" : "/content/dam/path/to/Image.jpg" }
       }).init();
       &lt;/script&gt;</code></p> <p>位置 <code>PUBLISHNODE</code> 是指一般Experience Manager發佈節點和 <code>IMAGESERVICEPUBLISHNODE</code> 參考影像服務URL。</p> <p>另請參閱 <a href="/help/assets/delivering-dynamic-media-assets.md">傳遞Dynamic Media資產</a>.</p> </td>
  </tr>
 </tbody>
</table>

### WCM Dynamic Media和互動媒體元件 {#wcm-dynamic-media-and-interactive-media-components}

參考Dynamic Media和互動媒體元件的WCM頁面會參考傳遞服務。
