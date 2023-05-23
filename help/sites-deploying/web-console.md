---
title: Adobe Experience Manager中的Web控制檯
seo-title: Web Console
description: 瞭解如何使用AEM Web主控台。
seo-description: Learn how to use the AEM web console.
uuid: 7856b2b3-4216-421d-a315-cd9a55936362
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: configuring
discoiquuid: 4a33fddd-0399-40e4-8687-564fb6765b76
feature: Configuring
exl-id: 9acbf61f-73a8-4998-9421-dd933f30ac8a
source-git-commit: a17b25e55a0bf16a0df42a7ba4768503618a19e2
workflow-type: tm+mt
source-wordcount: '722'
ht-degree: 1%

---

# Web 控制台{#web-console}

AEM中的Web主控台是以 [Apache Felix Web管理主控台](https://felix.apache.org/documentation/subprojects/apache-felix-web-console.html). Apache Felix是社群致力於實作OSGi R4服務平台，其中包括OSGi框架和標準服務。

>[!NOTE]
>
>在Web主控台上，提及預設設定的任何說明都與Sling預設值有關。
>
>AEM有自己的預設值，因此預設集可能與控制檯上記錄的有所不同。

Web主控台提供一系列用於維護OSGi套裝的標籤，包括：

* [設定](#configuration)：用於設定OSGi套件組合，因此是設定AEM系統引數的基礎機制
* [套裝](#bundles)：用於安裝套件組合
* [元件](#components)：用於控制AEM所需元件的狀態

所做的任何變更都會立即套用至執行中的系統。 不需要重新啟動。

控制檯可從以下位置存取： `../system/console`；例如：

`http://localhost:4502/system/console/components`

## 配置 {#configuration}

此 **設定** tab可用來設定OSGi組合，因此是設定AEM系統引數的基礎。

>[!NOTE]
>
>另請參閱 [使用Web主控台進行OSGi設定](/help/sites-deploying/configuring-osgi.md) 以取得更多詳細資料。

此 **設定** 索引標籤可透過以下任一方式存取：

* 下拉式功能表：

   **OSGi >**

* URL；例如：

   `http://localhost:4502/system/console/configMgr`

將會顯示設定清單：

![screen_shot_2012-02-15at52308pm](assets/screen_shot_2012-02-15at52308pm.png)

此畫面上的下拉式清單提供兩種型別的設定：

* **設定**
可讓您更新現有設定。 這些具有持續性身分(PID)，可以是：

   * 標準，是AEM不可或缺的一部分；若刪除這些值，則會傳回預設設定。
   * 從「工廠組態」建立的執行處理；這些執行處理是由使用者建立的，刪除會移除執行處理。

* **工廠組態**
可讓您建立所需功能物件的例項。

   這將會被分配一個持續性身分，然後會列在設定下拉式清單中。

從清單中選取任何專案，都會顯示與該組態相關的引數：

![chlimage_1-21](assets/chlimage_1-21a.png)

之後，您可以視需要更新引數，並且：

* **保存**

   儲存所做的變更。

   對於Factory Configuration，這將建立具有永久識別的新執行個體。 然後，新執行個體將列在「設定」下。

* **重置**

   將熒幕上顯示的引數重設為上次儲存的引數。

* **删除**

   刪除目前的設定。 若為標準，引數會傳回預設設定。 如果是從「工廠組態」建立，則會刪除特定的執行處理。

* **解除繫結**

   從套件組合中解除繫結目前設定。

* **取消**

   取消任何目前的變更。

## 套裝 {#bundles}

此 **套裝** tab是安裝AEM所需的OSGi套件組合的機制。 可透過下列其中一種方法來存取索引標籤：

* 下拉式功能表：

   **OSGi >**

* URL；例如：

   `http://localhost:4502/system/console/bundles`

將會顯示套件組合清單：

![screen_shot_2012-02-15at44740pm](assets/screen_shot_2012-02-15at44740pm.png)

使用此索引標籤，您可以：

* **安裝或更新**

   您可以 **瀏覽** 以尋找包含您的套件組合的檔案，並指定它是否應 **開始** 立即且 **開始層級**.

* **重新加载**

   重新整理顯示的清單。

* **重新整理封裝**

   這將檢查所有套件的參考，並在必要時重新整理。

   例如，在更新之後，由於先前的參照，舊版本和新版本可能仍在執行。 此選項將檢查並移動新版本的所有參考，允許舊版本停止。

* **启动**

   根據指定的開始層級啟動組合。

* **停止**

   停止該組合。

* **卸载**

   從系統解除安裝該套裝。

* **檢視狀態**

   清單會指定束的目前狀態；按一下包含進一步資訊的特定束的名稱即可顯示進一步的資訊。

>[!NOTE]
>
>晚於 **更新** 建議執行 **重新整理封裝**.

## 组件 {#components}

此 **元件** 索引標籤可讓您啟用和/或停用各種元件。 您可透過以下任一方式存取該區域：

* 下拉式功能表：

   **主要 >**

* URL；例如：

   `http://localhost:4502/system/console/components`

隨即顯示元件清單。 有各種圖示可讓您啟用、停用或（視情況而定）開啟特定元件的組態詳細資訊。

![screen_shot_2012-02-15at52144pm](assets/screen_shot_2012-02-15at52144pm.png)

按一下特定元件的名稱會顯示其狀態的進一步資訊。 您也可以在此處啟用、停用或重新載入元件。

![chlimage_1-22](assets/chlimage_1-22a.png)

>[!NOTE]
>
>啟用或停用元件只會套用到AEM/CRX重新啟動為止。
>
>開始狀態是在元件描述項中定義，在開發期間產生並在套件建立時儲存在套件中。
