---
title: 「教學課程：建立您的第一個最適化表單」
seo-title: "Tutorial: Create your first adaptive form"
description: 瞭解如何建立商務級、互動式和回應式表單。
seo-description: Learn to create business class, interactive, and responsive forms.
uuid: ee351a3f-ea6a-4b4c-8045-4948ad51b7c1
topic-tags: introduction
discoiquuid: 1142bcd4-e3a7-41ce-a710-132ae6c21dbe
docset: aem65
feature: Adaptive Forms
exl-id: 77a05f83-ac9a-4221-85ac-439e82623a28
source-git-commit: 318347178fd626dea8e5a15caa7cdad8fe353eba
workflow-type: tm+mt
source-wordcount: '965'
ht-degree: 9%

---

# 教學課程：建立第一個最適化表單 {#tutorial-create-your-first-adaptive-form}

![01-create-first-adaptive-form-hero-image](assets/01-create-first-adaptive-form-hero-image.png)

## 简介 {#introduction}

您是否正在尋找適合行動裝置的產品 **表單體驗** 可簡化註冊程式、增加參與度及縮短週轉時間， **調適型表單** 最適合您。 調適型表單提供適合行動裝置、自動化和分析的表單體驗。 您可以輕鬆建立具有回應式互動性質的表單、使用自動化程式來減少管理和重複工作，以及使用資料分析來改善客戶對表單的體驗並加以個人化。

本教學課程提供建立最適化表單的端對端架構。 本教學課程可組織為一個使用案例和多個指南。 每份指南都可協助您學習並將新功能新增至在本教學課程中建立的最適化表單。 每本指南後，您都有可正常使用的調適型表單。 建立最適化表單的指南已推出。 後續指南即將推出。 在本教學課程結束時，您將能夠：

* 建立最適化表單和表單資料模型。
* 設定最適化表單的樣式。
* 使用最適化表單規則編輯器來建立商業規則。
* 測試並發佈最適化表單。

![create-adaptive-form-workflow](assets/create-daptive-form-workflow.png)

歷程從學習使用案例開始：

網站為不同的客戶提供一系列產品。 客戶瀏覽入口網站、選取及訂購產品。 每個客戶都會建立帳戶，並提供送貨和帳單地址。 現有客戶Sara Rose正尋求將她的運送地址新增至網站。 網站提供線上表單，以新增和更新運送地址。

網站在Adobe Experience Manager (AEM)上執行並使用AEM [!DNL Forms] 以進行資料擷取與處理。 地址新增和更新表單為最適化表單。 網站會將客戶詳細資料儲存在資料庫中。 他們使用地址新增和更新表單來擷取和顯示可用的地址。 他們也會使用最適化表單來接受更新的和新的地址。

### 先决条件 {#prerequisite}

* 設定 [AEM作者執行個體](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/deploying/deploy.html#author-and-publish-installs)
* 安裝 [AEM Forms附加元件](../../forms/using/installing-configuring-aem-forms-osgi.md) 在作者執行個體上。
* 從資料庫提供者取得JDBC資料庫驅動程式（JAR檔案）。 教學課程中的範例是根據 [!DNL MySQL] 資料庫與使用 [!DNL Oracle's] [MySQL JDBC資料庫驅動程式](https://dev.mysql.com/downloads/connector/j/5.1.html).

* 設定包含客戶資料的資料庫，其欄位顯示如下。 資料庫對於建立最適化表單並非必要。 本教學課程使用資料庫來顯示AEM的表單資料模型和持續性功能 [!DNL Forms].

![adaptiveformdata](assets/adaptiveformdata.png)

## 步驟1：建立最適化表單 {#step-create-an-adaptive-form}

![03-create-adaptive-form-main-image_small](assets/03-create-adaptive-form-main-image_small.png)

調適型表單本質上是新一代的、吸引人的、回應式的、動態的和調適型。 使用調適型表單，您可以提供個人化和針對性的體驗。 AEM [!DNL Forms] 提供拖放WYSIWYG編輯器以建立調適型表單。 如需最適化表單的詳細資訊，請參閱 [製作調適型表單簡介](../../forms/using/introduction-forms-authoring.md).

目标：

* 建立可讓客戶新增送貨地址的最適化表單
* 用於顯示和接受客戶資訊的最適化表單的版面配置欄位
* 建立提交動作以傳送包含表單內容的電子郵件
* 預覽和提交最適化表單

[![参阅指南](https://helpx.adobe.com/content/dam/help/en/marketing-cloud/how-to/digital-foundation/_jcr_content/main-pars/image_1250343773/see-the-guide-sm.png)](create-adaptive-form.md)

## 步驟2：建立表單資料模型 {#step-create-form-data-model}

![05-create-form-data-model-main_small](assets/05-create-form-data-model-main_small.png)

表單資料模型允許將最適化表單連線到不同的資料來源。 例如，AEM使用者設定檔、RESTful Web服務、以SOAP為基礎的Web服務、OData服務和關聯式資料庫。 表單資料模型是連線資料來源中可用的商業實體和服務的統一資料表示架構。 您可以搭配最適化表單使用表單資料模型，以擷取、更新、刪除資料，並將其新增至連線的資料來源。

目标：

* 設定網站的資料庫執行個體([!DNL MySQL] database)作為資料來源
* 建立表單資料模型，使用 [!DNL MySQL] 資料庫做為資料來源
* 將資料模型物件新增至表單資料模型
* 設定表單資料模型的讀取和寫入服務
* 測試表單資料模型和已設定的服務（包含測試資料）

[![参阅指南](https://helpx.adobe.com/content/dam/help/en/marketing-cloud/how-to/digital-foundation/_jcr_content/main-pars/image_1250343773/see-the-guide-sm.png)](create-form-data-model.md)

## 步驟3：將規則套用至最適化表單欄位 {#step-apply-rules-to-adaptive-form-fields}

![07-apply-rules-to-adaptive-form_small](assets/07-apply-rules-to-adaptive-form_small.png)

調適型表單提供編輯器，可在調適型表單物件上編寫規則。 這些規則會根據預設條件、使用者輸入和使用者對表單的動作，定義要在表單物件上觸發的動作。 它有助於確保正確性並加速表單填寫體驗。

目标：

* 建立規則並套用至最適化表單欄位
* 使用規則來觸發表單資料模型服務，以將資料更新至資料庫

[![参阅指南](https://helpx.adobe.com/content/dam/help/en/marketing-cloud/how-to/digital-foundation/_jcr_content/main-pars/image_1250343773/see-the-guide-sm.png)](apply-rules-to-adaptive-form-fields.md)

## 步驟4：設定最適化表單的樣式 {#step-style-your-adaptive-form}

![](/help/forms/using/assets/09-style-your-adaptive-form-small.png)

最適化表單提供主題和 [編輯者](../../forms/using/themes.md) 為最適化表單建立主題。 主題包含元件和面板的樣式細節，您可以重複使用不同表單中的主題。 樣式包含背景顏色、狀態顏色、透明度、對齊方式及大小等屬性。 將主題套用至表單時，指定的樣式會反映在表單的對應元件上。 最適化表單也支援表單特定樣式的內嵌樣式。

目标：

* 將現成的主題套用至最適化表單
* 使用主題編輯器為最適化表單建立主題
* 在自訂主題中使用網頁字型

[![参阅指南](https://helpx.adobe.com/content/dam/help/en/marketing-cloud/how-to/digital-foundation/_jcr_content/main-pars/image_1250343773/see-the-guide-sm.png)](style-your-adaptive-form.md)

## 步驟5：發佈最適化表單 {#step-publish-your-adaptive-form}

![12-publish-your-adaptive-form-_small](assets/12-publish-your-adaptive-form-_small.png)

您可以將調適型表單發佈為獨立表單（單頁應用程式），包含在AEM中 [網站頁面](/help/forms/using/embed-adaptive-form-aem-sites.md)，或AEM上的清單 [!DNL Site] 使用 [Forms入口網站](../../forms/using/introduction-publishing-forms.md).

目标：

* 將最適化表單發佈為AEM頁面
* 將最適化表單內嵌於AEM [!DNL Sites] 頁面
* 將最適化表單內嵌於外部網頁(託管在AEM外部的非AEM網頁)中

[![参阅指南](https://helpx.adobe.com/content/dam/help/en/marketing-cloud/how-to/digital-foundation/_jcr_content/main-pars/image_1250343773/see-the-guide-sm.png)](publish-your-adaptive-form.md)
