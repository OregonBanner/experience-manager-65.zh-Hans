---
title: 部署社群
seo-title: Deploying Communities
description: 如何部署AEM Communities
seo-description: How to deploy AEM Communities
uuid: 18d9b424-004d-43b2-968a-318e27a93759
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
content-type: reference
topic-tags: deploying
discoiquuid: c8d7355f-5a70-40d1-bf22-62fab8002ea0
docset: aem65
exl-id: 5b3d572d-e73d-4626-b664-c985949469c9
source-git-commit: 9f9f80eb4cb74b687c7fadd41d0f8ea4ee967865
workflow-type: tm+mt
source-wordcount: '1699'
ht-degree: 1%

---

# 部署社群 {#deploying-communities}

## 前提条件 {#prerequisites}

* [AEM 6.5平台](/help/sites-deploying/deploy.md)

* AEM Communities授權

* 選購的授權：

   * [適用於社群的Adobe Analytics功能](/help/communities/analytics.md)
   * [MongoDB for MSRP](/help/communities/msrp.md)
   * [ASRP的Adobe雲端](/help/communities/asrp.md)

## 安裝檢查清單 {#installation-checklist}

**對於 [AEM平台](/help/sites-deploying/deploy.md#what-is-aem)**

* 安裝最新版本 [AEM 6.5更新](#aem64updates)

* 若不使用預設連線埠(4502、4503)，則 [設定復寫代理](#replication-agents-on-author)
* [復寫加密金鑰](#replicate-the-crypto-key)
* 如果支援全球化， [設定自動化翻譯](/help/sites-administering/translation.md)
（提供範例設定以供開發）

**對於 [Communities功能](/help/communities/overview.md)**

* 如果部署 [發佈陣列](/help/sites-deploying/recommended-deploys.md#tarmk-farm)， [識別主要發行者](#primary-publisher)

* [啟用通道服務](#tunnel-service-on-author)
* [啟用社交登入](/help/communities/social-login.md#adobe-granite-oauth-authentication-handler)
* [設定Adobe Analytics](/help/communities/analytics.md)
* 設定 [預設電子郵件服務](/help/communities/email.md)
* 識別 [共用的UGC儲存體](/help/communities/working-with-srp.md) (**SRP**)

   * 如果MongoDB SRP [(MSRP)](/help/communities/msrp.md)

      * [安裝及設定MongoDB](/help/communities/msrp.md#mongodb-configuration)
      * [設定Solr](/help/communities/solr.md)
      * [選取MSRP](/help/communities/srp-config.md)
   * 如果關聯式資料庫SRP [(DSRP)](/help/communities/dsrp.md)

      * [安裝適用於MySQL的JDBC驅動程式](#jdbc-driver-for-mysql)
      * [安裝及設定MySQL for DSRP](/help/communities/dsrp-mysql.md)
      * [設定Solr](/help/communities/solr.md)
      * [選取DSRP](/help/communities/srp-config.md)
   * 如果AdobeSRP [(ASRP)](/help/communities/asrp.md)

      * 與您的客戶代表合作以進行布建
      * [選取ASRP](/help/communities/srp-config.md)
   * 若為JCR SRP [(JSRP)](/help/communities/jsrp.md)

      * 不是共用的UGC存放區：

         * 從未復寫UGC
         * UGC只顯示在輸入它的AEM執行個體或叢集上

         * 預設為JSRP




## 最新版本 {#latest-releases}

AEM 6.5 Communities GA包含Communities套件。 瞭解AEM 6.5的更新 [Communities](/help/release-notes/release-notes.md#experiencemanagercommunities)，請參閱 [AEM 6.5發行說明](/help/release-notes/release-notes.md#communities-release-notes.html).

### AEM 6.5更新 {#aem-updates}

從AEM 6.4開始，Communities更新作為AEM Cumulative Fix Pack和Service Pack的一部分提供。

如需AEM 6.5的最新更新，請參閱 [Adobe Experience Manager 6.4 Cumulative Fix Pack和Service Pack](https://helpx.adobe.com/cn/experience-manager/aem-releases-updates.html).

### 版本历史记录 {#version-history}

和AEM 6.4及更高版本一樣，AEM Communities功能和Hotfix是AEM Communities Cumulative Fix Pack和Service Pack的一部分。 因此，沒有單獨的Feature Pack。

### MySQL的JDBC驅動程式 {#jdbc-driver-for-mysql}

一個Communities功能使用MySQL資料庫：

* 對象 [DSRP](/help/communities/dsrp.md)：儲存使用者產生的內容(UGC)

必須單獨取得並安裝MySQL聯結器。

必要的步驟如下：

1. 下載ZIP封存，從 [https://dev.mysql.com/downloads/connector/j/](https://dev.mysql.com/downloads/connector/j/)

   * 版本必須>= 5.1.38

1. 擷取mysql-connector-java-&lt;version>-bin.jar （套件）
1. 使用Web主控台來安裝並啟動套件組合：

   * 例如， https://localhost:4502/system/console/bundles
   * 选择 **`Install/Update`**
   * 瀏覽……以選取從下載的ZIP封存解壓縮的套件組合
   * 檢查 *oracle公司的MySQLcom.mysql.jdbc之JDBC驅動程式* 處於作用中狀態，如果沒有，則啟動它（或檢查記錄）

1. 如果在設定JDBC之後在現有部署上進行安裝，則從Web主控台重新儲存JDBC設定，以將JDBC重新繫結至新聯結器：
   * 例如， https://localhost:4502/system/console/configMgr
   * 尋找 `Day Commons JDBC Connections Pool` 設定
   * 選取以開啟
   * 选择 `Save`

1. 在所有製作和發佈執行個體上重複步驟3和4

如需有關安裝套裝的詳細資訊，請參閱 [網頁主控台](/help/sites-deploying/web-console.md) 頁面。

#### 範例：已安裝MySQL聯結器套件組合 {#example-installed-mysql-connector-bundle}

![connect-bundle](assets/connector-bundle.png)



### AEM進階MLS {#aem-advanced-mls}

為了讓SRP集合（MSRP或DSRP）支援進階多語言搜尋(MLS)，除了自訂結構描述和Solr設定外，還需要新的Solr外掛程式。 所有必要專案都會封裝成可下載的zip檔案。

進階MLS下載（也稱為「phasetwo」）可從Adobe存放庫取得：

* AEM-SOLR-MLS-phasetwo

   若要取得進階MLS套件，請參閱 [AEM進階MLS](deploy-communities.md#aem-advanced-mls) 在檔案的部署區段中。

   * 1.2.40版（2016年4月6日）
   * 下載AEM-SOLR-MLS-phasetwo-1.2.40.zip

如需詳細資訊和安裝資訊，請造訪 [Solr設定](/help/communities/solr.md) 用於SRP。

### 關於封裝共用的連結 {#about-links-to-package-share}

**AdobeAEM Cloud中可見的套件**

此頁面上的封裝連結不需要正在執行的AEM執行個體，因為它們要共用封裝 `adobeaemcloud.com`. 雖然可檢視套件，但 `Install` 按鈕用於將套件安裝至Adobe代管網站。 如果要在本機AEM執行個體上安裝，請選取 `Install` 將會導致錯誤。

**如何在本機AEM執行個體上安裝**

若要安裝中顯示的套件 `adobeaemcloud.com` 在本機AEM執行個體上，套件必須先下載至本機磁碟：

* 選取 **資產** 標籤
* 選取 **下載至磁碟**

在本機AEM執行個體上，使用封裝管理員(例如 [https://localhost:4502/crx/packmgr/](https://localhost:4502/crx/packmgr/))，以上傳至本機AEM套件存放庫。

或者，您也可以從本機AEM執行個體(例如， [https://localhost:4502/crx/packageshare/](https://localhost:4502/crx/packageshare/))， `Download` 按鈕將下載到本機AEM執行個體的封裝存放庫。

一旦進入本機AEM執行個體的封裝存放庫，請使用封裝管理員來安裝封裝。

如需詳細資訊，請造訪 [如何使用套件](/help/sites-administering/package-manager.md#package-share).

## 建議的部署 {#recommended-deployments}

在AEM Communities中，常用存放區用於儲存使用者產生的內容(UGC)，通常稱為 [儲存資源提供者(SRP)](/help/communities/working-with-srp.md). 建議的部署著重於為通用存放區選擇SRP選項。

通用存放區支援在發佈環境中稽核和分析UGC，同時消除了對的需求 [復寫](/help/communities/sync.md) UGC的。

* [社群內容存放區](/help/communities/working-with-srp.md) ：討論AEM社群的SRP儲存選項

* [建議的拓撲](/help/communities/topologies.md) ：根據使用案例和SRP選擇討論要使用的拓撲

## 升級 {#upgrading}

從舊版AEM升級至AEM 6.5平台時，請務必閱讀 [升級至AEM 6.5](/help/sites-deploying/upgrade.md).

除了升級平台以外，請閱讀 [升級至AEM Communities 6.5](/help/communities/upgrade.md) 以瞭解Communities變更。

## 配置 {#configurations}

### 主要發行者 {#primary-publisher}

當選擇的部署是 [發佈陣列](/help/communities/topologies.md#tarmk-publish-farm)，則必須將一個AEM發佈執行個體識別為 **`primary publisher`** 針對不應該在所有執行個體上發生的活動，例如依賴的功能 **通知** 或 **Adobe Analytics**.

根據預設， `AEM Communities Publisher Configuration` OSGi設定是使用 **`Primary Publisher`** 核取方塊，讓發佈伺服器陣列中的所有發佈執行個體可自我識別為主要執行個體。

因此，有必要 **編輯所有次要發佈執行個體的設定** 取消核取 **`Primary Publisher`** 核取方塊。

![primary-publisher](assets/primary-publisher.png)

對於發佈伺服器陣列中的所有其他（次要）發佈執行個體：

* 以管理員許可權登入
* 存取 [網頁主控台](/help/sites-deploying/configuring-osgi.md)

   * 例如， [https://localhost:4503/system/console/configMgr](https://localhost:4503/system/console/configMgr)

* 找到 `AEM Communities Publisher Configuration`
* 選取編輯圖示
* 取消勾選 **主要發行者** 方塊
* 選取 **儲存**

### 作者上的復寫代理 {#replication-agents-on-author}

復寫可用於在發佈環境中建立的網站內容（例如社群群組），以及使用 [通道服務](#tunnel-service-on-author).

對於主要發行者，請確定 [復寫代理程式設定](/help/sites-deploying/replication.md) 正確識別發佈伺服器和授權使用者。 預設授權使用者， `admin,` 已經擁有適當的許可權(是 `Communities Administrators`)。

為了讓其他使用者擁有適當的許可權，必須將其新增為的成員 `administrators` 使用者群組(也是 `Communities Administrators`)。

製作環境中有兩個復寫代理程式需要正確設定傳輸設定。

* 存取作者上的復寫主控台

   * 從全域導覽，導覽至 **[!UICONTROL 工具]** > **[!UICONTROL 部署]** > **[!UICONTROL 復寫]** > **[!UICONTROL 作者上的代理]**

* 兩個代理程式請遵循相同的程式：

   * **預設代理程式（發佈）**
   * **反向復寫代理程式（反向發佈）**

      1. 選取代理程式
      1. 選取 **編輯**
      1. 選取 **傳輸** 標籤
      1. 若非連線埠 `4503`，編輯 **URI** 指定正確的連線埠

      1. 若非使用者 `admin`，編輯 **使用者** 和 **密碼** 若要指定 `administrators` 使用者群組

下列影像顯示透過將連線埠從4503變更為6103的結果：

#### 預設代理程式（發佈） {#default-agent-publish}

![default-agent-publish](assets/default-agent-publish.png)

#### 反向復寫代理程式（反向發佈） {#reverse-replication-agent-publish-reverse}

![reverse-replication-agent](assets/reverse-replication-agent.png)

### 作者上的通道服務 {#tunnel-service-on-author}

使用製作環境時 [建立網站](/help/communities/sites-console.md)， [修改網站屬性](/help/communities/sites-console.md#modifying-site-properties) 或 [管理社群成員](/help/communities/members.md)時，必須存取在發佈環境中註冊的成員（使用者），而非在作者中註冊的使用者。

通道服務使用作者上的復寫代理程式提供此存取。

若要啟用通道服務：

* 以作者執行個體的管理許可權登入。
* 如果publisher不是localhost：4503，或傳輸使用者不是 `admin`，則 [設定復寫代理](#replication-agents-on-author)

* 存取 [網頁主控台](/help/sites-deploying/configuring-osgi.md)

   * 例如， [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)

* 找到 `AEM Communities Publish Tunnel Service`
* 選取編輯圖示
* 檢查 **啟用** 方塊
* 選取 **儲存**

   ![tunnel-service](assets/tunnel-service.png)

### 復寫加密金鑰 {#replicate-the-crypto-key}

AEM Communities有兩項功能需要所有AEM伺服器執行個體使用相同的加密金鑰。 這些是 [分析](/help/communities/analytics.md) 和 [ASRP](/help/communities/asrp.md).

從AEM 6.3開始，金鑰材料會儲存在檔案系統中，不再儲存在存放庫中。

若要將主要素材從作者複製到所有其他例項，您必須：

* 存取包含要複製之重要素材的AEM例項，通常是作者例項

   * 找到 `com.adobe.granite.crypto.file` 例如，本機檔案系統中的組合

      * `<author-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21`
      * 此 `bundle.info` 檔案將識別該組合
   * 導覽至資料夾，例如，

      * `<author-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21/data`

      * 複製hmac和主要節點檔案


* 針對每個目標AEM執行個體

   * 導覽至資料夾，例如，

      * `<publish-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21/data`
   * 貼上先前複製的2個檔案
   * 必須 [重新整理Granite加密套件組合](#refresh-the-granite-crypto-bundle) 如果目標AEM執行個體目前正在執行


>[!CAUTION]
>
>如果已設定了另一個以加密金鑰為基礎的安全性功能，則複製加密金鑰可能會損壞設定。 如需協助， [聯絡客戶服務](https://helpx.adobe.com/cn/marketing-cloud/contact-support.html).

#### 存放庫復寫 {#repository-replication}

在第一次啟動每個AEM執行個體（這會建立初始存放庫）時，指定下列系統屬性，即可保留存放庫中的金鑰資料(AEM 6.2及舊版的情況相同)：

* `-Dcom.adobe.granite.crypto.file.disable=true`

>[!NOTE]
>
>務必確認 [作者上的復寫代理](#replication-agents-on-author) 已正確設定。

將金鑰資料儲存在存放庫後，將加密金鑰從作者複製到其他執行個體的方式如下：

使用 [CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md)：

* 瀏覽至 [https://&lt;server>：&lt;port>/crx/de](https://localhost:4502/crx/de)
* 选择 `/etc/key`
* 開啟 `Replication` 標籤
* 选择 `Replicate`

* [重新整理Granite加密套件組合](#refresh-the-granite-crypto-bundle)

   ![復寫存放庫](assets/replicare-repository.png)

#### 重新整理Granite加密套件組合 {#refresh-the-granite-crypto-bundle}

* 在每個發佈執行個體上，存取 [網頁主控台](/help/sites-deploying/configuring-osgi.md)

   * 例如， [https://&lt;server>：&lt;port>/system/console/bundles](https://localhost:4503/system/console/bundles)

* 尋找 `Adobe Granite Crypto Support` 套件組合(com.adobe.granite.crypto)
* 選取 **重新整理**

   ![granite-crypto](assets/granite-crypto.png)

* 過了一會兒， **成功** 對話方塊應會出現：
   `Operation completed successfully.`

### Apache HTTP Server {#apache-http-server}

如果使用Apache HTTP伺服器，請確定您對所有相關專案使用正確的伺服器名稱。

請特別注意，請使用正確的伺服器名稱，而不是 `localhost`，在 `RedirectMatch`.

#### httpd.conf範例 {#httpd-conf-sample}

```shell
<IfModule alias_module>
     # XAMPP does not have a favicon; this prevents any 404 errors which may arise.
     Redirect 404 /favicon.ico
     <Location /favicon.ico>
         ErrorDocument 404 "No favicon"
     </Location>

    # Return from "Sign Out" generates response header directing you to "/", generating a 404 error
    # The RedirectMatch resolves it correctly when modified for the target Community Site :
    RedirectMatch ^/$ https://[server name]/content/sites/engage/en.html
 ...
 </IfModule>
```

### Dispatcher {#dispatcher}

如果使用Dispatcher，請參閱：

* AEM [Dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher.html) 檔案
* [安装 Dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-install.html)
* [為社群設定Dispatcher](/help/communities/dispatcher.md)
* [已知问题](/help/communities/troubleshooting.md#dispatcher-refetch-fails)

## 相關Communities檔案 {#related-communities-documentation}

* 造訪 [管理社群網站](/help/communities/administer-landing.md) 瞭解有關建立社群網站、設定社群網站範本、仲裁社群內容、管理成員和設定傳訊功能的資訊。

* 造訪 [開發社群](/help/communities/communities.md) 瞭解社交元件架構(SCF)和自訂Communities元件和功能。

* 造訪 [Authoring Communities元件](/help/communities/author-communities.md) 瞭解如何使用及設定Communities元件進行創作。
