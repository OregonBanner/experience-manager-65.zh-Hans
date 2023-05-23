---
title: 部署和維護
seo-title: Deploying and Maintaining
description: 瞭解如何開始安裝AEM。
seo-description: Learn how to get started with the AEM installation.
uuid: 4429ac4d-abd7-47d8-b19d-773accb7cc7a
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
discoiquuid: e48cc0ed-688c-44c8-b6d6-5f3c8593a295
docset: aem65
exl-id: 3df0662a-0768-4b56-8b94-c517657b4bd9
source-git-commit: 9052ed3e89fdc67d94fc60bbff64d42255565767
workflow-type: tm+mt
source-wordcount: '1802'
ht-degree: 3%

---

# 部署和維護{#deploying-and-maintaining}

在此頁面中，您會找到：

* [基本概念](#basic-concepts)

   * [什麼是AEM？](#what-is-aem)
   * [典型部署](#typical-deployment-scenarios)

      * [內部部署](#on-premise)
      * [使用Cloud Manager的Managed Services](#managed-services-using-cloud-manager)

* [快速入门](#getting-started)

   * [前提条件](#prerequisites)
   * [取得軟體](#getting-the-software)
   * [預設本機安裝](#default-local-install)
   * [Author和Publish安裝](#author-and-publish-installs)
   * [解壓縮的安裝目錄](#unpacked-install-directory)
   * [啟動和停止](#starting-and-stopping)

熟悉這些基本知識後，您將會在下列子頁面中找到更進階和詳細的資訊：

* [技術需求](/help/sites-deploying/technical-requirements.md)
* [建議的部署](/help/sites-deploying/recommended-deploys.md)
* [自訂獨立安裝](/help/sites-deploying/custom-standalone-install.md)
* [應用程式伺服器安裝](/help/sites-deploying/application-server-install.md)
* [疑难解答](/help/sites-deploying/troubleshooting.md)
* [命令列啟動和停止](/help/sites-deploying/command-line-start-and-stop.md)
* [配置](/help/sites-deploying/configuring.md)
* [升級至AEM 6.5](/help/sites-deploying/upgrade.md)
* [电子商务](/help/commerce/cif-classic/deploying/ecommerce.md)
* [設定操作說明文章](/help/sites-deploying/ht-deploy.md)
* [Web 控制台](/help/sites-deploying/web-console.md)
* [疑難排解復寫](/help/sites-deploying/troubleshoot-rep.md)
* [最佳实践](/help/sites-deploying/best-practices.md)
* [部署社群](/help/communities/deploy-communities.md)
* [AEM平台簡介](/help/sites-deploying/platform.md)
* [效能准則](/help/sites-deploying/performance-guidelines.md)
* [AEM Mobile快速入門](/help/mobile/getting-started-aem-mobile.md)
* [什麼是AEM Screens？](https://experienceleague.adobe.com/docs/experience-manager-screens/user-guide/aem-screens-introduction.html)

## 基本概念 {#basic-concepts}

### 什麼是AEM？ {#what-is-aem}

Adobe Experience Manager是網頁式使用者端伺服器系統，用於建立、管理和部署商業網站及相關服務。 它將許多基礎架構層級和應用程式層級的功能合併為單一整合套件。

在基礎架構層級，AEM提供下列功能：

* **Web應用程式伺服器**：AEM可以獨立模式部署（包含整合式Jetty Web伺服器），或部署為協力廠商應用程式伺服器內的Web應用程式。
* **Web應用程式架構**：AEM納入Sling Web應用程式架構，簡化RESTful內容導向Web應用程式的撰寫。
* **內容存放庫**： AEM包含Java Content Repository (JCR)，這是專為非結構化與半結構化資料而設計的階層式資料庫型別。 存放庫不僅儲存面向使用者的內容，也儲存應用程式使用的所有程式碼、範本和內部資料。

在此基礎之上，AEM還提供許多應用程式層級的功能，用於管理：

* **网站**
* **行動應用計畫**
* **數位出版物**
* **Forms**
* **数字资产**
* **社区**
* **線上商務**

最後，客戶可利用這些基礎結構和應用程式層級的建置組塊，自行建置應用程式以建立自訂解決方案。

AEM伺服器是 **以Java為基礎** 並會在大多數支援該平台的作業系統上執行。 所有使用者端與AEM的互動均透過 **網頁瀏覽器**.

### 典型部署案例 {#typical-deployment-scenarios}

在AEM術語中，「例項」是在伺服器上執行的AEM的副本。 AEM安裝通常至少涉及兩個執行個體，通常在不同電腦上執行：

* **作者**：AEM執行個體，用來建立、上傳和編輯內容以及管理網站。 一旦內容準備好上線，就會將其復寫到發佈執行個體。
* **發佈**：為公眾提供已發佈內容的AEM例項。

這些例項在安裝軟體方面完全相同。 它們僅能透過設定來區分。 此外，大部分安裝都使用Dispatcher：

* **Dispatcher**：靜態網頁伺服器(Apache httpd、Microsoft IIS等) 以AEM Dispatcher模組增強。 它缓存由发布实例生成的网页以提高性能。

此設定有許多進階選項和詳細說明，但作者、發佈和Dispatcher的基本模式是大多數部署的核心。 我們先從相對簡單的設定開始。 隨後將討論進階部署選項。

以下小節說明這兩種情況：

* **內部部署**：在您的企業環境中部署及管理AEM。

* **Managed Services - Adobe Experience Manager的Cloud Manager**：由Adobe Managed Services部署和管理的AEM。

### 內部部署 {#on-premise}

您可以在公司環境中的伺服器上安裝AEM。 典型安裝例項包括：開發、測試和發佈環境。 請參閱 [快速入門](/help/sites-deploying/deploy.md#getting%20started) 區段，以瞭解如何取得AEM軟體以在本機安裝。

若要進一步瞭解典型內部部署，請參閱 [建議的部署](/help/sites-deploying/recommended-deploys.md).

### 使用Cloud Manager的Managed Services {#managed-services-using-cloud-manager}

AEM Managed Services是數位體驗管理的完整解決方案。 它提供雲端體驗傳送解決方案的優點，同時保留內部部署的所有控制、安全性和自訂優點。 AEM Managed Services可讓客戶在雲端部署，並依賴Adobe的最佳實務和支援，以更快啟動。 組織和企業使用者只需最少的時間即可與客戶互動、提高市場份額，並專注於建立創新的行銷活動，同時減輕IT負擔。

透過AEM Managed Services，客戶可獲得下列優點：

**加快上市時間：** 藉由Adobe Managed Services的彈性雲端基礎結構，組織可以快速規劃、啟動和最佳化成功的數位體驗。 Adobe可管理雲端架構，不需要額外的資金、硬體或軟體，而Adobe的客戶解決方案工程師可協助AEM架構、布建、連線後端應用程式的自訂以及上線最佳實務。

**更高的效能：** 提供99.5%、99.9%、99.95%和99.99%四種服務可用性選項，為您的企業提供可靠的數位體驗。 此外，它還可提供自動備份和多模式災難回覆模式，協助確保可靠性和應急管理。

**最佳化的IT成本：** 主動式指引和專業知識可幫助組織隨時掌握最新版本的AEM。 AMS Enterprise/Basic的全新部署自動包含Adobe白金級維護和支援，提供技術專業知識和營運經驗，以協助組織維護其關鍵任務應用程式。 免費基本Analytics或Target功能提供額外價值，特別適用於對分析和個人化需求有限的中端市場組織。

**最高安全性：** 將客戶應用程式託管於受限制的存取設施、防火牆系統後面或虛擬私人雲端，確保企業級實體、網路和資料安全性。 它包含單一租使用者虛擬機器器，提供強大的資料儲存加密、防毒軟體和資料隔離功能。

**Cloud Manager**： Cloud Manager是Adobe Experience Manager Managed Services產品的一部分，是一個自助服務入口網站，可進一步讓組織在雲端中自行管理Adobe Experience Manager。 其包含一流的持續整合和持續傳遞(CI/CD)管道，可讓IT團隊和實作合作夥伴加速自訂或更新的傳遞，而不會影響效能或安全性。 Cloud Manager僅適用於Adobe Managed Service客戶。

若要進一步瞭解Cloud Manger及其資源，請參閱 [**Cloud Manager使用手冊**](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/introduction.html).

## 快速入门 {#getting-started}

### 前提条件 {#prerequisites}

雖然生產執行個體通常在執行官方支援的作業系統的專用電腦上執行(請參閱 [技術需求](/help/sites-deploying/technical-requirements.md))，則Experience Manager伺服器實際上會在任何支援 [**Java Standard Edition 8**](https://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).

為了熟悉和在AEM上進行開發，使用安裝在執行Apple OS X或Microsoft Windows或Linux案頭版本的本機電腦上的執行個體是很常見的。

在使用者端，AEM可與所有現代化瀏覽器搭配使用(**Microsoft Edge**， **Internet Explorer** 11， **Chrome **51+** **、**Firefox **47+、 **Safari** 8+)。 另請參閱 [支援的使用者端平台](/help/sites-deploying/technical-requirements.md#supported-client-platforms) 以取得詳細資訊。

### 取得軟體 {#getting-the-software}

AEM持有有效維護與支援合約的客戶應已收到內含程式碼的郵件通知，並可從 [**Adobe授權網站**](https://licensing.adobe.com/). 業務合作夥伴可從以下位置請求下載存取權： [**spphelp@adobe.com**](mailto:spphelp@adobe.com).

AEM軟體套件有兩種形式：

* **cq-quickstart-6.5.0.jar：** 獨立可執行檔 *jar* 包含啟動和執行所需一切的檔案。

* **cq-quickstart-6.5.0.war：** A *戰爭* 供部署至協力廠商應用程式伺服器的檔案。

在以下小節中，我們將說明 **獨立安裝**. 如需在應用程式伺服器中安裝AEM的詳細資訊，請參閱 [應用程式伺服器安裝](/help/sites-deploying/application-server-install.md).

### 預設本機安裝 {#default-local-install}

1. 在本機電腦上建立安裝目錄。 例如：

   UNIX安裝位置： **/opt/aem**

   Windows安裝位置： **`C:\Program Files\aem`**

   同樣地，將範例執行個體直接安裝在案頭上的資料夾中也很常見。 無論如何，我們都會以一般方式將此位置稱為：

   `<aem-install>`

   *請注意，檔案目錄的路徑只能包含美國ASCII字元。*

1. 放置 **jar** 和 **授權** 此目錄中的檔案：

   ```shell
   <aem-install>/
       cq-quickstart-6.5.0.jar
       license.properties
   ```

   如果您不提供 `license.properties` 檔案時，AEM會將您的瀏覽器重新導向至 **歡迎** 啟動時畫面，您可在此輸入授權金鑰。 如果您還沒有有效的授權金鑰，則需要向Adobe索取有效授權金鑰。

1. 若要在GUI環境中啟動執行個體，只需按兩下 **`cq-quickstart-6.5.0.jar`** 檔案。

   或者，您可以從命令列啟動AEM：

   ```shell
       java -Xmx1024M -jar cq-quickstart-6.5.0.jar
   ```

AEM需要幾分鐘的時間來解壓縮jar檔案、自行安裝並啟動。 上述程式會產生：

* 一個 **AEM作者** 例項
* 執行於 **localhost**
* 在連線埠上 **4502**

若要存取執行個體，請將瀏覽器指向：

**`https://localhost:4502`**

製作執行個體中的結果會自動設定為連線至 **發佈執行個體** 於 **`localhost:4503`**.

### Author和Publish安裝 {#author-and-publish-installs}

預設安裝(一個 **作者** 執行個體於 **`localhost:4502`**)的變數，只要重新命名 `jar` 首次啟動之前的檔案。 命名模式為：

**`cq-<instance-type>-p<port-number>.jar`**

例如，將檔案重新命名為

**`cq-author-p4502.jar`**

並啟動它將會導致編寫執行個體在 **`localhost:4502`**.

同樣地，重新命名和啟動檔案

**`cq-publish-p4503.jar`**

將導致發佈執行個體執行於 **`localhost:4503`**.

舉例來說，您可以將這兩個例項安裝在中

`<aem-install>/author`和

**`<aem-install>/publish`**

如需自訂安裝的詳細資訊，請參閱下列內容：

* [自訂獨立安裝](/help/sites-deploying/custom-standalone-install.md)
* [运行模式](/help/sites-deploying/configure-runmodes.md)

### 解壓縮的安裝目錄 {#unpacked-install-directory}

第一次啟動快速入門jar時，它會將其自身解壓縮到名為的新子目錄下的相同目錄中 `crx-quickstart`. 您最後應該會遇到以下問題：

```xml
<aem-install>/
    license.properties
    cq-quickstart-6.5.0.jar
    crx-quickstart/
        app/
        bin/
        conf/
        launchpad/
        logs/
        metrics/
        monitoring/
        opt/
        repository/
        threaddumps/
        eula-de_DE.html
        eula-en_US.html
        eula-fr_FR.html
        eula-ja_JP.html
        readme.txt
```

如果從UI安裝執行個體，則會自動開啟瀏覽器視窗，同時開啟案頭應用程式視窗，顯示執行個體的主機和連線埠，以及開啟/關閉開關：

![啟動畫面](assets/screen_shot_.png)

>[!NOTE]
>
>如果您使用符號連結，請檢視 [symlink的問題](https://helpx.adobe.com/experience-manager/kb/changing-symlink.html).

### 啟動和停止 {#starting-and-stopping}

在AEM自行解壓縮並初次啟動後，只要連按兩下安裝目錄中的jar檔案即可啟動執行個體，它不會重新安裝。

若要從GUI停止執行處理，只要按一下 **開啟/關閉** 開啟[案頭應用程式]視窗。

您也可以從命令列停止和啟動AEM。 假設您第一次安裝執行個體時， **命令列指令碼** 位於此處：

**`<aem-install>/crx-quickstart/bin/`**

此資料夾包含下列Unix bash shell指令碼：

* **`start`**：啟動執行個體
* `stop`：停止執行個體
* **`status`**：報告執行個體的狀態
* **`quickstart`**：如有需要，可用於設定開始資訊。

也有同等功能 **`bat`** Windows的檔案。 如需詳細資訊，請參閱：

* [命令列啟動和停止](/help/sites-deploying/command-line-start-and-stop.md)

AEM會啟動，並自動將您的網頁瀏覽器重新導向至適當的頁面，通常是登入頁面；例如：

`https://localhost:4502/`

![登入畫面](assets/screen_shot_2019-04-08at83533am.png)

登入後，您就可以存取AEM。 如需詳細資訊，請根據您的角色，參閱下列內容：

* [创作](/help/sites-authoring/home.md)
* [管理](/help/sites-administering/home.md)
* [开发](/help/sites-developing/home.md)
* [管理](/help/managing/best-practices.md)

## 進階部署 {#advanced-deployment}

上節應能讓您充分瞭解AEM安裝的基本概念。 不過，安裝AEM完整生產系統可能會涉及相當大的複雜性。 如需進階安裝的完整涵蓋範圍，請參閱下列子頁面：

* [技術需求](/help/sites-deploying/technical-requirements.md)
* [建議的部署](/help/sites-deploying/recommended-deploys.md)
* [自訂獨立安裝](/help/sites-deploying/custom-standalone-install.md)
* [應用程式伺服器安裝](/help/sites-deploying/application-server-install.md)
* [疑难解答](/help/sites-deploying/troubleshooting.md)
* [命令列啟動和停止](/help/sites-deploying/command-line-start-and-stop.md)
* [配置](/help/sites-deploying/configuring.md)
* [升級至AEM 6.5](/help/sites-deploying/upgrade.md)
* [电子商务](/help/commerce/cif-classic/deploying/ecommerce.md)
* [設定操作說明文章](/help/sites-deploying/ht-deploy.md)
* [Web 控制台](/help/sites-deploying/web-console.md)
* [疑難排解復寫](/help/sites-deploying/troubleshoot-rep.md)
* [最佳实践](/help/sites-deploying/best-practices.md)
* [部署社群](/help/communities/deploy-communities.md)
* [AEM平台簡介](/help/sites-deploying/platform.md)
* [效能准則](/help/sites-deploying/performance-guidelines.md)
* [AEM Mobile快速入門](/help/mobile/getting-started-aem-mobile.md)
* [什麼是AEM Screens？](https://experienceleague.adobe.com/docs/experience-manager-screens/user-guide/aem-screens-introduction.html)
