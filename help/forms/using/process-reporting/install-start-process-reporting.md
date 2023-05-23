---
title: 開始使用程式報告
description: 開始使用AEM Forms on JEE程式報告的步驟
uuid: 685cad39-da2c-411d-a0b0-201917438bcf
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: process-reporting
discoiquuid: 7c1fcde0-b983-4b24-bc19-fcee1d4f096b
docset: aem65
exl-id: 1272e854-fa64-4bfd-b073-8fbcf210e9b5
source-git-commit: 3d713021ac410ca2925a282c5dfca98ed4e483ee
workflow-type: tm+mt
source-wordcount: '1673'
ht-degree: 0%

---

# 開始使用程式報告{#getting-started-with-process-reporting}

程式報告讓AEM Forms使用者能夠查詢有關目前在AEM Forms實作中定義的AEM Forms程式的資訊。 不過，「程式報告」不會直接從AEM Forms存放庫存取資料。 資料會先依排程發佈至Process Reporting存放庫(*由ProcessDataPublisher和ProcessDataStorage服務提供* s)。 然後，會從發佈至存放庫的「程式報告」資料中產生「程式報告」中的報告和查詢。 程式報告會安裝為Forms Workflow模組的一部分。

本文詳細說明啟用將AEM Forms資料發佈到Process Reporting存放庫的步驟。 之後，您將能夠使用「程式報告」來執行報告和查詢。 文章也涵蓋設定「程式報告」服務時可用的選項。

## 程式報告先決條件 {#process-reporting-pre-requisites}

### 清除非必要處理 {#purge-non-essential-processes}

如果您目前使用Forms Workflow，AEM Forms資料庫可能會包含大量資料

Process Reporting發佈服務會發佈資料庫中目前可用的所有AEM Forms資料。 這表示，如果資料庫包含您不想執行報表和查詢的舊資料，即使報表不需要這些資料，也會將所有這些資料發佈到存放庫。 建議您在執行服務將資料發佈至Process Reporting存放庫之前，先清除此資料。 這麼做可改善發佈者服務和查詢資料以供報告的服務的效能。

如需有關清除AEM Forms程式資料的詳細資訊，請參閱 [清除程式資料](/help/forms/using/admin-help/purging-process-data.md).

>[!NOTE]
>
>如需「清除公用程式」的秘訣與技巧，請參閱Adobe Developer Connection文章，網址為 [永久刪除處理與工單](/help/forms/using/admin-help/purging-process-data.md).

## 設定程式Reporting Services {#configuring-process-reporting-services}

### 排程程式資料發佈 {#schedule-process-data-publishing}

Process Reporting Services會依排程將資料從AEM Forms資料庫發佈到Process Reporting存放庫。

這項作業需要大量資源，而且可能會影響AEM Forms伺服器的效能。 建議您在AEM Forms Server忙碌時段以外排程此作業。

根據預設，資料的發佈排程為每天凌晨2:00執行。

若要變更發佈排程，請執行下列步驟：

>[!NOTE]
>
>如果您在叢集上執行AEM Forms實作，請在叢集的每個節點上執行下列步驟。

1. 停止AEM Forms Server執行個體。
1. &#x200B;URL

   * （適用於Windows）開啟 `[JBoss root]/bin/run.conf.bat` 編輯器中儲存的檔案。
   * (適用於Linux®、AIX®和Solaris™) `[JBoss root]/bin/run.conf.sh` 編輯器中儲存的檔案。

1. 新增JVM引數 `-Dreporting.publisher.cron = <expression>.`

   範例：下列cron運算式會導致Process Reporting每五小時將AEM Forms資料發佈到Process Reporting存放庫：

   * `-Dreporting.publisher.cron = 0_0_0/5_*_*_?`

1. 儲存並關閉 `run.conf.bat` 檔案。

1. 重新啟動AEM Forms Server執行個體。

1. 停止AEM Forms Server執行個體。
1. 登入WebSphere®管理主控台。 在導覽樹狀結構中，按一下 **伺服器** > **應用程式伺服器** 然後在右窗格中，按一下伺服器名稱。

1. 在「伺服器基礎結構」下，按一下 **Java™和程式管理** > **程式定義**.

1. 在「其他屬性」下，按一下 **Java™虛擬機器器**.

   在「一般JVM引數」方塊中，新增引數 `-Dreporting.publisher.cron = <expression>.`

   **範例**：以下cron運算式會導致Process Reporting每五小時將AEM Forms資料發佈到Process Reporting存放庫：

   * `-Dreporting.publisher.cron = 0_0_0/5_*_*_?`

1. 按一下 **套用**，按一下「確定」 ，然後按一下 **直接儲存至主組態**.
1. 重新啟動AEM Forms Server執行個體。
1. 停止AEM Forms Server執行個體。
1. 登入WebLogic管理主控台。 WebLogic管理主控台的預設位址為 `https://[hostname]:[port]/console`.
1. 在「變更中心」下，按一下 **鎖定和編輯**.
1. 在「領域結構」下，按一下 **環境** > **伺服器** 然後在右窗格中，按一下Managed伺服器名稱。
1. 在下一個畫面中，按一下 **設定** 標籤> **伺服器啟動** 標籤。
1. 在引數方塊中，新增JVM引數 `-Dreporting.publisher.cron = <expression>`.

   **範例**：以下cron運算式會導致Process Reporting每五小時將AEM Forms資料發佈到Process Reporting存放庫：

   `-Dreporting.publisher.cron = 0_0_0/5_*_*_?`

1. 按一下 **儲存** 然後按一下 **啟用變更**.
1. 重新啟動AEM Forms Server執行個體。

![processdatapublisherservice](assets/processdatapublisherservice.png)

### ProcessDataStorage服務 {#processdatastorage-service}

ProcessDataStorageProvider服務會從ProcessDataPublisher服務接收程式資料，並將資料儲存到Process Reporting儲存庫。

在每個發佈週期，資料都會儲存到預先定義的根資料夾的子資料夾中。

您可以使用管理主控台來設定根(**預設**： `/content/reporting/pm`)位置和子資料夾(**預設**： `/yyyy/mm/dd/hh/mi/ss`)儲存程式資料的階層格式。

#### 設定「程式報告」存放庫位置 {#to-configure-the-process-reporting-repository-locations}

1. 登入 **管理主控台** 具有管理員認證。 管理主控台的預設URL為 `https://'[server]:[port]'/adminui`
1. 導覽至 **首頁** > **服務** > **應用程式和服務** >**服務管理** 並開啟 **ProcessDataStorageProvider** 服務。

   ![process-data-storage-service](assets/process-data-storage-service.png)

   **RootFolder**

   將儲存程式資料以用於報表的CRX位置。

   `Default`： `/content/reporting/pm`

   **資料夾階層**

   根據程式建立時間，將程式資料儲存於其中的資料夾階層。

   `Default`: `/yyyy/mm/dd/hh/mi/ss`

1. 单击“**保存**”。

### ReportConfiguration服務 {#reportconfiguration-service}

Process Reporting會使用ReportConfiguration服務來設定程式報告查詢服務。

#### 設定ReportingConfiguration服務的方式 {#to-configure-the-reportingconfiguration-service}

1. 登入 **設定管理員** 具有CRX管理員認證。 Configuration Manager的預設URL為 `https://'[server]:[port]'/lc/system/console/configMgr`
1. 開啟 **報告設定** 服務。
1. **記錄數**

   在存放庫上執行查詢時，結果可能包含許多記錄。 如果結果集很大，查詢執行可能會佔用伺服器資源。

   若要處理大型結果集，ReportConfiguration服務會將查詢處理分割成記錄批次。 這樣做會減少系統負載。

   `Default`: `1000`

   **CRX儲存路徑**

   要儲存程式資料以便進行報告的CRX位置。

   `Default`: `/content/reporting/pm`

   >[!NOTE]
   >
   >此位置與ProcessDataStorage組態選項中指定的位置相同 **根資料夾**.
   >
   >
   >如果您更新ProcessDataStorage設定中的Root Folder選項，則必須更新ReportConfiguration服務中的CRX Storage Path位置。

1. 按一下 **儲存** 並關閉 **CQ Configuration Manager**.

### ProcessDataPublisher服務 {#processdatapublisher-service}

ProcessDataPublisher服務會從AEM Forms資料庫匯入處理作業資料，並將資料發佈到ProcessDataStorageProvider服務以進行儲存。

#### 設定ProcessDataPublisher服務的方式   {#to-configure-processdatapublisher-service-nbsp}

1. 登入 **管理主控台** 具有管理員認證。

   預設URL為 `https://'server':port]/adminui/`.

1. 導覽至 **首頁** > **服務** > **應用程式和服務** >**服務管理** 並開啟 **ProcessDataPublisher** 服務。

![processdatapublisherservice-1](assets/processdatapublisherservice-1.png)

**發佈資料**

啟用此選項以開始發佈程式資料。 依預設，此選項為停用。

只有在正確設定與「程式報告」元件相關的所有設定時，才啟用「程式報告」。

或者，使用此選項可在不再需要流程資料發佈時停用它。

`Default`: `Off`

**批次間隔（秒）**

每次ProcessDataPublisher服務執行時，服務會依批次間隔分割自上次執行服務以來的時間。 然後，該服務會分別處理每個AEM Forms資料間隔，以幫助控制發佈者在一個週期內的每次執行（批次）期間端到端處理的資料大小。

例如，如果發佈程式每天執行，預設會將24個批次的處理分成每批次1小時，而不是在單一執行中處理一天的所有資料。

`Default`: `3600`

`Unit`: `Seconds`

**鎖定逾時（秒）**

發行者服務會在開始處理資料時取得鎖定，因此發行者的多個執行個體不會同時開始執行和處理資料。

如果取得鎖定的發行者服務閒置了「鎖定逾時」值所定義的秒數，則會釋放其鎖定，讓其他發行者服務執行個體可以繼續處理。

`Default`: `3600`

`Unit`: `Seconds`

**發佈資料來源**

AEM Forms環境包含設定環境時的資料。

依預設，ProcessDataPublisher服務會從AEM Forms資料庫匯入所有資料。

根據您的報告需求，如果您打算在特定日期和時間後對資料執行報告和查詢，建議您指定日期和時間。 發佈服務接著會發佈該時間之後的日期。

`Default`: `01-01-1970 00:00:00`

`Format`: `dd-MM-yyyy HH:mm:ss`

## 存取Process Reporting使用者介面 {#accessing-the-process-reporting-user-interface}

「程式報告」的使用者介面是以瀏覽器為基礎。

設定「程式報告」後，您可以在AEM Forms安裝的下列位置開始使用「程式報告」：

`https://<server>:<port>/lc/pr`

### 登入程式報告 {#log-in-to-process-reporting}

當您導覽至程式報告URL時(https://)&lt;server>：&lt;port>/lc/pr)，則會顯示登入畫面。

若要登入「程式報告」模組，請指定您的認證。

>[!NOTE]
>
>若要登入「程式報告」使用者介面，您需要下列AEM Forms許可權：
>
>`PERM_PROCESS_REPORTING_USER`

![登入程式報告](assets/capture1_new.png)

當您登入「程式報告」時， **[!UICONTROL 首頁]** 熒幕顯示。

### 程式報告首頁畫面 {#process-reporting-home-screen}

![process-reporting-home-screen](assets/process-reporting-home-screen.png)

**程式報告樹狀檢視：** 「首頁」畫面左側的樹狀檢視包含「程式報告」模組的專案。

樹狀結構檢視包含下列最上層專案：

**報告：** 此專案包含隨附於「處理報告」的現成可用報表。

如需預先定義報表的詳細資訊，請參閱 [處理中報表的預先定義報表](/help/forms/using/process-reporting/pre-defined-reports-in-process-reporting.md).

**臨機查詢：** 此專案包含用於執行以篩選條件為基礎的程式與工作搜尋的選項。

如需特定查詢的詳細資訊，請參閱 [程式報表中的臨時查詢](/help/forms/using/process-reporting/adhoc-queries-in-process-reporting.md).

**自訂：** 「自訂」節點會顯示您建立的自訂報表。

如需建立和顯示自訂報告的程式，請參閱 [自訂報告進行中報告](/help/forms/using/process-reporting/process-reporting-custom-reports.md).

**程式報告標題列：** 「程式報告」標題列包含一些通用選項，您可以在使用者介面中使用這些選項。

**程式報告標題：** 「程式報告」標題會顯示在標題列的左角。

隨時按一下標題以返回首頁畫面。

**上次更新時間：** 程式資料會按排程從AEM Forms資料庫發佈到程式報告存放庫。

「上次更新時間」會顯示資料更新推送至「程式報告」存放庫的上次日期和時間。

如需資料發佈服務以及如何排程此服務的詳細資訊，請參閱 [排程程式資料發佈](/help/forms/using/process-reporting/install-start-process-reporting.md#p-schedule-process-data-publishing-p) 在程式報告快速入門一文中。

**程式報告使用者：** 登入的使用者名稱會顯示在上次更新時間的右側。

**程式報表標題列下拉式清單：** 「程式報告」標題列右角的下拉式清單包含下列選項：

* **[!UICONTROL 同步]**：將內嵌的Process Reporting存放庫與AEM Forms資料庫同步。
* **[!UICONTROL 說明]**：檢視程式報告的說明檔案。
* **[!UICONTROL 登出]**：登出程式報告
