---
title: 疑難排解Dynamic Media - Scene7模式
description: 疑難排解Dynamic Media在Scene7模式下執行時的問題。
uuid: 77e04ccf-33dc-4d2f-8950-318d4b008f74
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: 0d48c031-d3ee-4143-b739-a79ba28fd63a
docset: aem65
role: User, Admin
exl-id: d4507059-a54d-4dc9-a263-e55dfa27eeb1
feature: Troubleshooting
mini-toc-levels: 3
source-git-commit: 9c3df2491f99fe31e4b64b47442dd583af06974e
workflow-type: tm+mt
source-wordcount: '1386'
ht-degree: 1%

---

# 疑難排解Dynamic Media - Scene7模式{#troubleshooting-dynamic-media-scene-mode}

以下檔案說明執行Dynamic Media的疑難排解 **dynamicmedia_scene7** 執行模式。

## 設定和組態 {#setup-and-configuration}

執行下列作業，確保Dynamic Media已正確設定：

* 啟動命令包含 `-r dynamicmedia_scene7` 執行模式引數。
* 已先安裝任何Adobe Experience Manager 6.4 Cumulative Fix Pack (CFP) *早於* 任何可用的Dynamic Media Feature Pack。
* 已安裝選用的Feature Pack 18912。

   此選用的Feature Pack僅適用於FTP支援，或適用於從Dynamic Media Classic將資產移轉至Dynamic Media的情況。

* 導覽至Cloud Services使用者介面，並確認布建的帳戶會顯示在 **[!UICONTROL 可用的設定]**.
* 確保 `Dynamic Media Asset Activation (scene7)` 復寫代理程式已啟用。

   此復寫代理程式位於「作者上的代理程式」下。

## 一般（所有資產） {#general-all-assets}

以下是適用於所有資產的一些一般提示和技巧。

### 資產同步狀態屬性 {#asset-synchronization-status-properties}

您可以在CRXDE Lite中檢閱以下資產屬性，以確認資產成功從Experience Manager同步到Dynamic Media：

| **属性** | **示例** | **描述** |
|---|---|---|
| `<object_node>/jcr:content/metadata/dam:scene7ID` | **`a\|364266`** | 節點連結至Dynamic Media的一般指標。 |
| `<object_node>/jcr:content/metadata/dam:scene7FileStatus` | **PublishComplete** 或錯誤文字 | 將資產上傳至Dynamic Media的狀態。 |
| `<object_node>/jcr:content/metadata/dam:scene7File` | **myCompany/myAssetID** | 必須填入，才能產生Dynamic Media遠端資產的URL。 |
| `<object_node>/jcr:content/dam:lastSyncStatus` | **成功** 或 **失敗：`<error text>`** | 集合（迴轉集、影像集等）、影像預設集、檢視器預設集、資產的影像地圖更新或已編輯影像的同步狀態。 |

### 同步記錄 {#synchronization-logging}

同步處理錯誤和問題已登入 `error.log` (Experience Manager伺服器目錄 `/crx-quickstart/logs/`)。 有充足的記錄可判斷大部分問題的根本原因，不過您可以增加對 `com.adobe.cq.dam.ips` 透過Sling主控台封裝([https://localhost:4502/system/console/slinglog](https://localhost:4502/system/console/slinglog))以收集更多資訊。

### 移動、複製、刪除 {#move-copy-delete}

執行「移動」、「複製」或「刪除」作業之前，請先執行下列動作：

* 針對影像和視訊，確認 `<object_node>/jcr:content/metadata/dam:scene7ID` 值存在於執行移動、複製或刪除作業之前。
* 對於影像和檢視器預設集，請確認 `https://<server>/crx/de/index.jsp#/etc/dam/presets/viewer/testpreset/jcr%3Acontent/metadata` 值存在於執行移動、複製或刪除作業之前。
* 如果缺少上述中繼資料值，您必須先重新上傳資產，才能進行移動、複製或刪除作業。

### 版本控制 {#version-control}

取代現有Dynamic Media資產（名稱和位置相同）時，您可以保留兩個資產或取代/建立版本：

* 同時保留兩者會為已發佈的資產URL建立具有唯一名稱的資產。 例如， `image.jpg` 是原始資產，且 `image1.jpg` 是新上傳的資產。

* Dynamic Media - Scene7模式傳送不支援建立版本。 新版本會取代傳遞中的現有資產。

## 影像和集合 {#images-and-sets}

如果您遇到影像和集的問題，請參閱下列疑難排解指南。

<table>
 <tbody>
  <tr>
   <td><strong>问题</strong></td>
   <td><strong>如何偵錯</strong></td>
   <td><strong>解决方案</strong></td>
  </tr>
  <tr>
   <td>無法存取資產詳細資料檢視中的複製URL/內嵌按鈕</td>
   <td>
    <ol>
     <li><p>前往CRX/DE：</p>
      <ul>
       <li>檢查JCR中的預設集 <code>/etc/dam/presets/viewer/&lt;preset&gt; has lastReplicationAction</code> 已定義。 如果您從Experience Manager6.x升級至6.4並選擇退出移轉，則此位置適用。 否則，位置為 <code>/conf/global/settings/dam/dm/presets/viewer</code>.</li>
       <li>確認JCR中的資產具有 <code>dam:scene7FileStatus</code><strong> </strong>在「中繼資料」下顯示為 <code>PublishComplete</code>.</li>
      </ul> </li>
    </ol> </td>
   <td><p>重新整理頁面/導覽至其他頁面並返回（側邊欄JSP必須重新編譯）</p> <p>如果這樣行不通：</p>
    <ul>
     <li>發佈資產。</li>
     <li>重新上傳資產並發佈。</li>
    </ul> </td>
  </tr>
  <tr>
   <td>集編輯器中的資產選擇器卡在持續載入中</td>
   <td><p>須在6.4中修正的已知問題</p> </td>
   <td><p>關閉選取器並重新開啟。</p> </td>
  </tr>
  <tr>
   <td><strong>選取</strong> 在編輯資產集時選取資產後，按鈕未啟用</td>
   <td><p> </p> <p>須在6.4中修正的已知問題</p> <p> </p> </td>
   <td><p>先在「資產選擇器」中的另一個資料夾上選取，然後返回以選取資產。</p> </td>
  </tr>
  <tr>
   <td>在幻燈片之間切換後，輪播熱點會四處移動</td>
   <td><p>檢查所有幻燈片的大小是否相同。</p> </td>
   <td><p>僅對輪播使用大小相同的影像。</p> </td>
  </tr>
  <tr>
   <td>影像未使用Dynamic Media檢視器預覽</td>
   <td><p>檢查資產是否包含 <code>dam:scene7File</code> 在中繼資料屬性(CRXDE Lite)中</p> </td>
   <td><p>檢查所有資產是否已完成處理。</p> </td>
  </tr>
  <tr>
   <td>上傳的資產未顯示在資產選擇器中</td>
   <td><p>檢查資產是否具有屬性 <code>jcr:content</code> &gt; <strong><code>dam:assetState</code></strong> = <code>processed</code> (CRXDE Lite)</p> </td>
   <td><p>檢查所有資產是否已完成處理。</p> </td>
  </tr>
  <tr>
   <td>卡片檢視上的橫幅顯示 <strong>新增</strong> 當資產尚未開始處理時</td>
   <td>檢查資產 <code>jcr:content</code> &gt; <code>dam:assetState</code> = if <code>unprocessed</code> 工作流程未擷取它。</td>
   <td>等到工作流程擷取資產為止。</td>
  </tr>
  <tr>
   <td>影像或集未顯示檢視器URL或內嵌程式碼</td>
   <td>檢查檢視器預設集是否已發佈。</td>
   <td><p>前往 <strong>工具</strong> &gt; <strong>資產</strong> &gt; <strong>檢視器預設集</strong> 並發佈檢視器預設集。</p> </td>
  </tr>
 </tbody>
</table>

## 视频 {#video}

如果您遇到視訊問題，請參閱下列疑難排解指南。

<table>
 <tbody>
  <tr>
   <td><strong>问题</strong></td>
   <td><strong>如何偵錯</strong></td>
   <td><strong>解决方案</strong></td>
  </tr>
  <tr>
   <td>無法預覽視訊</td>
   <td>
    <ul>
     <li>檢查資料夾是否已指派視訊設定檔（如果不支援的檔案格式）。 如果不支援，則只會顯示影像。</li>
     <li>視訊設定檔必須包含多個編碼預設集，才能產生AVS集（單一編碼會視為MP4檔案的視訊內容；對於不支援的檔案，則會視為未處理）。</li>
     <li>確認以檢查視訊是否已完成處理 <code>dam:scene7FileAvs</code> 之 <code>dam:scene7File</code> 在中繼資料中。</li>
    </ul> </td>
   <td>
    <ol>
     <li>將視訊設定檔指派至資料夾。</li>
     <li>編輯視訊設定檔以包含一個以上的編碼預設集。</li>
     <li>等候視訊完成處理。</li>
     <li>重新載入視訊時，請確定Dynamic Media編碼視訊工作流程未執行。<br /> </li>
     <li>重新上傳視訊。</li>
    </ol> </td>
  </tr>
  <tr>
   <td>視訊未編碼</td>
   <td>
    <ul>
     <li>檢查執行模式是否為 <code>dynamicmedia_scene7</code>.</li>
     <li>檢查是否已設定Dynamic Media雲端服務。</li>
     <li>檢查視訊設定檔是否與上傳資料夾相關聯。</li>
    </ul> </td>
   <td>
    <ol>
     <li>檢查您的Experience Manager執行個體，透過 <code>-r dynamicmedia_scene7</code></li>
     <li>檢查Cloud Services底下的Dynamic Media設定是否已正確設定。</li>
     <li>檢查資料夾是否有視訊設定檔。 此外，檢查視訊設定檔。</li>
    </ol> </td>
  </tr>
  <tr>
   <td>視訊處理需要太長的時間</td>
   <td><p>若要判斷視訊編碼是否仍在進行中，或已進入失敗狀態：</p>
    <ul>
     <li>檢查視訊狀態 <code>https://localhost:4502/crx/de/index.jsp#/content/dam/folder/videomp4/jcr%3Acontent</code> &gt; <code>dam:assetState</code></li>
     <li>從工作流程主控台監視視訊 <code>https://localhost:4502/libs/cq/workflow/content/console.html</code> &gt;執行個體、封存、失敗標籤。</li>
    </ul> </td>
   <td> </td>
  </tr>
  <tr>
   <td>視訊轉譯遺失</td>
   <td><p>已上傳視訊，但沒有已編碼的轉譯時：</p>
    <ul>
     <li>檢查資料夾是否已指派視訊設定檔。</li>
     <li>確認以檢查視訊是否已完成處理 <code>dam:scene7FileAvs</code> 在中繼資料中。</li>
    </ul> </td>
   <td>
    <ol>
     <li>將視訊設定檔指派至資料夾。</li>
     <li>等候視訊完成處理。<br /> </li>
    </ol> </td>
  </tr>
 </tbody>
</table>

## 查看器 {#viewers}

如果您遇到檢視器的問題，請參閱下列疑難排解指南。

### 問題：檢視器預設集未發佈 {#viewers-not-published}

**如何偵錯**

1. 繼續範例管理員診斷頁面： `https://localhost:4502/libs/dam/gui/content/s7dam/samplemanager/samplemanager.html`.
1. 觀察計算值。 正確操作時，您會看到下列內容： `_DMSAMPLE status: 0 unsyced assets - activation not necessary _OOTB status: 0 unsyced assets - 0 unactivated assets`.

   >[!NOTE]
   >
   >設定Dynamic Media雲端設定後，大約需要10分鐘的時間才能讓檢視器資產同步。

1. 如果仍保留未啟用的資產，請選取 **列出所有未啟用的資產** 按鈕以檢視詳細資訊。

**解决方案**

1. 導覽至管理工具中的檢視器預設集清單： `https://localhost:4502/libs/dam/gui/content/s7dam/samplemanager/samplemanager.html`
1. 選取所有檢視器預設集，然後選取 **發佈**.
1. 導覽回範例管理員，並觀察未啟用的資產計數現在為零。

### 問題：檢視器預設集圖稿從資產詳細資料中的預覽或複製URL/內嵌程式碼返回404 {#viewer-preset-404}

**如何偵錯**

在CRXDE Lite中，執行下列動作：

1. 導覽至 `<sync-folder>/_CSS/_OOTB` Dynamic Media同步資料夾中的資料夾(例如， `/content/dam/_CSS/_OOTB`)。
1. 尋找有問題資產的中繼資料節點(例如， `<sync-folder>/_CSS/_OOTB/CarouselDotsLeftButton_dark_sprite.png/jcr:content/metadata/`)。
1. 檢查是否存在 `dam:scene7*` 屬性。 如果資產已成功同步和發佈，您會看到 `dam:scene7FileStatus` 設定為 **PublishComplete**.
1. 串連下列屬性和字串常值的值，嘗試直接從Dynamic Media要求圖稿：

   * `dam:scene7Domain`
   * `"is/content"`
   * `dam:scene7Folder`
   * `<asset-name>`
示例: 
`https://<server>/is/content/myfolder/_CSS/_OOTB/CarouselDotsLeftButton_dark_sprite.png`

**解决方案**

如果範例資產或檢視器預設集圖稿尚未同步或發佈，請重新啟動整個複製/同步程式：

1. 導覽至「CRXDE Lite」。
1. 删除 `<sync-folder>/_CSS/_OOTB`.
1. 導覽至CRX封裝管理員： `https://localhost:4502/crx/packmgr/`.
1. 在清單中搜尋檢視器套件；其開頭為 `cq-dam-scene7-viewers-content`.
1. 選取 **重新安裝**.
1. 在Cloud Services底下，導覽至Dynamic Media設定頁面，然後開啟Dynamic Media - S7設定的設定對話方塊。
1. 不做變更，選取 **儲存**.
此儲存動作會再次觸發邏輯，以建立並同步範例資產、檢視器預設集CSS和圖稿。

### 問題：檢視器預設集製作中未載入影像預覽 {#image-preview-not-loading}

**解决方案**

1. 在Experience Manager中，選取Experience Manager標誌以存取全域導覽主控台，然後導覽至 **[!UICONTROL 工具]** > **[!UICONTROL 一般]** > **[!UICONTROL CRXDE Lite]**.
1. 在左側邊欄中，導覽至下列位置的範例內容資料夾：

   `/content/dam/_DMSAMPLE`

1. 刪除 `_DMSAMPLE` 資料夾。
1. 在左側邊欄中，導覽至下列位置的預設集資料夾：

   `/conf/global/settings/dam/dm/presets/viewer`

1. 刪除 `viewer` 資料夾。
1. 在CRXDE Lite頁面的左上角附近，選取 **[!UICONTROL 全部儲存]**.
1. 在CRXDE Lite頁面的左上角，選取 **返回首頁** 圖示。
1. 重新建立 [Cloud Services中的Dynamic Media設定](/help/assets/config-dms7.md#configuring-dynamic-media-cloud-services).
