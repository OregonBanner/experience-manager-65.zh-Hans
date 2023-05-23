---
title: 「教學課程：建立表單資料模型」
seo-title: Create Form Data Model Tutorial
description: 建立表單資料模型
seo-description: Create form data model
uuid: b9d2bb1b-90f0-44f4-b1e3-0603cdf5f5b8
contentOwner: khsingh
products: SG_EXPERIENCEMANAGER/6.3/FORMS
discoiquuid: 12e6c325-ace0-4a57-8ed4-6f7ceee23099
docset: aem65
exl-id: 40bc5af6-9023-437e-95b0-f85d3df7d8aa
source-git-commit: e147605ff4d5c3d2403632285956559db235c084
workflow-type: tm+mt
source-wordcount: '1512'
ht-degree: 1%

---

# 教學課程：建立表單資料模型 {#tutorial-create-form-data-model}

![04-create-form-data-model-main](assets/04-create-form-data-model-main.png)

本教學課程是 [建立第一個最適化表單](../../forms/using/create-your-first-adaptive-form.md) 數列。 建議您依照時間順序觀看本系列，以瞭解、執行和示範完整的教學課程使用案例。

## 關於教學課程 {#about-the-tutorial}

AEM [!DNL Forms] 資料整合模組可讓您從不同的後端資料來源(例如AEM使用者設定檔、RESTful Web服務、以SOAP為基礎的Web服務、OData服務和關聯式資料庫)建立表單資料模型。 您可以在表單資料模型中設定資料模型物件和服務，並將其與最適化表單建立關聯。 最適化表單欄位已繫結至資料模型物件屬性。 這些服務可讓您預填最適化表單，並將提交的表單資料寫入回資料模型物件。

如需表單資料整合和表單資料模型的詳細資訊，請參閱 [AEM Forms資料整合](../../forms/using/data-integration.md).

本教學課程將逐步引導您準備、建立、設定表單資料模型，並將其與最適化表單建立關聯的步驟。 在本教學課程結束時，您將能夠：

* [將MySQL資料庫設定為資料來源](#config-database)
* [使用MySQL資料庫建立表單資料模型](#create-fdm)
* [設定表單資料模型](#config-fdm)
* [測試表單資料模型](#test-fdm)

表單資料模型看起來類似下列：

![form-data-model_l](assets/form-data-model_l.png)

**答：** 已設定的資料來源 **B.** 資料來源結構描述 **C.** 可用服務 **D.** 資料模型物件 **E.** 已設定的服務

## 前提条件 {#prerequisites}

開始之前，請確定您具備下列條件：

* [!DNL MySQL] 包含下列專案之先決條件一節所述範例資料的資料庫： [建立第一個最適化表單](../../forms/using/create-your-first-adaptive-form.md)
* 適用於的OSGi套件組合 [!DNL MySQL] JDBC驅動程式，如中所述 [整合JDBC資料庫驅動程式](/help/sites-developing/jdbc.md#bundling-the-jdbc-database-driver)
* 適用性表單，如第一個教學課程中所述 [建立最適化表單](/help/forms/using/create-adaptive-form.md)

## 步驟1：將MySQL資料庫設定為資料來源 {#config-database}

您可以設定不同型別的資料來源，以建立表單資料模型。 在本教學課程中，我們將設定您設定的MySQL資料庫，並填入範例資料。 如需其他支援的資料來源以及如何設定這些來源的相關資訊，請參閱 [AEM Forms資料整合](../../forms/using/data-integration.md).

執行以下動作來設定您的 [!DNL MySQL] 資料庫：

1. 安裝適用於的JDBC驅動程式 [!DNL MySQL] 資料庫作為OSGi套件：

   1. 下載 [!DNL MySQL] JDBC驅動程式OSGi套件組合來源 `http://www.java2s.com/ref/jar/download-orgosgiservicejdbc100jar-file.html`. <!-- This URL is an insecure link but using https is not possible -->
   1. 登入AEM [!DNL Forms] 以管理員身分製作執行個體，並前往AEM Web主控台套件組合。 預設URL為 [https://localhost:4502/system/console/bundles](https://localhost:4502/system/console/bundles).

   1. 點選 **[!UICONTROL 安裝/更新]**. 一個 [!UICONTROL 上傳/安裝套件組合] 對話方塊隨即顯示。

   1. 點選 **[!UICONTROL 選擇檔案]** 瀏覽並選取 [!DNL MySQL] JDBC驅動程式OSGi套件。 選取 **[!UICONTROL 開始套件組合]** 和 **[!UICONTROL 重新整理封裝]**，然後點選 **[!UICONTROL 安裝或更新]**. 確保 [!DNL Oracle Corporation's] 的JDBC驅動程式 [!DNL MySQL] 處於作用中狀態。 已安裝驅動程式。

1. 設定 [!DNL MySQL] 資料庫做為資料來源：

   1. 前往AEM網頁主控台，網址為 [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr).
   1. 尋找 **Apache Sling Connection Pooled DataSource** 設定。 點選以在編輯模式中開啟設定。
   1. 在設定對話方塊中，指定下列詳細資訊：

      * **資料來源名稱：** 您可以指定任何名稱。 例如，指定 **WeRetailMySQL**.
      * **資料來源服務屬性名稱**：指定包含DataSource名稱的服務屬性名稱。 它是在將資料來源執行個體註冊為OSGi服務時指定的。 例如， **資料來源名稱**.
      * **JDBC驅動程式類別**：指定JDBC驅動程式的Java類別名稱。 對象 [!DNL MySQL] 資料庫，指定 **com.mysql.jdbc.Driver**.
      * **JDBC連線URI**：指定資料庫的連線URL。 對象 [!DNL MySQL] 資料庫執行於連線埠3306和結構描述weretail，URL為： `jdbc:mysql://'server':3306/weretail?autoReconnect=true&useUnicode=true&characterEncoding=utf-8`

      >[!NOTE]
      >
      > 當 [!DNL MySQL] 資料庫位於防火牆之後，則資料庫主機名稱不是公用DNS。 資料庫的IP位址需要新增至 */etc/hosts* AEM主機電腦的檔案。

      * **使用者名稱：** 資料庫的使用者名稱。 必須啟用JDBC驅動程式才能建立與資料庫的連線。
      * **密碼：** 資料庫的密碼。 必須啟用JDBC驅動程式才能建立與資料庫的連線。

      >[!NOTE]
      >
      >AEM Forms不支援NT驗證 [!DNL MySQL]. 前往AEM網頁主控台，網址為 [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr) 和搜尋「Apache Sling Connection Pooled Datasource」。若為「integratedSecurity」的「JDBC連線URI」屬性集值設為False，並使用建立的使用者名稱和密碼來連線 [!DNL MySQL] 資料庫。

      * **借入時測試：** 啟用 **[!UICONTROL 借入時測試]** 選項。
      * **回訪時測試：** 啟用 **[!UICONTROL 回訪時測試]** 選項。
      * **驗證查詢：** 指定SQL SELECT查詢來驗證集區的連線。 查詢至少必須傳回一列。 例如， **選取 &#42; 從customerdetails**.
      * **交易隔離**：將值設為 **READ_COMMITTED**.

         保留其他屬性為預設值 [值](https://tomcat.apache.org/tomcat-7.0-doc/jdbc-pool.html) 並點選 **[!UICONTROL 儲存]**.

         會建立類似下列的設定。

         ![relational-database-data-source-configuration](assets/relational-database-data-source-configuration.png)



## 步驟2：建立表單資料模型 {#create-fdm}

AEM [!DNL Forms] 提供直覺式使用者介面，用於 [建立表單資料模型](data-integration.md) 來自已設定的資料來源。 您可以在表單資料模型中使用多個資料來源。 在我們的使用案例中，我們將使用已設定的 [!DNL MySQL] 資料來源。

執行下列操作以建立表單資料模型：

1. 在AEM編寫執行個體中，導覽至 **[!UICONTROL Forms]** > **[!UICONTROL 資料整合]**.
1. 點選 **[!UICONTROL 建立]** > **[!UICONTROL 表單資料模型]**.
1. 在建立表單資料模型對話方塊中，指定 **名稱** 用於表單資料模型。 例如， **customer-shipping-billing-details**. 點選 **[!UICONTROL 下一個]**.
1. 選取資料來源畫面會列出所有已設定的資料來源。 選取 **WeRetailMySQL** 資料來源並點選 **[!UICONTROL 建立]**.

   ![data-source-selection](assets/data-source-selection.png)

此 **customer-shipping-billing-details** 表單資料模型已建立。

## 步驟3：設定表單資料模型 {#config-fdm}

設定表單資料模型涉及：

* 新增資料模型物件與服務
* 設定資料模型物件的讀取和寫入服務

執行下列操作以設定表單資料模型：

1. 在AEM作者執行個體上，導覽至 **[!UICONTROL Forms]** > **[!UICONTROL 資料整合]**. 預設URL為 [https://localhost:4502/aem/forms.html/content/dam/formsanddocuments-fdm](https://localhost:4502/aem/forms.html/content/dam/formsanddocuments-fdm).
1. 此 **customer-shipping-billing-details** 此處列出您先前建立的表單資料模型。 在編輯模式下開啟它。

   選取的資料來源 **WeRetailMySQL** 已在表單資料模型中設定。

   ![default-fdm](assets/default-fdm.png)

1. 展開WeRailMySQL資料來源樹狀結構。 從以下資料模型物件和服務中選取 **Weretail** > **customerdetails** 要建立資料模型的結構描述：

   * **資料模型物件**：

      * id
      * name
      * shippingAddress
      * 城市
      * 状态
      * 邮政编码
   * **服务:**

      * get
      * 更新

   點選 **新增選取專案** 將選取的資料模型物件和服務新增至表單資料模型。

   ![WeRetail結構](assets/weretail_schema_new.png)

   >[!NOTE]
   >
   >JDBC資料來源的預設get、update和insert服務隨表單資料模型一起提供現成可用。

1. 設定資料模型物件的讀取和寫入服務。

   1. 選取 **customerdetails** 資料模型物件並點選 **[!UICONTROL 編輯屬性]**.
   1. 選取 **[!UICONTROL get]** 從「讀取服務」下拉式清單。 此 **id** 引數，會自動新增customerdetails資料模型物件中的主索引鍵。 點選 ![aem_6_3_edit](assets/aem_6_3_edit.png) 並依照以下方式設定引數。

      ![read-default](assets/read-default.png)

   1. 同樣地，選取 **[!UICONTROL 更新]** 做為寫入服務。 此 **customerdetails** 物件會自動新增為引數。 引數的設定如下。

      ![write-default](assets/write-default.png)

      新增並設定 **id** 引數如下。

      ![id-arg](assets/id-arg.png)

   1. 點選 **[!UICONTROL 完成]** 以儲存資料模型物件屬性。 然後，點選 **[!UICONTROL 儲存]** 以儲存表單資料模型。

      此 **[!UICONTROL get]** 和 **[!UICONTROL 更新]** 服務會新增為資料模型物件的預設服務。

      ![data-model-object](assets/data-model-object.png)

1. 前往 **[!UICONTROL 服務]** 標籤並設定 **[!UICONTROL get]** 和 **[!UICONTROL 更新]** 服務。

   1. 選取 **[!UICONTROL get]** 服務並點選 **[!UICONTROL 編輯屬性]**. 屬性對話方塊開啟。
   1. 在「編輯屬性」對話方塊中指定下列專案：

      * **標題**：指定服務的標題。 例如：擷取送貨地址。
      * **說明**：指定包含服務詳細功能的說明。 例如：

         此服務會從擷取送貨地址和其他客戶詳細資料 [!DNL MySQL] 資料庫

      * **輸出模型物件**：選取包含客戶資料的結構描述。 例如：

         customerdetail結構描述

      * **傳回陣列**：停用 **傳回陣列** 選項。
      * **引數**：選取名為的引數 **ID**.

      點選 **[!UICONTROL 完成]**. 已設定從MySQL資料庫擷取客戶詳細資訊的服務。

      ![shiping-address-retrieval](assets/shiiping-address-retrieval.png)

   1. 選取 **[!UICONTROL 更新]** 服務並點選 **[!UICONTROL 編輯屬性]**. 屬性對話方塊開啟。

   1. 在「 」中指定以下內容 [!UICONTROL 編輯屬性] 對話方塊：

      * **標題**：指定服務的標題。 例如，更新送貨地址。
      * **說明**：指定包含服務詳細功能的說明。 例如：

         此服務會更新MySQL資料庫中的送貨地址和相關欄位

      * **輸入模型物件**：選取包含客戶資料的結構描述。 例如：

         customerdetail結構描述

      * **輸出型別**：選取 **布林值**.

      * **引數**：選取名為的引數 **ID** 和 **customerdetails**.
      點選 **[!UICONTROL 完成]**. 此 **[!UICONTROL 更新]** 更新客戶詳細資料的服務 [!DNL MySQL] 資料庫已設定。

      ![shiping-address-update](assets/shiiping-address-update.png)



已設定表單資料模型中的資料模型物件和服務。 您現在可以測試表單資料模型。

## 步驟4：測試表單資料模型 {#test-fdm}

您可以測試資料模型物件和服務，以確認表單資料模型已正確設定。

執行下列操作以執行測試：

1. 前往 **[!UICONTROL 模型]** 索引標籤中，選取 **customerdetails** 資料模型物件，然後點選 **[!UICONTROL 測試模型物件]**.
1. 在 [!UICONTROL 測試模型/服務] 視窗，選取 **[!UICONTROL 讀取模型物件]** 從 **[!UICONTROL 選取模型/服務]** 下拉式清單。
1. 在 **customerdetails** 區段，指定 **id** 存在於設定中的引數 [!DNL MySQL] 資料庫並點選 **[!UICONTROL 測試]**.

   系統會擷取與指定ID相關聯的客戶詳細資訊，並顯示在 **[!UICONTROL 輸出]** 區段，如下所示。

   ![test-read-model](assets/test-read-model.png)

1. 同樣地，您可以測試Write模型物件和服務。

   在下列範例中，更新服務已成功更新資料庫中ID7102715位址的詳細資訊。

   ![test-write-model](assets/test-write-model.png)

   現在，如果您再次測試id 7107215的讀取模式服務，它將擷取並顯示更新的客戶詳細資訊，如下所示。

   ![已讀取 — 已更新](assets/read-updated.png)
