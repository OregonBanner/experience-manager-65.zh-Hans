---
title: 如何在JEE伺服器叢集上設定和疑難排解AEM Forms？
description: 瞭解如何在JEE伺服器叢集上設定和疑難排解AEM Forms
exl-id: 230fc2f1-e6e5-4622-9950-dae9449ed3f6
source-git-commit: 1cdd15800548362ccdd9e70847d9df8ce93ee06e
workflow-type: tm+mt
source-wordcount: '4033'
ht-degree: 0%

---

# 在JEE伺服器叢集上設定和疑難排解AEM Forms {#configuring-troubleshooting-aem-forms-jee-server-cluster}

## 必備條件知識 {#prerequisites}

熟悉JEE、JBoss、WebSphere和Webogic應用程式伺服器上的AEM Forms、Red Hat Linux、SUSE Linux、Microsoft Windows、IBM AIX或Sun Solaris作業系統、Oracle、IBM DB2或SQL Server資料庫伺服器，以及Web環境。

## 使用者層級 {#user-level}

高级

JEE Cluster上的AEM Forms是拓撲，旨在讓JEE上的AEM Forms能夠復原叢集節點的故障，並擴充系統容量，超越單一節點的能力。 叢集會將多個節點結合為單一邏輯系統，以共用資料並允許交易在執行中跨越多個節點。 在JEE上擴充AEM Forms的最常見方式是叢集，因為可以支援處理任何工作負載組合的任何服務組合。 JEE叢集上的AEM Forms不一定最適合所有型別的部署，尤其是非叢集伺服器負載平衡架構在許多情況下可能較為合適。

本檔案的目的是討論您在JEE叢集上使用AEM Forms時可能會遇到的具體設定需求和潛在問題區域。

## 叢集中有什麼內容？ {#what-is-in-cluster}

JEE叢集節點上的AEM Forms會在彼此之間通訊，並共用資訊，讓整個叢集具有單一一致的設定和應用程式狀態。 叢集內的資訊共用是透過多種不同的方式同時完成的，這些方式會用於不同的前後關聯。 基本資訊分享方法如下圖所示：

![應用程式伺服器叢集](assets/application-server-cluster.jpg)

### 應用程式伺服器叢集 {#application-server-cluster}

JEE叢集上的AEM Forms仰賴基礎應用程式伺服器的叢集功能。 應用程式伺服器叢集可整體管理叢集組態，並提供低階的叢集服務，例如Java命名和目錄介面(JNDI)，讓軟體元件能在叢集中找到彼此。 叢集服務的複雜性以及應用程式伺服器所依賴的基礎技術相依性，取決於應用程式伺服器。 WebSphere和WebLogic具有適用於叢集的複雜管理功能，而JBoss則具有非常基本的方法。

### GemFire快取 {#gemfire-cache}

GemFire快取是在每個叢集節點中實作的分散式快取機制。 節點會尋找彼此，並建立單一邏輯快取，以維持節點間的一致性。 發現彼此的節點會連線在一起，以維持在圖1中顯示為雲端的單一概念快取。 與GDS和資料庫不同，快取是純粹的名義實體。 實際的快取內容會儲存在記憶體和 `LC_TEMP` 每個叢集節點的目錄。

### 数据库 {#database}

JEE上的AEM Forms資料庫（透過JDBC資料來源IDP_DS、EDC_DS和其他資料存取）由叢集的所有節點共用。 有關JEE上AEM Forms狀態的大多數持續性資料，例如正在進行的交易、與進行中交易相關聯的使用者資料、有關如何設定系統設定的資料等，都位於此資料庫中。

### 全域檔案儲存 {#global-document-storage}

Global Document Storage (GDS)是AEM Forms on JEE中Document Manager （IDPDocument類別）使用的檔案系統儲存區域。 GDS儲存短期和長期的檔案，叢集的所有節點都必須可以存取這些檔案。

### 其他專案 {#other-items}

除了這些主要共用資源之外，還有其他專案具有特定的叢集行為，例如Quartz。 Quartz是AEM Forms on JEE所使用的排程器子系統，它使用資料庫表格來儲存其已排程的資訊以及正在執行哪些已排程活動的資訊。 對於單節點安裝和叢集，Quartz的設定必須不同，而且它會從JEE設定的其他AEM Forms獲得提示。

## 常見設定問題 {#common-configuration}

維護或疑難排解JEE叢集上的AEM Forms最令人沮喪的事情之一，就是沒有單一位置可以明確確認叢集是否健康。 若要確認叢集中的所有專案都運作正常，需要進行一些調查和分析，而且叢集作業有幾種失敗模式，這取決於叢集設定有哪些問題。 下圖說明一個設定錯誤的叢集，其中數個共用資源被不當共用。

![設定錯誤的叢集](assets/bad-configuration-cluster.png)

請謹記一件有趣且重要的事情，即使使用者不打算在叢集的JEE上執行AEM Forms，也必須熟悉叢集的運作方式，以及要在叢集中尋找和驗證的種類。 這是因為JEE上AEM Forms的某些部分可能會根據他們的提示，在叢集中錯誤地操作，並出現您不期望的叢集行為。

那麼上圖中的共用設定有什麼問題嗎？ 以下各節說明問題：

### (1) GemFire叢集組態 {#gemfire-cluster-configuration}

Gemfire快取可能會發生一些問題。 兩種典型情況是：

* 應該能夠找到彼此的節點無法這麼做。

* 不應加入叢集的節點會在不應加入叢集時彼此尋找並共用快取。

如果您有想要叢集的節點，它們必須在網路上找到彼此。 依預設，它們會透過多點傳送UDP訊息來執行此操作。 每個節點都會傳送廣播訊息來宣告其存在，而任何收到此類訊息的節點都會開始與其找到的其他節點交談。 這種自動探索的方法非常常見，許多型別的軟體和裝置都會這麼做。

自動探索的一個常見問題是，多點傳送訊息可能是因為網路原則或軟體防火牆規則而由網路所篩選，或是可能只是無法路由傳送到存在於節點之間的網路。 由於讓UDP自動探索在複雜網路中運作的一般困難，生產部署通常會使用替代探索方法：TCP定位器。 有關TCP定位器的一般討論可在參考資料中找到。

**我如何知道我使用定位器或UDP？**

下列JVM屬性可控制GemFire快取用來尋找其他節點的方法。

多點傳送設定：

* `adobe.cache.multicast-port`：用來與分散式系統其他成員通訊的多點傳送連線埠。 如果將此值設為0，會停用成員探索和散發的多點傳送。

* `gemfire.mcast-address` （選用）：覆寫Gemfire使用的預設IP位址。

TCP定位器設定：

* `adobe.cache.cluster-locators`：系統成員用來與執行中的定位器通訊的所有定位器之TCP定位器和TCP定位器連線埠的IP位址/主機名稱。

此清單必須包含目前使用中的所有定位器，且叢集系統的每個成員都必須以一致的方式設定。

如果TCP定位器清單是空的，則不會使用定位器，而是使用多點傳送方法。

**如何檢查我的TCP定位器是否正在執行？**

首先，如果TCP定位器正在使用中，您應該在所有叢集節點的下列JVM屬性中列出您的TCP定位器：

`-Dadobe.cache.cluster-locators=aix01.adobe.com[22345],aix02.adobe.com[22345]`

不需要在JEE叢集節點上的AEM Forms上執行定位器，如果需要，它們可以在獨立於叢集的其他系統上執行。 一個以上的系統可以執行定位器，一般來說，最佳作法是將定位器執行於兩個位置，避免定位器單一失敗可能導致叢集重新啟動的問題。 在每個執行定位器的系統上，您應該能夠使用下列命令來驗證這些電腦是否正在執行：

`netstat -an | grep 22345`

預期的回應應為：

`tcp 0 0 *.22345 *.* LISTEN`

另一個驗證指令如下：

`ps -ef | grep gemfire`

預期的回應應如下所示：

`livecycl 331984 1 0 10:14:51 pts/0 0:03 java -cp ./gemfire.jar: -Dgemfire.license-type=production -Dlocators=localhost[22345] com.gemstone.gemfire.distributed.Locator 22345`

**如何檢視GemFire認為在叢集中的節點？**

GemFire會產生記錄資訊，可用來診斷GemFire快取已找到並採用的叢整合員。 這可用來驗證是否找到所有正確的叢整合員，以及是否不會發生額外或不正確的叢集節點探索。 GemFire的記錄檔位於已設定的AEM Forms on JEE暫存目錄中：

`.../LC_TEMP/adobeZZ__123456/Caching/Gemfire.log`

之後的數值字串 `adobeZZ_` 是伺服器節點專屬的，因此您必須搜尋暫存目錄的實際內容。 之後的兩個字元 `adobe` 取決於應用程式伺服器型別： `wl`， `jb`，或 `ws`.

下列範例記錄顯示當雙節點叢集找到自身時發生的情況。

在第一個節點上，AP-HP8：

```xml
[config 2011/08/05 09:28:09.143 EDT GemfireCacheAdapter <server.startup : 0> tid=0x65] This member, ap-hp8(4268):18763, is becoming group coordinator.
[info 2011/08/05 09:28:09.151 EDT GemfireCacheAdapter <server.startup : 0> tid=0x65] Entered into membership in group GF6.5.1.17 with ID ap-hp8(4268)<v0>:18763/56449.
[info 2011/08/05 09:28:09.152 EDT GemfireCacheAdapter <server.startup : 0> tid=0x65] Starting DistributionManager ap-hp8(4268)<v0>:18763/56449.
[info 2011/08/05 09:28:09.153 EDT GemfireCacheAdapter <server.startup : 0> tid=0x65] Initial (membershipManager) view =  [ap-hp8(4268)<v0>:18763/56449]
[info 2011/08/05 09:28:09.153 EDT GemfireCacheAdapter <server.startup : 0> tid=0x65] Admitting member <ap-hp8(4268)<v0>:18763/56449>. Now there are 1 non-admin member(s).
[info 2011/08/05 09:28:09.154 EDT GemfireCacheAdapter <server.startup : 0> tid=0x65] ap-hp8(4268)<v0>:18763/56449 is the elder and the only member.
[info 2011/08/05 09:28:09.163 EDT GemfireCacheAdapter <server.startup : 0> tid=0x65] Did not hear back from any other system. I am the first one.
[info 2011/08/05 09:28:09.164 EDT GemfireCacheAdapter <server.startup : 0> tid=0x65] DistributionManager ap-hp8(4268)<v0>:18763/56449 started on 239.192.81.1[33456]. There were 0 other DMs. others: []
[info 2011/08/05 09:28:20.841 EDT GemfireCacheAdapter <Pooled Message Processor 1> tid=0xc4] New administration member detected at ap-hp7(2821)<v1>:19498/59136.
```

在另一個節點上，AP-HP7：

```xml
[info 2011/08/05 09:28:09.830 EDT GemfireCacheAdapter <server.startup : 0> tid=0x64] Attempting to join distributed system whose membership coordinator is ap-hp8(4268)<v0>:18763 using membership ID ap-hp7(2821):19498
[info 2011/08/05 09:28:10.058 EDT GemfireCacheAdapter <server.startup : 0> tid=0x64] Entered into membership in group GF6.5.1.17 with ID ap-hp7(2821)<v1>:19498/59136.
[info 2011/08/05 09:28:10.059 EDT GemfireCacheAdapter <server.startup : 0> tid=0x64] Starting DistributionManager ap-hp7(2821)<v1>:19498/59136.
[info 2011/08/05 09:28:10.060 EDT GemfireCacheAdapter <server.startup : 0> tid=0x64] Initial (membershipManager) view =  [ap-hp8(4268)<v0>:18763/56449, ap-hp7(2821)<v1>:19498/59136]
[info 2011/08/05 09:28:10.060 EDT GemfireCacheAdapter <server.startup : 0> tid=0x64] Admitting member <ap-hp8(4268)<v0>:18763/56449>. Now there are 1 non-admin member(s).
[info 2011/08/05 09:28:10.060 EDT GemfireCacheAdapter <server.startup : 0> tid=0x64] Admitting member <ap-hp7(2821)<v1>:19498/59136>. Now there are 2 non-admin member(s).
[info 2011/08/05 09:28:10.128 EDT GemfireCacheAdapter <server.startup : 0> tid=0x64] DistributionManager ap-hp7(2821)<v1>:19498/59136 started on 239.192.81.1[33456]. There were 1 other DMs. others: [ap-hp8(4268)<v0>:18763/56449]
```

**如果GemFire找到不應該找到的節點怎麼辦？**

共用企業網路的每個不同叢集都應該使用單獨的TCP定位器集合（如果使用TCP定位器），或使用單獨的UDP連線埠號碼（如果使用多點傳送UDP組態）。 由於UDP自動探索是JEE上AEM Forms的預設設定，而相同的預設連線埠33456可能正由多個叢集使用，所以不應該嘗試通訊的叢集可能會意外地這樣做 — 例如，生產和QA叢集應該保持獨立，但可以透過UDP多點傳送相互連線。

在GemFire不正確叢集的網路中，最常見的情況是在叢集的啟動載入期間，發現重複的連線埠。 您可能會發現啟動程式沒有明確原因而失敗。 通常會看到這樣的錯誤：

```xml
Caused by: com.ibm.ejs.container.UnknownLocalException: nested exception is: com.adobe.pof.schema.ObjectTypeNotFoundException: Object Type: dsc.sc_service_configuration not found.
                at com.adobe.pof.schema.POFDefaultDomain.getObjectType(POFDefaultDomain.java:93)
                at com.adobe.idp.dsc.initializer.DSCInitializerBean.serviceConfigAuditAttributeExists(DSCInitializerBean.java:225)
                at com.adobe.idp.dsc.initializer.DSCInitializerBean.installSchema(DSCInitializerBean.java:186)
                at com.adobe.idp.dsc.initializer.DSCInitializerBean.bootstrap(DSCInitializerBean.java:94)
                at com.adobe.idp.dsc.initializer.EJSLocalStatelessDSCInitializerBeanLocalEJB_7bb34e85.bootstrap(Unknown Source)
                at com.adobe.livecycle.bootstrap.bootstrappers.DSCBootstrapper.bootstrap(DSCBootstrapper.java:68)
```

在此情況下，啟動載入程式會與GemFire一起存取必要的資料表，而且透過JDBC存取的資料表與GemFire傳回的快取資料表資訊之間有不一致的情況，該資料表來自具有不同基礎資料庫的不同叢集。

雖然重複連線埠通常會在啟動時顯現，但此情況可能稍後出現，當叢集在其他叢集的啟動時關機之後重新啟動時，或當網路組態變更為讓先前被隔離的叢集彼此可見時（為了多點傳送目的）。

若要診斷這些情況，最好檢視GemFire記錄檔，並仔細考慮是否僅找到預期的節點。 若要修正問題，必須變更

`adobe.cache.multicast-port`

屬性對應至一個或兩個叢集上的不同值。

### 2) GDS共用 {#gds-sharing}

GDS共用是在JEE本身的AEM Forms外部以O/S層級設定，您必須在此層級安排相同的共用目錄結構可供所有叢集節點使用。 在Windows型別系統上，這通常是通過從某個節點到另一個節點設定檔案共用，或從遠端檔案系統（例如NAS裝置）到所有節點來完成。 在UNIX系統上，GDS共用通常透過NFS檔案共用來完成，也可以從一個節點到另一個節點或從NAS裝置完成。

叢集可能的失敗模式是這個遠端檔案共用變得無法使用，或是有細微的問題。 遠端掛載可能會因為網路問題、安全性設定或不正確的設定而失敗。 系統重新開機可能會造成設定變更在幾天或幾週前生效，這可能會導致意外情況。

**如果NFS共用無法掛載會發生什麼情況？**

在UNIX上，即使掛載失敗，NFS掛載對應到目錄結構的方式也可以允許使用顯然可用的GDS目錄。 请考虑：

* NAS伺服器：NFS共用資料夾/u01/iapply/livecycle_gds
* 節點1：共用資料夾（託管於DB伺服器）的掛接點，位置如下： /u01/iapply/livecycle_gds
* 節點2：共用資料夾（託管於DB伺服器）的掛接點，位置如下： /u01/iapply/livecycle_gds

* LCES指定GDS的路徑： /u01/iapply/livecycle_gds

如果節點1上的掛載失敗，目錄結構仍會包含到空掛載點的路徑/u01/iapply/livecycle_gds，而且節點會顯示為正確執行。 但由於GDS內容並未實際與其他節點共用，因此叢集將無法正常運作。 這有可能發生，也確實會發生，結果導致叢集以神秘的方式失敗。

最佳作法是安排順序，讓Linux掛載點不作為GDS的根目錄，而是將其中某些目錄作為GDS根目錄：

* 如果您有NFS伺服器，則它可能有目錄：/some/storage/lc_cluster_dev/LC_GDS
* 而且您的叢集節點上有一個掛接點： /u01/iapply/shared
* 掛載nfs_server： /some/storage/lc_cluster_dev/u01/iapply/shared
* 將GDS指向/u01/iapply/shared/LC_GDS

現在，如果由於某種原因掛載失敗，裸掛載點不會包含LC_GDS目錄，而且您的叢集將會預期失敗，因為它根本找不到任何GDS。

**如何確認所有節點都看到相同的GDS並具有許可權？**

若要驗證GDS存取和共用，最好以互動式使用者身分存取每個節點，可透過SSH或telnet連線至UNIX節點，或透過遠端案頭連線至Windows系統。 您應該能夠瀏覽至每個節點上已設定的GDS目錄或檔案系統，並從所有其他節點中可見的每個節點建立測試檔案。

請留意AEM Forms on JEE據以操作的使用者ID。 在Windows整套金鑰安裝中，這是以本機管理員身分執行。 在UNIX上，它可能是啟動指令碼或應用程式伺服器設定中設定的特定服務使用者。 此使用者ID必須能在所有節點上平等地建立和操作GDS檔案。

在UNIX系統上，NFS設定通常預設為不信任檔案和物件的根擁有權或根存取權。 如果您以root使用者身分執行應用程式伺服器，您會發現您必須在NFS伺服器上指定選項、掛載檔案的節點，或同時指定兩者，才能允許雙邊存取和控制由某個節點建立並由另一個節點存取的檔案。

### (3)資料庫共用 {#database-sharing}

為了使叢集正常運作，所有叢整合員必須共用相同的資料庫。 發生錯誤的範圍大致為：

* 不小心在個別的叢集節點上以不同方式設定IDP_DS、EDC_DS、AdobeDefaultSA_DS或其他必要的資料來源，使節點指向不同的資料庫。
* 不小心設定了多個不同的節點，讓這些節點共用一個資料庫。

視您的應用程式伺服器而定，在叢集範圍定義JDBC連線是很自然的事，所以在不同的節點上不可能有不同的定義。 不過，在Jboss上，完全可以設定，讓資料來源（例如IDP_DS）指向節點1上的一個資料庫，但指向節點2上的其他內容。

相反的問題實際上更常見，也就是說，JEE節點上的多個獨立（或叢集）AEM Forms意外指向了同一個結構描述，而它們並非故意指向。 當DBA不知情地將JEE資料庫的連線資訊提供單一AEM Forms給DEV和QA設定團隊時，通常會發生這種情況，這些團隊都沒有意識到DEV和QA執行個體需要個別的資料庫。

## 應用程式伺服器叢集 {#application-server-cluster-1}

若要在JEE叢集上成功使用AEM Forms，應用程式伺服器必須正確設定並當做叢集運作。 在WebSphere和Weblogic中，這是一個直接明瞭的流程。 在Jboss中，叢集設定需要更多實際操作，而確保節點設定為可作為叢集，並且確實能夠找到並彼此通訊可能會很困難。 JBoss在內部依賴於JGroups，後者使用UDP多點傳送來尋找及協調對等節點，而GemFire中提到的一些問題可能會發生，例如節點在應該找到彼此時失敗，或在不應該找到彼此時失敗。

引用:

* [透過JBoss叢集提供高可用性企業服務](https://docs.jboss.org/jbossas/jboss4guide/r4/html/cluster.chapt.html)

* [oracleWebLogic Server — 使用叢集](https://docs.oracle.com/cd/E12840_01/wls/docs103/pdf/cluster.pdf)

### 如何檢查JBoss是否正確建立叢集？ {#check-jboss-clustering}

當JBoss啟動時，在探索叢整合員時，有關加入叢集之節點的INFO層級訊息會記錄到記錄檔/主控台。

如果在執行時透過 — g命令列選項指定了叢集名稱，您將會看到類似下列的訊息：

```xml
GMS: address is 10.36.34.44:55200 (cluster=QE_cluster)
GMS: address is 10.36.34.44:55200 (cluster=QE_cluster-HAPartitionCache)
and ones like:

[org.jboss.ha.framework.interfaces.HAPartition.QE_cluster] (JBoss System Threads(1)-3) Number of cluster members: 1
2011-07-14 11:34:03,072 INFO  [org.jboss.ha.framework.interfaces.HAPartition.QE_cluster] (JBoss System Threads(1)-3) Other members: 0
2011-07-14 11:34:03,138 INFO  [org.jboss.cache.RPCManagerImpl] (main) Received new cluster view: [10.36.34.44:55200|0] [10.36.34.44:55200]
2011-07-14 11:34:03,139 INFO  [org.jboss.cache.RPCManagerImpl] (main) Cache local address is 10.36.34.44:55200
```

### Quartz排程器 {#quartz-scheduler}

在大多數情況下，JEE上的AEM Forms在叢集中使用內部Quartz排程器時，在一般情況下應該自動遵循JEE上AEM Forms的全域叢集設定。 但是，如果將TCP定位器用作Gemfire而不是多點傳送自動探索，則會導致Quartz的自動叢集設定失敗。#2794033 在此情況下，Quartz將會在非叢集模式下不正確地執行。 這會在Quartz表格中造成死鎖和資料損毀。 在8.2.x版中，由於Quartz並未大量使用，但依然存在，因此其副作用比9.0版更嚴重。

此問題的修正程式如下： 8.2.1.2 QF2.143和9.0.0.2 QF2.44。

另外也有因應措施，也就是設定這兩個屬性：

* `-Dadobe.cache.cluster.locators=xxx`

* `-Dadobe.cache.cluster-locators=xxx`

請注意，其中一個設定使用「叢集」和「位置」之間的句點，而另一個設定則使用連字型大小。 這比套用軟體修補程式容易實作，風險也較低，但需要人為建立其他令人困惑且名稱錯誤的組態設定。

### 如何檢查Quartz是否以單一節點或叢集方式執行？ {#check-quartz}

若要判斷Quartz本身的設定方式，您必須檢視AEM Forms on JEE Scheduler服務在啟動期間產生的訊息。 這些訊息會以INFO嚴重程度產生，可能需要調整記錄層級並重新啟動以取得訊息。 在AEM Forms on JEE啟動序列中，Quartz初始化會以下列行開始：

資訊  `[com.adobe.idp.scheduler.SchedulerServiceImpl]` IDPchedulerService onLoad在記錄中找出這第一行很重要，因為有些應用程式伺服器也使用Quartz，而且其Quartz執行個體不應與AEM Forms on JEE Scheduler服務所使用的執行個體混淆。 這表示「排程器」服務正在啟動，後續的文字行將告訴您它是否以叢集模式正確啟動。 此順序會顯示數個訊息，而這是最後一個「已啟動」訊息，可顯示Quartz的設定方式：

以下是Quartz執行個體的名稱： `IDPSchedulerService_$_ap-hp8.ottperflab.adobe.com1312883903975`. 排程器的Quartz執行個體名稱一律以字串開頭 `IDPSchedulerService_$_`. 附加至此結尾的字串會告訴您Quartz是否以叢集模式執行。 從節點的主機名稱及長數字字串產生的長唯一識別碼，如下所述 `ap-hp8.ottperflab.adobe.com1312883903975`，表示它在叢集中運作。 如果以單一節點運作，則識別碼會是兩位數：「20」：

資訊  `[org.quartz.core.QuartzScheduler]` 排程器 `IDPSchedulerService_$_20` 已啟動。
這項檢查必須個別在所有叢集節點上完成，因為每個節點的排程器會獨立決定是否以叢集模式操作。

### 如果Quartz以錯誤的模式執行，會產生哪些問題？ {#quartz-running-in-wrong-mode}

如果將Quartz設定為以單一節點執行，但實際上在叢集中執行，並與其他節點共用Quartz資料庫表格，則會導致JEE排程器服務上的AEM Forms無法可靠運作，且通常會伴有資料庫死結。 這是相當典型的棧疊追蹤，您可能會在此情況下看到：

```xml
[1/20/11 10:40:57:584 EST] 00000035 ErrorLogger   E org.quartz.core.ErrorLogger schedulerError An error occured while marking executed job complete. job= 'Asynchronous.TaskFormDataSaved:12955380518320.5650479324757354'
 org.quartz.JobPersistenceException: Couldn't remove trigger: ORA-00060: deadlock detected while waiting for resource  [See nested exception: java.sql.SQLException: ORA-00060: deadlock detected while waiting for resource ]
        at org.quartz.impl.jdbcjobstore.JobStoreSupport.removeTrigger(JobStoreSupport.java:1405)
        at org.quartz.impl.jdbcjobstore.JobStoreSupport.triggeredJobComplete(JobStoreSupport.java:2888)
        at org.quartz.impl.jdbcjobstore.JobStoreSupport$38.execute(JobStoreSupport.java:2872)
        at org.quartz.impl.jdbcjobstore.JobStoreSupport$40.execute(JobStoreSupport.java:3628)
        at org.quartz.impl.jdbcjobstore.JobStoreSupport.executeInNonManagedTXLock(JobStoreSupport.java:3662)
        at org.quartz.impl.jdbcjobstore.JobStoreSupport.executeInNonManagedTXLock(JobStoreSupport.java:3624)
        at org.quartz.impl.jdbcjobstore.JobStoreSupport.triggeredJobComplete(JobStoreSupport.java:2868)
        at org.quartz.core.QuartzScheduler.notifyJobStoreJobComplete(QuartzScheduler.java:1698)
        at org.quartz.core.JobRunShell.run(JobRunShell.java:273)
        at org.quartz.simpl.SimpleThreadPool$WorkerThread.run(SimpleThreadPool.java:529)
Caused by: java.sql.SQLException: ORA-00060: deadlock detected while waiting for resource
```

### 如何在叢集中同步系統時鐘？ {#ynchronize-system-clocks-cluster}

若要讓叢集順利運作，所有叢集節點上的時鐘必須密切同步。 這無法靠手動完成，且必須由定期執行的某種形式的時間同步服務完成。 所有節點的時鐘必須彼此位於一秒內。 最佳實務不僅要求同步叢集節點，還要求負載平衡器、資料庫伺服器、GDS NAS伺服器以及任何其他元件。

Windows時間同步處理趨向於網域控制站。 UNIX系統可以使用NTP同步到不同的時間來源。 如果可能的話，最好將所有系統(包括JEE節點上的AEM Forms和其他系統元件)同步至相同的來源。

即使是在最暫時的測試環境中，手動設定節點的時鐘絕對不夠。 手動設定時鐘無法提供足夠的精確同步化，而且兩個節點上的時鐘不可避免地會彼此相對漂移，即使是在短短一天的時間內。 使用中的時間同步機制對於可靠的叢集作業至關重要。

### 負載平衡器 {#load-balancer}

提供使用者互動式服務之叢集的典型需求是HTTP負載平衡器，該負載平衡器會將HTTP請求分散至整個叢集。 若要在JEE叢集上成功搭配AEM Forms使用負載平衡器，需要設定下列專案：

* 工作階段粘著度

* URL重寫規則

* 節點健康情況檢查

### 負載平衡器健康情況檢查功能該怎麼辦？ {#load-balancer-health-check}

有些負載平衡器可設定為定期檢查負載平衡節點的健康狀況。 通常，這是負載平衡器將嘗試存取之應用程式函式的URL。 如果載入成功，則會假設節點狀況良好，並保留在負載平衡集中。 如果URL無法載入，則會假設該節點有問題並從集合中排除。 健康情況檢查URL通常只會連線至JEE AdminUI登入頁面上的AEM Forms 。 這不是叢整合員的理想狀況檢查，而且最好實作短期程式，並使用REST API URL作為狀況檢查函式。

## 暫存檔案路徑和類似的叢集設定 {#temporary-file-path-cluster-settings}

JEE版AEM Forms中的某些檔案路徑設定會在整個叢集內建立，且在每個節點上具有相同的有效設定，但在每個節點上會分別解譯，以參照本機檔案。 要考慮的關鍵問題是字型路徑設定和暫存目錄設定。 前往AdminUI核心設定畫面（首頁>設定>核心系統>核心設定）

應檢查下列設定：

1. 暫存目錄的位置
1. Adobe伺服器字型目錄的位置
1. Customer Fonts目錄的位置
1. System Fonts目錄的位置
1. 資料服務組態檔的位置

叢集對於這些組態設定中的每一項都只有單一路徑設定。 例如，您的臨時目錄位置可能是 `/home/project/QA2/LC_TEMP`. 在叢集中，每個節點都必須可實際存取此特定路徑。 如果一個節點具有預期的暫存檔案路徑，而另一個節點沒有，則無法正常運作的節點。

雖然這些檔案和路徑可以在節點之間共用，或分開放置，或是在遠端檔案系統上，但通常最佳實務是它們是本機節點磁碟儲存裝置上的本機復本。

尤其是不應在節點之間共用暫存目錄路徑。 驗證GDS的程式應該用於驗證暫存目錄未共用：前往每個節點，在路徑設定所指示的路徑中建立暫存檔案，然後驗證其他節點未共用該檔案。 若有可能，暫存目錄路徑應該參照每個節點上的本機磁碟儲存空間，並應加以檢查。

對於每個路徑設定，請確定路徑確實存在，並且可使用執行JEE版AEM Forms的有效使用身分識別，從叢集中的每個節點進行存取。 字型目錄內容必須是可讀的。 暫存目錄必須允許讀取、寫入和控制。
