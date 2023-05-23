---
title: 技術需求
description: Adobe Experience Manager支援的使用者端和伺服器平台清單。
topic-tags: platform
exl-id: 47529b9a-c4e5-434f-ac26-b01714ff863b
source-git-commit: fe9c77644daf3669df8cca18e65fb0f6918f853b
workflow-type: tm+mt
source-wordcount: '3513'
ht-degree: 1%

---

# 技術需求{#technical-requirements}

Adobe在平台上支援(AEM) Adobe Experience Manager，詳情請參閱本檔案的下列資訊。

若有任何與平台相關的問題，請聯絡平台廠商。

>[!NOTE]
>
>根據您安裝AEM的平台，使用者管理可能會有不同的需求集。

## 前提条件 {#prerequisites}

安裝Adobe Experience Manager的最低需求：

* 已安裝的Java™ Platform、Standard Edition JDK或其他支援的 [Java™虛擬機器器](#java-virtual-machines)
* Experience Manager快速入門檔案（獨立JAR或Web應用程式部署WAR）

### 大小需求下限 {#minimum-sizing-requirements}

執行Adobe Experience Manager的最低需求：

* 安裝目錄中有5 GB可用磁碟空間
* 2 GB記憶體

>[!NOTE]
>
>* 數位資產使用案例需要更多基本記憶體。 另請參閱 [部署和維護](/help/sites-deploying/deploy.md#default-local-install) 以取得詳細資訊。
>* [AEM Forms附加元件套件](/help/forms/using/installing-configuring-aem-forms-osgi.md) 需要15 GB的暫存空間。
>


如需進一步資訊，請參閱 [硬體大小調整准則](/help/managing/hardware-sizing-guidelines.md).

### 支援等級 {#support-levels}

本檔案列出Adobe Experience Manager支援的使用者端和伺服器平台。 Adobe提供幾個層級的支援，針對建議的設定和其他設定皆提供。

### 支援的設定 {#supported-configurations}

Adobe會推薦這些設定，並在標準軟體維護合約中提供完整支援。

<table>
 <tbody>
  <tr>
   <td>支持级别</td>
   <td>描述<br /> </td>
  </tr>
  <tr>
   <td><strong>答：支援</strong></td>
   <td>Adobe提供此設定的完整支援與維護。 此設定包含在Adobe品質保證程式中。</td>
  </tr>
  <tr>
   <td><strong>R：限制支援</strong></td>
   <td>為確保客戶專案成功，Adobe在受限制的支援方案中提供完整支援，這要求符合特定條件。 R級支援需要正式的客戶請求和Adobe的確認。 如需詳細資訊，請聯絡Adobe客戶服務。</td>
  </tr>
 </tbody>
</table>

### 不支援的設定 {#unsupported-configurations}

| 支持级别 | 描述 |
|---|---|
| **Z：不支援** | 不支援此設定。 Adobe不會陳述設定是否有效，也不支援此設定。 |

## 支援的平台 {#supported-platforms}

### Java™虛擬機器器 {#java-virtual-machines}

應用程式需要由Java™開發套件(JDK)散發提供的Java™虛擬機器器才能執行。

Adobe Experience Manager可搭配下列版本的Java™虛擬機器器運作：

>[!CAUTION]
>
>追蹤Java™廠商的安全性公告。 這麼做可確保生產環境的安全與保障。 此外，請務必安裝最新的Java™更新。

| **Platform** | **支持级别** | **链接** |
|---|---|---|
| oracleJava™ SE 17 JDK | Z：不支援 `[1]` |
| oracleJava™ SE 11 JDK - 64位元 | 答：支援 `[1]` | [下载](https://experience.adobe.com/#/downloads/content/software-distribution/en/general.html?fulltext=Oracle*+JDK*+11*&amp;orderby=%40jcr%3Acontent%2Fjcr%3AlastModified&amp;orderby.sort=desc&amp;layout=list&amp;p.offset=0&amp;p.limit=24&lt;td>) |
| oracleJava™ SE 10 JDK | Z：不支援 `[1]` |
| oracleJava™ SE 9 JDK | Z：不支援 `[1]` |
| oracleJava™ SE 8 JDK - 64位元 | 答：支援 `[1]` | [下载](https://experience.adobe.com/#/downloads/content/software-distribution/en/general.html?fulltext=Oracle*+JDK*+8*&amp;orderby=%40jcr%3Acontent%2Fjcr%3AlastModified&amp;orderby.sort=desc&amp;layout=list&amp;p.offset=0&amp;p.limit=10) |
| IBM® J9 VM — 版本編號2.9、JRE 1.8.0 | 答：支援 `[2]` |
| IBM® J9 VM — 版本編號2.8、JRE 1.8.0 | 答：支援 `[2]` |
| Azul Zulu OpenJDK 11 - 64位元 | 答：支援 `[3]` |  |
| Azul Zulu OpenJDK 8 - 64位元 | 答：支援 `[3]` |  |

1. oracle已移至OracleJava™ SE產品的「長期支援」(LTS)模型。 Java™ 9、Java™ 10和Java™ 12是依Oracle區分的非LTS版本(請參閱 [oracleJava™ SE支援藍圖](https://www.oracle.com/technetwork/java/eol-135779.html))。 若要在生產環境中部署AEM，Adobe僅支援Java™的LTS版本。 所有使用OracleJava™ SE技術的AEM客戶，可直接透過Adobe支援及發佈OracleJava™ SE JDK，包括公開更新結束之後的LTS版本的所有維護更新。 請參閱 [Adobe Experience Manager的Java™支援政策](assets/Java_Policy_for_Adobe_Experience_Manager.pdf).
   **重要：至少支援OracleJava™ 11到2026年9月。 對OracleJava™ 17的支援正在準備中。**

1. 僅支援IBM® JRE與WebSphere® Application Server。

1. 從6.5版SP9開始的內部部署AEM支援Azul Zulu OpenJDK LTS版本。 Azul Zulu JDK LTS版本的支援和發佈必須由Adobe客戶直接從Azul授權。


### 儲存與持續性 {#storage-persistence}

有多種選項可用來部署Adobe Experience Manager存放庫。 請參閱下列清單，瞭解支援的技術和儲存選項。

| **Platform** | **描述** | **支持级别** |
|---|---|---|
| **具有TAR檔案的檔案系統** `[1]` | 存储库 | 答：支援 |
| **具有資料存放區的檔案系統** `[1]` | 二進位檔案 | 答：支援 |
| 將二進位檔案儲存在檔案系統的TAR檔案中 `[1]` | 二進位檔案 | Z：不支援生產 |
| Amazon S3 | 二進位檔案 | 答：支援 |
| Microsoft® Azure Blob儲存體 | 二進位檔案 | 答：支援 |
| MongoDB Enterprise 4.4 | 存储库 | 答：支援 `[2, 3, 4]` |
| MongoDB Enterprise 4.2 | 存储库 | 答：支援 `[2, 3, 4]` |
| MongoDB Enterprise 4.0 | 存储库 | Z：不支援 |
| MongoDB Enterprise 3.6 | 存储库 | Z：不支援 |
| MongoDB Enterprise 3.4 | 存储库 | Z：不支援 |
| IBM® DB2® 10.5 | 存放庫和Forms資料庫 | R：限制支援 `[5]` |
| oracle資料庫12c (12.1.x) | 存放庫和Forms資料庫 | R：限制支援 |
| Microsoft® SQL Server 2016 | Forms資料庫 | 答：支援 |
| **Apache Lucene （快速入門內建）** | 搜尋服務 | 答：支援 |
| Apache Solr | 搜尋服務 | 答：支援 |

1. 「檔案系統」包括符合POSIX的區塊儲存。 包括網路儲存技術。 請記住，檔案系統效能可能會有所不同，並影響整體效能。 使用網路/遠端檔案系統進行負載測試AEM。
1. MongoDB Enterprise 4.2和4.4版至少需要AEM 6.5 SP9。
1. AEM不支援MongoDB分片。
1. 僅支援MongoDB儲存引擎WiredTiger。
1. 支援AEM Forms升級客戶。 新安裝不支援。

>[!NOTE]
另請參閱 [部署社群](/help/communities/deploy-communities.md) 以取得有關AEM Communities功能的其他資訊。

>[!NOTE]
MongoDB是協力廠商軟體，未包含在AEM授權套件中。 如需詳細資訊，請參閱 [MongoDB授權原則](https://www.mongodb.com/community/licensing) 頁面。
若要透過MongoDB充分利用AEM部署，Adobe建議授權MongoDB企業版，以獲得專業支援。 另請參閱 [建議的部署](/help/sites-deploying/recommended-deploys.md#prerequisites-and-recommendations-when-deploying-aem-with-mongomk) 以取得詳細資訊。
授權包含標準復本集，該復本集由一個主要和兩個次要執行個體組成，可用於作者或發佈部署。
如果您想要在MongoDB上同時執行author和publish，則必須購買兩個不同的授權。
Adobe客戶服務可協助解決與AEM搭配使用MongoDB相關的資格確認問題。
如需詳細資訊，請參閱 [適用於Adobe Experience Manager的MongoDB頁面](https://www.mongodb.com/lp/contact/mongodb-adobe-experience-manager).

>[!NOTE]
以上所列的支援關聯式資料庫是協力廠商軟體，未包含在AEM授權套件中。
若要使用支援的關聯式資料庫執行AEM 6.5，需要與資料庫廠商訂立個別的支援合約。 Adobe客戶服務可協助解決與AEM 6.5使用關聯式資料庫相關的合格問題。
**目前AEM 6.5的Level-R支援大多數關聯式資料庫，其中包含支援條件和支援方案，如上述Level-R說明中所述。**

### Servlet引擎/應用程式伺服器 {#servlet-engines-application-servers}

Adobe Experience Manager可作為獨立伺服器（快速入門JAR檔案）執行，或作為協力廠商應用程式伺服器（WAR檔案）中的Web應用程式執行。

需要的最低Servlet API版本是Servlet 3.1

| Platform | 支持级别 |
|---|---|
| **快速入門內建Servlet引擎(Jetty 9.4)** | 答：支援 |
| oracleWebLogic Server 12.2 (12cR2) | Z：不支援 |
| IBM® WebSphere® Application Server Continuous Delivery (LibertyProfile)搭配Web Profile 7.0和IBM® JRE 1.8 | R：限制新合約的支援 `[2]` |
| IBM® WebSphere® Application Server 9.0和IBM® JRE 1.8 | R：限制新合約的支援 `[1]` `[2]` |
| Apache Tomcat 8.5.x | R：限制新合約的支援 `[2]` |
| JBoss® EAP 7.2.x搭配JBoss® Application Server | Z：不支援 |
| JBoss® EAP 7.1.4搭配JBoss® Application Server | R：限制新合約的支援 `[1]` `[2]` |
| JBoss® EAP 7.0.x (含JBoss® Application Server) | Z：不支援 |

1. 建議使用AEM Forms進行部署。
1. 在應用程式伺服器上啟動AEM 6.5部署後，會移至「限制支援」。 現有客戶可升級至AEM 6.5，並繼續使用應用程式伺服器。 對於新客戶，如上方Level-R說明中所述，它隨附支援條件和支援計畫。

### 伺服器作業系統 {#server-operating-systems}

Adobe Experience Manager可搭配下列伺服器平台用於生產環境：

| **Platform** | **支持级别** |
|---|---|
| **Linux®，以Red Hat®版本為基礎** | 答：支援 `[1]` `[3]` |
| Linux®，根據Debian分佈，包括 Ubuntu | 答：支援 `[1]` `[2]` |
| Linux®，根據SUSE®分佈 | 答：支援 `[1]` |
| Microsoft® Windows Server 2019 `[4]` | R：限制新合約的支援 `[5]` |
| Microsoft® Windows Server 2016 `[4]` | R：限制新合約的支援 `[5]` |
| Microsoft® Windows Server 2012 R2 | Z：不支援 |
| oracleSolaris™ 11 | Z：不支援 |
| IBM® AIX® 7.2 | Z：不支援 |

1. Linux® Kernel 2.6、3。 x， 4. x和5. x包含來自Red Hat®發佈的衍生版本，包括Red Hat® Enterprise Linux®、CentOS、Oracle Linux®和Amazon Linux®。 只有CentOS 7、Red Hat® Enterprise Linux® 7、Red Hat® Enterprise Linux® 8和Red Hat® Enterprise Linux® 9支援AEM Forms附加元件功能。
1. Ubuntu 20.04 LTS支援AEM Forms。
1. Adobe Managed Services支援的Linux®發佈。
1. 升級至6.5的客戶以及非生產使用的客戶支援Microsoft® Windows生產部署。 AEM Sites和Assets的新部署會根據請求進行。
1. Microsoft® Window Server支援AEM Forms，且沒有支援層級R限制。

>[!NOTE]
如果您要安裝AEM Forms 6.5，請確定您已安裝下列32位元Microsoft® Visual C++可轉散發套件。
* Microsoft® Visual C++ 2008可轉散發套件
* Microsoft® Visual C++ 2010可轉散發套件
* Microsoft® Visual C++ 2012可轉散發套件
* Microsoft® Visual C++ 2013可轉散發套件（截至6.5版）



### 虛擬與雲端運算環境 {#virtual-cloud-computing-environments}

支援在雲端運算環境的虛擬機器器中執行Adobe Experience Manager。 這些環境包括Microsoft®Azure和Amazon Web Services (AWS)，依照本頁所列的技術要求以及Adobe的標準支援條款執行。

對於雲端原生環境，請檢閱AEM產品線的最新產品：Adobe Experience Manager as a Cloud Service。 另請參閱 [Adobe Experience Manager as a Cloud Service檔案](https://experienceleague.adobe.com/docs/experience-manager-cloud-service.html?lang=en) 以取得詳細資訊。

Adobe也提供Adobe Managed Services功能，以便在Azure或AWS上部署AEM。 Adobe Managed Services為專家提供在這些雲端運算環境中部署和操作AEM的經驗和技能。 另請參閱 [有關Adobe Managed Services的其他檔案](https://business.adobe.com/products/experience-manager/managed-services.html?aemClk=t).

在其他所有在Azure或AWS或任何雲端運算環境上部署AEM的情況下，虛擬運算環境都包含Adobe的支援。 該虛擬環境必須依照本頁所列的技術規格執行。 任何報告的問題與AEM在任何雲端環境中執行相關，必須可獨立於雲端運算環境特定的任何雲端服務重複產生。 也就是說，除非本頁所列的技術需求支援雲端服務，例如Azure Blob儲存空間或AWS S3。

如需如何在Adobe Managed Services以外的Azure或AWS上部署AEM的建議，Adobe建議直接與雲端提供者合作。 或者，與Adobe合作夥伴合作，支援在您選擇的雲端環境中部署AEM。 選取的雲端服務供應商或合作夥伴負責架構的規模規格、設計和實作，以符合您的特定效能、負載、擴充性和安全性需求。

### Dispatcher平台（網頁伺服器） {#dispatcher-platforms-web-servers}

Dispatcher是快取和負載平衡元件。 [下載最新的Dispatcher版本](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/getting-started/release-notes.html?lang=en). Experience Manager6.5需要Dispatcher版本4.3.2或更新版本。

下列Web伺服器支援與Dispatcher版本4.3.2搭配使用：

| Platform | 支持级别 |
|---|---|
| **Apache httpd 2.4.x** `[1,2]` | 答：支援 |
| Microsoft® IIS 10 (Internet Information Server) | 答：支援 |
| Microsoft® IIS 8.5 (Internet Information Server) | Z：不支援 |

1. 以Apache httpd原始程式碼為基礎建立的Web伺服器，與其所根據的httpd版本具有同樣多的支援。 如有疑問，請要求Adobe確認與個別伺服器產品相關的支援等級。 下列情況：

   1. HTTP伺服器僅使用官方的Apache來源發佈建置，或
   1. HTTP伺服器是作為執行伺服器之作業系統的一部分提供。 範例： IBM® HTTP伺服器、OracleHTTP伺服器

1. Dispatcher不適用於適用於Windows作業系統的Apache 2.4.x。

## 支援的使用者端平台 {#supported-client-platforms}

### 編寫使用者介面的支援瀏覽器 {#supported-browsers-for-authoring-user-interface}

Adobe Experience Manager使用者介面可與下列使用者端平台搭配使用。 所有瀏覽器都會以一組預設的外掛程式和附加元件進行測試。

AEM使用者介面已針對大型熒幕（通常是筆記型電腦和桌上型電腦）和平板電腦外形規格(例如Apple iPad或Microsoft® Surface)進行最佳化。 不支援電話外形規格。

>[!NOTE]
**支援具有快速發行週期的瀏覽器：**
Mozilla Firefox、Google Chrome和Microsoft® Edge每隔幾個月會發佈一次更新。 Adobe致力於提供Adobe Experience Manager的更新，以透過這些瀏覽器的未來版本維持以下所述的支援等級。

<table>
 <tbody>
  <tr>
   <td><strong>浏览器</strong></td>
   <td><strong>支援UI<br /> </strong></td>
   <td><strong>支援傳統UI</strong></td>
  </tr>
  <tr>
   <td><strong>Google Chrome （常青）</strong></td>
   <td>答：支援</td>
   <td>答：支援</td>
  </tr>
  <tr>
   <td>Microsoft® Edge （長青）</td>
   <td>答：支援</td>
   <td>答：支援</td>
  </tr>
  <tr>
   <td>Microsoft® Internet Explorer 11</td>
   <td>Z：不支援</td>
   <td>Z：不支援</td>
  </tr>
  <tr>
   <td>Mozilla Firefox （常青）</td>
   <td>答：支援</td>
   <td>答：支援</td>
  </tr>
  <tr>
   <td>Mozilla Firefox上一個ESR [1]</td>
   <td>答：支援</td>
   <td>答：支援</td>
  </tr>
  <tr>
   <td>macOS上的Apple Safari （常青）</td>
   <td>答：支援</td>
   <td>答：支援</td>
  </tr>
  <tr>
   <td>macOS上的Apple Safari 11.x</td>
   <td>Z：不支援</td>
   <td>Z：不支援</td>
  </tr>
  <tr>
   <td>iOS 12.x上的Apple Safari</td>
   <td>答：支援[2]</td>
   <td>Z：不支援</td>
  </tr>
  <tr>
   <td>iOS 11.x上的Apple Safari</td>
   <td>Z：不支援</td>
   <td>Z：不支援</td>
  </tr>
 </tbody>
</table>

1. Firefox的延伸支援版本 [進一步瞭解mozilla.org](https://www.mozilla.org/en-US/firefox/enterprise/)
1. 支援Apple iPad

### 支援的網站瀏覽器 {#supported-browsers-for-websites}

一般而言，AEM Sites所轉譯網站的瀏覽器支援取決於AEM頁面範本、設計和元件輸出的實作，因此能控制實作這些部分的當事方。

### WebDAV使用者端 {#webdav-clients}

**Microsoft® Windows 7+**

當使用Microsoft® Windows 7+連線到未使用SSL加密的AEM執行個體時，必須在Windows中啟用透過不安全網路的基本驗證。 它需要在WebClient的Windows登入中進行變更：

1. 找到登入子機碼：

   * HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\WebClient\Parameters

1. 使用2或以上的值將BasicAuthLevel登入專案新增至此子機碼。

## 其他平台注意事項 {#additional-platform-notes}

本節提供執行Adobe Experience Manager及其附加元件之相關特殊附註和更多詳細資訊。

### IPv4和IPv6 {#ipv-and-ipv}

Adobe Experience Manager的所有元素（例項、Dispatcher）都可以安裝在IPv4和IPv6網路中。

操作是順暢的，因為不需要特殊設定。 如有必要，您可以使用適合您網路型別的格式來指定IP位址。

當必須指定IP位址時，您可以（視需要）從下列專案選取：

* ipv6位址。 例如，`https://[ab12::34c5:6d7:8e90:1234]:4502`

* ipv4位址。 例如，`https://123.1.1.4:4502`

* 伺服器名稱。 例如，`https://www.yourserver.com:4502`

* 預設大小寫為 `localhost` 會解譯為IPv4和IPv6網路安裝。 例如，`https://localhost:4502`

### AEM Dynamic Media附加元件的需求 {#requirements-for-aem-dynamic-media-add-on}

AEM Dynamic Media預設為停用。 請參閱此處 [啟用Dynamic Media](/help/assets/config-dynamic.md#enabling-dynamic-media).

啟用Dynamic Media後，將適用下列其他技術要求。

>[!NOTE]
這些系統需求 **僅限** 若您使用Dynamic Media — 混合模式，則套用；Dynamic Media — 混合模式具有內嵌影像伺服器，此伺服器僅在某些作業系統上通過認證。
適用於執行Dynamic Media - Scene7模式的Dynamic Media客戶(也就是說， **dynamicmedia_scene7** 執行模式)，沒有額外的系統需求；只有與AEM相同的系統需求。 Dynamic Media - Scene7模式架構使用雲端型影像服務，而非內嵌於AEM中的服務。

#### 硬體 {#hardware}

下列硬體需求適用於Linux®和Windows：

* Intel Xeon®或AMD® Opteron CPU，至少配備四個核心
* 至少16 GB的RAM

#### Linux® {#linux}

如果您在Linux®上使用Dynamic Media，必須符合下列先決條件：

* Red Hat® Enterprise 7或CentOS 7及更新版本，提供最新的修正修補程式
* 64位元作業系統
* 交換功能已停用（建議）
* SELinux已停用（請參閱以下說明）

>[!NOTE]
如果locale設定為LC_CTYPE不等於 `en_US.UTF-8`，會導致Dynamic Media無法運作。 若要檢視其值，請在命令提示字元處輸入「locale」。 若未正確設定，請在執行AEM前輸入「export LC_CTYPE=」，將LC_CTYPE環境變數設定為空字串。

>[!NOTE]
**停用SELinux：** 開啟SELinux時，「影像伺服」無法運作。 此選項預設為啟用。 若要修正此問題，請編輯 **/etc/selinux/config** 檔案並將SELinux值從下列位置變更：
`SELINUX=enforcing` **至** `SELINUX=disabled`

>[!NOTE]
**NUMA架構：** 搭載AMD64和Intel® EM64T處理器的系統通常設定為非統一記憶體架構(NUMA)平台。 也就是說，核心會在開機時建構多個記憶體節點，而不是建構單一記憶體節點。
多節點結構可能會導致一或多個節點的記憶體耗盡，之後其他節點就會耗盡。 當記憶體用盡時，即使有可用的記憶體，核心仍可以決定終止處理序（例如，影像伺服器或平台伺服器）。
因此，Adobe建議，如果您要執行這樣的系統，您應該使用 **numa=off** 開機選項，以避免核心停止這些程式。

>[!NOTE]
**伺服器主機名稱必須解析：** 確定伺服器的主機名稱可解析為IP位址。 如果無法執行此操作，請將完整主機名稱和IP位址新增至 **/etc/hosts**：
`<ip address> <fully qualified hostname>`

#### Windows {#windows}

* Microsoft® Windows Server 2016
* 交換空間至少相當於實體記憶體(RAM)容量的兩倍

若要在Windows上使用Dynamic Media，請安裝Microsoft®適用於x64和x86的Visual Studio 2010、2013和2015可轉散發套件。

若是Windows x64：

* 取得Microsoft® Visual Studio 2010可轉散發套件，網址為 [https://www.microsoft.com/en-us/download/details.aspx?id=26999](https://www.microsoft.com/en-us/download/details.aspx?id=26999)
* 取得Microsoft® Visual Studio 2013可轉散發套件，網址為 [https://www.microsoft.com/en-us/download/details.aspx?id=40784](https://www.microsoft.com/en-us/download/details.aspx?id=40784)
* 取得Microsoft® Visual Studio 2015可轉散發套件，網址為 [https://www.microsoft.com/en-us/download/details.aspx?id=48145](https://www.microsoft.com/en-us/download/details.aspx?id=48145)

若是Windows x86：

* 取得Microsoft® Visual Studio 2010可轉散發套件，網址為 [https://www.microsoft.com/en-us/download/details.aspx?id=26999](https://www.microsoft.com/en-us/download/details.aspx?id=26999)
* 取得Microsoft® Visual Studio 2013可轉散發套件，網址為 [https://www.microsoft.com/en-in/download/details.aspx?id=40769](https://www.microsoft.com/en-in/download/details.aspx?id=40769)
* 取得Microsoft® Visual Studio 2015可轉散發套件，網址為 [https://www.microsoft.com/en-us/download/details.aspx?id=52685](https://www.microsoft.com/en-us/download/details.aspx?id=52685)

#### macOS {#macos}

* 10.9.x和更新版本
* 僅支援試用和示範用途

### AEM FormsPDF產生器的需求 {#requirements-for-aem-forms-pdf-generator}

### PDF產生器的軟體支援 {#software-support-for-pdf-generator}

<table>
 <tbody>
  <tr>
   <th><p><strong>产品</strong></p> </th>
   <th><p><strong>支援的PDF轉換格式</strong></p> </th>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/acrobat/release-note/release-notes-acrobat-reader.html">Acrobat 2020 classic路線</a> 最新版本</td>
   <td>XPS、影像格式(BMP、GIF、JPEG、JPG、TIF、TIFF、PNG、JPF、JPX、JP2、J2K、J2C、JPC)、HTML、HTM、DWG、DXF和DWF</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/acrobat/release-note/release-notes-acrobat-reader.html">Acrobat 2017 classic路線</a> 最新版本（已棄用）</td>
   <td>XPS、影像格式(BMP、GIF、JPEG、JPG、TIF、TIFF、PNG、JPF、JPX、JP2、J2K、J2C、JPC)、HTML、HTM、DWG、DXF和DWF</td>
  </tr>
  <tr>
   <td>Microsoft® Office 2019</td>
   <td>DOC、DOCX、XLS、XLSX、PPT、PPTX、RTF和TXT</td>
  </tr>
  <tr>
   <td>Microsoft® Office 2016 （已棄用）</td>
   <td>DOC、DOCX、XLS、XLSX、PPT、PPTX、RTF和TXT</td>
  </tr>
  <tr>
   <td>WordPerfect 2020<br /> </td>
   <td>WP、WPD</td>
  </tr>
  <tr>
   <td>Microsoft® Office Visio 2016 （已棄用）<br /> </td>
   <td>VSD、VSDX</td>
  </tr>
  <tr>
   <td>Microsoft®發佈商2019<br /> </td>
   <td>公共</td>
  </tr>
  <tr>
   <td>Microsoft® Publisher 2016 （已棄用）<br /> </td>
   <td>公共</td>
  </tr>
  <tr>
   <td>Microsoft®專案2016 （已棄用）<br /> </td>
   <td>MPP</td>
  </tr>
  <tr>
   <td>OpenOffice 4.1.10</td>
   <td>ODT、ODP、ODS、ODG、ODF、SXW、SXI、SXC、SXD、XLS、XLSX、DOC、DOCX、PPT、PPTX、影像格式(BMP、GIF、JPEG、JPG、TIF、TIFF、PNG、JPF、JPX、JP2、J2K、J2C、JPC)、HTML、HTM、RTF、和TXT</td>
  </tr>
  <tr>
   <td>OpenOffice 4.1.2 （已棄用）</td>
   <td>ODT、ODP、ODS、ODG、ODF、SXW、SXI、SXC、SXD、XLS、XLSX、DOC、DOCX、PPT、PPTX、影像格式(BMP、GIF、JPEG、JPG、TIF、TIFF、PNG、JPF、JPX、JP2、J2K、J2C、JPC)、HTML、HTM、RTF、和TXT</td>
  </tr>  
 </tbody>
</table>

>[!NOTE]
PDF產生器僅支援英文、法文、德文和日文版本的支援作業系統和應用程式。
此外，
* PDF產生器需要32位元版本的 [Acrobat 2020 classic路線20.004.30006版](https://helpx.adobe.com/acrobat/release-note/release-notes-acrobat-reader.html) 或Acrobat 2017 17.011.30078版來執行轉換。
* 僅在Windows和Linux®上支援OpenOffice的PDF產生器轉換。
* PDF產生器僅支援32位元零售版的Microsoft® Office Professional Plus，以及Windows作業系統上轉換所需的其他軟體。
* PDF產生器支援Linux®作業系統上的32位元和64位元版本的OpenOffice。
* PDF產生器不支援Microsoft® Office 365。
* 只有Windows支援OCRPDF、Optimize PDF和Export PDF功能。
* Acrobat版本與AEM Forms搭配，可啟用PDF產生器功能。 在AEM Forms授權期間，僅能透過AEM Forms以程式設計方式存取隨附版本，以便與AEM FormsPDF產生器搭配使用。 如需詳細資訊，請參閱根據您的部署說明的AEM Forms產品說明([內部部署](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-manager-on-premise.html) 或 [Managed Services](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-manager-managed-services.html))
* PDF產生器服務不支援Microsoft® Windows 10。
* PDF產生器無法使用Microsoft® Visio 2019轉換檔案。 您可以繼續使用Microsoft® Visio 2016來轉換 `.VSD` 和 `.VSDX` 檔案。
* PDF產生器無法使用Microsoft® Project 2019轉換檔案。 您可以繼續使用Microsoft® Project 2016進行轉換 `.VSD` 和 `.VSDX` 檔案。
>


### AEM Forms Designer的需求 {#requirements-for-aem-forms-designer}

* Microsoft® Windows® 2016 Server、Microsoft® Windows® 2019 Server或Microsoft® Windows® 10
* 1 GHz或更快的處理器，支援PAE、NX和SSE2。
* 32位元的1 GB RAM或64位元作業系統的2 GB RAM
* 16 GB磁碟空間，適用於32位元或20 GB磁碟空間，適用於64位元作業系統
* 顯示卡記憶體：128 MB的GPU （建議使用256 MB）
* 2.35 GB的可用硬碟空間
* 1024 X 768畫素或更高的熒幕解析度
* 視訊硬體加速（選購）
* Acrobat Pro DC、Acrobat Standard DC或Adobe Acrobat Reader DC。
* 安裝Designer的管理許可權。

### AEM Assets XMP中繼資料回寫的需求 {#requirements-for-aem-assets-xmp-metadata-write-back}

下列平台和檔案格式支援並啟用XMP回寫：

* **作業系統：**

   * Linux® （64位元系統上的32位元和32位元應用程式支援）。 如需安裝32位元使用者端程式庫的步驟，請參閱 [如何在64位元Red Hat® Linux®上啟用XMP擷取和回寫](https://helpx.adobe.com/experience-manager/kb/enable-xmp-write-back-64-bit-redhat.html).

   * Windows Server
   * macOS X （64位元）

* **檔案格式**：JPEG、PNG、TIFF、PDF、INDD、AI和EPS。

### AEM Assets在Linux上處理中繼資料密集的資產的需求® {#assetsonlinux}

XMPFilesProcessor程式需要程式庫GLIBC_2.14才能運作。 使用包含GLIBC_2.14的Linux®核心，例如Linux®核心3.1.x版。它可改善處理包含大量中繼資料的資產的效能，例如PSD檔案。 使用舊版GLIBC會導致以開頭的記錄中出現錯誤 `com.day.cq.dam.core.impl.handler.xmp.NCommXMPHandler Failed to read XMP`.
