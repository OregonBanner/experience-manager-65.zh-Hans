---
title: 設定輸出的快取
seo-title: Configuring caching for Output
description: 輸出服務可快取表單設計、片段和影像。 瞭解如何設定輸出的快取。
seo-description: The Output service caches the form designs, fragments and images. Learn how to configure the caching for output.
uuid: 00bffeb5-c9c4-4a46-98b5-e14ec9f4514e
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_output
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: e5398abd-f62c-485d-9f4b-a316c0de2b6b
exl-id: 1015f5c9-6ab8-4656-a5c8-40f82b9938b9
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1440'
ht-degree: 0%

---

# 設定輸出的快取  {#configuring-caching-for-output}

Output服務會合併XML表單資料與在Designer中建立的表單設計，以建立各種格式的檔案輸出資料流。

Administration Console中的Output頁面包含控制Output服務快取專案方式的設定。 您可以調整這些設定，以最佳化Output服務的效能。

Output服務會快取下列專案：

* **表單設計：** Output服務會根據設計從存放庫或HTTP來源擷取快取。 此快取可改善效能，因為對於後續的轉譯要求，Output服務會從快取中擷取表單設計，而不是從存放庫擷取。
* **片段和影像：** 輸出服務可以快取表單設計中使用的片段和影像。 當Output服務快取這些物件時，它會改善效能，因為片段和影像只有在第一次請求時才會從存放庫讀取。

輸出會將快取儲存在兩個位置：

* **在記憶體中：** 專案會儲存在記憶體中，以便快速存取。 記憶體中的快取記憶體大小有限，當您重新啟動伺服器時會刪除它。
* **在磁碟上：** 專案會儲存在伺服器的檔案系統中。 磁碟快取的容量大於記憶體中的快取，而且會在您重新啟動伺服器時保留。 磁碟快取的位置取決於您的應用程式伺服器。 有關變更磁碟快取位置的資訊，請參閱 [指定輸出的檔案位置](/help/forms/using/admin-help/specify-file-locations-output.md#specify-file-locations-for-output).

## 指定快取模式 {#specifying-the-cache-mode}

輸出支援兩種快取模式：

* 無條件
* 使用快取檢查點

如果您在快取模式之間切換，請重新啟動Output服務以使變更生效。 若要重新啟動此服務，請使用Workbench或參閱 [啟動或停止與AEM表單模組關聯的服務](/help/forms/using/admin-help/starting-stopping-services.md#start-or-stop-the-services-associated-with-aem-forms-modules) 以取得指示。

當您在模式之間切換時，會自動重設快取檢查點時間。

### 使用無條件快取 {#using-unconditional-caching}

在此模式中，當輸出服務收到請求時，會驗證所需的資源（表單設計和任何相關資產，例如片段和影像）。 Output服務會將存放庫中的資源時間戳記與快取中的資源時間戳記進行比較。 如果快取中的資源較舊，則輸出服務會進行更新。

此快取模式可確保使用最新的資源。 不過，效能會受到影響，因為Output服務會在每次請求時根據存放庫驗證快取的專案。 此快取模式適用於開發和中繼環境，因為這類環境會經常更新資源，而且效能不是主要考量。

**指定無條件快取**

1. 在Administration Console中，按一下「服務>輸出」。
1. 在「輸出快取控制設定」下，選取無條件並按一下「儲存」。

### 使用快取檢查點 {#use-the-cache-check-point}

在此模式中，只有當快取資源的時間戳記早於快取檢查點時間時，Output服務才會檢查存放庫是否有較新版本的資源。 最後一個快取檢查點時間會顯示在管理控制檯的「輸出」頁面上。

在高效能生產環境中，使用這個快取模式會考量效能問題，而且很少變更資源。 當您想要部署對存放庫資源所做的任何變更時，可以重設快取檢查點。

**指定使用快取檢查點**

1. 在Administration Console中，按一下「服務>輸出」。
1. 在「輸出快取控制設定」下方，選取只有當其上次驗證是在快取檢查點時間之前完成時，然後按一下「儲存」。

**重設快取檢查點**

1. 在Administration Console中，按一下「服務>輸出」。
1. 在「輸出快取控制設定」下，按一下「快取檢查點」。

### 重設快取內容 {#reset-the-cache-contents}

您可以隨時清除快取的內容。 快取重設後，每個表單的第一個請求速度會變慢，因為Output服務會執行完整的轉譯並建立新的快取內容。

1. 在Administration Console中，按一下「服務>輸出」。
1. 在「輸出快取控制設定」下，按一下「重設快取」。

## 正在設定快取設定 {#configuring-cache-settings}

您可以指定輸出用於快取的設定，這會最佳化AEM表單環境的效能。

若要存取這些設定，請在Administration Console中按一下「服務>輸出」。

>[!NOTE]
>
>快取的磁碟需求應等於存放庫。

### 指定全域快取設定 {#specifying-global-cache-settings}

中的設定 **全域快取設定** 區域會影響所有快取型別。 如果您變更其中一項設定，請重新啟動Output服務以使變更生效。 若要重新啟動此服務，請使用Workbench或參閱 [啟動或停止與AEM表單模組關聯的服務](/help/forms/using/admin-help/starting-stopping-services.md#start-or-stop-the-services-associated-with-aem-forms-modules) 以取得指示。

**快取檔案大小上限(KB)：** 可儲存在任何記憶體內快取記憶體中的表單設計或其他資源的大小上限（以KB為單位）。 此全域設定適用於所有記憶體中的快取。 如果資源大於此值，則不會在記憶體中快取。 預設值為1024 KB。 此設定不會影響磁碟快取。

**表單轉譯快取已啟用：** 依預設，此選項處於選取狀態，這表示已快取呈現的表單以供後續擷取。 此設定對Output服務的效能幾乎沒有影響，因為它不會快取非互動式檔案。 當您使用Output服務來輸出使用者端上轉譯的非互動式檔案時，此選項確實有效。

### 快取表單設計 {#caching-form-designs}

當輸出服務收到轉譯器請求時，會從存放庫或HTTP來源擷取表單設計並加以快取。 此快取可改善效能，因為對於後續的轉譯要求，Output服務會從快取中擷取表單設計，而不是從存放庫擷取。

Output服務一律會從磁碟設計快取。 如果表單設計儲存在伺服器上，則這些檔案會被視為磁碟快取。 Output服務也會根據 **記憶體中的範本快取** 區域。 如果您變更這些設定，請重新啟動Output服務以使變更生效。 若要重新啟動此服務，請使用Workbench或參閱 [啟動或停止與AEM表單模組關聯的服務](/help/forms/using/admin-help/starting-stopping-services.md#start-or-stop-the-services-associated-with-aem-forms-modules) 以取得指示。

**範本組態快取大小：** 要保留在記憶體中的範本組態物件數目上限。 默认值为 100。建議將此值設定為大於或等於「範本快取大小」值。 此設定不會影響磁碟快取。

**範本快取大小：** 要保留在記憶體中的範本內容物件數上限。 默认值为 100。此設定不會影響磁碟快取。

**已啟用：** 預設會選取此核取方塊，表示表單範本會快取到記憶體中。 未選取此選項時，表單範本只會快取在磁碟上。

### 快取片段和影像 {#caching-fragments-and-images}

Output服務會快取磁碟上表單設計中使用的片段和影像。 這樣可改善效能，因為片段和影像僅在第一次請求時才會從存放庫讀取。 接著，在後續的請求中，輸出服務會從磁碟快取讀取片段和影像。 片段和影像隻會快取在磁碟上，而不會在記憶體中。

您可以使用下列設定來控制磁碟上片段和影像的快取。 這些設定位於 **範本資源快取設定** 區域：

**資源快取** 從清單中選取下列其中一個選項：

**為片段和影像啟用：** 輸出服務可快取片段和影像。 這是預設選項。

**為片段啟用：** 輸出服務快取片段，但不快取影像。

**已停用：** 輸出服務不會快取片段或影像。

**清除間隔（秒）：** 指定Output服務移除舊版無效快取檔案的頻率。 輸出服務未移除有效的快取檔案。 如果您變更清除間隔，請重新啟動Output服務以使變更生效。 若要重新啟動此服務，請使用Workbench，或參閱啟動或停止與AEM表單模組相關聯的服務以取得指示。

## 快取的叢集考量事項 {#clustering-considerations-for-caches}

在叢集環境中，每個節點都會維護自己的記憶體內部和磁碟快取。 每個節點上的快取內容取決於該節點上已轉譯的表單。

叢集的每個節點上的快取位置必須相同（相同的磁碟和路徑）。 請勿將快取放在共用儲存體上。

如果您使用Administration Console中的「輸出」頁面來變更特定節點的快取設定值，則當請求進入該節點時，會更新其他節點上的快取設定值。 此行為也會套用至「重設快取」按鈕。 如果您按一下某個節點的「重設快取」按鈕，則會立即從該節點移除快取。 當請求進入其他節點時，會清除該節點上的快取。
