---
title: 使用AEM Forms存放庫
seo-title: Working with AEM Forms Repository
description: 管理AEM Forms存放庫，以使用Java API和Web服務API建立資料夾、寫入、清單、讀取、更新和搜尋資源。 此外，瞭解如何建立資源關係、鎖定和刪除資源。
seo-description: Manage AEM Forms repository to create folders, write, list, read, update resources, and search resources using the Java API and Web Service API. In addition, learn how to create resource relationships, lock and delete resources.
uuid: 6ead49f9-ca0d-4ee4-86a6-0a9ced6ec4f8
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: d2c95881-6c02-4e34-85af-84607df54287
role: Developer
exl-id: a07e51ca-fea0-4719-8071-1b7e805de2ae
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '9117'
ht-degree: 0%

---

# 使用AEM Forms存放庫 {#working-with-aem-forms-repository}

**本檔案中的範例和範例僅適用於JEE環境上的AEM Forms 。**

**關於存放庫服務**

存放庫服務可為AEM Forms提供資源儲存和管理服務。 當開發人員建立 *AEM Forms* 應用程式後，他們便可以部署存放庫中的資產，而非檔案系統。 資產可包含任何型別的附屬資料，包括XML表單、PDF forms(包括Acrobat表單)、表單片段、影像、設定檔、原則、SWF檔案、DDX檔案、XML結構描述、WSDL檔案和測試資料。

例如，假設下列名為的Forms應用程式 *應用程式/表單應用程式*：

![ww_ww_formrepository](assets/ww_ww_formrepository.png)

請注意，FormsFolder中有一個名為Loan.xdp的檔案。 若要存取此表單設計，請指定完整路徑（包括版本）： `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.

>[!NOTE]
>
>如需使用Workbench建立Forms應用程式的詳細資訊，請參閱 [Workbench說明](https://www.adobe.com/go/learn_aemforms_workbench_63).

位於AEM Forms存放庫中的資源路徑為：

`Applications/Application-name/Application-version/Folder.../Filename`

下列值顯示一些URI值的範例：

* Applications/AppraisalReport/1.0/Forms/FullForm.xdp
* Applications/AnotherApp/1.1/Assets/picture.jpg
* Applications/SomeApp/2.0/Resources/Data/XSDs/MyData.xsd

>[!NOTE]
>
>您可以使用網頁瀏覽器瀏覽AEM Forms存放庫。 若要瀏覽存放庫，請在網頁瀏覽器中輸入下列URL `https://[server name]:[server port]/repository`. 您可以使用網頁瀏覽器來驗證與「使用AEM Forms存放庫」區段關聯的快速入門結果。 例如，如果您將內容新增至AEM Forms存放庫，即可在網頁瀏覽器中檢視內容。 (請參閱 [快速入門（SOAP模式）：使用Java API編寫資源](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-writing-a-resource-using-the-java-api).)

存放庫API提供了許多操作，可用於儲存和檢索存放庫中的資訊。 例如，當處理應用程式時需要資源時，您可以取得資源清單或擷取儲存於存放庫中的特定資源。

>[!NOTE]
>
>存放庫API無法用於與內容服務互動（已棄用）。 若要與內容服務（已棄用）互動，請使用檔案管理API。

使用存放庫服務API，您可以完成下列工作：

* 创建文件夹. 另請參閱 [建立資料夾](aem-forms-repository.md#creating-folders).
* 寫入資源及其屬性。 另請參閱 [寫入資源](aem-forms-repository.md#writing-resources).
* 列出指定集合中或其他相關資源的資源。 另請參閱 [列出資源](aem-forms-repository.md#listing-resources).
* 讀取資源及其屬性。 另請參閱 [正在讀取資源](aem-forms-repository.md#reading-resources).
* 更新資源及其屬性。 另請參閱 [更新資源](aem-forms-repository.md#updating-resources).
* 搜尋資源，包括其歷史記錄、相關資源和屬性。 另請參閱 [搜尋資源](aem-forms-repository.md#searching-for-resources).
* 指定資源之間的關係。 另請參閱 [建立資源關係](aem-forms-repository.md#creating-resource-relationships).
* 管理資源存取控制，包括鎖定和解鎖資源，以及讀取和寫入存取控制清單(ACL)。 另請參閱 [鎖定資源](aem-forms-repository.md#locking-resources).
* 刪除資源及其屬性。 另請參閱 [刪除資源](aem-forms-repository.md#deleting-resources).

>[!NOTE]
>
>使用存放庫API時，您無法使用ECM存放庫管理資源存取控制、搜尋資源或指定資源關係。

>[!NOTE]
>
>將加密的PDF寫入存放庫時，無法使用自動關係擷取功能。 否則，加密的PDF可以儲存在存放庫中，並於稍後擷取。 從PDF存放庫中擷取事件後，擷取器可以選擇將它解密。

>[!NOTE]
>
>如需儲存庫服務的詳細資訊，請參閱 [AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63).

## 建立資料夾 {#creating-folders}

資料夾（資源集合）可用來將物件（檔案或資源）儲存在有組織的群組中。 資料夾可以包含資源和其他資料夾，也稱為子資料夾。 資源一次只能儲存在一個資料夾中。

檔案從資料夾繼承存取控制清單(ACL)，子資料夾從其父資料夾繼承ACL。 因此，在建立子資料夾之前，父資料夾必須存在。 IDE僅允許您逐個資料夾進行互動，而不是逐個檔案進行互動。 您無法對資料夾進行版本設定，因此沒有必要這樣做；資料夾本身並不包含資料。 反之，它只是包含資料之資源的容器。 預設ACL是系統層級的許可權，這表示使用者必須擁有系統層級的許可權（讀取、寫入、周遊、管理ACL），直到有人授予他們特定檔案夾的許可權為止。 ACL只能在IDE中運作。

>[!NOTE]
>
>如需儲存庫服務的詳細資訊，請參閱 [AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63).

### 步驟摘要 {#summary-of-steps}

若要建立資料夾，請執行下列步驟：

1. 包含專案檔案。
1. 建立服務使用者端。
1. 建立資料夾。
1. 將資料夾寫入存放庫。

**包含專案檔案**

在您的開發專案中包含必要的檔案。 如果您使用Java建立使用者端應用程式，請包含必要的JAR檔案。 如果您使用Web服務，請包含Proxy檔案。

**建立服務使用者端**

您必須先建立連線並提供認證，才能以程式設計方式建立資源集合。 這是透過建立服務使用者端來完成。

**建立資料夾**

叫用存放庫服務方法建立資源集合，並填入識別資訊的資源集合，包括其UUID、資料夾名稱和說明。

**將資料夾寫入存放庫**

叫用存放庫服務方法來寫入資源集合，指定目標資料夾的URI。

**另请参阅**

[使用Java API建立資料夾](aem-forms-repository.md#create-folders-using-the-java-api)

[使用Web服務API建立資料夾](aem-forms-repository.md#create-folders-using-the-web-service-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[存放庫服務API快速啟動](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### 使用Java API建立資料夾 {#create-folders-using-the-java-api}

使用存放庫服務API (Java)建立資料夾：

1. 包含專案檔案

   將專案檔案包含在Java專案的類別路徑中。

1. 建立服務使用者端

   建立 `ResourceRepositoryClient` 物件，使用它的建構函式並傳遞 `ServiceClientFactory` 包含連線屬性的物件。

1. 建立資料夾

   若要建立資源集合，您必須先建立 `com.adobe.repository.infomodel.bean.RepositoryInfomodelFactoryBean` 物件。

   叫用 `repositoryInfomodelFactoryBean` 物件的 `newResourceCollection` 方法，並傳入下列引數：

   * A `com.adobe.repository.infomodel.Id` 要指派給資源的UUID識別碼。
   * A `com.adobe.repository.infomodel.Lid` 要指派給資源的UUID識別碼。
   * A `java.lang.String` 包含資源集合的名稱。 例如：`FormsFolder`。

   方法會傳回 `com.adobe.repository.infomodel.bean.ResourceCollection` 代表新資料夾的物件。

   使用設定資料夾的說明 `setDescription` 方法並傳遞下列引數：

   * A `String` 描述資源集合。 在此範例中， `"test Folder"` 已使用 `.`


1. 將資料夾寫入存放庫

   叫用 `ResourceRepositoryClient` 物件的 `writeResource` 方法並傳入資料夾的URI和 `ResourceCollection` 物件。 例如，資料夾的URI可以是以下值 `/Applications/FormsApplication/1.0/`.

   方法會傳回新建立的例項 `com.adobe.repository.infomodel.bean.Resource` 物件。 例如，您可以透過叫用 `com.adobe.repository.infomodel.bean.Resource` 物件的 `getId` 方法。

**另请参阅**

[建立資料夾](aem-forms-repository.md#creating-folders)

[快速入門（SOAP模式）：使用Java API建立資料夾](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-creating-a-folder-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服務API建立資料夾 {#create-folders-using-the-web-service-api}

使用存放庫服務API （Web服務）建立資料夾：

1. 包含專案檔案

   * 使用base64建立使用存放庫WSDL的Microsoft .NET使用者端元件。
   * 參考Microsoft .NET使用者端元件。

1. 建立服務使用者端

   使用Microsoft .NET使用者端元件，建立 `RepositoryServiceService` 物件，透過叫用其預設建構函式。 設定其 `Credentials` 屬性使用 `System.Net.NetworkCredential` 包含使用者名稱和密碼的物件。

1. 建立資料夾

   使用「 」的預設建構函式建立資料夾 `ResourceCollection` 類別並傳遞下列引數：

   * 一個 `Id` 物件，這是透過叫用預設建構函式建立的 `Id` 類別並指派給 `Resource` 物件的 `id` 欄位。
   * 一個 `Lid` 物件，這是透過叫用預設建構函式建立的 `Lid` 類別並指派給 `Resource` 物件的 `lid` 欄位。
   * 包含資源集合名稱的字串，該資源集合會指派給 `Resource` 物件的 `name` 欄位。 此範例中使用的名稱為 `"testfolder"`.
   * 包含資源集合說明的字串，該資源集合說明已指派給 `Resource` 物件的 `description` 欄位。 此範例中使用的說明為 `"test folder"`.

1. 將資料夾寫入存放庫

   叫用 `RepositoryServiceService` 物件的 `writeResource` 方法並傳遞下列引數：

   * 要建立資料夾的路徑。
   * 此 `ResourceCollection` 代表資料夾的物件。
   * 通過 `null` 其他兩個引數的設定值。

**另请参阅**

[建立資料夾](aem-forms-repository.md#creating-folders)

[使用Base64編碼叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## 寫入資源 {#writing-resources}

您可以在存放庫中的指定位置建立資源。 自然檔案大小受資料庫限制和工作階段逾時影響。 對於預設設定，檔案限製為25 MB。 若要提高或降低檔案大小上限，您必須變更資料庫組態。

寫入資源等同於將資料儲存在存放庫中。 將資源寫入存放庫後，存放庫生態系統中的所有使用者端都可存取該資源。 將資源（例如XML結構描述、XDP檔案和XSD檔案）寫入存放庫時，會根據MIME型別來剖析內容。 如果支援MIME型別，剖析器會判斷是否有與其他內容的隱含關係。 例如，如果階層式樣式表(CSS)具有參照通用CSS的相對URL，您應該也會將通用CSS提交至存放庫。 兩個資源之間的關係會儲存為未決關係，為期30天，不可調整。 當您在30天內將通用CSS提交至存放庫時，就會建立關係。

當您建立資源時，存取控制清單(ACL)繼承自父資料夾。 在建立初始資源或資料夾之前，根資料夾具有系統層級的許可權，此時資源或資料夾會獲得預設的ACL許可權。

您可以使用存放庫服務Java API或Web服務API，以程式設計方式寫入資源。

>[!NOTE]
>
>如需儲存庫服務的詳細資訊，請參閱 [AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63).

### 步驟摘要 {#summary_of_steps-1}

若要寫入資源，請遵循下列步驟：

1. 包含專案檔案。
1. 建立存放庫服務使用者端。
1. 指定要讀取的資源的URI。
1. 讀取資源。

**包含專案檔案**

在您的開發專案中包含必要的檔案。 如果您使用Java建立使用者端應用程式，請包含必要的JAR檔案。 如果您使用Web服務，請包含Proxy檔案。

**建立服務使用者端**

您必須先建立連線並提供認證，才能以程式設計方式讀取資源。 這是透過建立服務使用者端來完成。

**指定資源目標資料夾的URI**

建立包含要讀取之資源URI的字串。 語法包括正斜線，如以下範例所示：「/*路徑*/*資料夾*「。

**建立資源**

叫用存放庫服務方法來建立資源，並將識別資訊（包括其UUID、資源名稱和說明）填入資源。

**指定資源內容**

叫用存放庫服務方法建立資源內容，並將該內容儲存在資源中。

**將資源寫入目標資料夾**

叫用存放庫服務方法來寫入資源，指定目標資料夾的URI。

**另请参阅**

[使用Java API編寫資源](aem-forms-repository.md#write-resources-using-the-java-api)

[使用Web服務API寫入資源](aem-forms-repository.md#write-resources-using-the-web-service-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[存放庫服務API快速啟動](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### 使用Java API編寫資源 {#write-resources-using-the-java-api}

使用存放庫服務API (Java)編寫資源：

1. 包含專案檔案

   在您的Java專案的類別路徑中包含使用者端JAR檔案。

1. 建立服務使用者端

   建立 `ResourceRepositoryClient` 物件，使用它的建構函式並傳遞 `ServiceClientFactory` 包含連線屬性的物件。

1. 指定資源目標資料夾的URI

   指定資源目標資料夾的URI。 在此案例中，因為資源命名為 `testResource` 將會儲存在名為的資料夾中 `testFolder`，資料夾的URI為 `"/testFolder"`. URI會儲存為 `java.lang.String` 物件。

1. 建立資源

   若要建立資源，您必須先建立 `com.adobe.repository.infomodel.bean.RepositoryInfomodelFactoryBean` 物件。

   叫用 `RepositoryInfomodelFactoryBean` 物件的 `newResource` 方法，會建立 `com.adobe.repository.infomodel.bean.Resource` 物件。 在此範例中，提供下列引數：

   * A `com.adobe.repository.infomodel.Id` 物件，這是透過叫用預設建構函式建立的 `Id` 類別。
   * A `com.adobe.repository.infomodel.Lid` 物件，這是透過叫用預設建構函式建立的 `Lid` 類別。
   * A `java.lang.String` 包含資源的檔案名稱。

   若要指定資源的說明，請叫用 `Resource` 物件的 `setDescription` 方法並傳遞包含說明的字串。 在此範例中，說明為 `"test resource"`.

1. 指定資源內容

   若要建立資源的內容，請叫用 `RepositoryInfomodelFactoryBean` 物件的 `newResourceContent` 方法，會傳回 `com.adobe.repository.infomodel.bean.ResourceContent` 物件。 將內容新增至 `ResourceContent` 物件。 在此範例中，這是透過執行下列工作來完成：

   * 叫用 `ResourceContent` 物件的 `setDataDocument` 方法和傳入 `com.adobe.idp.Document` 物件
   * 叫用 `ResourceContent` 物件的 `setSize` 方法並傳入的大小（位元組） `Document` 物件

   透過叫用將內容新增到資源 `Resource` 物件的 `setContent` 方法並傳入 `ResourceContent` 物件。 如需詳細資訊，請參閱 [AEM Forms API參考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

1. 將資源寫入目標資料夾

   叫用 `ResourceRepositoryClient` 物件的 `writeResource` 方法並傳入資料夾的URI，以及 `Resource` 物件。

**另请参阅**

[寫入資源](aem-forms-repository.md#writing-resources)

[快速入門（SOAP模式）：使用Java API編寫資源](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-writing-a-resource-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服務API寫入資源 {#write-resources-using-the-web-service-api}

使用存放庫服務API （Web服務）寫入資源：

1. 包含專案檔案

   * 使用base64建立使用存放庫WSDL的Microsoft .NET使用者端元件。
   * 參考Microsoft .NET使用者端元件。

1. 建立服務使用者端

   使用Microsoft .NET使用者端元件，建立 `RepositoryServiceService` 物件，透過叫用其預設建構函式。 設定其 `Credentials` 屬性使用 `System.Net.NetworkCredential` 包含使用者名稱和密碼的物件。

1. 指定資源目標資料夾的URI

   指定資源目標資料夾的URI。 在此案例中，因為資源命名為 `testResource` 將會儲存在名為的資料夾中 `testFolder`，資料夾的URI為 `"/testFolder"`. 使用與Microsoft .NET Framework相容的語言時（例如C#），請將URI儲存在 `System.String` 物件。

1. 建立資源

   若要建立資源，請叫用預設建構函式 `Resource` 類別。 在此範例中，下列資訊儲存在 `Resource` 物件：

   * A `com.adobe.repository.infomodel.Id` 物件，這是透過叫用預設建構函式建立的 `Id` 類別並指派給 `Resource` 物件的 `id` 欄位。
   * A `com.adobe.repository.infomodel.Lid` 物件，這是透過叫用預設建構函式建立的 `Lid` 類別並指派給 `Resource` 物件的 `lid` 欄位。
   * 包含指派給資源的檔案名稱的字串。 `Resource` 物件的 `name` 欄位。 此範例中使用的名稱為 `"testResource"`.
   * 包含資源說明(已指派給 `Resource` 物件的 `description` 欄位。 此範例中使用的說明為 `"test resource"`.

1. 指定資源內容

   若要建立資源的內容，請叫用預設建構函式 `ResourceContent` 類別。 然後將內容新增至 `ResourceContent` 物件。 在此範例中，這是透過執行下列工作來完成：

   * 指派 `BLOB` 包含檔案的物件至 `ResourceContent` 物件的 `dataDocument` 欄位。
   * 指派的大小（位元組） `BLOB` 物件至 `ResourceContent` 物件的 `size` 欄位。

   透過指派以下專案將內容新增至資源： `ResourceContent` 物件至 `Resource` 物件的 `content` 欄位。

1. 將資源寫入目標資料夾

   叫用 `RepositoryServiceService` 物件的 `writeResource` 方法並傳入資料夾的URI，以及 `Resource` 物件。 通過 `null` 其他兩個引數的設定值。

**另请参阅**

[寫入資源](aem-forms-repository.md#writing-resources)

[使用Base64編碼叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## 列出資源 {#listing-resources}

您可以透過列出資源來探索資源。 系統會針對存放庫執行查詢，以尋找與指定資源集合相關的所有資源。

組織資源後，您可以透過檢視結構的特定分支來檢查您建立的結構，就像在作業系統中操作一樣。

列出資源會依關係操作：資源是資料夾的成員。 成員資格由「member of」型別的關係表示。 當您在指定資料夾中列出資源時，會查詢與關係「member of」指定的資料夾相關的資源。 關係是方向性的：關係的成員具有作為目標成員的來源。 來源是資源；目標是父資料夾。

>[!NOTE]
>
>如需儲存庫服務的詳細資訊，請參閱 [AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63).

### 步驟摘要 {#summary_of_steps-2}

若要列出資源，請遵循下列步驟：

1. 包含專案檔案。
1. 建立服務使用者端。
1. 指定資料夾路徑。
1. 擷取資源清單。

**包含專案檔案**

在您的開發專案中包含必要的檔案。 如果您使用Java建立使用者端應用程式，請包含必要的JAR檔案。 如果您使用Web服務，請包含Proxy檔案。

**建立服務使用者端**

您必須先建立連線並提供認證，才能以程式設計方式建立資源集合。 這是透過建立服務使用者端來完成。

**指定資料夾路徑**

建立包含資源之資料夾路徑的字串。 語法包括正斜線，如以下範例所示：「/*路徑*/*資料夾*「。

**擷取資源清單**

叫用存放庫服務方法來擷取資源清單，指定目標資料夾的路徑。

**另请参阅**

[使用Java API列出資源](aem-forms-repository.md#list-resources-using-the-java-api)

[使用Web服務API列出資源](aem-forms-repository.md#list-resources-using-the-web-service-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[存放庫服務API快速啟動](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### 使用Java API列出資源 {#list-resources-using-the-java-api}

使用存放庫服務API (Java)列出資源：

1. 包含專案檔案

   在您的Java專案的類別路徑中包含使用者端JAR檔案。

1. 建立服務使用者端

   建立 `ResourceRepositoryClient` 物件，使用它的建構函式並傳遞 `ServiceClientFactory` 包含連線屬性的物件。

1. 指定資料夾路徑

   指定要查詢之資源集合的URI。 在這種情況下，其URI為 `"/testFolder"`. URI會儲存為 `java.lang.String` 物件。

1. 擷取資源清單

   叫用 `ResourceRepositoryClient` 物件的 `listMembers` 方法並傳入資料夾的URI。

   方法會傳回 `java.util.List` 之 `com.adobe.repository.infomodel.bean.Resource` 物件，作為的來源 `com.adobe.repository.infomodel.bean.Relation` 型別 `Relation.TYPE_MEMBER_OF` 並將資源集合URI作為目標。 您可以逐一檢視此 `List` 以擷取每個資源。 在此範例中，會顯示每個資源的名稱和說明。

**另请参阅**

[列出資源](aem-forms-repository.md#listing-resources).

[快速入門（SOAP模式）：使用Java API列出資源](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-listing-resources-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服務API列出資源 {#list-resources-using-the-web-service-api}

使用存放庫服務API （Web服務）列出資源：

1. 包含專案檔案

   * 建立使用存放庫WSDL的Microsoft .NET使用者端元件。
   * 參考Microsoft .NET使用者端元件。

1. 建立服務使用者端

   使用Microsoft .NET使用者端元件，建立 `RepositoryServiceService` 物件，透過叫用其預設建構函式。 設定其 `Credentials` 屬性使用 `System.Net.NetworkCredential` 包含使用者名稱和密碼的物件。

1. 指定資料夾路徑

   指定包含要查詢之資料夾URI的字串。 在這種情況下，其URI為 `"/testFolder"`. 使用與Microsoft .NET Framework相容的語言時（例如C#），請將URI儲存在 `System.String` 物件。

1. 擷取資源清單

   叫用 `RepositoryServiceService` 物件的 `listMembers` 方法，並將資料夾的URI傳入作為第一個引數。 通過 `null` 其他兩個引數的設定值。

   方法會傳回可強制轉換至的物件陣列 `Resource` 物件。 您可以逐一檢視物件陣列，以擷取每個相關資源。 在此範例中，會顯示每個資源的名稱和說明。

**另请参阅**

[列出資源](aem-forms-repository.md#listing-resources).

[使用Base64編碼叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## 正在讀取資源 {#reading-resources}

您可以從存放庫中的指定位置擷取資源，以讀取其內容和中繼資料。 工作流程會以初始化表單作為前端。 此程式擁有讀取表單所需的所有許可權。 系統會擷取資料表單，並從存放庫中讀取內容。 存放庫會授予對內容和中繼資料的存取權（甚至知道資源存在的能力）。

存放庫有以下四種許可權型別：

* **周遊**：可讓您列出資源；也就是讀取資源中繼資料，但不讀取資源內容
* **讀取**：可讓您讀取資源內容
* **寫入**：可讓您寫入資源內容
* **管理存取控制清單(ACL)**：可讓您操控資源上的ACL

使用者只有具備執行程式的許可權時，才能執行程式。 IDE使用者需要遍歷和讀取許可權才能與存放庫同步。 ACL只會在設計時套用，因為執行階段發生在系統內容中。

您可以使用存放庫服務Java API或Web服務API，以程式設計方式讀取資源。

>[!NOTE]
>
>如需儲存庫服務的詳細資訊，請參閱 [AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63).

### 步驟摘要 {#summary_of_steps-3}

若要讀取資源，請遵循下列步驟：

1. 包含專案檔案。
1. 建立存放庫服務使用者端。
1. 指定要讀取的資源的URI。
1. 讀取資源。

**包含專案檔案**

在您的開發專案中包含必要的檔案。 如果您使用Java建立使用者端應用程式，請包含必要的JAR檔案。 如果您使用Web服務，請包含Proxy檔案。

**建立服務使用者端**

您必須先建立連線並提供認證，才能以程式設計方式讀取資源。 這是透過建立服務使用者端來完成。

**指定要讀取的資源的URI**

建立包含要讀取之資源URI的字串。 語法包括正斜線，如以下範例所示：「/*路徑*/*資源*「。

**讀取資源**

叫用存放庫服務方法以讀取資源，指定URI。

**另请参阅**

[使用Java API讀取資源](aem-forms-repository.md#read-resources-using-the-java-api)

[使用Web服務API讀取資源](aem-forms-repository.md#reading-resources-using-the-web-service-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[存放庫服務API快速啟動](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### 使用Java API讀取資源 {#read-resources-using-the-java-api}

使用存放庫服務API (Java)讀取資源：

1. 包含專案檔案

   在您的Java專案的類別路徑中包含使用者端JAR檔案。

1. 建立服務使用者端

   建立 `ResourceRepositoryClient` 物件，使用它的建構函式並傳遞 `ServiceClientFactory` 包含連線屬性的物件。

1. 指定要讀取的資源的URI

   指定代表要擷取之資源的URI的字串值。 例如，假設資源名為 *testResource* 位在名為的資料夾中 *testFolder*，指定 `/testFolder/testResource`.

1. 讀取資源

   叫用 `ResourceRepositoryClient` 物件的 `readResource` 方法並傳遞資源的URI作為引數。 此方法會傳回 `Resource` 代表資源的執行個體。

**另请参阅**

[正在讀取資源](aem-forms-repository.md#reading-resources)

[快速入門（SOAP模式）：使用Java API讀取資源](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-reading-a-resource-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服務API讀取資源 {#reading-resources-using-the-web-service-api}

使用存放庫服務API （Web服務）讀取資源：

1. 包含專案檔案

   * 建立使用存放庫WSDL的Microsoft .NET使用者端元件。 (請參閱 [建立使用Base64編碼的.NET使用者端元件](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding).)
   * 參考Microsoft .NET使用者端元件。 (請參閱 [建立使用Base64編碼的.NET使用者端元件](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding).)

1. 建立服務使用者端

   使用Microsoft .NET使用者端元件，建立 `RepositoryServiceService` 物件，透過叫用其預設建構函式。 設定其 `Credentials` 屬性使用 `System.Net.NetworkCredential` 包含使用者名稱和密碼的物件。

1. 指定要讀取的資源的URI

   指定包含要擷取之資源URI的字串。 在此案例中，因為資源命名為 `testResource` 位於名為的資料夾中 `testFolder`，其URI為 `"/testFolder/testResource"`. 使用與Microsoft .NET Framework相容的語言時（例如C#），請將URI儲存在 `System.String` 物件。

1. 讀取資源

   叫用 `RepositoryServiceService` 物件的 `readResource` 方法，並將資源的URI傳遞為第一個引數。 通過 `null` 其他兩個引數的設定值。

**另请参阅**

[正在讀取資源](aem-forms-repository.md#reading-resources)

[使用Base64編碼叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## 更新資源 {#updating-resources}

您可以擷取並更新存放庫中的資源內容。 當您更新資源時，這些資源的存取控制在各版本之間保持不變。 執行更新時，您可以選擇遞增主要版本。 如果您不選擇遞增主要版本，次要版本會自動更新。

更新資源時，會根據指定的資源屬性建立新版本。 更新資源時，您會指定兩個重要引數：目標URI和包含所有已更新中繼資料的資源執行個體。 請務必注意，如果您未變更特定屬性（例如，名稱），則在您傳入的執行個體中仍需要該屬性。 剖析內容時建立的關係會新增至特定版本，除非另有指定，否則不會轉寄。

例如，如果您更新XDP檔案並且它包含對其他資源的參照，這些額外的參照也會被記錄。 假設form.xdp 1.0版有兩個外部參照：一個標誌和一個樣式表，而您之後更新了form.xdp，使其現在有三個參照：一個標誌、一個樣式表和一個結構描述檔案。 在更新期間，存放庫會將第三個關係（到結構描述檔案）新增到其擱置關係表中。 一旦結構描述檔案出現在存放庫中，關係就會自動形成。 不過，如果form.xdp 2.0版不再使用標誌，form.xdp 2.0版將不會與標誌建立關係。

所有更新操作都是原子和交易式的。 例如，如果兩個使用者讀取相同的資源，且都決定將1.0版更新為2.0版，則其中一個會成功，而其中一個會失敗，系統會維持存放庫的完整性，且兩個使用者都會收到一則確認成功或失敗的訊息。 如果交易未確認，它將在資料庫失敗時回覆，並會逾時或回覆，視應用程式伺服器而定。

您可以使用存放庫服務Java API或Web服務API，以程式設計方式更新資源。

>[!NOTE]
>
>如需儲存庫服務的詳細資訊，請參閱 [AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63).

### 步驟摘要 {#summary_of_steps-4}

若要更新資源，請遵循下列步驟：

1. 包含專案檔案。
1. 建立存放庫服務使用者端。
1. 擷取要更新的資源。
1. 更新資源。

**包含專案檔案**

在您的開發專案中包含必要的檔案。 如果您使用Java建立使用者端應用程式，請包含必要的JAR檔案。 如果您使用Web服務，請包含Proxy檔案。

**建立服務使用者端**

您必須先建立連線並提供認證，才能以程式設計方式讀取資源。 這是透過建立服務使用者端來完成。

**擷取要更新的資源**

讀取資源。 如需詳細資訊，請參閱 [正在讀取資源](aem-forms-repository.md#reading-resources).

**更新資源**

在資源中設定新資訊，並叫用存放庫服務方法來更新資源，指定URI、更新的資源以及應如何更新版本資訊。

**另请参阅**

[使用Java API更新資源](aem-forms-repository.md#update-resources-using-the-java-api)

[使用Web服務API更新資源](aem-forms-repository.md#update-resources-using-the-web-service-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[存放庫服務API快速啟動](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### 使用Java API更新資源 {#update-resources-using-the-java-api}

使用存放庫服務API (Java)更新資源：

1. 包含專案檔案

   在您的Java專案的類別路徑中包含使用者端JAR檔案。

1. 建立服務使用者端

   建立 `ResourceRepositoryClient` 物件，使用它的建構函式並傳遞 `ServiceClientFactory` 包含連線屬性的物件。

1. 擷取要更新的資源

   指定要擷取和讀取資源的資源URI。 在此範例中，資源的URI為 `"/testFolder/testResource"`.

1. 更新資源

   更新 `Resource` 物件的資訊。 在此範例中，若要更新說明，請叫用 `Resource` 物件的 `setDescription` 方法，並將新說明字串當做引數傳遞。

   然後叫用 `ServiceClientFactory` 物件的 `updateResource` 方法，並傳入下列引數：

   * A `java.lang.String` 包含資源URI的物件。
   * 此 `Resource` 包含已更新資源資訊的物件。
   * A `boolean` 指示是更新主要版本還是次要版本的值。 在此範例中，值 `true` 會傳入，以表示主要版本會增加。

**另请参阅**

[更新資源](aem-forms-repository.md#updating-resources)

[快速入門（SOAP模式）：使用Java API更新資源](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-updating-a-resource-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服務API更新資源 {#update-resources-using-the-web-service-api}

使用存放庫API （Web服務）更新資源：

1. 包含專案檔案

   * 建立使用存放庫WSDL的Microsoft .NET使用者端元件。
   * 參考Microsoft .NET使用者端元件。

1. 建立服務使用者端

   使用Microsoft .NET使用者端元件，建立 `RepositoryServiceService` 物件，透過叫用其預設建構函式。 設定其 `Credentials` 屬性使用 `System.Net.NetworkCredential` 包含使用者名稱和密碼的物件。

1. 擷取要更新的資源

   指定要擷取的資源URI並讀取資源。 在此範例中，資源的URI為 `"/testFolder/testResource"`. 如需詳細資訊，請參閱 [正在讀取資源](aem-forms-repository.md#reading-resources).

1. 更新資源

   更新 `Resource` 物件的資訊。 在此範例中，若要更新說明，請將新值指派給 `Resource` 物件的 `description` 欄位。

1. 叫用 `RepositoryServiceService` 物件的 `updateResource` 方法，並傳入下列引數：

   * A `System.String` 包含資源URI的物件。
   * 此 `Resource` 包含已更新資源資訊的物件。
   * A `boolean` 指示是更新主要版本還是次要版本的值。 在此範例中，值 `true` 會傳入，以表示主要版本會增加。
   * 通過 `null` 其餘兩個引數。

**另请参阅**

[更新資源](aem-forms-repository.md#updating-resources)

[使用Base64編碼叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## 搜尋資源 {#searching-for-resources}

您可以建構用於搜尋存放庫中資源（包括歷史記錄、相關資源和屬性）的查詢。

您可以擷取相關資源，以判斷表單與其片段之間的相依性。 例如，如果您有表單，您可以決定它使用哪些片段或外部資源。 如果您有影像，也可以找出使用影像的表單。 您也可以使用根據屬性篩選來搜尋相關資源。 例如，您可以搜尋使用具有指定名稱之影像的所有表單，或尋找由具有指定名稱之表單使用的任何影像。 您也可以使用資源屬性來搜尋。 例如，您可以執行查詢來尋找其名稱以指定字串開頭的所有表單或資源，該字串可能包含&#39;%&#39;和&#39;_&#39;萬用字元。 請記住，基於屬性的搜尋不是基於關係；此類搜尋是基於您對指定資源具有特定知識的假設。

**查詢陳述式**

A *查詢* 包含一或多個邏輯上以條件聯結的陳述式。 A *陳述式* 由左運算元、運算元和右運算元組成。 此外，您可以指定搜尋結果要使用的排序順序。 此 *排序順序* 包含相當於SQL的資訊 `ORDER BY` 子句和由元素組成，這些元素包含搜尋所依據的屬性，以及一個指示是否要使用遞增或遞減順序的值。

您可以使用存放庫服務Java API，以程式設計方式搜尋資源。 目前無法使用Web服務API來搜尋資源。

**排序行為**

叫用時未遵循排序順序 `ResourceRepositoryClient` 物件的 `searchProperties` 方法並指定排序順序。 例如，假設您建立具有三個自訂屬性的資源，其中屬性名稱為 `name`， `secondName`、和 `asecondName`. 接下來，您在屬性名稱上建立排序順序元素，並設定 `ascending` 值至 `true`.

然後您叫用 `ResourceRepositoryClient` 物件的 `searchProperties` 方法和以排序順序傳遞。 搜尋會傳回正確的資源，包含三個屬性。 不過，屬性並未依屬性名稱排序。 它們會依新增的順序傳回： `name`， `secondName`、和 `asecondName`.

>[!NOTE]
>
>如需儲存庫服務的詳細資訊，請參閱 [AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63).

### 步驟摘要 {#summary_of_steps-5}

若要搜尋資源，請遵循下列步驟：

1. 包含專案檔案。
1. 建立存放庫服務使用者端。
1. 指定搜尋的目標資料夾。
1. 指定搜尋中使用的屬性。
1. 建立用於搜尋的查詢。
1. 建立搜尋結果的排序順序。
1. 搜尋資源。
1. 從搜尋結果擷取資源。

**包含專案檔案**

在您的開發專案中包含必要的檔案。 如果您使用Java建立使用者端應用程式，請包含必要的JAR檔案。 如果您使用Web服務，請包含Proxy檔案。

**建立服務使用者端**

您必須先建立連線並提供認證，才能以程式設計方式讀取資源。 這是透過建立服務使用者端來完成。

**指定搜尋的目標資料夾**

建立字串，其中包含進行搜尋的基本路徑。 語法包括正斜線，如以下範例所示：「/*路徑*/*資料夾*「。

**指定搜尋中使用的屬性**

您可以根據資源中所包含的屬性進行搜尋。 指定要執行搜尋的屬性值。

**建立用於搜尋的查詢**

使用陳述式和條件來建構查詢。 每個陳述式都會指定搜尋所依據的屬性、要使用的條件，以及要在搜尋中使用的屬性值。

**建立搜尋結果的排序順序**

排序順序由元素組成，每個元素都包含搜尋中使用的其中一個屬性，以及一個指示要使用升序或降序的值。

**搜尋資源**

使用資料夾、查詢和排序順序來搜尋資源。 此外，指出搜尋的深度以及要傳回的結果數目上限。

**從搜尋結果擷取資源**

逐一檢視傳回的資源清單，並擷取資訊以供進一步處理。

**另请参阅**

[使用Java API搜尋資源](aem-forms-repository.md#search-for-resources-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[存放庫服務API快速啟動](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### 使用Java API搜尋資源 {#search-for-resources-using-the-java-api}

使用存放庫服務API (Java)搜尋資源：

1. 包含專案檔案

   在您的Java專案的類別路徑中包含使用者端JAR檔案。

1. 建立服務使用者端

   建立 `ResourceRepositoryClient` 物件，使用它的建構函式並傳遞 `ServiceClientFactory` 包含連線屬性的物件。

1. 指定搜尋的目標資料夾

   指定要執行搜尋的基本路徑URI。 在此範例中，資源的URI為 `/testFolder`.

1. 指定搜尋中使用的屬性

   指定要執行搜尋的屬性值。 屬性存在於 `com.adobe.repository.infomodel.bean.Resource` 物件。 在此範例中，將會對name屬性進行搜尋；因此， `java.lang.String` 包含 `Resource` 會使用物件的名稱，也就是 `testResource` 在此案例中。

1. 建立用於搜尋的查詢

   若要建立查詢，請建立 `com.adobe.repository.query.Query` 物件，方法是叫用預設建構函式 `Query` 類別並新增陳述式至查詢。

   若要建立陳述式，請叫用 `com.adobe.repository.query.Query.Statement` 類別並傳遞下列引數：

   * 包含資源屬性常數的左側運算元。 在此範例中，由於資源名稱是用作搜尋的基礎，因此靜態值 `Resource.ATTRIBUTE_NAME` 已使用。
   * 包含用於搜尋屬性的條件的運運算元。 運運算元必須是中的靜態常數之一 `Query.Statement` 類別。 在此範例中，靜態值 `Query.Statement.OPERATOR_BEGINS_WITH` 已使用。
   * 包含進行搜尋之屬性值的右運算元。 在此範例中，name屬性、 `String` 包含值 `"testResource"`，則會使用。

   透過叫用 `Query.Statement` 物件的 `setNamespace` 方法並傳入 `com.adobe.repository.infomodel.bean.ResourceProperty` 類別。 在此示例中，使用 `ResourceProperty.RESERVED_NAMESPACE_REPOSITORY`。

   透過叫用 `Query` 物件的 `addStatement` 方法並傳入 `Query.Statement` 物件。

1. 建立搜尋結果的排序順序

   若要指定搜尋結果中使用的排序順序，請建立 `com.adobe.repository.query.sort.SortOrder` 物件，方法是叫用預設建構函式 `SortOrder` 類別，並將元素新增至排序順序。

   若要建立排序順序的元素，請叫用其中一個建構函式 `com.adobe.repository.query.sort.SortOrder.Element` 類別。 在此範例中，由於資源名稱是用作搜尋的基礎，因此靜態值 `Resource.ATTRIBUTE_NAME` 會作為第一個引數，並以遞增順序排列(a `boolean` 值 `true`)指定為第二個引數。

   透過叫用 `SortOrder` 物件的 `addSortElement` 方法並傳入 `SortOrder.Element` 物件。

1. 搜尋資源

   若要搜尋 `resources` 根據屬性屬性，叫用 `ResourceRepositoryClient` 物件的 `searchProperties` 方法並傳遞下列引數：

   * A `String` 包含執行搜尋的基本路徑。 在這種情況下， `"/testFolder"` 已使用。
   * 搜尋中使用的查詢。
   * 搜尋的深度。 在這種情況下， `com.adobe.repository.infomodel.bean.ResourceCollection.DEPTH_INFINITE` 用於表示要使用基本路徑及其所有資料夾。
   * 一個 `int` 表示要從中選取未分頁結果集的第一個列的值。 在此範例中， `0` 已指定。
   * 一個 `int` 表示要傳回的結果數目上限的值。 在此範例中， `10` 已指定。
   * 搜尋中使用的排序順序。

   方法會傳回 `java.util.List` 之 `Resource` 物件以指定的排序順序。

1. 從搜尋結果擷取資源

   若要擷取搜尋結果中包含的資源，請逐一檢視 `List` 並將每個物件轉換為 `Resource` 以擷取其資訊。 在此範例中，會顯示每個資源的名稱。

**另请参阅**

[搜尋資源](aem-forms-repository.md#searching-for-resources)

[快速入門（SOAP模式）：使用Java API搜尋資源](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-searching-for-resources-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 建立資源關係 {#creating-resource-relationships}

您可以指定存放庫中資源之間的關係。 有三種關係：

* **相依性**：資源相依於其他資源的關係，這表示存放庫需要所有相關資源。
* **成員資格（檔案系統）**：資源位於指定資料夾中的關係。
* **自訂**：您指定的資源之間的關係。 例如，如果一個資源已棄用，而另一個資源已引入存放庫，您可以指定自己的替代關係。

您可以建立自己的自訂關係。 例如，如果您將HTML檔案儲存在存放庫中，而且它使用影像，則可以指定自訂關係來將HTML檔案與影像相關聯（因為通常只有XML檔案會使用存放庫定義的相依關係與影像相關聯）。 另一個自訂關係的範例是，如果您想使用循環圖表結構而不是樹狀結構來建置存放庫的不同檢視。 您可以定義圓形圖表以及檢視器來周遊這些關係。 最後，您可以指出一個資源會取代另一個資源，即使這兩個資源完全不同。 在這種情況下，您可以定義保留範圍以外的關係型別，並在這兩個資源之間建立關係。 您的應用程式將是唯一可以偵測及處理該關係的使用者端，並且可用於搜尋該關係。

您可以使用存放庫服務Java API或Web服務API，以程式設計方式指定資源之間的關係。

>[!NOTE]
>
>如需儲存庫服務的詳細資訊，請參閱 [AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63).

### 步驟摘要 {#summary_of_steps-6}

若要指定兩個資源之間的關係，請遵循下列步驟：

1. 包含專案檔案。
1. 建立存放庫服務使用者端。
1. 指定要相關之資源的URI。
1. 建立關係。

**包含專案檔案**

在您的開發專案中包含必要的檔案。 如果您使用Java建立使用者端應用程式，請包含必要的JAR檔案。 如果您使用Web服務，請包含Proxy檔案。

**建立服務使用者端**

您必須先建立連線並提供認證，才能以程式設計方式讀取資源。 這是透過建立服務使用者端來完成。

**指定要相關之資源的URI**

建立包含要關聯之資源的URI的字串。 語法包括正斜線，如以下範例所示：「/*路徑*/*資源*「。

**建立關係**

叫用存放庫服務方法以建立並指定關係型別。

**另请参阅**

[使用Java API建立關係資源](aem-forms-repository.md#create-relationship-resources-using-the-java-api)

[使用Web服務API建立關係資源](aem-forms-repository.md#create-relationship-resources-using-the-web-service-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[存放庫服務API快速啟動](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### 使用Java API建立關係資源 {#create-relationship-resources-using-the-java-api}

使用存放庫服務Java API建立關係資源，執行以下工作：

1. 包含專案檔案

   在您的Java專案的類別路徑中包含使用者端JAR檔案。

1. 建立服務使用者端

   建立 `ResourceRepositoryClient` 物件，使用它的建構函式並傳遞 `ServiceClientFactory` 包含連線屬性的物件。

1. 指定要相關之資源的URI

   指定要相關之資源的URI。 在此情況下，因為資源已命名 `testResource1` 和 `testResource2` 和位於名為的資料夾中 `testFolder`，其URI為 `"/testFolder/testResource1"` 和 `"/testFolder/testResource2"`. URI會儲存為 `java.lang.String` 物件。 在此範例中，資源會先寫入存放庫，然後擷取其URI。 如需有關寫入資源的詳細資訊，請參閱 [寫入資源](aem-forms-repository.md#writing-resources).

1. 建立關係

   叫用 `ResourceRepositoryClient` 物件的 `createRelationship` 方法並傳遞下列引數：

   * 來源資源的URI。
   * 目標資源的URI。
   * 關聯性型別，此為中的靜態常數之一 `com.adobe.repository.infomodel.bean.Relation` 類別。 在此範例中，相依關係是透過指定值來建立 `Relation.TYPE_DEPENDANT_OF`.
   * A `boolean` 指示目標資源是否自動更新為 `com.adobe.repository.infomodel.Id`新head資源的 — based識別碼。 在此範例中，由於相依關係，值 `true` 已指定。

   您也可以透過叫用 `ResourceRepositoryClient` 物件的 `getRelated` 方法並傳入下列引數：

   * 要擷取相關資源的資源URI。 在此範例中，來源資源( `"/testFolder/testResource1"`)已指定。
   * A `boolean` 指示指定的資源是否為關係中的來源資源的值。 在此範例中，值 `true` 已指定，因為情況如此。
   * 關聯性型別，此型別為中的靜態常數之一。 `Relation` 類別。 在此範例中，相依關係是使用先前使用的相同值來指定： `Relation.TYPE_DEPENDANT_OF`.

   此 `getRelated` 方法傳回 `java.util.List` 之 `Resource` 物件，您可以透過它來反複擷取每一個相關資源，轉換包含在 `List` 至 `Resource` 隨心所欲。 在此範例中， `testResource2` 預期會位於傳回資源的清單中。

**另请参阅**

[建立資源關係](aem-forms-repository.md#creating-resource-relationships)

[快速入門（SOAP模式）：使用Java API建立資源之間的關係](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-creating-relationships-between-resources-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服務API建立關係資源 {#create-relationship-resources-using-the-web-service-api}

使用存放庫API （Web服務）建立關係資源：

1. 包含專案檔案

   * 建立使用存放庫WSDL的Microsoft .NET使用者端元件。
   * 參考Microsoft .NET使用者端元件。

1. 建立服務使用者端

   使用Microsoft .NET使用者端元件，建立 `RepositoryServiceService` 物件，透過叫用其預設建構函式。 設定其 `Credentials` 屬性使用 `System.Net.NetworkCredential` 包含使用者名稱和密碼的物件。

1. 指定要相關之資源的URI

   指定要相關之資源的URI。 在此情況下，因為資源已命名 `testResource1` 和 `testResource2` 和位於名為的資料夾中 `testFolder`，其URI為 `"/testFolder/testResource1"` 和 `"/testFolder/testResource2"`. 使用與Microsoft .NET Framework相容的語言時（例如C#），URI會儲存為 `System.String` 物件。 在此範例中，資源會先寫入存放庫，然後擷取其URI。 如需有關寫入資源的詳細資訊，請參閱 [寫入資源](aem-forms-repository.md#writing-resources).

1. 建立關係

   叫用 `RepositoryServiceService` 物件的 `createRelationship` 方法並傳遞下列引數：

   * 來源資源的URI。
   * 目標資源的URI。
   * 關係的型別。 在此範例中，相依關係是透過指定值來建立 `3`.
   * A `boolean` 指示是否已指定關係型別的值。 在此範例中，值 `true` 已指定。
   * A `boolean` 指示目標資源是否自動更新為 `Id`新head資源的 — based識別碼。 在此範例中，由於相依關係，值 `true` 已指定。
   * A `boolean` 指示是否已指定目標標頭的值。 在此範例中，值 `true` 已指定。
   * 通過 `null` 最後一個引數。

   您也可以透過叫用 `RepositoryServiceService` 物件的 `getRelated` 方法並傳入下列引數：

   * 要擷取相關資源的資源URI。 在此範例中，來源資源( `"/testFolder/testResource1"`)已指定。
   * A `boolean` 指示指定的資源是否為關係中的來源資源的值。 在此範例中，值 `true` 已指定，因為情況如此。
   * A `boolean` 指示是否已指定來源資源的值。 在此範例中，值 `true` 「 」提供。
   * 包含關係型別的整數陣列。 在此範例中，相依關係是在陣列中使用與先前所用的相同值來指定的： `3`.
   * 通過 `null` 其餘兩個引數。

   此 `getRelated` 方法會傳回可以轉型為的物件陣列 `Resource` 物件，您可以透過這些物件反複擷取每一個相關資源。 在此範例中， `testResource2` 預期會位於傳回資源的清單中。

**另请参阅**

[建立資源關係](aem-forms-repository.md#creating-resource-relationships)

[使用Base64編碼叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## 鎖定資源 {#locking-resources}

您可以鎖定資源或資源集，以供特定使用者獨佔使用，或供多個使用者共用。 共用鎖定表示資源會發生什麼事，但不會阻止其他人對該資源採取動作。 共用鎖定應視為訊號機制。 獨佔鎖定表示鎖定資源的使用者將會變更資源，而鎖定可確保除非使用者不再需要存取資源且已解除鎖定，否則其他人無法變更。 如果存放庫管理員解除鎖定資源，則該資源的所有專屬和共用鎖定都會自動移除。 這類動作適用於使用者已無法使用且尚未解除鎖定資源的情況。

鎖定資源時，當您檢視位於Workbench中的「資源」標籤時，會出現鎖定圖示，如下圖所示。

![lr_lr_lockrepository](assets/lr_lr_lockrepository.png)

您可以使用存放庫服務Java API或Web服務API，以程式設計方式控制對資源的存取。

>[!NOTE]
>
>如需儲存庫服務的詳細資訊，請參閱 [AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63).

### 步驟摘要 {#summary_of_steps-7}

若要鎖定和解鎖資源，請遵循下列步驟：

1. 包含專案檔案。
1. 建立存放庫服務使用者端。
1. 指定要鎖定的資源的URI。
1. 鎖定資源。
1. 擷取資源的鎖定。
1. 解除鎖定資源

**包含專案檔案**

在您的開發專案中包含必要的檔案。 如果您使用Java建立使用者端應用程式，請包含必要的JAR檔案。 如果您使用Web服務，請包含Proxy檔案。

**建立服務使用者端**

您必須先建立連線並提供認證，才能以程式設計方式讀取資源。 這是透過建立服務使用者端來完成。

**指定要鎖定的資源的URI**

建立包含要鎖定之資源的URI的字串。 語法包括正斜線，如以下範例所示：「/*路徑*/*資源*「。

**鎖定資源**

叫用存放庫服務方法來鎖定資源，指定URI、鎖定型別和鎖定深度。

**擷取資源的鎖定**

叫用存放庫服務方法以擷取資源的鎖定，指定URI。

**解除鎖定資源**

叫用存放庫服務方法以解除鎖定資源，指定URI。

**另请参阅**

[使用Java API鎖定資源](aem-forms-repository.md#lock-resources-using-the-java-api)

[使用Web服務API鎖定資源](aem-forms-repository.md#lock-resources-using-the-web-service-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[存放庫服務API快速啟動](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### 使用Java API鎖定資源 {#lock-resources-using-the-java-api}

使用存放庫服務API (Java)鎖定資源：

1. 包含專案檔案

   在您的Java專案的類別路徑中包含使用者端JAR檔案。

1. 建立服務使用者端

   建立 `ResourceRepositoryClient` 物件，使用它的建構函式並傳遞 `ServiceClientFactory` 包含連線屬性的物件。

1. 指定要鎖定的資源的URI

   指定要鎖定的資源的URI。 在此案例中，因為資源命名為 `testResource` 位於名為的資料夾中 `testFolder`，其URI為 `"/testFolder/testResource"`. URI會儲存為 `java.lang.String` 物件。

1. 鎖定資源

   叫用 `ResourceRepositoryClient` 物件的 `lockResource` 方法並傳遞下列引數：

   * 資源的URI。
   * 鎖定範圍。 在此範例中，由於資源將被鎖定以供獨佔使用，因此鎖定範圍指定為 `com.adobe.repository.infomodel.bean.Lock.SCOPE_EXCLUSIVE`.
   * 鎖定深度。 在此範例中，由於鎖定只會套用至特定資源，不會套用至其任何成員或子系，因此鎖定深度會指定為 `Lock.DEPTH_ZERO`.

   >[!NOTE]
   >
   >多載版本的 `lockResource` 需要四個引數的方法會擲回例外狀況。 確保使用 `lockResource` 方法需要三個引數，如本逐步說明所示。

1. 擷取資源的鎖定

   叫用 `ResourceRepositoryClient` 物件的 `getLocks` 方法並傳遞資源的URI作為引數。 方法會傳回Lock物件清單，您可以透過該清單進行反複運算。 在此範例中，會透過叫用每個Lock物件的 `getOwnerUserId`， `getDepth`、和 `getType` 方法。

1. 解除鎖定資源

   叫用 `ResourceRepositoryClient` 物件的 `unlockResource` 方法並傳遞資源的URI作為引數。 如需詳細資訊，請參閱 [AEM Forms API參考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

**另请参阅**

[鎖定資源](aem-forms-repository.md#locking-resources)

[快速入門（SOAP模式）：使用Java API鎖定資源](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-locking-a-resource-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服務API鎖定資源 {#lock-resources-using-the-web-service-api}

使用存放庫服務API （Web服務）鎖定資源：

1. 包含專案檔案

   * 使用Base64建立使用存放庫WSDL的Microsoft .NET使用者端元件。
   * 參考Microsoft .NET使用者端元件。

1. 建立服務使用者端

   使用Microsoft .NET使用者端元件，建立 `RepositoryServiceService` 物件，透過叫用其預設建構函式。 設定其 `Credentials` 屬性使用 `System.Net.NetworkCredential` 包含使用者名稱和密碼的物件。

1. 指定要鎖定的資源的URI

   指定包含要鎖定之資源URI的字串。 在此案例中，因為資源命名為 `testResource` 在資料夾中 `testFolder`，其URI為 `"/testFolder/testResource"`. 使用與Microsoft .NET Framework相容的語言時（例如C#），請將URI儲存在 `System.String` 物件。

1. 鎖定資源

   叫用 `RepositoryServiceService` 物件的 `lockResource` 方法並傳遞下列引數：

   * 資源的URI。
   * 鎖定範圍。 在此範例中，由於資源將被鎖定以供獨佔使用，因此鎖定範圍指定為 `11`.
   * 鎖定深度。 在此範例中，由於鎖定只會套用至特定資源，不會套用至其任何成員或子系，因此鎖定深度會指定為 `2`.
   * 一個 `int` 表示鎖定到期前的秒數的值。 在此範例中，值 `1000` 已使用。
   * 通過 `null` 最後一個引數。

1. 擷取資源的鎖定

   叫用 `RepositoryServiceService` 物件的 `getLocks` 方法並傳遞資源的URI作為第一個引數，然後 `null` 第二個引數。 方法會傳回 `object` 陣列包含 `Lock` 您可用來反複處理的物件。 在此範例中，透過存取每個物件來列印每個物件的鎖定擁有者、深度和範圍 `Lock` 物件的 `ownerUserId`， `depth`、和 `type` 欄位。

1. 解除鎖定資源

   叫用 `RepositoryServiceService` 物件的 `unlockResource` 方法並傳遞資源的URI作為第一個引數，然後 `null` 第二個引數。

**另请参阅**

[鎖定資源](aem-forms-repository.md#locking-resources)

[使用Base64編碼叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## 刪除資源 {#deleting-resources}

您可以使用存放庫服務Java API (SOAP)，以程式設計方式從存放庫中的指定位置刪除資源。

當您刪除資源時，刪除通常是永久性的，但在某些情況下，ECM存放庫可能會根據其歷史記錄機制來儲存資源的版本。 因此，在刪除資源時，請務必確保您不會再需要該資源。 刪除資源的常見原因包括需要增加資料庫中的可用空間。 您可以刪除資源的某個版本，但如果您這樣做，您必須指定資源識別碼，而不是其邏輯識別碼(LID)或路徑。 如果您刪除資料夾，則該資料夾中的所有內容（包括子資料夾和資源）都會自動刪除。

不會刪除相關資源。 例如，如果您有一個使用logo.gif檔案的表單，而您刪除了logo.gif，則關係會儲存在擱置關係表格中。 另外，對於版本淘汰，請將最新版本的物件狀態設定為deprecated。

刪除操作在ECM系統中不是交易安全的。 例如，如果您嘗試刪除100個資源，而第50個資源的作業失敗，則會刪除前49個執行個體，但其餘的執行個體不會刪除。 否則，預設行為是回覆（非承諾）。

>[!NOTE]
>
>使用時 `com.adobe.repository.bindings.dsc.client.ResourceRepositoryClient.deleteResources()` 方法與ECM存放庫(EMC Documentum Content Server和IBM FileNet P8 Content Manager)，如果刪除其中一個指定資源失敗，則不會復原交易，這表示無法刪除已刪除的檔案。

>[!NOTE]
>
>如需儲存庫服務的詳細資訊，請參閱 [AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63).

### 步驟摘要 {#summary_of_steps-8}

若要刪除資源，請遵循下列步驟：

1. 包含專案檔案。
1. 建立存放庫服務使用者端。
1. 指定要刪除之資源的URI。
1. 刪除資源。

**包含專案檔案**

在您的開發專案中包含必要的檔案。 如果您使用Java建立使用者端應用程式，請包含必要的JAR檔案。 如果您使用Web服務，請包含Proxy檔案。

**建立服務使用者端**

您必須先建立連線並提供認證，才能以程式設計方式讀取資源。 這是透過建立服務使用者端來完成。

**指定要刪除之資源的URI**

建立包含要刪除之資源URI的字串。 語法包括正斜線，如以下範例所示：「/*路徑*/*資源*「。 如果要刪除的資源是資料夾，則會遞回刪除。

**刪除資源**

叫用存放庫服務方法以刪除資源，指定URI。

**另请参阅**

[使用Java API刪除資源](aem-forms-repository.md#delete-resources-using-the-java-api-soap)

[使用Web服務API刪除資源](aem-forms-repository.md#delete-resources-using-the-web-service-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[存放庫服務API快速啟動](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### 使用Java API(SOAP)刪除資源 {#delete-resources-using-the-java-api-soap}

使用存放庫API (Java)刪除資源：

1. 包含專案檔案

   在您的Java專案的類別路徑中包含使用者端JAR檔案。

1. 建立服務使用者端

   建立 `ResourceRepositoryClient` 物件，使用它的建構函式並傳遞 `ServiceClientFactory` 包含連線屬性的物件。

1. 指定要刪除之資源的URI

   指定要擷取的資源URI。 在這種情況下，由於名為testResourceToBeDeleted的資源位於名為testFolder的資料夾中，其URI為 `/testFolder/testResourceToBeDeleted`. URI會儲存為 `java.lang.String` 物件。 在此範例中，資源會先寫入存放庫，然後擷取其URI。 如需有關寫入資源的詳細資訊，請參閱 [寫入資源](aem-forms-repository.md#writing-resources).

1. 刪除資源

   叫用 `ResourceRepositoryClient` 物件的 `deleteResource` 方法並傳遞資源的URI作為引數。

**另请参阅**

[刪除資源](aem-forms-repository.md#deleting-resources)

[快速入門（SOAP模式）：使用Java API搜尋資源](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-searching-for-resources-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服務API刪除資源 {#delete-resources-using-the-web-service-api}

使用存放庫API （Web服務）刪除資源：

1. 包含專案檔案

   * 使用Base64建立使用存放庫WSDL的Microsoft .NET使用者端元件。
   * 參考Microsoft .NET使用者端元件。

1. 建立服務使用者端

   使用Microsoft .NET使用者端元件，建立 `RepositoryServiceService` 物件，透過叫用其預設建構函式。 設定其 `Credentials` 屬性使用 `System.Net.NetworkCredential` 包含使用者名稱和密碼的物件。

1. 指定要刪除之資源的URI

   指定要擷取的資源URI。 在此案例中，因為資源命名為 `testResourceToBeDeleted` 位於名為的資料夾中 `testFolder`，其URI為 `"/testFolder/testResourceToBeDeleted"`. 在此範例中，資源會先寫入存放庫，然後擷取其URI。 如需有關寫入資源的詳細資訊，請參閱 [寫入資源](aem-forms-repository.md#writing-resources).

1. 刪除資源

   叫用 `RepositoryServiceService` 物件的 `deleteResources` 方法並傳遞 `System.String` 陣列，包含資源的URI作為第一個引數。 通過 `null` 第二個引數。

**另请参阅**

[刪除資源](aem-forms-repository.md#deleting-resources)

[使用Base64編碼叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
