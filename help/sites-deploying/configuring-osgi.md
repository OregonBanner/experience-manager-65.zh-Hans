---
title: 設定OSGi
seo-title: Configuring OSGi
description: OSGi是Adobe Experience Manager (AEM)技術棧疊中的基本元素。 它可用來控制AEM的複合套件組合及其設定。 本文詳細說明如何管理這類套裝的組態設定。
seo-description: OSGi is a fundamental element in the technology stack of Adobe Experience Manager (AEM). It is used to control the composite bundles of AEM and their configuration. This article details how you can manage the configuration settings for such bundles.
uuid: b39059a5-dd61-486a-869a-0d7a732c3a47
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
discoiquuid: d701e4ba-417f-4b57-b103-27fd25290736
feature: Configuring
exl-id: 5ecd09a3-c4be-4361-9816-03106435346f
source-git-commit: 2981f11565db957fac323f81014af83cab2c0a12
workflow-type: tm+mt
source-wordcount: '1949'
ht-degree: 0%

---

# 設定OSGi{#configuring-osgi}

[osgi](https://www.osgi.org/) 是Adobe Experience Manager (AEM)技術棧疊中的基本元素。 它可用來控制AEM的複合套件組合及其設定。

OSGi 」*提供標準化的基本概念，讓應用程式可由小型、可重複使用的合作元件所建構。 這些元件可組成應用程式並部署*「。

如此一來，就能輕鬆地管理套件組合，因為套件組合可以個別停止、安裝和啟動。 系統會自動處理相依性。 每個OSGi元件(請參閱 [OSGi規格](https://docs.osgi.org/specification/))包含在多個套件組合之一中。

您可以透過以下任一方式管理此類套裝的組態設定：

* 使用 [Adobe CQ Web主控台](#osgi-configuration-with-the-web-console)
* 使用 [組態檔](#osgi-configuration-with-configuration-files)
* 設定 [content-nodes ( `sling:OsgiConfig`)時，不會受到任何限制](#osgi-configuration-in-the-repository)

雖然有細微差異，但可以使用任一方法，主要與 [執行模式](/help/sites-deploying/configure-runmodes.md)：

* [Adobe CQ Web主控台](#osgi-configuration-with-the-web-console)

   * Web主控台是OSGi設定的標準介面。 它提供用於編輯各種屬性的UI，其中可以從預先定義的清單中選擇可能的值。

      因此，這是最簡單的方法。

   * 使用Web主控台進行的所有設定都會立即套用並適用於目前的執行個體，無論目前的執行模式或執行模式的任何後續變更為何。

* [組態檔](#osgi-configuration-with-configuration-files)

   * 包含在Web主控台中定義的設定。
   * 可包含在內容套件中，以供在其他執行個體上使用。

* [存放庫中的content-nodes (sling：osgiConfig)](#osgi-configuration-in-the-repository)

   * 需要使用CRXDE Lite手動設定。
   * 由於的命名慣例 `sling:OsgiConfig` 節點，您可以將設定連結至特定 [執行模式](/help/sites-deploying/configure-runmodes.md). 您甚至可以在同一個存放庫中儲存多個執行模式的設定。
   * 任何適當的設定都會立即套用（取決於執行模式）。

無論您使用哪種方法，這些設定方法皆有：

* 請確定複製或復寫存放庫內容會重新建立相同的設定。
* 可讓您將組態出庫至FileVault或Subversion；以取得安全性或進一步的更新。
* 可儲存在套件中，以便在設定其他執行個體時使用。
* 可讓您使用指令碼執行設定轉出，以傳播設定詳細資訊。

>[!NOTE]
>
>某些重要設定的詳細資訊列於 [OSGi組態設定。](/help/sites-deploying/osgi-configuration-settings.md)

## 使用Web主控台進行OSGi設定 {#osgi-configuration-with-the-web-console}

此 [網頁主控台](/help/sites-deploying/web-console.md) AEM中提供標準化介面來設定組合。 此 **設定** tab可用來設定OSGi組合，因此是設定AEM系統引數的基礎。

所做的任何變更都會立即套用至相關的OSGi設定，不需要重新啟動。

>[!NOTE]
>
>在Web主控台中所做的變更會儲存在存放庫中，做為 [組態檔](#osgi-configuration-with-configuration-files). 這些檔案可包含在內容套件中，以供後續安裝重複使用。

>[!NOTE]
>
>在Web主控台上，提及預設設定的任何說明都與Sling預設值有關。
>
>Adobe Experience Manager有自己的預設值，因此設定的預設值可能與主控台上記錄的預設值不同。

若要使用Web主控台更新設定：

1. 存取 **設定** Web Console的索引標籤，方法是：

   * 從上的連結開啟Web主控台 **工具 — >作業** 功能表。 登入主控台後，您可以使用下拉式功能表：

      **OSGi >**

   * 直接URL；例如：

      `http://localhost:4502/system/console/configMgr`
   隨即顯示清單。

1. 透過下列任一方式選取您要設定的組合：

   * 按一下 **編輯** 該套件組合圖示
   * 按一下 **名稱** 束的

1. 對話方塊開啟。 您可以在這裡視需要編輯。 例如，設定 **記錄層級** 至 `INFO`：

   ![chlimage_1-140](assets/chlimage_1-140.png)

   >[!NOTE]
   >
   >更新會儲存在存放庫中，做為 [組態檔](#osgi-configuration-with-configuration-files). 例如，若要在之後找到這些檔案，以便包含在內容套件中以供其他執行個體使用，請記下永久性身分( `PID`)。

1. 单击“**保存**”。

   您的變更會立即套用至執行中系統的相關OSGi設定，不需要重新啟動。

   >[!NOTE]
   >
   >您現在可以找到相關的 [組態檔](#osgi-configuration-with-configuration-files). 例如，包含在內容套件中以供其他執行個體使用。

## 具有組態檔的OSGi組態 {#osgi-configuration-with-configuration-files}

使用Web主控台進行的組態變更會以組態檔的形式保留在存放庫中( `.config`)下：

`/apps`

這些檔案可包含在內容套件中，並可在其他執行個體上重複使用。

>[!NOTE]
>
>組態檔的格式是特定的 — 請參閱 [Sling Apache檔案](https://sling.apache.org/documentation/development/slingstart.html#default-configuration-format) 以取得完整詳細資訊。
>
>因此，建議您在Web主控台中進行實際變更，以建立和維護設定檔案。

Web主控台不會顯示存放庫中儲存變更的位置，但可以輕鬆找到它們：

1. 建立設定檔案的方式： [在Web主控台中進行初始變更](#osgi-configuration-with-the-web-console).
1. 開啟CRXDE Lite。
1. 在 **工具** 功能表，選取 **查詢……** .
1. 若要搜尋已更新之設定的PID，請提交 **型別** `SQL`.

   例如， **Apache Felix OSGi管理主控台** 具有下列專案的永久性身分(PID)：

   `org.apache.felix.webconsole.internal.servlet.OsgiManager`

   因此，SQL查詢可以是：

   ```shell
   select * from nt:base where jcr:path like '/apps/%' and contains(*, 'org.apache.felix.webconsole.internal.servlet.OsgiManager')
   ```

1. 隨即顯示組態檔節點。

   對於上述範例：

   `/apps/system/config/org.apache.felix.webconsole.internal.servlet.OsgiManager.config`

   >[!CAUTION]
   >
   >您可以開啟此檔案來檢視您的變更，但為避免輸入錯誤，建議使用主控台進行實際變更。

1. 您現在可以建立包含此節點的內容套件，並視需要在其他執行個體上使用。

## 存放庫中的OSGi設定 {#osgi-configuration-in-the-repository}

除了使用Web主控台，您也可以在存放庫中定義設定詳細資訊。 如此可讓您輕鬆設定不同的執行模式。

這些設定是透過建立 `sling:OsgiConfig` 供系統參考的存放庫中的節點。 這些節點會反映OSGi設定，並在其中形成使用者介面。 若要更新設定資料，請更新節點屬性。

如果您修改存放庫中的設定資料，變更會立即套用至相關的OSGi設定。 就好像變更是使用Web主控台進行的，並附上適當的驗證和一致性檢查。 此工作流程也適用於複製設定的動作 `/libs/` 至 `/apps/`.

由於相同的組態引數位於數個位置，因此系統：

* 搜尋型別為的所有節點 `sling:OsgiConfig`
* 根據服務名稱篩選
* 根據執行模式篩選

>[!NOTE]
>
>另請閱讀 [如何只為特定執行個體定義存放庫型設定](https://experienceleague.adobe.com/docs/experience-cloud-kcs/kbarticles/KA-17500.html?lang=zh-Hans).

### 新增設定至存放庫 {#adding-a-new-configuration-to-the-repository}

#### 您需要瞭解的事項 {#what-you-need-to-know}

若要將設定新增至存放庫，您必須知道下列內容：

1. 此 **持續性身分** (PID)的服務。

   參考 **設定** 欄位。 該名稱會顯示在束名稱后的方括弧中(或在 **設定資訊** （朝向頁面底部）。

   例如，建立節點 `com.day.cq.wcm.core.impl.VersionManagerImpl.` 進行設定 **AEM WCM版本管理員**.

   ![chlimage_1-141](assets/chlimage_1-141.png)

1. 為特定 [執行模式](/help/sites-deploying/configure-runmodes.md) 必填？ 建立資料夾：

   * `config`  — 適用於所有執行模式
   * `config.author`  — 適用於作者環境
   * `config.publish`  — 適用於發佈環境
   * `config.<run-mode>` - 酌情

1. 是 **設定** 或 **工廠設定** 需要？
1. 要設定的個別引數，包括必須重新建立的任何現有引數定義。

   參考Web主控台中的個別引數欄位。 每個引數的名稱都會以方括弧顯示。

   例如，建立屬性
   `versionmanager.createVersionOnActivation` 進行設定 **啟動時建立版本**.

   ![chlimage_1-142](assets/chlimage_1-142.png)

1. 設定是否存在於 `/libs`？ 若要列出執行個體中的所有設定，請使用 **查詢** CRXDE Lite工具，可提交下列SQL查詢：

   `select * from sling:OsgiConfig`

   如果是這樣，此設定可複製到 ` /apps/<yourProject>/`，然後在新位置自訂。

#### 在存放庫中建立設定 {#creating-the-configuration-in-the-repository}

若要將新設定實際新增至存放庫：

1. 使用CRXDE Lite來導覽至：

   ` /apps/<yourProject>`

1. 如果不存在，請建立 `config` 資料夾( `sling:Folder`)：

   * `config`  — 適用於所有執行模式
   * `config.<run-mode>`  — 特定執行模式專用

1. 在此資料夾下，建立節點：

   * 类型: `sling:OsgiConfig`
   * 名稱：永久性身分(PID)；

      例如，AEM WCM版本管理員使用 `com.day.cq.wcm.core.impl.VersionManagerImpl`
   >[!NOTE]
   >
   >附加工廠組態時 `-<identifier>` 至名稱。
   >
   >如所示： `org.apache.sling.commons.log.LogManager.factory.config-<identifier>`
   >
   >位置 `<identifier>` 會取代為您（必須）輸入以識別例證的自由文字（您無法省略此資訊）；例如：
   >
   >`org.apache.sling.commons.log.LogManager.factory.config-MINE`

1. 針對您要設定的每個引數，在此節點上建立屬性：

   * 名稱：引數名稱，如Web主控台中所示；名稱會顯示在欄位說明結尾的方括弧中。 例如， `Create Version on Activation` use `versionmanager.createVersionOnActivation`
   * 型別：視情況而定。
   * 值：視需要。

   您只能為您要設定的引數建立屬性，其他引數仍會採用AEM設定的預設值。

1. 儲存所有變更。

   透過重新啟動服務來更新節點時，會套用變更（如同在Web主控台中所做的變更）。

>[!CAUTION]
>
>請勿變更 `/libs` 路徑。

>[!CAUTION]
>
>設定的完整路徑必須正確，才能在啟動時讀取。

## 設定詳細資料 {#configuration-details}

### 啟動時的解決順序 {#resolution-order-at-startup}

使用下列優先順序：

1. 下的存放庫節點 `/apps/*/config...`.with type `sling:OsgiConfig` 或屬性檔案。

1. 具有型別的存放庫節點 `sling:OsgiConfig` 在 `/libs/*/config...`. （現成定義）。

1. 任何 `.config` 檔案來源 `<*cq-installation-dir*>/crx-quickstart/launchpad/config/...`. 在本機檔案系統上。

中的一般設定 `/libs` 可被中的專案特定設定遮罩 `/apps`.

### 執行階段的解決順序 {#resolution-order-at-runtime}

系統執行時所做的設定變更會觸發使用修改後的設定重新載入。

然後套用下列優先順序：

1. 在Web主控台中修改設定會立即生效，因為它在執行階段具有優先權。
1. 修改中的設定 `/apps` 立即生效。
1. 修改中的設定 `/libs` 立即生效，除非被中的設定遮罩 `/apps`.

### 多個執行模式的解析度 {#resolution-of-multiple-run-modes}

對於執行模式特定的配置，可以組合多個執行模式。 例如，您可以建立以下樣式的組態資料夾：

`/apps/*/config.<runmode1>.<runmode2>/`

如果所有執行模式都符合啟動時定義的執行模式，則會套用此類資料夾中的設定。

例如，如果執行個體是以執行模式啟動 `author,dev,emea`，設定中的節點 `/apps/*/config.emea`， `/apps/*/config.author.dev/`、和 `/apps/*/config.author.emea.dev/` 套用，而設定節點位於 `/apps/*/config.author.asean/` 和 `/config/author.dev.emea.noldap/` 不會套用。

如果適用於同一PID的多個設定，則會套用符合執行模式數量最多的設定。

例如，如果執行個體是以執行模式啟動 `author,dev,emea`，和二者 `/apps/*/config.author/` 和 `/apps/*/config.emea.author/` 定義設定
`com.day.cq.wcm.core.impl.VersionManagerImpl`，中的設定 `/apps/*/config.emea.author/` 「 」已套用。

此規則的詳細程度為PID層級。
您無法在中為相同的PID定義某些屬性 `/apps/*/config.author/` 以及中更具體的專案 `/apps/*/config.emea.author/` 相同PID的。
符合執行模式數量最多的設定對整個PID有效。

### 標準設定 {#standard-configurations}

下列清單顯示存放庫中提供的一小部分設定（在標準安裝中）：

* 作者 — AEM WCM篩選器：

   `libs/wcm/core/config.author/com.day.cq.wcm.core.WCMRequestFilter`

* 發佈 — AEM WCM篩選器：

   `libs/wcm/core/config.publish/com.day.cq.wcm.core.WCMRequestFilter`

* 發佈 — AEM WCM頁面統計資料：

   `libs/wcm/core/config.publish/com.day.cq.wcm.core.stats.PageViewStatistics`

>[!NOTE]
>
>因為這些設定位於 `/libs` 不可直接編輯，但可複製到您的應用程式區域( `/apps`)。

若要列出執行個體中的所有設定節點，請使用 **查詢** CRXDE Lite功能，可提交下列SQL查詢：

`select * from sling:OsgiConfig`

### 設定持續性 {#configuration-persistence}

* 如果您透過Web主控台變更組態，該組態（通常）會寫入存放庫：

   `/apps/{somewhere}`

   * 依預設 `{somewhere}` 是 `system/config` 因此設定會寫入

      `/apps/system/config`

   * 不過，如果您要編輯的設定最初來自存放庫中的其他位置，例如：

      /libs/foo/config/someconfig

      然後，更新的設定會寫入原始位置下；例如：

      `/apps/foo/config/someconfig`

* 變更的設定 `admin` 儲存在 `*.config` 檔案位於：

   ```
      /crx-quickstart/launchpad/config
   ```

   * 此區域是OSGi設定管理員的私人資料，並保留以下專案指定的所有設定詳細資訊： `admin`，無論使用者如何進入系統。
   * 此區域是實作詳細資料，您絕不能直接編輯此目錄。
   * 不過，瞭解這些組態檔的位置會很有用，這樣就可以擷取復本進行備份、進行多項安裝，或兩者兼而有之：

      * Apache Felix OSGi管理主控台

         `../crx/org/apache/felix/webconsole/internal/servlet/OsgiManager.config`

      * CRX Sling使用者端存放庫

         `../com/day/crx/sling/client/impl/CRXSlingClientRepository/<pid-nr>.config`

>[!CAUTION]
>
>切勿編輯下列資料夾或檔案：
>
>`/crx-quickstart/launchpad/config`
