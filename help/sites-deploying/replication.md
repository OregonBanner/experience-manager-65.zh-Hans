---
title: 复制
seo-title: Replication
description: 瞭解如何在AEM中設定和監控復寫代理。
seo-description: Learn how to configure and monitor replication agents in AEM.
uuid: 6c0bc2fe-523a-401f-8d93-e5795f2e88b9
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: configuring
discoiquuid: 3cae081e-93e3-4317-b307-1316283c307a
docset: aem65
feature: Configuring
exl-id: 09943de5-8d62-4354-a37f-0521a66b4c49
source-git-commit: 840ea373537799af995c3b8ce0c8bf575752775b
workflow-type: tm+mt
source-wordcount: '3425'
ht-degree: 4%

---

# 复制{#replication}

復寫代理程式是Adobe Experience Manager (AEM)的核心，因為此機制可用於：

* [發佈（啟動）](/help/sites-authoring/publishing-pages.md#activatingcontent) 內容從作者環境移至發佈環境。
* 明確地從Dispatcher快取排清內容。
* 從發佈環境將使用者輸入（例如表單輸入）傳回至作者環境（在作者環境的控制下）。

請求為 [已排入佇列](/help/sites-deploying/osgi-configuration-settings.md#apacheslingjobeventhandler) 至適當的代理程式以進行處理。

>[!NOTE]
>
>使用者資料（使用者、使用者群組和使用者設定檔）不會在製作和發佈執行個體之間復寫。
>
>對於多個發佈執行個體，使用者資料在以下情況下為Sling分發： [使用者同步](/help/sites-administering/sync.md) 已啟用。

## 從作者復寫至發佈 {#replicating-from-author-to-publish}

復寫至發佈執行個體或Dispatcher的過程分為幾個步驟：

* 作者要求發佈（啟動）特定內容；這可以由手動請求或預先設定的自動觸發器啟動。
* 此請求會傳遞至適當的預設復寫代理程式；一個環境可以有多個預設代理程式，這些代理程式將一律被選取用於此類動作。
* 復寫代理程式會將內容「封裝」並放置在復寫佇列中。
* 在網站標籤中 [彩色狀態指示器](/help/sites-authoring/publishing-pages.md#determiningpagepublicationstatus) 已為個別頁面設定。
* 內容會從佇列中提取，並使用設定的通訊協定傳輸至發佈環境；這通常是HTTP。
* 發佈環境中的servlet會收到請求並發佈收到的內容；預設servlet為 `https://localhost:4503/bin/receive`.

* 可以設定多個作者和發佈環境。

![chlimage_1-21](assets/chlimage_1-21.png)

### 從發佈復寫至作者 {#replicating-from-publish-to-author}

部分功能可讓使用者在發佈執行個體上輸入資料。

在某些情況下，需要稱為反向復寫的復寫型別，才能將此資料傳回製作環境，然後從該環境重新散發至其他發佈環境。 基於安全性考量，從發佈到作者環境的任何流量都必須受到嚴格控制。

反向復寫會在參考作者環境的發佈環境中使用代理程式。 此代理程式會將資料放入寄件匣。 此寄件匣與製作環境中的復寫接聽程式相符。 監聽器會輪詢寄件匣以收集輸入的任何資料，然後視需要加以分發。 這可確保製作環境可控制所有流量。

在其他情況下，例如對於Communities功能（例如論壇、部落格、評論和評論），在發佈環境中輸入的使用者產生內容(UGC)量難以使用復寫在AEM執行個體之間有效同步。

AEM [Communities](/help/communities/overview.md) 絕不會針對UGC使用復寫。 Communities的部署需要UGC的共同存放區(請參閱 [社群內容儲存](/help/communities/working-with-srp.md))。

### 復寫 — 立即可用 {#replication-out-of-the-box}

AEM標準安裝中包含的We-Retail網站可用於說明復寫。

若要遵循此範例並使用預設的復寫代理，您需要 [安裝AEM](/help/sites-deploying/deploy.md) 替換為：

* 連線埠上的作者環境 `4502`
* 連線埠上的發佈環境 `4503`

>[!NOTE]
>
>默认为已启用 :
>
>* 作者代理程式：預設代理程式（發佈）
>
>預設有效停用(自AEM 6.1起)：
>
>* 作者代理程式：反向復寫代理程式(publish_reverse)
>* 發佈代理程式：反向復寫（寄件匣）
>
>若要檢查代理程式或佇列的狀態，請使用 **工具** 主控台。
>另請參閱 [監視復寫代理](#monitoring-your-replication-agents).

#### 復寫（作者至發佈） {#replication-author-to-publish}

1. 導覽至作者環境上的支援頁面。
   **https://localhost:4502/content/we-retail/us/en/experience.html** `<pi>`
1. 編輯頁面以新增一些文字。
1. **啟動頁面** 以發佈變更。
1. 在發佈環境中開啟支援頁面：
   **https://localhost:4503/content/we-retail/us/en/experience.html**
1. 您現在可以看到您在作者上輸入的變更。

系統會從製作環境執行此復寫：

* **預設代理程式（發佈）**
此代理程式會將內容復寫至預設發佈執行個體。
可以從作者環境的「工具」控制檯存取此專案的詳細資訊（設定和記錄）；或：

   `https://localhost:4502/etc/replication/agents.author/publish.html`。

#### 復寫代理 — 立即可用 {#replication-agents-out-of-the-box}

下列代理程式適用於標準AEM安裝：

* [預設代理程式](#replication-author-to-publish)
用於從作者復寫至發佈。

* Dispatcher排清這是用於管理Dispatcher快取。 另請參閱 [使編寫環境中的Dispatcher快取失效](https://helpx.adobe.com/experience-manager/dispatcher/using/page-invalidate.html#invalidating-dispatcher-cache-from-the-authoring-environment) 和 [使發佈執行個體中的Dispatcher快取失效](https://helpx.adobe.com/experience-manager/dispatcher/using/page-invalidate.html#invalidating-dispatcher-cache-from-a-publishing-instance) 以取得詳細資訊。

* [反向復寫](#reverse-replication-publish-to-author)
用於從發佈複製到作者。 反向復寫不適用於Communities功能，例如論壇、部落格和評論。 由於未啟用寄件匣，因此此功能實際上已停用。 使用反向復寫需要自訂設定。

* 靜態代理程式這是一個「將節點的靜態表示儲存到檔案系統中的代理程式」。
例如，若使用預設設定，內容頁面和DAM資產會儲存在 `/tmp`，以HTML或適當資產格式顯示。 請參閱 `Settings` 和 `Rules` 用於設定的標籤。
已要求此專案，以便當直接從應用程式伺服器要求頁面時，可以看到內容。 這是專門的代理程式，（可能）在大多數執行個體中不是必要的。

## 復寫代理程式 — 設定引數 {#replication-agents-configuration-parameters}

從「工具」控制檯設定復寫代理程式時，對話方塊中有四個索引標籤可用：

### 设置 {#settings}

* **名称**

   復寫代理程式的唯一名稱。

* **描述**

   此復寫代理程式將服務的用途說明。

* **启用**

   指出目前是否啟用復寫代理程式。

   當代理程式為 **已啟用** 佇列將顯示為：

   * **作用中** 處理專案時。
   * **閒置** 當佇列為空時。
   * **已封鎖** 當專案在佇列中，但無法處理時；例如，當接收佇列停用時。

* **序列化类型**

   序列化的型別：

   * **預設**：設定是否要自動選取代理程式。
   * **Dispatcher排清**：如果要使用代理程式來排清Dispatcher快取，請選取此選項。

* **重试延迟**

   如果發生問題，兩次重試之間的延遲（等待時間，以毫秒為單位）。

   默认: `60000`

* **代理用户 ID**

   根據環境，代理程式將使用此使用者帳戶來：

   * 從製作環境收集內容並封裝
   * 在發佈環境中建立並寫入內容

   將此欄位留空將使用系統使用者帳戶(在sling中定義為管理員使用者的帳戶；預設為 `admin`)。

   >[!CAUTION]
   >
   >此帳戶適用於作者環境上的代理程式 *必須* 擁有您要復寫之所有路徑的讀取存取權。

   >[!CAUTION]
   >
   >對於發佈環境上的代理程式，此帳戶 *必須* 具有復寫內容所需的建立/寫入許可權。

   >[!NOTE]
   >
   >這可作為選取特定內容進行復寫的一種機制。

* **日志级别**

   指定用於記錄訊息的詳細資訊等級。

   * `Error`：僅記錄錯誤
   * `Info`：將記錄錯誤、警告和其他資訊訊息
   * `Debug`：訊息將使用高層次的詳細資料，主要用於偵錯

   默认: `Info`

* **使用反转复制**

   指出此代理程式是否將用於反向復寫；傳回從發佈環境到製作環境的使用者輸入。

* **别名更新**

   選取此選項會啟用對Dispatcher的別名或虛名路徑失效請求。 另請參閱 [設定Dispatcher Flush代理程式](/help/sites-deploying/replication.md#configuring-a-dispatcher-flush-agent).

#### 传输 {#transport}

* **URI**

   這會指定目標位置的接收servlet。 尤其是，您可以在此處指定目標執行個體的主機名稱（或別名）和內容路徑。

   例如：

   * 預設代理程式可復寫至 `https://localhost:4503/bin/receive`
   * Dispatcher Flush代理程式可以復寫到 `https://localhost:8000/dispatcher/invalidate.cache`

   此處指定的通訊協定（HTTP或HTTPS）將決定傳輸方法。

   對於Dispatcher Flush代理程式，只有當您使用以路徑為根據的虛擬主機專案來區分陣列時，才會使用URI屬性，而您會使用此欄位來鎖定要失效的陣列。 例如，场 #1 的虚拟主机为 `www.mysite.com/path1/*`，场 #2 的虚拟主机为 `www.mysite.com/path2/*`。您可以使用 URL `/path1/invalidate.cache` 定位第一个场，使用 `/path2/invalidate.cache` 定位第二个场。

* **用户**

   用於存取目標的帳戶使用者名稱。

* **密码**

   用於存取目標的帳戶密碼。

* **NTLM 域**

   NTML驗證的網域。

* **NTLM 主机**

   NTML驗證的主機。

* **启用宽松 SSL**

   若要接受自我認證的SSL憑證，請啟用。

* **允许过期的证书**

   若要接受過期的SSL憑證，請啟用。

#### 代理 {#proxy}

只有在需要Proxy時，才需要下列設定：

* **代理主机**

   用於傳輸的Proxy主機名稱。

* **代理端口**

   Proxy的連線埠。

* **代理用户**

   要使用的帳戶使用者名稱。

* **代理密码**

   要使用的帳戶密碼。

* **代理 NTLM 域**

   Proxy NTLM網域。

* **代理·NTLM 主机**

   Proxy NTLM網域。

#### 扩展 {#extended}

* **接口**

   您可以在此處定義要繫結的通訊端介面。

   這會設定建立連線時要使用的本機位址。 如果未設定，則使用預設地址。 這對於指定要在多主節點或叢集系統上使用的介面非常有用。

* **HTTP 方法**

   要使用的HTTP方法。

   對於Dispatcher Flush代理程式，這幾乎總是GET且不應變更(POST可能是另一個可能的值)。

* **HTTP 头**

   這些用於Dispatcher Flush代理程式，並指定必須清除的元素。

   對於Dispatcher Flush代理程式，不需要變更三個標準專案：

   * `CQ-Action:{action}`
   * `CQ-Handle:{path}`
   * `CQ-Path:{path}`

   系統會視情況使用這些值，指出排清控制代碼或路徑時要使用的動作。 子引數是動態的：

   * `{action}` 表示復寫動作

   * `{path}` 表示路徑

   這些變數會由與請求相關的路徑/動作取代，因此不需要「硬式編碼」：

   >[!NOTE]
   >
   >如果您在建議預設內容以外的內容中安裝AEM，則需要在HTTP標頭中註冊該內容。 例如：
   >`CQ-Handle:/<*yourContext*>{path}`

* **关闭连接**

   啟用以在每次請求後關閉連線。

* **连接超时**

   嘗試建立連線時要套用的逾時（毫秒）。

* **套接字超时**

   建立連線後等待流量時所套用的逾時（毫秒）。

* **协议版本**

   通訊協定版本；例如 `1.0` 適用於HTTP/1.0。

#### 触发器 {#triggers}

這些設定用於定義自動復寫的觸發程式：

* **忽略默认值**

   如果勾選，代理將從預設復寫中排除；這意味著如果內容作者發出復寫動作，將不使用該代理。

* **修改**

   在此，修改頁面時，將自動觸發此代理程式的復寫。 這主要用於Dispatcher Flush代理程式，但也用於反向復寫。

* **在分发时**

   如果勾選，代理程式會在修改內容時自動復寫標示為要散佈的內容。

* **已達到開啟/關閉時間**

   這會在為頁面定義的準時或離線時間發生時，觸發自動復寫（以視需要啟用或停用頁面）。 這主要用於Dispatcher Flush代理程式。

* **接收时**

   如果勾選，代理將在收到復寫事件時進行鏈結復寫。

* **无状态更新**

   核取後，代理將不會強制復寫狀態更新。

* **无版本控制**

   勾選後，代理將不會強制對已啟用的頁面進行版本設定。

## 設定復寫代理 {#configuring-your-replication-agents}

如需有關使用MSSL將復寫代理程式連線至發佈執行個體的資訊，請參閱 [使用雙向SSL復寫](/help/sites-deploying/mssl-replication.md).

### 從製作環境設定復寫代理 {#configuring-your-replication-agents-from-the-author-environment}

在製作環境的Tools標籤中，您可以設定位於製作環境中的復寫代理(**作者上的代理**)或發佈環境(**發佈代理程式**)。 以下程式說明作者環境的代理程式設定，但可用於兩者。

>[!NOTE]
>
>當Dispatcher處理作者或發佈執行個體的HTTP請求時，來自復寫代理程式的HTTP請求必須包含PATH標頭。 除了以下程式外，您還必須將PATH標頭新增到使用者端標頭的Dispatcher清單中。 (請參閱 [/clientheaders （使用者端標頭）](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html#specifying-the-http-headers-to-pass-through-clientheaders).

1. 存取 **工具** AEM索引標籤中的「 」。
1. 按一下 **復寫** （左窗格以開啟資料夾）。
1. 按兩下 **作者上的代理** （左側或右側窗格）。
1. 按一下適當的代理程式名稱（連結）以顯示該代理程式的詳細資訊。
1. 按一下 **編輯** 若要開啟設定對話方塊：

   ![chlimage_1-22](assets/chlimage_1-22.png)

1. 提供的值應足以進行預設安裝。 若您進行變更，請按一下 **確定** 以儲存它們(請參閱 [復寫代理程式 — 設定引數](#replication-agents-configuration-parameters) 以取得個別引數的詳細資訊)。

>[!NOTE]
>
>AEM的標準安裝會指定 `admin` 在預設復寫代理程式中作為傳輸認證的使用者。
>
>這應該變更為具有複製所需路徑之許可權的站台特定複製使用者帳戶。

### 設定反向復寫 {#configuring-reverse-replication}

反向復寫可用於將發佈執行個體上產生的使用者內容傳回作者執行個體。 這通常用於調查和登錄檔單等功能。

基於安全理由，大多數網路拓撲都不允許連線 *從* 「非軍事區」(將外部服務公開至不受信任的網路（例如網際網路）的子網路)。

由於發佈環境通常位於DMZ中，因此若要將內容取回製作環境，必須從製作執行個體啟動連線。 可透過以下方式完成：

* 一個 *寄件匣* 內容所在的發佈環境中。
* 製作環境中的代理程式（發佈），會定期輪詢寄件匣以取得新內容。

>[!NOTE]
>
>適用於AEM [Communities](/help/communities/overview.md)，復寫不適用於發佈執行個體上使用者產生的內容。 另請參閱 [社群內容儲存](/help/communities/working-with-srp.md).

若要這麼做，您需要：

**製作環境中的反向復寫代理程式** 這會作為使用中元件，從發佈環境中的寄件匣收集資訊：

如果您想使用反向復寫，請確定此代理程式已啟用。

![chlimage_1-23](assets/chlimage_1-23.png)

**發佈環境中的反向復寫代理程式（寄件匣）** 這是被動元素，因為它可當作「寄件匣」。 使用者輸入會放置在這裡，由作者環境中的代理程式從中收集。

![chlimage_1-1](assets/chlimage_1-1.jpeg)

### 為多個發佈執行個體設定復寫 {#configuring-replication-for-multiple-publish-instances}

>[!NOTE]
>
>僅複製內容 — 不複製使用者資料（使用者、使用者群組和使用者設定檔）。
>
>若要同步多個發佈執行個體的使用者資料，請啟用 [使用者同步](/help/sites-administering/sync.md).

在安裝時，已設定預設代理程式，以便將內容復寫至在localhost的連線埠4503上執行的發佈執行個體。

若要為其他發佈執行個體設定內容復寫，您需要建立和設定新的復寫代理程式：

1. 開啟 **工具** AEM索引標籤中的「 」。
1. 選取 **復寫**，則 **作者上的代理** 在左側面板中。
1. 選取 **新增……**.
1. 設定 **標題** 和 **名稱**，然後選取 **復寫代理**.
1. 按一下 **建立** 以建立新的代理程式。
1. 連按兩下新代理程式專案以開啟設定面板。
1. 按一下 **編輯** - **代理程式設定** 對話方塊將會開啟 —  **序列化型別** 已定義為「預設」，此狀態必須維持不變。

   * 在 **設定** 標籤：

      * 啟動 **已啟用**.
      * 輸入 **說明**.
      * 設定 **重試延遲** 至 `60000`.

      * 離開 **序列化型別** 作為 `Default`.
   * 在 **傳輸** 標籤：

      * 輸入新發佈執行個體的必要URI；例如，
         `https://localhost:4504/bin/receive`。

      * 輸入用於復寫的特定於站台的使用者帳戶。
      * 您可以視需要設定其他引數。


1. 按一下 **確定** 以儲存設定。

然後，您可以透過更新然後發佈作者環境中的頁面來測試操作。

更新將顯示在已如上配置的所有發佈執行個體上。

如果您遇到任何問題，可以檢查作者執行個體上的記錄。 視所需的詳細程度而定，您也可以設定 **記錄層級** 至 `Debug` 使用 **代理程式設定** 對話方塊。

>[!NOTE]
>
>這可以結合使用 [代理使用者ID](#agentuserid) 以選取不同的內容來復寫至個別發佈環境。 對於每個發佈環境：
>
>1. 設定復寫代理程式以復寫至該發佈環境。
>1. 設定使用者帳戶；具有讀取將復寫至該特定發佈環境之內容所需的存取許可權。
>1. 將使用者帳戶指派為 **代理使用者ID** 用於復寫代理程式。

>


### 設定Dispatcher Flush代理程式 {#configuring-a-dispatcher-flush-agent}

預設代理程式會包含在安裝中。 不過，您仍需要某些設定，如果您定義新的代理程式，也同樣需要此設定：

1. 開啟 **工具** AEM索引標籤中的「 」。
1. 按一下 **部署**.
1. 選取 **復寫** 然後 **發佈代理程式**.
1. 連按兩下 **Dispatcher排清** 專案，以開啟「概述」。
1. 按一下 **編輯** - **代理程式設定** 對話方塊將會開啟：

   * 在 **設定** 標籤：

      * 啟動 **已啟用**.
      * 輸入 **說明**.
      * 離開 **序列化型別** 作為 `Dispatcher Flush`，或若建立新代理程式，則將其設定為依此類推。

      * （選用）選取 **別名更新** 啟用對Dispatcher的別名或虛名路徑失效請求。
   * 在 **傳輸** 標籤：

      * 輸入新發佈執行個體的必要URI；例如，
         `https://localhost:80/dispatcher/invalidate.cache`。

      * 輸入用於復寫的特定於站台的使用者帳戶。
      * 您可以視需要設定其他引數。

   對於Dispatcher Flush代理程式，只有當您使用以路徑為根據的虛擬主機專案來區分陣列時，才會使用URI屬性，而您會使用此欄位來鎖定要失效的陣列。 例如，场 #1 的虚拟主机为 `www.mysite.com/path1/*`，场 #2 的虚拟主机为 `www.mysite.com/path2/*`。您可以使用 URL `/path1/invalidate.cache` 定位第一个场，使用 `/path2/invalidate.cache` 定位第二个场。

   >[!NOTE]
   >
   >如果您已在非建議預設內容中安裝AEM，則您需要設定 [HTTP標頭](#extended) 在 **延伸** 標籤。

1. 按一下 **確定** 以儲存變更。
1. 返回 **工具** 標籤，從這裡您可以 **啟動** 此 **Dispatcher排清** 代理(**發佈代理程式**)。

此 **Dispatcher排清** 復寫代理程式在作者上未啟用。 您可以使用對等的URI （例如），在發佈環境中存取相同的頁面。 `https://localhost:4503/etc/replication/agents.publish/flush.html`.

### 控制對復寫代理程式的存取 {#controlling-access-to-replication-agents}

對用來設定復寫代理的頁面的存取權，可以透過上的使用者和/或群組頁面許可權來控制 `etc/replication` 節點。

>[!NOTE]
>
>設定這類許可權不會影響使用者復寫內容（例如從網站主控台或Sidekick選項）。 復寫架構在復寫頁面時，不會使用目前使用者的「使用者工作階段」來存取復寫代理。

### 從CRXDE Lite設定復寫代理 {#configuring-your-replication-agents-from-crxde-lite}

>[!NOTE]
>
>僅支援建立復寫代理程式 `/etc/replication` 存放庫位置。 為了正確處理關聯的ACL，需要此屬性。 在樹狀結構的其他位置建立復寫代理程式可能會導致未經授權的存取。

您可以使用CRXDE Lite設定復寫代理的各種引數。

如果您導覽至 `/etc/replication` 您可以看到下列三個節點：

* `agents.author`
* `agents.publish`
* `treeactivation`

兩個 `agents` 保留適當環境的設定資訊，且僅在該環境執行時有效。 例如， `agents.publish` 將僅用於發佈環境。 以下熒幕擷圖顯示製作環境中的發佈代理程式(隨AEM WCM提供)：

![chlimage_1-24](assets/chlimage_1-24.png)

## 監視復寫代理 {#monitoring-your-replication-agents}

監督復寫代理程式：

1. 存取 **工具** AEM索引標籤中的「 」。
1. 按一下 **復寫**.
1. 連按兩下適當環境的代理程式連結（左窗格或右窗格）；例如 **作者上的代理**.

   產生的視窗會顯示製作環境之所有復寫代理程式的概觀，包括其目標和狀態。

1. 按一下適當的代理程式名稱（連結）以顯示該代理程式的詳細資訊：

   ![chlimage_1-2](assets/chlimage_1-2.jpeg)

   在此编辑器中，您可以：

   * 檢視代理程式是否已啟用。
   * 檢視任何復寫的目標。
   * 檢視復寫佇列目前是否啟用。
   * 檢視佇列中是否有任何專案。
   * **重新整理** 或 **清除** 更新佇列專案的顯示；這有助於您檢視進入和離開佇列的專案。

   * **檢視記錄** 存取復寫代理程式的任何動作記錄。
   * **測試連線** 至目標執行個體。
   * **強制重試** 在任何佇列專案上（如有需要）。

   >[!CAUTION]
   >
   >請勿對發佈執行個體上的「反向復寫寄件匣」使用「測試連線」連結。
   >
   >
   >如果對Outbox佇列執行復寫測試，則任何早於測試復寫的專案都會透過每次反向復寫重新處理。
   >
   >
   >如果佇列中已有此類專案，可在下列XPath JCR查詢中找到並移除這些專案。
   >
   >
   >`/jcr:root/var/replication/outbox//*[@cq:repActionType='TEST']`

## 批次復寫 {#batch-replication}

批次復寫不會復寫個別頁面或資產，但會根據時間或大小等待觸發兩者的第一個臨界值。

然後它會將所有復寫專案封裝到一個封裝中，然後以單一檔案的形式復寫到發行者。

發佈者會解壓縮所有專案、儲存專案，並向作者回報。

### 設定批次復寫 {#configuring-batch-replication}

1. 转到 `http://serveraddress:serverport/siteadmin`
1. 按下 **[!UICONTROL 工具]** 圖示上方顯示
1. 從左側導覽邊欄，前往 **[!UICONTROL 復寫 — 作者上的代理]** 並按兩下 **[!UICONTROL 預設代理程式]**.
   * 您也可以直接前往「 」，存取預設發佈復寫代理程式。 `http://serveraddress:serverport/etc/replication/agents.author/publish.html`
1. 按下 **[!UICONTROL 編輯]** 按鈕進行複製。
1. 在下列視窗中，前往 **[!UICONTROL 批次]** 標籤：
   ![批次復寫](assets/batchreplication.png)
1. 設定代理。

### 参数 {#parameters}

* `[!UICONTROL Enable Batch Mode]`  — 啟用或停用批次複製模式
* `[!UICONTROL Max Wait Time]`  — 批次要求啟動前的等待時間上限（以秒為單位）。 預設值為2秒。
* `[!UICONTROL Trigger Size]`  — 在此大小限制時開始批次復寫

## 其他资源 {#additional-resources}

如需疑難排解的詳細資訊，請參閱 [疑難排解復寫](/help/sites-deploying/troubleshoot-rep.md) 頁面。
