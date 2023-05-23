---
title: 翻譯使用者產生的內容
seo-title: Translating User Generated Content
description: 翻譯功能的運作方式
seo-description: How the translation feature works
uuid: 7ee3242c-2aca-4787-a60d-b807161401ad
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: bfaf80c5-448b-47fb-9f22-57ee0eb169b2
role: Admin
exl-id: ac54f06e-1545-44bb-9f8f-970f161ebb72
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '1108'
ht-degree: 0%

---

# 翻譯使用者產生的內容 {#translating-user-generated-content}

AEM Communities的翻譯功能進一步擴展了 [翻譯頁面內容](../../help/sites-administering/translation.md) 發佈至社群網站的使用者產生內容(UGC)，使用 [社交元件架構(SCF)元件](scf.md).

UGC的翻譯可讓網站訪客和成員移除語言障礙，體驗全球社群。

例如，假設：

* 一位來自法國的成員在多國烹飪網站的社群論壇中張貼法文食譜。
* 來自日本的另一位成員使用該翻譯功能來觸發配方從法文翻譯成日文。
* 在閱讀日文的食譜後，這位日本成員便發表日文的評論。
* 來自法國的成員使用翻譯功能將日文註解翻譯成法文。
* 全球通訊。

## 概述 {#overview}

本檔案本節具體說明翻譯服務如何與UGC搭配運作，並假設您瞭解如何將AEM連線至 [翻譯服務提供者](../../help/sites-administering/translation.md#connectingtoatranslationserviceprovider) 並透過設定 [翻譯整合框架](../../help/sites-administering/tc-tic.md).

當翻譯服務提供者與網站相關聯時，網站的每個語言副本都會維護其透過SCF元件（例如註解）張貼的UGC對話串。

除了翻譯服務提供者之外，當設定翻譯整合框架時，網站的每個語言副本都可以共用單一UGC對話串，因此提供跨語言副本的全球通訊。 不是由語言分隔的討論對話串，而是設定的 [全域共用存放區](#global-translation-of-ugc) 無論檢視的是哪種語言副本，都能顯示整個對話串。 此外，可以設定多個翻譯整合設定，為全域參與者的邏輯分組（例如按區域）指定不同的全域共用存放區。

## 預設翻譯服務 {#the-default-translation-service}

AEM Communities包含 [試用授權](../../help/sites-administering/tc-msconf.md#microsoft-translator-trial-license) 對於 [預設翻譯服務](../../help/sites-administering/tc-msconf.md) 已啟用多種語言。

時間 [建立社群網站](sites-console.md)，預設翻譯服務會在以下情況下啟用： `Allow Machine Translation` 「 」已勾選 [翻譯](sites-console.md#translation) 子面板。

>[!CAUTION]
>
>預設翻譯服務僅供示範。
>
>對於生產系統，需要授權的翻譯服務。 若未授權，預設翻譯服務應為 [關閉](../../help/sites-administering/tc-msconf.md#microsoft-translator-trial-license-geometrixx-outdoors).

## UGC的全球翻譯 {#global-translation-of-ugc}

當網站有多個時 [語言副本](../../help/sites-administering/tc-prep.md)，預設翻譯服務無法辨識一個網站上輸入的UGC是否可能與另一個網站上輸入的UGC有關，因為該UGC基本上是由相同元件（包含元件的頁面語言副本）產生。

這類似於討論主題的人群，他們不知道自己以外的群組正在發表評論，而大型群組中的每個人都參與同一個對話。

如果需要「一個群組對話」，則可以在具有多種語言副本的網站上啟用全域翻譯，以便檢視整個對話串，無論檢視的是哪種語言副本。

例如，如果在基本網站上建立論壇、建立語言副本，並啟用全域翻譯，則以單一語言副本發佈到論壇的主題將顯示在所有語言副本中。 無論輸入回覆的語言副本為何，任何回覆亦然。 結果，無論檢視主題所用的語言副本為何，都會顯示主題及其整個回覆對話串。

>[!CAUTION]
>
>全域翻譯之前存在的任何UGC都不再可見。
>
>當UGC仍然在 [公用存放區](working-with-srp.md)，而位於特定語言的UGC位置底下，同時從全域共用存放區位置擷取設定全域翻譯後新增的新內容。
>
>沒有移轉工具可將特定語言的內容移動或合併至全域共用存放區。

### 翻譯整合設定 {#translation-integration-configuration}

若要建立新的翻譯整合，將翻譯服務聯結器與作者執行個體上的網站整合：

* 以管理員身分登入
* 從 [主功能表](http://localhost:4502/)
* 選取 **[!UICONTROL 工具]**
* 選取 **[!UICONTROL 作業]**
* 選取 **[!UICONTROL 雲端]**
* 選取 **[!UICONTROL Cloud Services]**
* 向下捲動至 **[!UICONTROL 翻譯整合]**

   ![translation-integration](assets/translation-integration.png)

* 選取 **[!UICONTROL 顯示設定]**

   ![show-configuration](assets/translation-integration1.png)

* 選取 `[+]` 圖示旁邊 **[!UICONTROL 可用的設定]** 以建立新組態

#### 建立設定對話方塊 {#create-configuration-dialog}

![create-configuration](assets/translation-integration2.png)

* **[!UICONTROL 父配置]**

   （必要）通常會保留為預設值。 預設為 `/etc/cloudservices/translation`.

* **[!UICONTROL 标题]**

   （必要）輸入您選擇的顯示標題。 無預設值。

* **[!UICONTROL 名称]**

   （選擇性）輸入組態的名稱。 預設值是根據標題的節點名稱。

* 選取 **[!UICONTROL 建立]**

#### 翻譯設定對話方塊 {#translation-config-dialog}

![configuration-dialog](assets/translation-integration3.png)

如需詳細指示，請造訪 [建立翻譯整合設定](../../help/sites-administering/tc-tic.md#creating-a-translation-integration-configuration)

* **[!UICONTROL 網站]** tab：可保留為預設值。

* **[!UICONTROL Communities]** 標籤：
   * **[!UICONTROL 翻譯提供者]**
從下拉式清單中選取翻譯提供者。 預設為 
`microsoft`，此為試用服務。

   * **[!UICONTROL 內容類別]**
選取說明正在翻譯之內容的類別。 預設為 
`General.`

   * **[!UICONTROL 選擇地區……]**
（選擇性）選取儲存UGC的語言環境，所有語言副本的貼文都會出現在同一個全域對話中。 依照慣例，選擇 [基本語言](sites-console.md#translation) 適用於網站。 選擇 `No Common Store` 將會停用全域翻譯。 預設會停用全域翻譯。

* **[!UICONTROL 資產]** tab：可保留為預設值。
* 選取 **[!UICONTROL 確定]**

#### 激活 {#activation}

發佈環境需要啟動新的翻譯整合雲端服務。 與網站建立關聯時，如果尚未啟動，則啟動工作流程會在發佈此雲端服務設定的關聯頁面時提示發佈此雲端服務設定。

## 管理翻譯設定 {#managing-translation-settings}

>[!NOTE]
>
>**偏好語言**
>
>為了偵測貼文的語言是否與慣用語言不同，必須建立網站訪客的慣用語言。
>
>偏好語言是網站訪客登入且已指定語言偏好設定時，使用者設定檔中設定的語言偏好設定。
>
>當網站訪客為匿名或未在其設定檔中指定語言偏好設定時，偏好的語言是頁面範本的基本語言。

### 使用者偏好設定 {#user-preference}

#### 用户配置文件 {#user-profile}

所有社群網站都會提供使用者設定檔，登入的成員可以編輯此設定檔，以在社群中識別自己並設定其偏好設定。

其中一項設定是是否一律以偏好語言顯示社群內容。 預設不會設定此設定，而是預設為系統設定。 使用者可以將設定變更為開啟或關閉，藉此覆寫系統設定。

當頁面自動翻譯成使用者偏好的語言時，仍提供用於顯示原始文字和改善翻譯的UI。

![user-profile](assets/translation-integration4.png)

### 社群網站設定 {#community-site-setting}

建立社群網站時，可啟用並設定翻譯選項。 此翻譯設定對匿名網站訪客可檢視的內容有效，但會被使用者的設定檔設定覆寫。
