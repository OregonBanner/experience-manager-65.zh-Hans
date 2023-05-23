---
title: AEM Forms 服务器性能优化
seo-title: Performance tuning of AEM Forms server
description: 若要讓AEM Forms以最佳方式執行，您可以微調快取設定和JVM引數。 此外，使用網頁伺服器可增強AEM Forms部署的效能。
seo-description: For AEM Forms to perform optimally, you can fine-tune the cache settings and JVM parameters. Also, using a web server can enhance the performance of AEM Forms deployment.
uuid: bf23b62c-7559-4726-8f4e-cc8b1457e501
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Configuration
discoiquuid: 38c0ec46-5686-4656-bfb4-7125ec194673
docset: aem65
role: Admin
exl-id: 22926757-9cdb-4f8a-9bd9-16ddbc3f954a
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '893'
ht-degree: 1%

---

# AEM Forms 服务器性能优化{#performance-tuning-of-aem-forms-server}

本文會討論您可以實作的策略和最佳實務，以減少瓶頸並最佳化AEM Forms部署的效能。

## 快取設定 {#cache-settings}

您可以使用「 」設定和控制AEM Forms的快取策略 **行動Forms設定** AEM Web Configuration Console中的元件，位於：

* (OSGi上的AEM Forms) `https://'[server]:[port]'/system/console/configMgr`
* (JEE版AEM Forms) `https://'[server]:[port]'/lc/system/console/configMgr`

可用的快取選項如下：

* **無**：強制不要快取任何成品。 實際上，這會減慢效能，而且因為沒有快取記憶體，所以需要高可用記憶體。
* **保守**：指定僅快取在轉譯表單前產生的那些中間成品，例如包含內嵌片段和影像的範本。
* **積極進取**：強制快取幾乎所有可以快取的內容，包括演算的HTML內容，以及保守快取層級的所有成品。 這樣不僅可產生最佳效能，而且會消耗更多記憶體來儲存快取的成品。 積極快取策略表示在快取呈現的內容時，您在呈現表單時將獲得持續的時間效能。

AEM Forms的預設快取設定可能不足以達到最佳效能。 因此，建議使用以下設定：

* **快取策略**：積極進取
* **快取大小** （根據表格數量）：視需要
* **物件大小上限**：視需要

![行動Forms設定](assets/snap.png)

>[!NOTE]
>
>如果您使用AEM Dispatcher快取調適型表單，它也會快取調適型表單，該表單包含具有預填資料的表單。 如果從AEM Dispatcher快取中提供這類表單，可能會導致向使用者提供預先填入或過時的資料。 因此，請使用AEM Dispatcher快取不使用預先填入資料的最適化表單。 此外，Dispatcher快取不會自動讓快取片段失效。 因此，請勿將其用於快取表單片段。 對於此類表單和片段，請使用 [調適型表單快取](../../forms/using/configure-adaptive-forms-cache.md).

## JVM引數 {#jvm-parameters}

為獲得最佳效能，建議使用下列JVM `init` 引數來設定 `Java heap` 和 `PermGen`.

```shell
set CQ_JVM_OPTS=%CQ_JVM_OPTS% -Xms8192m
set CQ_JVM_OPTS=%CQ_JVM_OPTS% -Xmx8192m
set CQ_JVM_OPTS=%CQ_JVM_OPTS% -XX:PermSize=256m
set CQ_JVM_OPTS=%CQ_JVM_OPTS% -XX:MaxPermSize=1024m
```

>[!NOTE]
>
>建議的設定適用於Windows 2008 R2 8 Core和OracleHotSpot 1.7 （64位元） JDK，並應根據您的系統組態進行擴充或縮放。

## 使用網頁伺服器 {#using-a-web-server}

調適型表單和HTML5表單會轉譯為HTML5格式。 結果輸出可能會很大，具體取決於表單大小和表單中的影像等因素。 為了最佳化資料傳輸，建議使用提供請求的Web伺服器壓縮HTML回應。 此方法可減少回應大小、網路流量，以及在伺服器和使用者端電腦之間串流資料所需的時間。

例如，執行以下步驟，透過JBoss在Apache Web Server 2.0 32位元上啟用壓縮：

>[!NOTE]
>
>下列指示不適用於Apache Web Server 2.0 32位元以外的任何伺服器。 如需任何其他伺服器特定的步驟，請參閱相應的產品檔案。

下列步驟示範使用Apache Web Server啟用壓縮所需的變更

**取得適用於您作業系統的Apache Web Server軟體**

* Windows：從Apache HTTP Server Project網站下載Apache Web Server。
* Solaris 64位元：從Sunfreeware for Solaris網站下載Apache Web Server。
* Linux： Linux系統上已預先安裝Apache Web Server。

Apache可以使用HTTP通訊協定與CRX通訊。 這些設定是使用HTTP進行最佳化。

1. 取消註解中的下列模組設定 `APACHE_HOME/conf/httpd.conf` 檔案。

   ```shell
   LoadModule proxy_balancer_module modules/mod_proxy.so
   LoadModule proxy_balancer_module modules/mod_proxy_http.so
   LoadModule deflate_module modules/mod_deflate.so
   ```

   >[!NOTE]
   >
   >若是Linux，預設值為 `APACHE_HOME` 是 `/etc/httpd/`.

1. 在crx的連線埠4502上設定Proxy。
在中新增以下設定 `APACHE_HOME/conf/httpd.conf` 設定檔。

   ```shell
   ProxyPass / https://<server>:4502/
   ProxyPassReverse / https://<server>:4502/
   ```

1. 啟用壓縮。 在中新增以下設定 `APACHE_HOME/conf/httpd.conf` 設定檔。

   **適用於HTML5表單**

   ```xml
   <Location /content/xfaforms>
       <IfModule mod_deflate.c>
           SetOutputFilter DEFLATE
           #Don’t compress
           SetEnvIfNoCase Request_URI \.(?:gif|jpe?g|png)$ no-gzip dont-vary
           SetEnvIfNoCase Request_URI \.(?:exe|t?gz|zip|bz2|sit|rar)$ no-gzip dont-vary
           #Dealing with proxy servers
               <IfModule mod_headers.c>
                   Header append Vary User-Agent
               </IfModule>
       </IfModule>
   </Location>
   ```

   **適用最適化表單**

   ```xml
   <Location /content/forms/af>
       <IfModule mod_deflate.c>
           SetOutputFilter DEFLATE
           #Don’t compress
           SetEnvIfNoCase Request_URI \.(?:gif|jpe?g|png)$ no-gzip dont-vary
           SetEnvIfNoCase Request_URI \.(?:exe|t?gz|zip|bz2|sit|rar)$ no-gzip dont-vary
           #Dealing with proxy servers
               <IfModule mod_headers.c>
                   Header append Vary User-Agent
               </IfModule>
       </IfModule>
   </Location>
   ```

   若要存取crx伺服器，請使用 `https://'server':80`，其中 `server` 是執行Apache伺服器的伺服器名稱。

## 在執行AEM Forms的伺服器上使用防毒 {#using-an-antivirus-on-server-running-aem-forms}

在執行防毒軟體的伺服器上，您可能會遇到效能變慢的情況。 一律開啟防毒（隨存取掃描）軟體會掃描系統的所有檔案。 它可能會減慢伺服器的速度，且AEM Forms的效能會受到影響。

若要改善效能，您可以指示防毒軟體從永遠開啟（隨選）掃描中排除下列AEM Forms檔案和資料夾：

* AEM安裝目錄。 如果無法排除完整的目錄，請排除下列專案：

   * [AEM安裝目錄]\crx-repository\temp
   * [AEM安裝目錄]\crx-repository\repository
   * [AEM安裝目錄]\crx-repository\launchpad

* 應用程式伺服器暫存目錄。 預設位置為：

   * (Jboss) [AEM安裝目錄]\jboss\standalone\tmp
   * (Weblogic) \Oracle\Middleware\user_projects\domains\LCDomain\servers\LCServer1\tmp
   * (Websphere) \計畫Files\IBM\WebSphere\AppServer\profiles\AppSrv01\temp

* **(僅限JEE上的AEM Forms)** 全域檔案儲存(GDS)目錄。 預設位置為：

   * (JBos) [appserver根目錄]/server/&#39;server&#39;/svcnative/DocumentStorage
   * (WebLogic) [appserverdomain]/&#39;server&#39;/adobe/LiveCycleServer/DocumentStorage
   * (WebSphere) [appserver根目錄]/installedApps/adobe/&#39;server&#39;/DocumentStorage

* **(僅限JEE上的AEM Forms)** AEM Forms伺服器記錄檔和暫存目錄。 預設位置為：

   * 伺服器記錄 —  [AEM Forms安裝目錄]\Adobe\AEM forms\[app-server]\server\all\logs
   * 暫存目錄 —  [AEM Forms安裝目錄]\temp

>[!NOTE]
>
>* 如果您使用GDS和暫存目錄的其他位置，請開啟AdminUI，網址為 `https://'[server]:[port]'/adminui`，導覽至 **首頁>設定>核心系統設定>核心設定** 以確認使用中的位置。
* 如果AEM Forms伺服器即使在排除建議的目錄之後也執行速度緩慢，則也要排除Java可執行檔(java.exe)。
>

