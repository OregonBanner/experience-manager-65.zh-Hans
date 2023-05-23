---
title: 「教學課程：在AEM Forms中建立表單資料模型」
description: 建立互動式通訊的表單資料模型
uuid: b56d3dac-be54-4812-b958-38a085686218
contentOwner: anujkapo
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: e5413fb3-9d50-4f4f-9db8-7e53cd5145d5
docset: aem65
feature: Interactive Communication
exl-id: c8a6037c-46bd-4058-8314-61cb925ba5a8
source-git-commit: a2fd3c0c1892ac648c87ca0dec440e22144c37a2
workflow-type: tm+mt
source-wordcount: '2739'
ht-degree: 0%

---

# 教學課程：在AEM Forms中建立表單資料模型{#tutorial-create-form-data-model}

![04-create-form-data-model-main](assets/04-create-form-data-model-main.png)

本教學課程是 [建立您的第一個互動式通訊](/help/forms/using/create-your-first-interactive-communication.md) 數列。 建議您依照時間順序觀看本系列，以瞭解、執行和示範完整的教學課程使用案例。

## 關於教學課程 {#about-the-tutorial}

AEM Forms資料整合模組可讓您從不同的後端資料來源(例如AEM使用者設定檔、RESTful Web服務、以SOAP為基礎的Web服務、OData服務和關聯式資料庫)建立表單資料模型。 您可以在表單資料模型中設定資料模型物件和服務，並將其與最適化表單建立關聯。 最適化表單欄位已繫結至資料模型物件屬性。 這些服務可讓您預填最適化表單，並將提交的表單資料寫入回資料模型物件。

如需表單資料整合和表單資料模型的詳細資訊，請參閱 [AEM Forms資料整合](https://helpx.adobe.com/experience-manager/6-3/forms/using/data-integration.html).

本教學課程將引導您完成準備、建立、設定表單資料模型，並將其與互動式通訊建立關聯的步驟。 在本教學課程結束時，您將能夠：

* [設定資料庫](../../forms/using/create-form-data-model0.md#step-set-up-the-database)
* [將MySQL資料庫設定為資料來源](../../forms/using/create-form-data-model0.md#step-configure-mysql-database-as-data-source)
* [建立表單資料模型](../../forms/using/create-form-data-model0.md#step-create-form-data-model)
* [設定表單資料模型](../../forms/using/create-form-data-model0.md#step-configure-form-data-model)
* [測試表單資料模型](../../forms/using/create-form-data-model0.md#step-test-form-data-model-and-services)

表單資料模型看起來類似下列：

![表單資料模型](assets/form_data_model_callouts_new.png)

**答：** 已設定的資料來源 **B.** 資料來源結構描述 **C.** 可用服務 **D.** 資料模型物件 **E.** 已設定的服務

## 前提条件 {#prerequisites}

開始之前，請確定您具備下列條件：

* 含有範例資料的MySQL資料庫，如 [設定資料庫](../../forms/using/create-form-data-model0.md#step-set-up-the-database) 區段。
* 適用於MySQL JDBC驅動程式的OSGi套件組合，如中所述 [整合JDBC資料庫驅動程式](https://helpx.adobe.com/experience-manager/6-3/help/sites-developing/jdbc.html#bundling-the-jdbc-database-driver)

## 步驟1：設定資料庫 {#step-set-up-the-database}

資料庫是建立互動式通訊的必要條件。 本教學課程使用資料庫來顯示表單資料模型和互動式通訊的持續性功能。 設定包含客戶、帳單和呼叫表格的資料庫。
下圖說明customer表格的範例資料：

![sample_data_cust](assets/sample_data_cust.png)

使用下列DDL陳述式來建立 **客戶** 資料庫的資料表。

```sql
CREATE TABLE `customer` (
   `mobilenum` int(11) NOT NULL,
   `name` varchar(45) NOT NULL,
   `address` varchar(45) NOT NULL,
   `alternatemobilenumber` int(11) DEFAULT NULL,
   `relationshipnumber` int(11) DEFAULT NULL,
   `customerplan` varchar(45) DEFAULT NULL,
   PRIMARY KEY (`mobilenum`),
   UNIQUE KEY `mobilenum_UNIQUE` (`mobilenum`)
 ) ENGINE=InnoDB DEFAULT CHARSET=utf8
```

使用下列DDL陳述式來建立 **帳單** 資料庫的資料表。

```sql
CREATE TABLE `bills` (
   `billplan` varchar(45) NOT NULL,
   `latepayment` decimal(4,2) NOT NULL,
   `monthlycharges` decimal(4,2) NOT NULL,
   `billdate` date NOT NULL,
   `billperiod` varchar(45) NOT NULL,
   `prevbal` decimal(4,2) NOT NULL,
   `callcharges` decimal(4,2) NOT NULL,
   `confcallcharges` decimal(4,2) NOT NULL,
   `smscharges` decimal(4,2) NOT NULL,
   `internetcharges` decimal(4,2) NOT NULL,
   `roamingnational` decimal(4,2) NOT NULL,
   `roamingintnl` decimal(4,2) NOT NULL,
   `vas` decimal(4,2) NOT NULL,
   `discounts` decimal(4,2) NOT NULL,
   `tax` decimal(4,2) NOT NULL,
   PRIMARY KEY (`billplan`)
 ) ENGINE=InnoDB DEFAULT CHARSET=utf8
```

使用下列DDL陳述式來建立 **呼叫** 資料庫的資料表。

```sql
CREATE TABLE `calls` (
   `mobilenum` int(11) DEFAULT NULL,
   `calldate` date DEFAULT NULL,
   `calltime` varchar(45) DEFAULT NULL,
   `callnumber` int(11) DEFAULT NULL,
   `callduration` varchar(45) DEFAULT NULL,
   `callcharges` decimal(4,2) DEFAULT NULL,
   `calltype` varchar(45) DEFAULT NULL
 ) ENGINE=InnoDB DEFAULT CHARSET=utf8
```

此 **呼叫** 此表格包含通話詳細資訊，例如，通話日期、通話時間、通話號碼、通話期間和通話費用。 此 **客戶** 表格會使用「行動電話號碼(mobilenum)」欄位連結至通話表格。 針對每個列出的行動電話號碼 **客戶** 表格中，有多個記錄 **呼叫** 表格。 例如，您可以擷取以下專案的呼叫詳細資料： **1457892541** 行動電話號碼(透過參考 **呼叫** 表格。

此 **帳單** 此表格包含帳單明細，例如，帳單日期、帳單期間、每月費用及通話費用。 此 **客戶** 表格連結至 **帳單** 使用「帳單計畫」欄位建立表格。 有一個計畫與中的每個客戶相關聯 **客戶** 表格。 此 **帳單** 表格包含所有現有計畫的訂價明細。 例如，您可以擷取計畫詳細資訊 **Sarah** 從 **客戶** 表格並使用這些詳細資料來擷取訂價詳細資訊 **帳單** 表格。

## 步驟2：將MySQL資料庫設定為資料來源 {#step-configure-mysql-database-as-data-source}

您可以設定不同型別的資料來源，以建立表單資料模型。 在本教學課程中，您將設定已設定並填入範例資料的MySQL資料庫。 如需其他支援的資料來源以及如何設定這些來源的相關資訊，請參閱 [AEM Forms資料整合](https://helpx.adobe.com/experience-manager/6-3/forms/using/data-integration.html).

執行下列操作來設定您的MySQL資料庫：

1. 以OSGi套件安裝MySQL資料庫的JDBC驅動程式：

   1. 以管理員身分登入AEM Forms作者執行個體，並前往AEM網頁主控台套件組合。 預設URL為 [https://localhost:4502/system/console/bundles](https://localhost:4502/system/console/bundles).
   1. 點選 **安裝/更新**. 一個 **上傳/安裝套件組合** 對話方塊隨即顯示。

   1. 點選 **選擇檔案** 瀏覽並選取MySQL JDBC驅動程式OSGi套件。 選取 **開始套件組合** 和 **重新整理封裝**，然後點選 **安裝** 或 **更新**. 請確定Oracle Corporation的MySQL的JDBC驅動程式作用中。 已安裝驅動程式。

1. 將MySQL資料庫設定為資料來源：

   1. 前往AEM網頁主控台，網址為 [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr).
   1. 尋找 **Apache Sling Connection Pooled DataSource** 設定。 點選以在編輯模式中開啟設定。
   1. 在設定對話方塊中，指定下列詳細資訊：

      * **資料來源名稱：** 您可以指定任何名稱。 例如，指定 **MySQL**.

      * **資料來源服務屬性名稱**：指定包含DataSource名稱的服務屬性名稱。 它是在將資料來源執行個體註冊為OSGi服務時指定的。 例如， **資料來源名稱**.

      * **JDBC驅動程式類別**：指定JDBC驅動程式的Java類別名稱。 對於MySQL資料庫，請指定 **com.mysql.jdbc.Driver**.

      * **JDBC連線URI**：指定資料庫的連線URL。 對於在連線埠3306和結構描述teleca上執行的MySQL資料庫，URL是： `jdbc:mysql://'server':3306/teleca?autoReconnect=true&useUnicode=true&characterEncoding=utf-8`
      * **使用者名稱：** 資料庫的使用者名稱。 必須啟用JDBC驅動程式才能建立與資料庫的連線。
      * **密碼：** 資料庫的密碼。 必須啟用JDBC驅動程式才能建立與資料庫的連線。
      * **借入時測試：** 啟用 **借入時測試** 選項。

      * **回訪時測試：** 啟用 **回訪時測試** 選項。

      * **驗證查詢：** 指定SQL SELECT查詢來驗證集區的連線。 查詢至少必須傳回一列。 例如， **選取 &#42; 來自客戶**.

      * **交易隔離**：將值設為 **READ_COMMITTED**.
   保留其他屬性為預設值 [值](https://tomcat.apache.org/tomcat-7.0-doc/jdbc-pool.html) 並點選 **儲存**.

   會建立類似下列的設定。

   ![Apache設定](assets/apache_configuration_new.png)

## 步驟3：建立表單資料模型 {#step-create-form-data-model}

AEM Forms提供直覺式使用者介面，可 [建立表單資料模式](https://helpx.adobe.com/experience-manager/6-3/forms/using/data-integration.html#main-pars_header_1524967585)l來自已設定的資料來源。 您可以在表單資料模型中使用多個資料來源。 針對本教學課程的使用案例，您將使用MySQL作為資料來源。

執行下列操作以建立表單資料模型：

1. 在AEM編寫執行個體中，導覽至 **Forms** > **資料整合**.
1. 點選 **建立** > **表單資料模型**.
1. 在建立表單資料模型精靈中，指定 **名稱** 用於表單資料模型。 例如， **FDM_Create_First_IC**. 點選 **下一個**.
1. 選取資料來源畫面會列出所有已設定的資料來源。 選取 **MySQL** 資料來源並點選 **建立**.

   ![MYSQL資料來源](assets/fdm_mysql_data_source_new.png)

1. 按一下 **完成**. 此 **FDM_Create_First_IC** 表單資料模型已建立。

## 步驟4：設定表單資料模型 {#step-configure-form-data-model}

設定表單資料模型包含：

* [新增資料模型物件和服務](#add-data-model-objects-and-services)
* [建立資料模型物件的計運算元屬性](#create-computed-child-properties-for-data-model-object)
* [新增資料模型物件之間的關聯](#add-associations-between-data-model-objects)
* [編輯資料模型物件屬性](#edit-data-model-object-properties)
* [為資料模型物件設定服務](#configure-services)

### 新增資料模型物件和服務 {#add-data-model-objects-and-services}

1. 在AEM作者執行個體上，導覽至 **Forms** > **資料整合**. 預設URL為 [https://localhost:4502/aem/forms.html/content/dam/formsanddocuments-fdm](https://localhost:4502/aem/forms.html/content/dam/formsanddocuments-fdm).
1. 此 **FDM_Create_First_IC** 此處列出您先前建立的表單資料模型。 選取並點選 **編輯**.

   選取的資料來源 **MySQL** 會顯示在 **資料來源** 窗格。

   ![FDM的MYSQL資料來源](assets/mysql_fdm_new.png)

1. 展開 **MySQL** 資料來源樹狀結構。 從以下資料模型物件和服務中選取 **teleca** 綱要：

   * **資料模型物件**：

      * 帳單
      * 呼叫
      * 客戶
   * **服务:**

      * get
      * 更新

   點選 **新增選取專案** 將選取的資料模型物件和服務新增至表單資料模型。

   ![選取資料模型物件服務](assets/select_data_model_object_services_new.png)

   帳單、呼叫和客戶資料模型物件會顯示在的右窗格 **模型** 標籤。 取得和更新服務會顯示在 **服務** 標籤。

   ![資料模型物件](assets/data_model_objects_new.png)

### 建立資料模型物件的計運算元屬性 {#create-computed-child-properties-for-data-model-object}

計算屬性是根據規則或運算式計算其值的屬性。 您可以使用規則將計算屬性的值設定為常值字串、數字、數學運算式的結果或表單資料模型中其他屬性的值。

根據使用案例，建立 **使用費用** 中的子計算屬性 **帳單** 資料模型物件使用下列數學運算式：

* 使用費=通話費+電話會議費+ SMS費+行動網際網路費+漫遊國家+漫遊國際+ VAS （所有這些屬性都存在於帳單資料模型物件中）如需詳細資訊，請參閱 **使用費用** 子計算屬性，請參閱 [規劃互動式通訊](/help/forms/using/planning-interactive-communications.md).

執行以下步驟來建立用料表資料模型物件的計運算元屬性：

1. 選取上方的核取方塊 **帳單** 資料模型物件以選取並點選 **建立子屬性**.
1. 在 **建立子屬性** 窗格：

   1. 輸入 **使用費用** 做為子屬性的名稱。
   1. 啟用 **已計算**.
   1. 選取 **浮點數** 作為型別並點選 **完成** 將子屬性新增至 **帳單** 資料模型物件。

   ![建立子屬性](assets/create_child_property_new.png)

1. 點選 **編輯規則** 以開啟規則編輯器。
1. 點選 **建立**. 此 **設定值** 規則視窗隨即開啟。
1. 從選取選項下拉式清單中選取 **數學運算式**.

   ![使用量收費規則編輯器](assets/usage_charges_rule_editor_new.png)

1. 在數學運算式中，選取 **callcharges** 和 **confcallcharges** 分別做為第一和第二物件。 選取 **加** 作為運運算元。 在數學運算式中點選，然後點選 **延伸運算式** 新增 **smscharges**， **網際費用**， **roamingnational**， **roamingintel**、和 **vas** 物件至運算式。

   下圖說明規則編輯器中的數學運算式：

   ![使用量費用規則](assets/usage_charges_rule_all_new.png)

1. 點選 **完成**. 規則會在規則編輯器中建立。
1. 點選 **關閉** 以關閉「規則編輯器」視窗。

### 新增資料模型物件之間的關聯 {#add-associations-between-data-model-objects}

定義資料模型物件後，您就可以建立它們之間的關聯。 關聯可以是一對一或一對多。 例如，一個員工可以有多個相依關係。 它稱為一對多關聯，在連線關聯資料模型物件的線上以1：n表示。 不過，如果關聯針對指定的員工ID傳回唯一員工名稱，則稱為一對一關聯。

當您將資料來源中的關聯資料模型物件新增至表單資料模型時，它們的關聯會保留並顯示為以箭頭線連線。

根據使用案例，在資料模型物件之間建立下列關聯：

| 關聯 | 資料模型物件 |
|---|---|
| 1：n | customer：calls （每月帳單中可將多個來電與客戶相關聯） |
| 1:1 | customer：bills （一張帳單與特定月份的客戶相關聯） |

執行以下步驟來建立資料模型物件之間的關聯：

1. 選取上方的核取方塊 **客戶** 資料模型物件以選取並點選 **新增關聯**. 此 **新增關聯** 屬性窗格開啟。
1. 在 **新增關聯** 窗格：

   * 指定關聯的標題。 此為選用欄位。
   * 選取 **一對多** 從 **型別** 下拉式清單。

   * 選取 **呼叫** 從 **模型物件** 下拉式清單。

   * 選取 **get** 從 **服務** 下拉式清單。

   * 點選 **新增** 連結 **客戶** 資料模型物件至 **呼叫** 使用屬性的資料模型物件。 根據使用案例，呼叫資料模型物件必須連結至客戶資料模型物件中的行動號碼屬性。 此 **新增引數** 對話方塊開啟。

   ![新增關聯](assets/add_association_new.png)

1. 在 **新增引數** 對話方塊：

   * 選取 **mobilenum** 從 **名稱** 下拉式清單。 行動號碼屬性是客戶中可用的常見屬性，可呼叫資料模型物件。 因此，它可用來建立customer與呼叫資料模型物件之間的關聯。
對於客戶資料模型物件中可用的每個行動電話號碼，呼叫表格中有多個可用的呼叫記錄。

   * 指定引數的選用標題和說明。
   * 選取 **客戶** 從 **繫結至** 下拉式清單。

   * 選取 **mobilenum** 從 **繫結值** 下拉式清單。

   * 點選 **新增**.

   ![新增引數的關聯](assets/add_association_argument_new.png)

   mobilenum屬性會顯示在 **引數** 區段。

   ![新增引數關聯](assets/add_argument_association_new.png)

1. 點選 **完成** 在客戶和呼叫資料模型物件之間建立1：n關聯。

   在客戶與呼叫資料模型物件之間建立關聯後，在客戶與帳單資料模型物件之間建立1:1關聯。

1. 選取上方的核取方塊 **客戶** 資料模型物件以選取並點選 **新增關聯**. 此 **新增關聯** 屬性窗格開啟。
1. 在 **新增關聯** 窗格：

   * 指定關聯的標題。 此為選用欄位。
   * 選取 **一對一** 從 **型別** 下拉式清單。

   * 選取 **帳單** 從 **模型物件** 下拉式清單。

   * 選取 **get** 從 **服務** 下拉式清單。 此 **billplan** 屬性是bills表格的主索引鍵，已可在 **引數** 區段。
帳單與客戶資料模型物件分別使用帳單計畫(bills)與客戶計畫(customerplan)屬性進行連結。 在這些屬性之間建立繫結，以擷取MySQL資料庫中任何可用客戶的計畫詳細資訊。

   * 選取 **客戶** 從 **繫結至** 下拉式清單。

   * 選取 **customerplan** 從 **繫結值** 下拉式清單。

   * 點選 **完成** 建立billplan和customerplan屬性之間的繫結。

   ![新增客戶帳單的關聯](assets/add_association_customer_bills_new.png)

   下列影像說明資料模型物件與用來建立它們之間關聯的屬性之間的關聯：

   ![fdm_associations](assets/fdm_associations.gif)

### 編輯資料模型物件屬性 {#edit-data-model-object-properties}

在客戶與其他資料模型物件之間建立關聯後，編輯客戶屬性以定義屬性，系統會根據此屬性從資料模型物件中擷取資料。 根據使用案例，行動電話號碼會作為屬性，以從客戶資料模型物件中擷取資料。

1. 選取上方的核取方塊 **客戶** 資料模型物件以選取並點選 **編輯屬性**. 此 **編輯屬性** 窗格開啟。
1. 指定 **客戶** 作為 **頂層模型物件**.
1. 選取 **get** 從 **讀取服務** 下拉式清單。
1. 在 **引數** 區段：

   * 選取 **請求屬性** 從 **繫結至** 下拉式清單。

   * 指定 **mobilenum** 做為繫結值。

1. 選取 **更新** 從 **寫入** 「服務」下拉式清單。
1. 在 **引數** 區段：

   * 對象 **mobilenum** 屬性，選取 **客戶** 從 **繫結至** 下拉式清單。

   * 選取 **mobilenum** 從 **繫結值** 下拉式清單。

1. 點選 **完成** 以儲存屬性。

   ![設定服務](assets/configure_services_customer_new.png)

1. 選取上方的核取方塊 **呼叫** 資料模型物件以選取並點選 **編輯屬性**. 此 **編輯屬性** 窗格開啟。
1. 停用 **頂層模型物件** 的 **呼叫** 資料模型物件。
1. 點選 **完成**.

   重複步驟8 - 10以設定屬性 **帳單** 資料模型物件。

### 設定服務 {#configure-services}

1. 前往 **服務** 標籤。
1. 選取 **get** 服務並點選 **編輯屬性**. 此 **編輯屬性** 窗格開啟。
1. 在 **編輯屬性** 窗格：

   * 輸入選用的標題和說明。
   * 選取 **客戶** 從 **輸出模型物件** 下拉式清單。

   * 點選 **完成** 以儲存屬性。

   ![编辑属性](assets/edit_properties_get_details_new.png)

1. 選取 **更新** 服務並點選 **編輯屬性**. 此 **編輯屬性** 窗格開啟。
1. 在 **編輯屬性** 窗格：

   * 輸入選用的標題和說明。
   * 選取 **客戶** 從 **輸入模型物件** 下拉式清單。

   * 點選 **完成**.
   * 點選 **儲存** 以儲存表單資料模型。

   ![更新服務屬性](assets/update_service_properties_new.png)

## 步驟5：測試表單資料模型與服務 {#step-test-form-data-model-and-services}

您可以測試資料模型物件和服務，以確認表單資料模型已正確設定。

執行下列操作以執行測試：

1. 前往 **模型** 索引標籤中，選取 **客戶** 資料模型物件，然後點選 **測試模型物件**.
1. 在 **測試表單資料模型** 視窗，選取 **讀取模型物件** 從 **選取模型/服務** 下拉式清單。
1. 在 **輸入** 區段，指定 **mobilenum** 已設定之MySQL資料庫中存在的屬性，然後點選 **測試**.

   會擷取與指定mobilenum屬性相關聯的客戶詳細資訊，並顯示在「輸出」區段中，如下所示。 關閉對話方塊。

   ![測試資料模型](assets/test_data_model_new.png)

1. 前往 **服務** 標籤。
1. 選取 **get** 服務並點選 **測試服務。**
1. 在 **輸入** 區段，指定 **mobilenum** 已設定之MySQL資料庫中存在的屬性，然後點選 **測試**.

   會擷取與指定mobilenum屬性相關聯的客戶詳細資訊，並顯示在「輸出」區段中，如下所示。 關閉對話方塊。

   ![測試服務](assets/test_service_new.png)

### 編輯並儲存範例資料 {#edit-and-save-sample-data}

表單資料模型編輯器可讓您為表單資料模型中的所有資料模型物件屬性（包括計算屬性）產生範例資料。 這是一組隨機值，符合為每個屬性設定的資料型別。 您也可以編輯並儲存資料，即使您重新產生範例資料，也會保留資料。

執行下列動作，產生、編輯和儲存範例資料：

1. 在表單資料模型頁面上，點選 **編輯範例資料**. 它會在「編輯範例資料」視窗中產生並顯示範例資料。

   ![編輯範例資料](assets/edit_sample_data_new.png)

1. 在 **編輯範例資料** 視窗，視需要編輯資料，然後點選 **儲存**. 關閉視窗。
