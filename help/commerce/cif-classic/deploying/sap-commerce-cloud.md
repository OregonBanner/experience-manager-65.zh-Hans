---
title: 使用SAPCommerce Cloud部署電子商務
description: 瞭解如何使用SAPCommerce Cloud部署電子商務。
contentOwner: Guillaume Carlino
topic-tags: e-commerce
content-type: reference
exl-id: ecbd0097-c407-4581-bab2-4729a71df4a3
source-git-commit: e1a0b114ce16d0e7f6a464e9d30b8f111297bcc6
workflow-type: tm+mt
source-wordcount: '724'
ht-degree: 2%

---

# SAPCOMMERCE CLOUD{#sap-commerce-cloud}

>[!NOTE]
>
>此頁面包含Hybris網站的連結。 對於某些頁面，您需要帳戶才能登入。

## 使用SAPCommerce Cloud部署eCommerce {#deploying-ecommerce-with-sap-commerce-cloud}

>[!NOTE]
>
>以下程式使用下列示範目錄來說明部署：
>
>`Geometrixx Outdoors Site English (US)`

部署 [必要的電子商務套件](#packages-needed-for-ecommerce-with-hybris) 將提供eCommerce架構的完整功能，以及hybris實作所提供的電子商務功能參考實作（包括示範目錄）

這可在英文（美國）分支下取得( `/content/geometrixx-outdoors/en_US`)的Geometrixx Outdoors網站：

* [產品資訊](#productinformationwithcolorvariants) （在適當時搭配顏色變體）

* [購物車內容概觀](#shoppingcartcontentoverview)
* [客戶註冊](#customersignup) 和 [客戶登入](#customersignin)

* [存取Hybris管理主控台](#accesstothehybrismanagementconsole)

### 技術需求 — hybris伺服器 {#technical-requirements-hybris-server}

更新eCommerce Integration Framework的hybris擴充功能，以支援Hybris 5 （作為預設值），同時維持與的回溯相容性 [Hybris 4](/help/commerce/cif-classic/developing/sap-commerce-cloud.md#developing-for-hybris).

>[!NOTE]
>
>* 支援18.11版及更高版本。
>* 您需要Java 7才能執行 [hybris 5伺服器。](https://www.hybris.com/en/architecture-technology)
>* hybris附加元件， [Telco加速器](https://www.hybris.com/en/products/telecommunication)AEM擴充功能不支援。
>


### 具有hybris的電子商務所需的套件 {#packages-needed-for-ecommerce-with-hybris}

若要安裝電子商務功能，您需要：

* 您的hybris伺服器
* AEM電子商務架構：

   * 這是標準AEM安裝的一部分

* AEM全Geometrixx套件：

   * `cq-geometrixx-all-pkg`

* AEM hybris內容套件：

   * `cq-hybris-content-6.3.2`
   * hybris專屬的API實作
   * `cq-geometrixx-hybris-content-6.3.2`
   * 說明使用hybris ( `geometrixx-outdoors/en_US`)

### 使用Hybris安裝電子商務 {#installation-of-ecommerce-with-hybris}

若要安裝完整的組態(使用示範目錄、Geometrixx Outdoors)，基本步驟如下：

1. [安裝AEM](/help/sites-deploying/deploy.md).
1. 安裝全Geometrixx套件

   1. ` [cq-geometrixx-all-pkg](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq60/product/cq-geometrixx-all-pkg)`

1. 使用安裝示範內容套件 [封裝管理員](/help/sites-administering/package-manager.md)：

   1. ` [cq-hybris-content-6.3.2](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq630/product/cq-hybris-content)`
   1. ` [cq-geometrixx-hybris-content-6.3.2](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq630/product/cq-geometrixx-hybris-content)`

1. [下載並建置您的hybris伺服器](#download-and-build-your-hybris-server).
1. 在電子商務引擎中建構您的目錄：

   1. [設定Geometrixx戶外商店](#setup-the-geometrixx-outdoors-store).

1. [作者](/help/sites-authoring/qg-page-authoring.md) 您在AEM中所需的任何補充頁面。

>[!CAUTION]
>
>使用hybris伺服器需要個別的hybris授權。

>[!NOTE]
>
>適用於開發人員 [API檔案](/help/commerce/cif-classic/developing/ecommerce.md#api-documentation) 也可供下載。

### 下載並建置您的hybris伺服器 {#download-and-build-your-hybris-server}

此程式中的步驟將下載並建置hybris伺服器。 它也會進行hybris和cq之間連線所需的初始設定。 之後，擴充功能即可使用預設設定。

>[!CAUTION]
>
>不支援5.5.1之前的Hybris版本。

>[!NOTE]
>
>若要完成此作業，您需要 [Groovy](https://groovy-lang.org/) 已安裝在您的系統上。

1. 下載 **hybris Commerce Suite** 從hybris下載網站發佈。

   >[!CAUTION]
   >
   >您需要帳戶（來自hybris）才能存取此專案。

1. 將散發檔案解壓縮至所需位置(稱為 &lt;hybris-root-directory>)。
1. 從命令列，執行下列動作：

   ```shell
   cd <hybris-root-directory>/bin/platform
   . ./setantenv.sh
   ant clean all
   cd ../..
   ```

   >[!NOTE]
   >
   >執行時：
   >
   >`ant clean all`
   >
   >按下 `Return` 必要時。

1. 將下列檔案下載至解壓縮的hybris散佈的根資料夾，

   ```
       <hybris-root-directory>
   ```


[获取文件](/help/sites-deploying/assets/setup.groovy)

   >[!NOTE]
   >
   >對於hybris 5.6.0和更新版本，請使用下列setup.groovy。

   5.6.0和更新版本

[获取文件](/help/sites-deploying/assets/setup-1.groovy)

1. 從命令列，執行下列至：

   * 更新hybris伺服器的設定（根據擴充功能的要求）
   * 使用修改後的設定重新建置hybris伺服器
   * 啟動伺服器

   ```shell
   groovy setup.groovy
   cd bin/platform
   ant clean all
   sh hybrisserver.sh
   ```

   >[!NOTE]
   >
   >視您的系統而定，這些步驟中的數個可能需要幾分鐘才能完成。

1. 在您的瀏覽器中，導覽至 **hybris管理主控台** 於：

   [http://localhost:9002](http://localhost:9002)

1. 按一下 **初始化** 然後確認初始化動作（因為它將會刪除現有資料）。

   進度將顯示在主控台上，包含 `FINISHED` 表示完成。

   >[!NOTE]
   >
   >視您的系統而定，這可能需要幾分鐘才能完成。

### 設定Geometrixx Outdoors存放區 {#setup-the-geometrixx-outdoors-store}

此程式將上傳並設定示範存放區 — 線上Geometrixx。

1. 啟動您的hybris執行個體。 從命令列，執行下列動作：

   ```shell
   cd <hybris-root-directory>/bin/platform
   sh hybrisserver.sh
   ```

1. 在您的瀏覽器中，導覽至 **hybris管理主控台** 於：

   [https://localhost:9002/backoffice](https://localhost:9002/backoffice)

   使用這些認證：
   * 使用者名稱：管理員
   * 密碼： nimda

1. 在側欄導覽中，展開 **系統** 和 **工具**. 然後選取 **匯入** 以開啟 **精靈：CSV匯入** 視窗。
1. 在 **設定** 標籤， **上傳** 下列專案 **匯入檔案**：

[获取文件](/help/sites-deploying/assets/geometrixx-outdoors-export.csv)

1. 設定 **地區設定** 至：

   `en_US - English (United States)`

1. 開啟 **資源** 標籤。
1. **上傳** 下列專案 **Media-Zip**：

[获取文件](/help/sites-deploying/assets/geometrixx-outdoors-images.zip)

1. 按一下 **開始** 以匯入指定的檔案。 此 **結果** 索引標籤會顯示任何記錄專案。

1. 按一下 **完成** 以關閉匯入視窗。

1. 從側邊欄中選取 **系統**，則 **工具**，則 **匯入**.

1. **上傳** 下列專案 **匯入檔案**：

[获取文件](/help/sites-deploying/assets/base-store.csv)

   對於hybris 5.7，請使用下列專案：

[获取文件](/help/sites-deploying/assets/base-store-5_7.csv)

1. 設定 **地區設定** 至：

   `en_US - English (United States)`

1. 按一下 **開始** 以匯入指定的檔案。 此 **結果** 索引標籤會顯示任何記錄專案。

1. 按一下 **完成** 以關閉匯入視窗。

1. 您現在可以使用產品駕駛艙來檢視匯入的目錄和產品：

   [http://localhost:9002/productcockpit](http://localhost:9002/productcockpit)
