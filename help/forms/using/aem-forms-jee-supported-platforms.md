---
title: AEM Forms on JEE的支援平台
seo-title: Supported Platforms for AEM Forms on JEE
description: 在JEE上安裝AEM Forms所需和支援的基礎結構元件清單
seo-description: List of infrastructure components required and supported for installing AEM Forms on JEE
uuid: 777f943b-4cb4-444e-a036-8032b9fce5be
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
geptopics: SG_AEMFORMS/categories/jee
discoiquuid: f777865e-d4a8-40ef-87b0-130c19eb1b91
docset: aem65
role: Admin
exl-id: 74d22cf4-56b2-48f5-92d9-928eaa134866
source-git-commit: 26e71c5f09eb9fa3f3eda01deb871ac63e348a30
workflow-type: tm+mt
source-wordcount: '3699'
ht-degree: 1%

---


# AEM Forms on JEE的支援平台 {#supported-platforms-for-aem-forms-on-jee}

## 支援的平台 {#supported-platforms}

<div class="preview">

Adobe已發行 [完整安裝程式](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html) JEE版AEM 6.5 Forms Service Pack 12 (6.5.12.0)及修補程式安裝程式。 完整版安裝程式支援新平台，而修補程式安裝程式僅包含錯誤修正。

如果您要在JEE環境中執行全新安裝或計畫使用最新軟體AEM 6.5 Forms，Adobe建議使用 [AEM 6.5.12.0 Forms on JEE完整安裝程式](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html) 2022年3月3日發行，而非2019年4月8日發行的AEM 6.5 Forms安裝程式。

</div>

### 支援層級 {#support-levels}

JEE伺服器上的AEM Forms可使用任何支援的作業系統、應用程式伺服器、資料庫、資料庫驅動程式、JDK、LDAP伺服器和電子郵件伺服器的組合進行設定。

本檔案列出AEM Forms on JEE支援的使用者端和伺服器平台。 Adobe針對我們建議的設定和其他設定，提供多個層級的支援。 本檔案也會列出其他支援的軟體及其版本、例外、修補程式定義，以及協力廠商軟體修補程式支援原則。

>[!NOTE]
>
>- 如需受支援伺服器平台的例外狀況完整清單，請參閱 [支援的伺服器平台例外](../../forms/using/aem-forms-jee-supported-platforms.md#p-exceptions-to-supported-server-platforms-p).
>- AEM Forms on JEE僅支援英文、法文、德文和日文版本的支援作業系統和應用程式。


### 建議的設定 {#recommendedconfigurations}

Adobe建議使用這些設定，並在標準軟體維護合約中提供完整或有限的支援：

<table>
 <tbody>
  <tr>
   <th>支持级别</th>
   <th>描述</th>
  </tr>
  <tr>
   <td>答：支援<br /> </td>
   <td>Adobe提供此設定的完整支援與維護。 此設定包含在Adobe品質保證程式中。</td>
  </tr>
  <tr>
   <td>R：限制支援</td>
   <td>在滿足某些先決條件後，Adobe就會提供此設定的完整支援。 請聯絡Adobe企業支援，瞭解必要條件並提出支援請求。</td>
  </tr>
  <tr>
   <td>L：有限支援</td>
   <td>在滿足某些先決條件後，Adobe會提供此設定的完整支援與維護。 並非所有功能都可在設定上使用。 請聯絡Adobe企業支援，瞭解必要條件並提出支援請求。<br /> </td>
  </tr>
 </tbody>
</table>

### 不支援的設定 {#unsupported-configurations}

| 支持级别 | 描述 |
| ------------------- | -------------------------------------------------------------------------------------------------------------------------------------- |
| E：預期可運作 | 設定預期可運作，且沒有相反的報告。 |
| Z：不支援 | 不支援此設定。 Adobe不會就設定是否運作發表任何宣告，也不支援該設定。 |

>[!NOTE]
>
>為協助AEM Forms客戶降低擁有成本、簡化部署架構及匯入最新的開發棧疊，Adobe Experience Manager企業平台正從應用程式伺服器部署轉向獨立的OSGi部署。 Adobe持續支援AEM Forms JEE棧疊，並減少基礎架構元件的矩陣。
>
>在6.5版中，我們不再支援使用率最低的客戶之基礎結構元件，如下所示：
>
>- IBM DB2資料庫
>- IBM AIX和Sun Solaris作業系統
>
>若為新安裝，建議在可行的情況下，將AEM Forms部署在現代OSGi棧疊上，以善用關於回應式最適化Forms的最新創新，用於行動、多頻道互動式通訊和使用表單資料模型的後端資料整合。
>
>我們瞭解現有使用者需要繼續在JEE棧疊上部署AEM Forms。 在這種情況下，Adobe需要在支援的基礎架構上部署AEM Forms JEE，如本檔案所述。 如果您要升級至AEM 6.5 Forms並使用不支援的平台(在舊版AEM Forms上)，請聯絡Adobe支援以取得升級至支援平台的協助。

### Java虛擬機器器(JVM) {#java-virtual-machines-jvm}

Adobe Experience Manager Forms需要由Java Development Kit (JDK)散發提供的Java Virtual Machine才能執行。 Adobe Experience Manager可搭配下列版本的Java虛擬機器器運作：

<table>
 <tbody>
  <tr>
   <th><p><strong>Platform</strong></p> </th>
   <th><p><strong>支持级别</strong></p> </th>
   <th><p><strong>支援的修補程式定義</strong></p> </th>
  </tr>
  <tr> 
   <td><p>oracleJava™ SE 11 （64位元） <sup> [8] </sup> </p>  </td>
   <td><p>答：支援</p> </td>
   <td><p>次要版本和更新 </p> </td>
  </tr>
  <tr>
   <td>Azul Zulu OpenJDK 11 - 64位元</td>
   <td>Z：不支援</td>
   <td><p> </p> </td>
  </tr>
  <tr>
   <td>Azul Zulu OpenJDK 8 - 64位元</td>
   <td>Z：不支援</td>
   <td><p> </p> </td>
  </tr>
  <tr>
   <td>oracleJava™ SE 8 （64位元）</td>
   <td>答：支援</td>
   <td>次要版本和更新</td>
  </tr>
  <tr>
   <td>IBM® J9虛擬機器器（版本編號2.9、JRE 1.8.0） IBM®JDK SR6-FP26<br /> </td>
   <td>答：支援</td>
   <td>次要版本和更新</td>
  </tr>
  <tr>
   <td>IBM JAVA1.8.0_291（版本編號8.0.6.30）<br /> </td>
   <td>答：支援</td>
   <td>次要版本和更新</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>- 建議追蹤Java廠商的安全公告，以確保生產環境的安全與保障，並安裝最新的Java更新。
>- JEE上的AEM Forms在生產環境中僅支援64位元JVM。


### 資料庫和CRX持續性 {#databases-and-crx-persistence}

<table>
 <tbody>
  <tr>
   <td><p><strong>Platform</strong></p> </td>
   <td><p><strong> 描述</strong></p> </td>
   <td><p><strong>支持级别</strong></p> </td>
  </tr>
  <tr>
   <td><p>檔案系統</p> </td>
   <td><p>存放庫微核心（TAR MK檔案）</p> </td>
   <td><p>支持</p> </td>
  </tr>
  <tr>
   <td><p> MongoDB Enterprise 4.0 （已棄用） </p> </td>
   <td><p>存放庫微核心</p> </td>
   <td><p>支持</p> </td>
  </tr>
  <tr>
   <td><p>MongoDB Enterprise 4.2 </p> </td>
   <td><p>存放庫微核心</p> </td>
   <td><p>支持</p> </td>
  </tr>
  <tr>
   <td><p>oracle Database 12c版本2 (12.2.0.1.0) （已棄用）</p> </td>
   <td><p>存放庫微核心</p> </td>
   <td><p>支持</p> </td>
  </tr>
   <tr>
   <td>oracle資料庫19c (標準、Real Application Clusters (RAC)和Enterprise版本) </td>
   <td>存放庫微核心 </td>
   <td>支持</td>
  </tr>
  <tr>
   <td><p>Microsoft SQL Server 2016 （已棄用）</p> </td>
   <td><p>存放庫微核心</p> </td>
   <td><p>支持</p> </td>
  </tr>
  <tr>
   <td><p>Microsoft SQL Server 2019</p> </td>
   <td><p>存放庫微核心</p> </td>
   <td><p>支持</p> </td>
  </tr>
  <tr>
   <td>IBM DB2 11.1 （已棄用）</td>
   <td>存放庫微核心</td>
   <td>R：限制支援</td>
  </tr>
  <tr>
   <td>MySQL 5.7.35 （已棄用） </td>
   <td>-</td>
   <td>R：限制支援</td>
  </tr>
  <tr>
   <td>MySQL 8.0.27</td>
   <td>-</td>
   <td>R：限制支援</td>
  </tr>
 </tbody>
</table>

- 全新安裝不支援IBM DB2。 僅現有客戶升級至AEM 6.5 Forms時支援此功能。
- MongoDB是協力廠商軟體，未包含在AEM授權套件中。 如需詳細資訊，請參閱 [MongoDB授權原則](https://www.mongodb.org/about/licensing/) 頁面。
- 為了充分利用AEM部署，Adobe建議授權MongoDB Enterprise版本，以受益於專業支援。
- Adobe客戶服務將協助解決與AEM使用MongoDB相關的資格確認問題。 如需詳細資訊，請參閱 [適用於Adobe Experience Manager的MongoDB頁面](https://www.mongodb.com/lp/contact/mongodb-adobe-experience-manager).
- 「檔案系統」包含符合POSIX的區塊儲存。 這包括網路儲存技術。 請記住，檔案系統效能可能會有所不同，並影響整體效能。 建議將負載測試AEM與網路/遠端檔案系統結合。
- 僅支援MongoDB儲存引擎WiredTiger。
- AEM不支援MongoDB分片。
- JEE上的AEM Forms不支援MySQL for RDBMK持續性。
- Document Security模組不使用內容存放庫。 這表示，如果您只使用Document Security，並且不打算使用HTML工作區、HTML5表單或調適型表單，則不要安裝內容存放庫。
- JEE上的AEM Forms不支援使用MySQL來儲存AEM存放庫(CRX-Repository)。

### 資料庫驅動程式 {#database-drivers}

<table>
 <tbody>
  <tr>
   <th>数据库 </th>
   <th><p><strong>Platform</strong></p> </th>
   <th><p><strong>支援的修補程式定義</strong></p> </th>
  </tr>
  <tr>
   <td>MySQL</td>
   <td><p>MySQL Connector/J 5.7</p> <p>mysql-connector-java-5.1.44-bin.jar （5.1.44版）</p> </td>
   <td><p>JEE安裝時隨AEM Forms提供</p> </td>
  </tr>
  <tr>
   <td>Microsoft SQL Server<br /> </td>
   <td><p>Microsoft® SQL Server JDBC驅動程式6.2.1.0 （已棄用） <br /> </p> <p>sqljdbc6.jar</p> </td>
   <td><p>隨附於AEM Forms的JEE安裝。</p> </td>
  </tr>
    <tr>
   <td>Microsoft SQL Server<br /> </td>
   <td><p>Microsoft® SQL Server JDBC驅動程式6.2.2.0 <br /> </p> <p>sqljdbc6.jar</p> </td>
   <td><p>隨附於AEM Forms的JEE安裝。</p> </td>
  </tr>
  <tr>
   <td>Microsoft SQL Server<br /> </td>
   <td><p>Microsoft® SQL Server JDBC驅動程式8.2.2<br /> </p> <p>sqljdbc8.jar</p> </td>
   <td><p>從Microsoft網站下載。</p> </td>
  </tr>
  <tr>
   <td>oracle</td>
   <td><p>oracle資料庫19.3.0.0.0 JDBC驅動程式</p> <p>ojdbc8.jar （19.3.0.0.0版）<br /> </p> </td>
   <td><p>下載來源 <a href="https://www.oracle.com/database/technologies/appdev/jdbc-ucp-19c-downloads.html">oracle網站</a>.</p> </td>
  </tr>
 </tbody>
</table>

### 應用程式伺服器 {#application-servers}

<table>
 <tbody>
  <tr>
   <td><p><strong> Platform</strong></p> </td>
   <td><p><strong>支持级别</strong></p> </td>
   <td><p><strong>支援的修補程式定義</strong></p> </td>
  </tr>
  <tr>
   <td>oracleWebLogic Server 12.2.1 (12c R2)</td>
   <td>答：支援</td>
   <td>Service Pack和重要更新</td>
  </tr>
  <tr>
   <td>IBM® WebSphere® Application Server 9.0.0.10 <sup>[1] [4]</sup><br /> </td>
   <td>答：支援</td>
   <td>Service Pack和重要更新</td>
  </tr>
  <tr>
   <td><p>JBoss® Enterprise Application Platform (EAP) 7.1.4 <sup>[2] [3] [7]</sup> （已棄用） </p> </td>
   <td><p>答：支援</p> </td>
   <td><p>支援的EAP版本的修補程式和累積修補程式</p> </td>
  </tr>
  <tr>
   <td><p>JBoss® Enterprise Application Platform (EAP) 7.4 <sup>[2] [3] [7]</sup> </p> </td>
   <td><p>答：支援</p> </td>
   <td><p>支援的EAP版本的修補程式和累積修補程式</p> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>僅網路部署版本支援IBM® WebSphere®叢集。

### 伺服器作業系統 {#server-operating-systems}

#### 生產環境 {#production-environments}

<table>
 <tbody>
  <tr>
   <th><p><strong> Platform</strong></p> </th>
   <th><p><strong>支援等級</strong></p> </th>
   <th><p><strong>支援的修補程式定義</strong></p> </th>
  </tr>
   <tr>
   <td>Microsoft Windows Server 2019 （64位元）</td>
   <td>答：支援</td>
   <td>Service Pack和重要更新</td>
  </tr>
  <tr>
   <td>Ubuntu 20.04</td>
   <td>答：支援</td>
   <td>Service Pack和重要更新</td>
  </tr>
  <tr>
   <td> Microsoft Windows Server 2016 （64位元） （已棄用）</td>
   <td>答：支援</td>
   <td>Service Pack和重要更新</td>
  </tr>
  <tr>
   <td><p>Red Hat Enterprise Linux 8 （核心4.x） （64位元）</p> </td>
   <td><p>答：支援</p> </td>
   <td><p>次要版本、累積更新和關鍵更新</p> </td>
  </tr>
  <tr>
   <td><p>Red Hat Enterprise Linux 7 （核心3.x） （64位元） （已棄用）</td>
   <td><p>答：支援</p> </td>
   <td><p>次要版本、累積更新和關鍵更新</p> </td>
  </tr>
  <tr>
   <td><p>SUSE® Linux® Enterprise Server 12 （64位元）</p> </td>
   <td><p>答：支援</p> </td>
   <td><p>Service Pack、累積修補程式和重要安全性更新</p> </td>
  </tr>
  <tr>
   <td>oracleLinux® 7更新3 （64位元）</td>
   <td>答：支援</td>
   <td>Service Pack、累積修補程式和重要安全性更新</td>
  </tr>
  <tr>
   <td>CentOS 7 （64位元）<sup> [6]</sup></td>
   <td>答：支援</td>
   <td>Service Pack、累積修補程式和重要安全性更新</td>
  </tr>
 </tbody>
</table>

#### 虛擬化環境 {#virtualized-environment}

您可以在JEE上的實體電腦或虛擬環境中執行AEM Forms。 不過，如果您在虛擬環境中遇到AEM Forms的任何問題，請嘗試在實體機器上複製此問題。 如果實體電腦上持續發生問題，請聯絡Adobe支援以尋求解決方案。 針對您無法在實體機器上復寫的問題，請連絡您的虛擬環境廠商。

#### 開發環境 {#development-environments}

<table>
 <tbody>
  <tr>
   <th><p><strong>平台（基礎版本）</strong></p> </th>
   <th>支持级别</th>
   <th><p><strong>支援的修補程式定義</strong></p> </th>
  </tr>
  <tr>
   <td><p>Microsoft® Windows® 10 64位元</p> </td>
   <td>E：預期可運作</td>
   <td><p>Service Pack和重要更新</p> </td>
  </tr>
 </tbody>
</table>

### 支援的伺服器平台例外 {#exceptions-to-supported-server-platforms}

選擇在JEE伺服器上設定AEM Forms的平台時，請考量下列例外情況。

1. JEE上的AEM Forms不支援搭配MySQL使用的IBM® WebSphere®。
1. JEE上的AEM Forms不支援SUSE Linux Enterprise Server 12上的JBoss。 SUSE Linux Enterprise Server 12僅支援IBM WebSphere。
1. 除OracleJava™ SE外，JEE上的AEM Forms不支援任何具®JBoss的JDK。
1. JEE上的AEM Forms不支援任何具有IBM® WebSphere®的JDK，IBM® JDK除外。
1. CRX-repository支援TarMK、MongoDB和關聯式資料庫(RDBMK)型別的持續性。 應用程式伺服器和CRX-repository之間不能有兩個不同的資料庫系統。 不過，在JEE環境上的AEM Forms上，您可以搭配CRX儲存庫和支援的關聯式資料庫與應用程式伺服器使用MongoMK。
1. JEE上的AEM Forms不支援CentOS上的WebSphere應用程式伺服器。
1. JEE上的AEM Forms不支援JBoss角色型存取控制(RBAC)。
1. JEE上的AEM Forms僅支援應用程式伺服器JBoss EAP 7.4的OracleJava™ SE 11 （64位元） SDK。

此外，選擇在JEE部署上AdobeAEM Forms的軟體時，請考量下列幾點：

- JEE版AEM Forms除了支援軟體的指定主要和次要版本以外，也支援更新、修補程式和修正套件。 不過，除非另有指定，否則不支援更新至下一個主要或次要版本。
- 叢集式安裝不支援TarMK持續性。 如需有關支援的持續性的資訊，請參閱 [為AEM Forms安裝選擇持續性型別](/help/forms/using/choosing-persistence-type-for-aem-forms.md).
- AEM Forms on JEE支援各種協力廠商軟體，具體如下： [協力廠商軟體支援政策](../../forms/using/aem-forms-jee-supported-platforms.md#p-third-party-patch-support-policy-p).
- 根據協力廠商提供的支援，JEE上的AEM Forms可支援平台。 協力廠商可能不允許某些組合。 例如，許多廠商尚未認證其應用程式伺服器的Oracle。 因此，JEE上的AEM Forms也不支援這些組合。 為確保您選擇支援的軟體版本，請一併參閱協力廠商的支援矩陣。
- JEE上的AEM Forms不支援TarMK冷待命。
- JEE上的AEM Forms不支援垂直叢集。
- JEE上的AEM Forms不支援叢集環境上的MySQL資料庫。
- 如需已移除或更新平台的清單，請參閱 [AEM 6.5 Forms新功能摘要](../../forms/using/whats-new.md) 檔案。

### LDAP伺服器（選購） {#ldap-servers-optional}

<table>
 <tbody>
  <tr>
   <th><p><strong>產品（基本版本）</strong></p> </th>
   <th><p><strong>支援的修補程式定義</strong></p> </th>
  </tr>
  <tr>
   <td>Microsoft Active Directory 2016</td>
   <td>維護版本和修正套件</td>
  </tr>
  <tr>
   <td><p>IBM® Tivoli Directory Server 6.4</p> </td>
   <td><p>功能套件和暫時修正</p> </td>
  </tr>
 </tbody>
</table>

### 電子郵件伺服器（選購） {#email-servers-optional}

| 产品 |
| ----------------------- |
| Microsoft Exchange 2013 |
| Microsoft Office 365 |

### 內容管理員和對應的聯結器 {#content-managers-and-corresponding-connectors}

<table>
 <tbody>
  <tr>
   <td><strong>产品<br /> </strong></td>
   <td><strong>版本</strong></td>
  </tr>
  <tr>
   <td>EMC Documentum</td>
   <td>7.3</td>
  </tr>
  <tr>
   <td>IBM Filenet</td>
   <td>5.5.2</td>
  </tr>
  <tr>
   <td>IBM Content Manager伺服器（已棄用） </td>
   <td>8.5 Fix Pack 2</td>
  </tr>
  <tr>
   <td> IBM內容管理員使用者端（已棄用）</td>
   <td>8.5 </td>
  </tr>
  <tr>
   <td>Microsoft Sharepoint </td>
   <td>2016 （已棄用）<br /> </td>
  </tr>
  <tr>
   <td>Microsoft Sharepoint </td>
   <td>2019<br /> </td>
  </tr>
 </tbody>
</table>

### 支援Cordova {#support-for-cordova}

AEM Forms應用程式現在支援Apache Cordova。 以下是支援的平台特定版本Cordova：

- Apache Cordova 6.4.0
- Cordova iOS 4.3.0
- Cordova Android 6.0.0
- Cordova Windows 4.4.3

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
此外：
- PDF產生器需要32位元版本的 [Acrobat 2020 classic路線20.004.30006版](https://helpx.adobe.com/acrobat/release-note/release-notes-acrobat-reader.html) 或Acrobat 2017 17.011.30078版來執行轉換。
- PDF產生器僅支援32位元零售版的Microsoft Office Professional Plus以及其他轉換所需的軟體。
- PDF產生器不支援Microsoft Office 365。
- 僅在Windows和Linux上支援OpenOffice的PDF產生器轉換。
- 只有Windows支援OCRPDF、Optimize PDF和Export PDF功能。
- Acrobat版本與AEM Forms搭配，可啟用PDF產生器功能。 套件版本僅可透過AEM Forms (在AEM Forms授權期間)以程式設計方式存取，以與AEM FormsPDF產生器搭配使用。 如需詳細資訊，請參閱根據您的部署說明的AEM Forms產品說明([內部部署](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-manager-on-premise.html) 或 [Managed Services](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-manager-managed-services.html))」
- PDF產生器服務不支援Microsoft Windows 10。
- PDF產生器無法使用Microsoft Visio 2019轉換檔案。 您可以繼續使用Microsoft Visio 2016來轉換.VSD和.VSDX檔案。
- PDF產生器無法使用Microsoft Project 2019轉換檔案。 您可以繼續使用Microsoft Project 2016來轉換.MPP檔案。
>


### 協助工具支援的例外情況 {#exceptions-to-accessibility-support}

下列AEM Forms子系統不是 [508](https://www.section508.gov/) 相容：

- 最適化Forms編寫UI
- Forms Manager編寫UI
- Correspondence Management編寫UI
- Admin UI (Administration Console UI)

## JEE版AEM Forms的系統需求 {#system-requirements-for-aem-forms-on-jee}

### 最低硬體需求 {#minimum-hardware-requirements}

<table>
 <tbody>
  <tr>
   <td>Platform</td>
   <td>最低硬體需求</td>
  </tr>
  <tr>
   <td>Microsoft Windows Server</td>
   <td>Intel® Xeon® E5-2680、2.4 GHz處理器或同等處理器<br /> VMWare ESX 5.1或更新版本<br /> RAM：6 GB （64位元作業系統搭配64位元JVM）<br /> 可用磁碟空間：15GB的暫存空間加上22GB<br /> 適用於AEM Forms on JEE的</td>
  </tr>
  <tr>
   <td>SUSE Linux Enterprise Server</td>
   <td>Intel Xeon E5-2670v2,1個vCPU，2.5 GHz處理器<br /> AWS m3.medium （3個ECU）<br /> RAM：6 GB （64位元作業系統搭配64位元JVM）<br /> 可用磁碟空間：6 GB的暫存空間加上22 GB<br /> 適用於AEM Forms on JEE的</td>
  </tr>
  <tr>
   <td>Red Hat Enterprise Linux</td>
   <td>Intel Xeon E5-2670v2,1個vCPU，2.5 GHz處理器<br /> AWS m3.medium （3個ECU）<br /> RAM：6 GB （64位元作業系統搭配64位元JVM）<br /> 可用磁碟空間：6 GB的暫存空間加上22 GB<br /> 適用於AEM Forms on JEE的<br /> </td>
  </tr>
  <tr>
   <td>小型生產環境的硬體需求</td>
   <td>
    <ul>
     <li><strong>Intel支援的環境</strong>：Intel® Xeon® E5-2680,2.4 GHz或更高。 使用雙核心處理器可進一步提升效能</li>
     <li><strong>記憶體： </strong>4 GB <br /> </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

如需其他需求，請參閱：

- [JEE部署之單一伺服器AEM Forms的系統需求](https://www.adobe.com/go/learn_aemforms_sysreq_single_65)
- [JEE部署上叢集AEM Forms的系統需求](https://www.adobe.com/go/learn_aemforms_sysreq_cluster_65)

## AEM Forms on JEE的支援使用者端 {#supported-clients-for-aem-forms-on-jee}

### Workbench {#workbench}

<table>
 <tbody>
  <tr>
   <th><p><strong>Platform</strong></p> </th>
   <th><p><strong>支援的修補程式定義</strong></p> </th>
  </tr>
  <tr>
   <td><p>Microsoft® Windows® 10 (Enterprise、Pro、Basic)</p> <p>32位元或64位元版本</p> <p> </p> </td>
   <td>Service Pack和重要更新</td>
  </tr>
  <tr>
   <td>Microsoft® Windows® 2016 Server</td>
   <td>Service Pack和重要更新</td>
  </tr>
 </tbody>
</table>

- 安裝磁碟空間：1.7 GB （僅適用於Workbench）、2.7 GB （僅適用於Workbench、Designer完整安裝的單一磁碟機），以及範例元件400 MB （適用於暫存安裝目錄）：200 MB （位於使用者暫存目錄）和200 MB （位於Windows暫存目錄）。 如果所有這些位置都位於單一磁碟機上，安裝期間必須有1.5 GB的可用空間。 安裝完成時，會刪除複製到暫存目錄的檔案。

- 執行Workbench所需的記憶體：2 GB的RAM
- 硬體需求：Intel® Pentium® 4或AMD同等處理器，1 GHz處理器
- 最低1024 X 768畫素或更高的熒幕解析度（含16位元色彩或更高）
- 與JEE伺服器上AEM Forms的TCP/IPv4或TCP/IPv6網路連線
- 您必須具有系統管理許可權，才能在Windows上安裝Workbench。 如果您使用非管理員帳戶進行安裝，安裝程式會提示您輸入適當帳戶的認證。

### Designer {#designer}

- Microsoft® Windows® 2016 Server、Microsoft® Windows® 2019 Server或Microsoft® Windows® 10
- 1 GHz或更快的處理器，支援PAE、NX和SSE2。
- 32位元的1 GB RAM或64位元作業系統的2 GB RAM
- 16 GB磁碟空間，適用於32位元或20 GB磁碟空間，適用於64位元作業系統
- 顯示卡記憶體：128 MB的GPU （建議使用256 MB）
- 2.35 GB的可用硬碟空間
- 1024 X 768畫素或更高的熒幕解析度
- 視訊硬體加速（選購）
- Acrobat Pro DC、Acrobat Standard DC或Adobe Acrobat Reader DC。
- 安裝Designer的管理許可權。

### Adobe Acrobat和Adobe Reader {#adobe-acrobat-and-adobe-reader}

<table>
 <tbody>
  <tr>
   <th><p><strong>Acrobat和Adobe Reader （基礎版）</strong></p> </th>
   <th><p><strong>支援的修補程式定義</strong></p> </th>
  </tr>
  <tr>
   <td>Acrobat 2020 （傳統路線）</td>
   <td>20.004.30006版或更新版本<br /> </td>
  </tr>
  <tr>
   <td>Acrobat 2017 （傳統路線） （已棄用）</td>
   <td>17.011.30078版或更新版本<br /> </td>
  </tr>

</tbody>
</table>

>[!NOTE]
Acrobat DC產品系列為Acrobat和Reader引進了兩種路線，本質上是不同的產品：「Classic」和「Continuous」。 如需詳細資訊和兩個曲目的比較，請參閱 [https://www.adobe.com/go/acrobatdctracks.](https://www.adobe.com/go/acrobatdctracks)

### 瀏覽器 {#browsers}

#### 桌上型 {#desktops}

<table>
 <tbody>
  <tr>
   <th><p><strong>瀏覽器（基本）</strong></p> </th>
   <th><p><strong>支援等級</strong></p> </th>
   <th><p><strong>支援的修補程式定義</strong></p> </th>
  </tr>
  <tr>
   <td><p>Microsoft Edge （長青）</p> </td>
   <td><p>答：支援</p> </td>
   <td><p>Service Pack和更新</p> </td>
  </tr>
  <tr>
   <td><p>Mozilla Firefox （常青）</p> </td>
   <td><p>答：支援</p> </td>
   <td>所有更新</td>
  </tr>
  <tr>
   <td>Mozilla Firefox ESR</td>
   <td>E：預期可運作</td>
   <td> 所有更新</td>
  </tr>
  <tr>
   <td><p>Google Chrome （常青）</p> </td>
   <td><p>答：支援</p> </td>
   <td>所有更新</td>
  </tr>
  <tr>
   <td>macOS上的Apple Safari</td>
   <td>答：支援</td>
   <td>所有更新</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
桌上型電腦的一些瀏覽器相關例外狀況如下：
- 只有Macintosh OS X支援Safari。
- Workspace支援Macintosh OS X 10.6和10.7上的Safari 5.1 (含Acrobat DC或更新版本)。 如需Safari 5.1與Adobe Reader、Acrobat相容性的詳細資訊，請參閱 [https://helpx.adobe.com/x-productkb/multi/safari-5-1-incompatible-reader.html](https://helpx.adobe.com/x-productkb/multi/safari-5-1-incompatible-reader.html).
- Safari不支援管理主控台。
- Correspondence Management不支援AEM 6.1表單適用的Windows® Internet Explorer 9.0。
- Forms入口網站支援Internet Explorer 11上的JAWS 14.0熒幕助讀程式軟體，以提供協助工具。


#### 行動使用者端 {#mobile-clients}

<table>
 <tbody>
  <tr>
   <th><p><strong>瀏覽器（基本）</strong></p> </th>
   <th><p><strong>支援的修補程式定義</strong></p> </th>
  </tr>
  <tr>
   <td><p>Android™ 4.1.2及更高版本上的Chrome</p> </td>
   <td><p>所有更新</p> </td>
  </tr>
  <tr>
   <td>iOS 15.1及更高版本上的Safari</td>
   <td>所有更新</td>
  </tr>
  <tr>
   <td>Microsoft Edge<br /> </td>
   <td>所有更新<br /> </td>
  </tr>
  <tr>
   <td>Android™ 4.4及更高版本上的原生Android瀏覽器</td>
   <td>所有更新</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
- Forms入口網站僅在iPad上的Safari上受支援。


### AEM Forms應用程式 {#aem-forms-workspace-app}

#### 行動裝置支援 {#mobile-device-support}

AEM Forms應用程式適用於下列平台：

| **Platform** | **支援的裝置** |
| ----------------- | ------------------------------------------------------------------------------------------------------------------- |
| Apple iOS | Apple iPhone、iPad、iPad Air和執行iOS 15.1及更高版本的iPad mini。 |
| Google Android | Android 5.1及更高版本。 AEM Forms應用程式已通過7英吋及10英吋Samsung Galaxy平板電腦及熱門智慧型手機的認證。 |
| Microsoft Windows | 執行Microsoft Windows 10作業系統的Microsoft Surface裝置、平板電腦、筆記型電腦和桌上型電腦。 |

### Microsoft Office適用的AdobeDocument Security Extension {#adobe-rights-management-extension-for-microsoft-office}

按一下 [此處](https://www.adobe.com/products/livecycle/rightsmanagement/extension/downloads.html) 若要檢視Microsoft® Office適用的AdobeDocument Security Extension的系統需求。

### 使用者端支援的例外 {#exceptions-to-client-support}

JEE版AEM Forms除了支援軟體的指定主要和次要版本以外，也支援更新、修補程式和修正套件。 不過，除非另有指定，否則不支援更新至下一個主要或次要版本。

## 協力廠商修補程式支援原則 {#third-party-patch-support-policy}

JEE版AEM Forms的協力廠商軟體需求記錄在各自產品檔案的「系統需求」一節中。 所有檔案都可從以下位置存取： [https://adobe.com/go/learn_aemforms_documentation_65](https://adobe.com/go/learn_aemforms_documentation_65) .

JEE上的AEM Forms第三方參考平台會說明在JEE上AEM Forms開發和發行期間第三方基礎架構的特定修補程式層級，以及該版本AEM Forms on JEE支援之基礎架構的最低修補程式/Service Pack層級。

Adobe支援協力廠商在發行時發出的緊急或建議修補程式，並假設協力廠商保證回溯相容於AEM Forms on JEE支援的版本。 Adobe僅支援在AEM Forms on JEE檔案中規定的最低修補程式等級之後發行的修補程式。

在某些情況下，Adobe不支援變更主要功能的協力廠商更新，因此不支援完全的回溯相容性。 如需支援更新的詳細資訊，請參閱 [支援的修補程式定義](https://helpx.adobe.com/aem-forms/aem-forms-third-party-software-patch.html) 適用於特定廠商的產品和Adobe支援的修補程式型別。

在Adobe無法控制的情況下，聲稱回溯相容性的協力廠商修補程式可能會對Adobe產品或客戶環境造成負面影響。 在這種情況下，Adobe建議客戶在將第三方提供的任何緊急修補程式套用至關鍵系統之前，先評估其影響。 Adobe將與第三方合作，透過正常的Adobe支援計畫或第三方修正修補程式中的問題，透過合理的業務努力來解決此類問題。 這並不保證Adobe支援的新發行協力廠商修補程式將可如供應商記錄或在JEE上與AEM Forms搭配運作。

Adobe保留隨時變更AEM Forms on JEE版本支援的第三方參考平台及其支援之修補程式定義的權利。

您也可以在Adobe企業支援網站中搜尋與產品相關的知識庫文章，以找到第三方修補程式的其他資訊。

## 平台更新 {#platform-updates}

以下平台在2022年6月2日發行的AEM Forms 6.5.13.0中標示為已過時：

- Microsoft SharePoint 2016

下列平台在2022年3月3日發行的AEM Forms 6.5.12.0中標示為已過時：

- MongoDB Enterprise 4.0
- IBM DB2 11.1
- oracle資料庫12c發行版本2
- MySQL 5.7.35
- Microsoft® SQL Server JDBC驅動程式6.2.1.0
- JBoss® Enterprise Application Platform (EAP) 7.1.4
- IBM Content Manager Server 8.5 Fix Pack 2
- IBM Content Manager Client 8.5
- Microsoft SQL Server 2016

以下平台在2021年9月7日發行的AEM Forms 6.5.10.0中標示為已過時：

- Adobe Acrobat 2017 - [Adobe Acrobat 2017的核心支援將於2022年6月6日終止](https://helpx.adobe.com/cn/support/programs/eol-matrix.html).
- Microsoft Windows Server 2016 （64位元）
- Red Hat Enterprise Linux 7 （核心3.x） （64位元）
- Microsoft® Office 2016
- OpenOffice 4.1.2

>[!NOTE]
標示為 [AEM Forms 6.5.12.0和6.5.10.0已棄用，直到AEM Forms 6.5 Service Pack 18 (6.5.18.0)發行版本為止，仍提供支援](https://helpx.adobe.com/cn/support/programs/eol-matrix.html).

## 修訂歷史記錄 {#revision-history}

- 2022年9月01日

   - 新增應用程式伺服器JBoss EAP 7.4的OracleJava™ SE 11 （64位元） SDK支援。

- 2022年3月03日

   - 移除對下列專案的支援：
      - IBM® J9虛擬機器器（版本編號2.8、JRE 1.8.0）
      - oracle資料庫12c發行版本1
      - oracle資料庫18c
      - oracle Unified Directory (OUD) 11g版本2
      - IBM Lotus Domino 9.0
      - IBM Filenet 5.2
      - AdobeFlash Player

- 2021年10月10日

   - 將適用於AEM Forms應用程式的iOS支援版本變更為iOS 15.1。舊版為iOS 12。

- 2021年9月07日
   - **平台更新**： [!DNL Adobe Experience Manager Forms] on JEE已新增對下列平台的支援：
      - [!DNL Adobe Acrobat 2020]
      - [!DNL Ubuntu 20.04]
      - [!DNL Open Office 4.1.10]
      - [!DNL Microsoft Office 2019]
      - [!DNL Microsoft Windows Server 2019]
      - [!DNL RHEL8]

- 2020年12月03日
   - 為下列平台新增AEM Forms 6.5.7.0或更新版本的支援：
      - [!DNL Microsoft SQL Server 2019]

- 2020年9月09日

   - 將適用於AEM Forms應用程式的iOS支援版本變更為iOS 12。 舊版為iOS 11。

