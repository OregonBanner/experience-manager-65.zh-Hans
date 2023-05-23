---
title: 管理使用者
seo-title: Managing Users
description: 使用User Management API建立使用者端應用程式，以管理角色、許可權和主體（可以是使用者或群組），並驗證使用者。
seo-description: Use the User Management API to create client applications that can manage roles, permissions, and principals (which can be users or groups), as well as authenticate users.
uuid: 68d8a0bc-6e3d-4286-ba5c-534dcf58cb84
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 95804bff-9e6f-4807-aae4-790bd9e7cb57
role: Developer
exl-id: d7c5bb84-a988-4b2e-a587-f4e5b50fea58
source-git-commit: 135f50cc80f8bb449b2f1621db5e2564f5075968
workflow-type: tm+mt
source-wordcount: '6228'
ht-degree: 0%

---

# 管理使用者 {#managing-users}

**本檔案中的範例和範例僅適用於JEE環境上的AEM Forms 。**

**關於使用者管理**

您可以使用User Management API建立使用者端應用程式，以管理角色、許可權和主體（可以是使用者或群組），並驗證使用者。 使用者管理API包含下列AEM Forms API：

* 目錄管理員服務API
* Authentication Manager服務API
* 授權管理員服務API

使用者管理可讓您指派、移除及決定角色和許可權。 它也可讓您指派、移除和查詢網域、使用者和群組。 最後，您可以使用「使用者管理」來驗證使用者。

在 [新增使用者](users.md#adding-users) 您將瞭解如何以程式設計方式新增使用者。 本節使用目錄管理員服務API。

在 [刪除使用者](users.md#deleting-users) 您將瞭解如何以程式設計方式刪除使用者。 本節使用目錄管理員服務API。

在 [管理使用者和群組](users.md#managing-users-and-groups) 您將瞭解本機使用者和目錄使用者之間的差異，並參閱如何使用Java和Web服務API以程式設計方式管理使用者和群組的範例。 本節使用目錄管理員服務API。

在 [管理角色和許可權](users.md#managing-roles-and-permissions) 您將瞭解系統角色和許可權，以及可以用程式設計方式做哪些事來增強它們，並檢視如何使用Java和Web服務API以程式設計方式管理角色和許可權的範例。 本節同時使用目錄管理員服務API和授權管理員服務API。

在 [驗證使用者](users.md#authenticating-users) 您將會看到如何使用Java和Web服務API以程式設計方式驗證使用者的範例。 本節使用授權管理員服務API。

**瞭解驗證流程**

「使用者管理」提供內建的驗證功能，也讓您能夠將其與自己的驗證提供者連線。 當User Management收到驗證要求時（例如，使用者嘗試登入），會將使用者資訊傳遞給驗證提供者以進行驗證。 「使用者管理」會在驗證使用者之後，從驗證提供者接收結果。

下圖顯示嘗試登入的一般使用者、「使用者管理」和驗證提供者之間的互動。

![mu_mu_umauth_process](assets/mu_mu_umauth_process.png)

下表說明驗證程式的每個步驟。

<table>
 <thead>
  <tr>
   <th><p>步骤</p></th>
   <th><p>描述</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>1</p></td>
   <td><p>使用者嘗試登入叫用使用者管理的服務。 使用者指定使用者名稱和密碼。 </p></td>
  </tr>
  <tr>
   <td><p>2</p></td>
   <td><p>「使用者管理」會將使用者名稱和密碼以及組態資訊傳送給驗證提供者。</p></td>
  </tr>
  <tr>
   <td><p>3</p></td>
   <td><p>驗證提供者會連線至使用者存放區並驗證使用者。</p></td>
  </tr>
  <tr>
   <td><p>4</p></td>
   <td><p>驗證提供者會將結果傳回給「使用者管理」。</p></td>
  </tr>
  <tr>
   <td><p>5</p></td>
   <td><p>使用者管理可讓使用者登入或拒絕存取產品。</p></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>如果伺服器時區與使用者端時區不同，在WebSphere Application Server叢集上使用.NET使用者端的原生SOAP棧疊上使用AEM Forms產生PDF服務的WSDL時，可能會發生下列「使用者管理」驗證錯誤：

`[com.adobe.idp.um.webservices.WSSecurityHandler] errorCode:12803 errorCodeHEX:0x3203 message:WSSecurityHandler: UM authenticate returns exception : An error was discovered processing the <wsse:Security> header. (WSSecurityEngine: Invalid timestamp The security semantics of message have expired).`

**瞭解目錄管理**

User Management封裝了支援連線至LDAP目錄的目錄服務提供者(DirectoryManagerService)。 如果您的組織使用非LDAP存放庫來儲存使用者記錄，您可以建立自己的目錄服務提供者，與您的存放庫搭配使用。

目錄服務提供者會應使用者管理的要求，從使用者存放區擷取記錄。 「使用者管理」會定期快取資料庫中的使用者和群組記錄，以改善效能。

目錄服務提供者可用來將「使用者管理」資料庫與使用者存放區同步。 此步驟可確保所有使用者目錄資訊以及所有使用者和群組記錄都是最新的。

此外，DirectoryManagerService可讓您建立和管理網域。 網域會定義不同的使用者群。 網域邊界通常根據組織結構方式或使用者存放區的設定方式定義。 User Management網域提供驗證提供者和目錄服務提供者使用的組態設定。

在User Management匯出的設定XML中，屬性值為 `Domains` 包含為「使用者管理」定義的每個網域的XML元素。 這些元素中的每一個都包含其他元素，這些元素定義了與特定服務提供者相關聯之網域的各個方面。

**瞭解objectSID值**

使用Active Directory時，請務必瞭解 `objectSID` 值不是跨多個網域的唯一屬性。 此值會儲存物件的安全性識別碼。 在多重網域環境中（例如網域樹狀結構）， `objectSID` 值可以不同。

一個 `objectSID` 如果物件從一個Active Directory網域移動到另一個網域，值會變更。 有些物件具有相同的 `objectSID` 值。 例如，BUILTIN\Administrators、BUILTIN\Power Users等群組將具有相同的 `objectSID` 值（不論網域為何）。 這些 `objectSID` 值是眾所周知的。

## 新增使用者 {#adding-users}

您可以使用目錄管理員服務API （Java和Web服務），以程式設計方式將使用者新增到AEM Forms。 新增使用者後，您可以在執行需要使用者的服務操作時使用該使用者。 例如，您可以將任務指派給新使用者。

### 步驟摘要 {#summary-of-steps}

若要新增使用者，請執行下列步驟：

1. 包含專案檔案。
1. 建立DirectoryManagerService使用者端。
1. 定義使用者資訊。
1. 將使用者新增至AEM Forms。
1. 確認使用者已新增。

**包含專案檔案**

在您的開發專案中包含必要的檔案。 如果您使用Java建立使用者端應用程式，請包含必要的JAR檔案。 如果您使用Web服務，請包含Proxy檔案。

**建立DirectoryManagerService使用者端**

以程式設計方式執行「目錄管理員」服務作業之前，請先建立「目錄管理員服務API」使用者端。

**定義使用者資訊**

當您使用目錄管理員服務API新增使用者時，請定義該使用者的資訊。 通常，在新增使用者時，您會定義以下值：

* **網域名稱**：使用者所屬的網域(例如， `DefaultDom`)。
* **使用者識別碼值**：使用者的識別碼值(例如， `wblue`)。
* **主體型別**：使用者型別(例如，您可以指定 `USER)`.
* **名字**：使用者的指定名稱(例如， `Wendy`)。
* **姓氏**：使用者的姓氏(例如， `Blue)`.
* **地區設定**：使用者的地區設定資訊。

**將使用者新增至AEM Forms**

定義使用者資訊後，您可以將使用者新增至AEM Forms。 若要新增使用者，請叫用 `DirectoryManagerServiceClient` 物件的 `createLocalUser` 方法。

**確認使用者已新增**

您可以驗證是否已新增使用者，以確保未發生任何問題。 使用使用者識別碼值來尋找新使用者。

**另请参阅**

[使用Java API新增使用者](users.md#add-users-using-the-java-api)

[使用Web服務API新增使用者](users.md#add-users-using-the-web-service-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[刪除使用者](users.md#deleting-users)

### 使用Java API新增使用者 {#add-users-using-the-java-api}

使用目錄管理員服務API (Java)新增使用者：

1. 包含專案檔案。

   在您的Java專案的類別路徑中包含使用者端JAR檔案，例如adobe-usermanager-client.jar。

1. 建立DirectoryManagerServices使用者端。

   建立 `DirectoryManagerServiceClient` 物件，使用它的建構函式並傳遞 `ServiceClientFactory` 包含連線屬性的物件。

1. 定義使用者資訊。

   * 建立 `UserImpl` 物件（使用其建構函式）。
   * 透過叫用 `UserImpl` 物件的 `setDomainName` 方法。 傳遞指定網域名稱的字串值。
   * 透過叫用 `UserImpl` 物件的 `setPrincipalType` 方法。 傳遞指定使用者型別的字串值。 例如，您可以指定 `USER`.
   * 透過叫用 `UserImpl` 物件的 `setUserid` 方法。 傳遞字串值，指定使用者識別碼值。 例如，您可以指定 `wblue`.
   * 透過叫用 `UserImpl` 物件的 `setCanonicalName` 方法。 傳遞字串值，指定使用者的正式名稱。 例如，您可以指定 `wblue`.
   * 透過叫用 `UserImpl` 物件的 `setGivenName` 方法。 傳遞字串值，指定使用者的名字。 例如，您可以指定 `Wendy`.
   * 透過叫用 `UserImpl` 物件的 `setFamilyName` 方法。 傳遞字串值，指定使用者的姓氏。 例如，您可以指定 `Blue`.

   >[!NOTE]
   >
   >叫用屬於以下專案的方法： `UserImpl` 物件以設定其他值。 例如，您可以叫用 `UserImpl` 物件的 `setLocale` 方法。

1. 將使用者新增至AEM Forms。

   叫用 `DirectoryManagerServiceClient` 物件的 `createLocalUser` 方法並傳遞下列值：

   * 此 `UserImpl` 代表新使用者的物件
   * 代表使用者密碼的字串值

   此 `createLocalUser` 方法會傳回指定本機使用者識別碼值的字串值。

1. 確認使用者已新增。

   * 建立 `PrincipalSearchFilter` 物件（使用其建構函式）。
   * 透過叫用 `PrincipalSearchFilter` 物件的 `setUserId` 方法。 傳遞代表使用者識別碼值的字串值。
   * 叫用 `DirectoryManagerServiceClient` 物件的 `findPrincipals` 方法並傳遞 `PrincipalSearchFilter` 物件。 此方法會傳回 `java.util.List` 例項，其中每個元素為 `User` 物件。 循環瀏覽 `java.util.List` 執行個體以尋找使用者。

**另请参阅**

[步驟摘要](users.md#summary-of-steps)

[快速入門（SOAP模式）：使用Java API新增使用者](/help/forms/developing/user-manager-java-api-quick.md#quick-start-soap-mode-adding-users-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服務API新增使用者 {#add-users-using-the-web-service-api}

使用Directory Manager Service API （Web服務）新增使用者：

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET專案。 請確定您使用下列WSDL定義作為服務參考： `http://localhost:8080/soap/services/DirectoryManagerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Replace `localhost` 搭配裝載AEM Forms之伺服器的IP位址。

1. 建立DirectoryManagerService使用者端。

   * 建立 `DirectoryManagerServiceClient` 物件（使用其預設建構函式）。
   * 建立 `DirectoryManagerServiceClient.Endpoint.Address` 物件，使用 `System.ServiceModel.EndpointAddress` 建構函式。 將指定WSDL的字串值傳遞至AEM Forms服務(例如， `http://localhost:8080/soap/services/DirectoryManagerService?blob=mtom`)。 您不需要使用 `lc_version` 屬性。 當您建立服務參考時，會使用此屬性。 請務必指定 `?blob=mtom`.
   * 建立 `System.ServiceModel.BasicHttpBinding` 物件，方法是取得 `DirectoryManagerServiceClient.Endpoint.Binding` 欄位。 將傳回值轉換為 `BasicHttpBinding`.
   * 設定 `System.ServiceModel.BasicHttpBinding` 物件的 `MessageEncoding` 欄位至 `WSMessageEncoding.Mtom`. 此值可確保使用MTOM。
   * 執行下列工作來啟用基本HTTP驗證：

      * 將AEM表單使用者名稱指派給欄位 `DirectoryManagerServiceClient.ClientCredentials.UserName.UserName`.
      * 將對應的密碼值指派給欄位 `DirectoryManagerServiceClient.ClientCredentials.UserName.Password`.
      * 指派常數值 `HttpClientCredentialType.Basic` 至欄位 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * 指派常數值 `BasicHttpSecurityMode.TransportCredentialOnly` 至欄位 `BasicHttpBindingSecurity.Security.Mode`.

1. 定義使用者資訊。

   * 建立 `UserImpl` 物件（使用其建構函式）。
   * 將字串值指派給，以設定目的地名稱 `UserImpl` 物件的 `domainName` 欄位。
   * 將字串值指派給 `UserImpl` 物件的 `principalType` 欄位。 例如，您可以指定 `USER`.
   * 將字串值指派給，以設定使用者識別碼值 `UserImpl` 物件的 `userid` 欄位。
   * 將字串值指派給 `UserImpl` 物件的 `canonicalName` 欄位。
   * 將字串值指派給，以設定指定的名稱值 `UserImpl` 物件的 `givenName` 欄位。
   * 將字串值指定給 `UserImpl` 物件的 `familyName` 欄位。

1. 將使用者新增至AEM Forms。

   叫用 `DirectoryManagerServiceClient` 物件的 `createLocalUser` 方法並傳遞下列值：

   * 此 `UserImpl` 代表新使用者的物件
   * 代表使用者密碼的字串值

   此 `createLocalUser` 方法會傳回指定本機使用者識別碼值的字串值。

1. 確認使用者已新增。

   * 建立 `PrincipalSearchFilter` 物件（使用其建構函式）。
   * 將代表使用者識別碼值的字串值指派給，藉此設定使用者的使用者識別碼值 `PrincipalSearchFilter` 物件的 `userId` 欄位。
   * 叫用 `DirectoryManagerServiceClient` 物件的 `findPrincipals` 方法並傳遞 `PrincipalSearchFilter` 物件。 此方法會傳回 `MyArrayOfUser` 集合物件，其中每個元素為 `User` 物件。 循環瀏覽 `MyArrayOfUser` 集合以找出使用者。

**另请参阅**

[步驟摘要](users.md#summary-of-steps)

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 刪除使用者 {#deleting-users}

您可以使用目錄管理員服務API （Java和Web服務），以程式設計方式從AEM Forms中刪除使用者。 刪除使用者後，該使用者無法再用來執行需要使用者的服務操作。 例如，您無法將任務指派給已刪除的使用者。

### 步驟摘要 {#summary_of_steps-1}

若要刪除使用者，請執行下列步驟：

1. 包含專案檔案。
1. 建立DirectoryManagerService使用者端。
1. 指定要刪除的使用者。
1. 從AEM Forms刪除使用者。

**包含專案檔案**

在您的開發專案中包含必要的檔案。 如果您使用Java建立使用者端應用程式，請包含必要的JAR檔案。 如果您使用Web服務，請包含Proxy檔案。

**建立DirectoryManagerService使用者端**

以程式設計方式執行「目錄管理員服務API」作業之前，請先建立「目錄管理員」服務使用者端。

**指定要刪除的使用者**

您可以使用使用者的識別碼值來指定要刪除的使用者。

**從AEM Forms刪除使用者**

若要刪除使用者，請叫用 `DirectoryManagerServiceClient` 物件的 `deleteLocalUser` 方法。

**另请参阅**

[使用Java API刪除使用者](users.md#delete-users-using-the-java-api)

[使用Web服務API刪除使用者](users.md#delete-users-using-the-web-service-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[新增使用者](users.md#adding-users)

### 使用Java API刪除使用者 {#delete-users-using-the-java-api}

使用目錄管理員服務API (Java)刪除使用者：

1. 包含專案檔案。

   在您的Java專案的類別路徑中包含使用者端JAR檔案，例如adobe-usermanager-client.jar。

1. 建立DirectoryManagerService使用者端。

   建立 `DirectoryManagerServiceClient` 物件，使用它的建構函式並傳遞 `ServiceClientFactory` 包含連線屬性的物件。

1. 指定要刪除的使用者。

   * 建立 `PrincipalSearchFilter` 物件（使用其建構函式）。
   * 透過叫用 `PrincipalSearchFilter` 物件的 `setUserId` 方法。 傳遞代表使用者識別碼值的字串值。
   * 叫用 `DirectoryManagerServiceClient` 物件的 `findPrincipals` 方法並傳遞 `PrincipalSearchFilter` 物件。 此方法會傳回 `java.util.List` 例項，其中每個元素為 `User` 物件。 循環瀏覽 `java.util.List` 例項，以找出要刪除的使用者。

1. 從AEM Forms刪除使用者。

   叫用 `DirectoryManagerServiceClient` 物件的 `deleteLocalUser` 方法並傳遞的值 `User` 物件的 `oid` 欄位。 叫用 `User` 物件的 `getOid` 方法。 使用 `User` 物件擷取自 `java.util.List` 執行個體。

**另请参阅**

[步驟摘要](users.md#summary-of-steps)

[快速入門（EJB模式）：使用Java API刪除使用者](/help/forms/developing/user-manager-java-api-quick.md#quick-start-soap-mode-deleting-users-using-the-java-api)

[快速入門（SOAP模式）：使用Java API刪除使用者](/help/forms/developing/user-manager-java-api-quick.md#quick-start-soap-mode-deleting-users-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服務API刪除使用者 {#delete-users-using-the-web-service-api}

使用Directory Manager Service API （Web服務）刪除使用者：

1. 包含專案檔案。

   在您的Java專案的類別路徑中包含使用者端JAR檔案，例如adobe-usermanager-client.jar。

1. 建立DirectoryManagerService使用者端。

   * 建立 `DirectoryManagerServiceClient` 物件（使用其預設建構函式）。
   * 建立 `DirectoryManagerServiceClient.Endpoint.Address` 物件，使用 `System.ServiceModel.EndpointAddress` 建構函式。 將指定WSDL的字串值傳遞至AEM Forms服務(例如， `http://localhost:8080/soap/services/DirectoryManagerService?blob=mtom`)。 您不需要使用 `lc_version` 屬性。 當您建立服務參考時，會使用此屬性。 請務必指定 `blob=mtom.`
   * 建立 `System.ServiceModel.BasicHttpBinding` 物件，方法是取得 `DirectoryManagerServiceClient.Endpoint.Binding` 欄位。 將傳回值轉換為 `BasicHttpBinding`.
   * 設定 `System.ServiceModel.BasicHttpBinding` 物件的 `MessageEncoding` 欄位至 `WSMessageEncoding.Mtom`. 此值可確保使用MTOM。
   * 執行下列工作來啟用基本HTTP驗證：

      * 將AEM表單使用者名稱指派給欄位 `DirectoryManagerServiceClient.ClientCredentials.UserName.UserName`.
      * 將對應的密碼值指派給欄位 `DirectoryManagerServiceClient.ClientCredentials.UserName.Password`.
      * 指派常數值 `HttpClientCredentialType.Basic` 至欄位 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * 指派常數值 `BasicHttpSecurityMode.TransportCredentialOnly` 至欄位 `BasicHttpBindingSecurity.Security.Mode`.

1. 指定要刪除的使用者。

   * 建立 `PrincipalSearchFilter` 物件（使用其建構函式）。
   * 將字串值指派給，以設定使用者識別碼值 `PrincipalSearchFilter` 物件的 `userId` 欄位。
   * 叫用 `DirectoryManagerServiceClient` 物件的 `findPrincipals` 方法並傳遞 `PrincipalSearchFilter` 物件。 此方法會傳回 `MyArrayOfUser` 集合物件，其中每個元素為 `User` 物件。 循環瀏覽 `MyArrayOfUser` 集合以找出使用者。 此 `User` 物件擷取自 `MyArrayOfUser` 集合物件可用來刪除使用者。

1. 從AEM Forms刪除使用者。

   傳遞以下內容以刪除使用者： `User` 物件的 `oid` 的欄位值 `DirectoryManagerServiceClient` 物件的 `deleteLocalUser` 方法。

**另请参阅**

[步驟摘要](users.md#summary-of-steps)

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 建立群組 {#creating-groups}

您可以使用目錄管理員服務API （Java和Web服務）以程式設計方式建立AEM Forms群組。 建立群組之後，您可以使用該群組來執行需要群組的服務作業。 例如，您可以將使用者指派給新群組。 (請參閱 [管理使用者和群組](users.md#managing-users-and-groups).)

### 步驟摘要 {#summary_of_steps-2}

若要建立群組，請執行下列步驟：

1. 包含專案檔案。
1. 建立DirectoryManagerService使用者端。
1. 確定群組不存在。
1. 建立群組。
1. 對群組執行動作。

**包含專案檔案**

在您的開發專案中包含必要的檔案。 如果您使用Java建立使用者端應用程式，請包含必要的JAR檔案。

下列JAR檔案必須新增到專案的類別路徑中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar (如果AEM Forms部署在JBoss上，則為必要)
* jbossall-client.jar (如果AEM Forms部署在JBoss上，則為必要)

有關這些JAR檔案位置的資訊，請參見 [包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**建立DirectoryManagerService使用者端**

以程式設計方式執行「目錄管理員」服務作業之前，請先建立「目錄管理員服務API」使用者端。

**判斷群組是否存在**

建立群組時，請確定群組不存在於同一個網域中。 也就是說，兩個群組在同一網域中不能有相同的名稱。 若要執行此工作，請執行搜尋並根據兩個值篩選搜尋結果。 將主體型別設定為 `com.adobe.idp.um.api.infomodel.Principal.PRINCIPALTYPE_GROUP` 以確保只傳回群組。 此外，請務必指定網域名稱。

**建立群組**

確定群組不存在於領域之後，請建立群組並指定下列屬性：

* **通用名稱**：群組的名稱。
* **網域**：新增群組的網域。
* **說明**：群組的說明。

**對群組執行動作**

建立群組後，您可以使用群組執行動作。 例如，您可以將使用者新增至群組。 若要新增使用者至群組，請擷取使用者和群組的唯一識別碼值。 將這些值傳遞至 `addPrincipalToLocalGroup` 方法。

**另请参阅**

[使用Java API建立群組](users.md#create-groups-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[新增使用者](users.md#adding-users)

[刪除使用者](users.md#deleting-users)

### 使用Java API建立群組 {#create-groups-using-the-java-api}

使用目錄管理員服務API (Java)建立群組：

1. 包含專案檔案。

   在您的Java專案的類別路徑中包含使用者端JAR檔案，例如adobe-usermanager-client.jar。

1. 建立DirectoryManagerService使用者端。

   建立 `DirectoryManagerServiceClient` 物件，使用它的建構函式並傳遞 `ServiceClientFactory` 包含連線屬性的物件。

1. 判斷群組是否存在。

   * 建立 `PrincipalSearchFilter` 物件（使用其建構函式）。
   * 透過叫用 `PrincipalSearchFilter` 物件的 `setPrincipalType` 物件。 傳遞值 `com.adobe.idp.um.api.infomodel.Principal.PRINCIPALTYPE_GROUP`.
   * 透過叫用 `PrincipalSearchFilter` 物件的 `setSpecificDomainName` 物件。 傳遞指定網域名稱的字串值。
   * 若要尋找群組，請叫用 `DirectoryManagerServiceClient` 物件的 `findPrincipals` 方法（主體可以是群組）。 傳遞 `PrincipalSearchFilter` 指定主體型別和網域名稱的物件。 此方法會傳回 `java.util.List` 每個元素為的例項 `Group` 執行個體。 每個群組例項都符合透過使用的所指定的篩選器。 `PrincipalSearchFilter` 物件。
   * 循環瀏覽 `java.util.List` 執行個體。 對於每個元素，擷取群組名稱。 確保群組名稱不等於新群組名稱。

1. 建立群組。

   * 如果群組不存在，請叫用 `Group` 物件的 `setCommonName` 方法，並傳遞指定群組名稱的字串值。
   * 叫用 `Group` 物件的 `setDescription` 方法並傳遞指定群組說明的字串值。
   * 叫用 `Group` 物件的 `setDomainName` 方法並傳遞指定網域名稱的字串值。
   * 叫用 `DirectoryManagerServiceClient` 物件的 `createLocalGroup` 方法並傳遞 `Group` 執行個體。

   此 `createLocalUser` 方法會傳回指定本機使用者識別碼值的字串值。

1. 對群組執行動作。

   * 建立 `PrincipalSearchFilter` 物件（使用其建構函式）。
   * 透過叫用 `PrincipalSearchFilter` 物件的 `setUserId` 方法。 傳遞代表使用者識別碼值的字串值。
   * 叫用 `DirectoryManagerServiceClient` 物件的 `findPrincipals` 方法並傳遞 `PrincipalSearchFilter` 物件。 此方法會傳回 `java.util.List` 例項，其中每個元素為 `User` 物件。 循環瀏覽 `java.util.List` 執行個體以尋找使用者。
   * 透過叫用將使用者新增到群組 `DirectoryManagerServiceClient` 物件的 `addPrincipalToLocalGroup` 方法。 傳遞的傳回值 `User` 物件的 `getOid` 方法。 傳遞的傳回值 `Group` 物件的 `getOid` 方法(使用 `Group` 代表新群組的執行個體)。

**另请参阅**

[步驟摘要](users.md#summary-of-steps)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 管理使用者和群組 {#managing-users-and-groups}

本主題說明如何使用(Java)以程式設計方式指派、移除和查詢網域、使用者和群組。

>[!NOTE]
>
>設定網域時，您必須為群組和使用者設定唯一識別碼。 選擇的屬性不僅必須在LDAP環境中是唯一的，而且必須不可變，並且不會在目錄中變更。 此屬性也必須是簡單字串資料型別(目前Active Directory 2000/2003允許的唯一例外為 `"objectsid"`，為二進位值)。 Novell eDirectory屬性 `"GUID"`例如，不是簡單的字串資料型別，因此將無法運作。

* 對於Active Directory，請使用 `"objectsid"`.
* 對於SunOne，請使用 `"nsuniqueid"`.

>[!NOTE]
>
>不支援在LDAP目錄同步處理進行中時建立多個本機使用者和群組。 嘗試此程式可能會導致錯誤。

### 步驟摘要 {#summary_of_steps-3}

若要管理使用者和群組，請執行下列步驟：

1. 包含專案檔案。
1. 建立DirectoryManagerService使用者端。
1. 叫用適當的使用者或群組作業。

**包含專案檔案**

在您的開發專案中包含必要的檔案。 如果您使用Java建立使用者端應用程式，請包含必要的JAR檔案。 如果您使用Web服務，請務必包含Proxy檔案。

**建立DirectoryManagerService使用者端**

您必須先建立「目錄管理員」服務使用者端，才能以程式設計方式執行「目錄管理員」服務作業。 使用Java API時，可透過建立 `DirectoryManagerServiceClient` 物件。 使用Web服務API時，這是透過建立 `DirectoryManagerServiceService` 物件。

**叫用適當的使用者或群組作業**

建立服務使用者端後，您就可以叫用使用者或群組管理作業。 服務使用者端可讓您指派、移除和查詢網域、使用者和群組。 請注意，可以將目錄主體或本機主體新增至本機群組，但不能將本機主體新增至目錄群組。

**另请参阅**

[使用Java API管理使用者和群組](users.md#managing-users-and-groups-using-the-java-api)

[使用Web服務API管理使用者和群組](users.md#managing-users-and-groups-using-the-web-service-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[使用者管理員API快速入門](/help/forms/developing/user-manager-java-api-quick.md#user-manager-java-api-quick-start-soap)

### 使用Java API管理使用者和群組 {#managing-users-and-groups-using-the-java-api}

若要使用(Java)以程式設計方式管理使用者、群組和網域，請執行下列工作：

1. 包含專案檔案。

   在您的Java專案的類別路徑中包含使用者端JAR檔案，例如adobe-usermanager-client.jar。 如需有關這些檔案位置的資訊，請參閱 [包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

1. 建立DirectoryManagerService使用者端。

   建立 `DirectoryManagerServiceClient` 物件，使用它的建構函式並傳遞 `ServiceClientFactory` 包含連線屬性的物件。 如需詳細資訊，請參閱 [設定連線屬性&#x200B;](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)*.*

1. 叫用適當的使用者或群組作業。

   若要尋找使用者或群組，請叫用 `DirectoryManagerServiceClient` 物件尋找主體的方法（因為主體可以是使用者或群組）。 在以下範例中， `findPrincipals` 使用搜尋篩選器(a)呼叫方法 `PrincipalSearchFilter` 物件)。

   因為在此案例中，傳回值是 `java.util.List` 包含 `Principal` 物件，反複檢查結果並轉換 `Principal` 物件變更為任一 `User` 或 `Group` 物件。

   使用結果 `User` 或 `Group` 物件(兩者繼承自 `Principal` 介面)，擷取您在工作流程中所需的資訊。 例如，網域名稱和規範名稱值組合在一起時，會唯一識別主參與者。 這些檔案是透過叫用 `Principal` 物件的 `getDomainName` 和 `getCanonicalName` 方法。

   若要刪除本機使用者，請叫用 `DirectoryManagerServiceClient` 物件的 `deleteLocalUser` 方法，並傳遞使用者的識別碼。

   若要刪除本機群組，請叫用 `DirectoryManagerServiceClient` 物件的 `deleteLocalGroup` 方法，並傳遞群組的識別碼。

**另请参阅**

[步驟摘要](users.md#summary-of-steps)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服務API管理使用者和群組 {#managing-users-and-groups-using-the-web-service-api}

若要使用「目錄管理員服務API」（Web服務）以程式設計方式管理使用者、群組和網域，請執行下列工作：

1. 包含專案檔案。

   * 建立使用「目錄管理員」WSDL的Microsoft .NET使用者端元件。 (請參閱 [使用Base64編碼叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding).)
   * 參考Microsoft .NET使用者端元件。 (請參閱 [建立使用Base64編碼的.NET使用者端元件](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding).)

1. 建立DirectoryManagerService使用者端。

   建立 `DirectoryManagerServiceService` 物件。

1. 叫用適當的使用者或群組作業。

   若要尋找使用者或群組，請叫用 `DirectoryManagerServiceService` 物件尋找主體的方法（因為主體可以是使用者或群組）。 在以下範例中， `findPrincipalsWithFilter` 使用搜尋篩選器(a)呼叫方法 `PrincipalSearchFilter` 物件)。 使用時 `PrincipalSearchFilter` 物件，只有當 `isLocal` 屬性已設定為 `true`. 此行為與Java API的情況不同。

   >[!NOTE]
   >
   >如果未在搜尋篩選條件中指定結果數目上限(透過 `PrincipalSearchFilter.resultsMax` 欄位)，最多可傳回1000個結果。 這與使用Java API時的行為不同，在後一種情況下，預設最大值為10個結果。 此外，搜尋方法如 `findGroupMembers` 將不會產生任何結果，除非在搜尋篩選條件中指定了結果數目上限(例如，透過 `GroupMembershipSearchFilter.resultsMax` 欄位)。 這適用於繼承自以下專案的所有搜尋篩選器： `GenericSearchFilter` 類別。 如需詳細資訊，請參閱 [AEM Forms API參考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

   因為在此案例中，傳回值是 `object[]` 包含 `Principal` 物件，反複檢查結果並轉換 `Principal` 物件變更為任一 `User` 或 `Group` 物件。

   使用結果 `User` 或 `Group` 物件(兩者繼承自 `Principal` 介面)，擷取您在工作流程中所需的資訊。 例如，網域名稱和規範名稱值組合在一起時，會唯一識別主參與者。 這些檔案是透過叫用 `Principal` 物件的 `domainName` 和 `canonicalName` 欄位。

   若要刪除本機使用者，請叫用 `DirectoryManagerServiceService` 物件的 `deleteLocalUser` 方法，並傳遞使用者的識別碼。

   若要刪除本機群組，請叫用 `DirectoryManagerServiceService` 物件的 `deleteLocalGroup` 方法，並傳遞群組的識別碼。

**另请参阅**

[步驟摘要](users.md#summary-of-steps)

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

## 管理角色和許可權 {#managing-roles-and-permissions}

本主題說明如何使用授權管理員服務API (Java)以程式設計方式指派、移除及決定角色和許可權。

在AEM Forms， *角色* 是一組存取一或多個系統層級資源的許可權。 這些許可權是透過「使用者管理」建立並由服務元件強制執行。 例如，管理員可以將「原則集作者」的角色指派給一組使用者。 然後，Rights Management將允許該角色群組的使用者透過administration console建立原則集。

角色有兩種型別： *預設角色* 和 *自訂角色*. 預設角色(*系統角色)* 已位於AEM Forms中。 假設管理員無法刪除或修改預設角色，因此這些角色是不可變的。 管理員建立的自訂角色之後可能會修改或刪除它們，因此是可變的。

角色可讓您更輕鬆地管理許可權。 將角色指派給主體時，系統會自動將一組許可權指派給該主體，且主體的所有特定存取相關決定都根據該整體指派的許可權集作出。

### 步驟摘要 {#summary_of_steps-4}

若要管理角色和許可權，請執行下列步驟：

1. 包含專案檔案。
1. 建立AuthorizationManagerService使用者端。
1. 叫用適當的角色或許可權作業。

**包含專案檔案**

在您的開發專案中包含必要的檔案。 如果您使用Java建立使用者端應用程式，請包含必要的JAR檔案。 如果您使用Web服務，請務必包含Proxy檔案。

**建立AuthorizationManagerService使用者端**

您必須先建立AuthorizationManagerService使用者端，才能以程式設計方式執行User Management AuthorizationManagerService作業。 使用Java API時，可透過建立 `AuthorizationManagerServiceClient` 物件。

**叫用適當的角色或許可權作業**

建立服務使用者端後，您就可以叫用角色或許可權作業。 服務使用者端可讓您指派、移除及決定角色和許可權。

**另请参阅**

[使用Java API管理角色和許可權](users.md#managing-roles-and-permissions-using-the-java-api)

[使用Web服務API管理角色和許可權](users.md#managing-roles-and-permissions-using-the-web-service-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[使用者管理員API快速入門](/help/forms/developing/user-manager-java-api-quick.md#user-manager-java-api-quick-start-soap)

### 使用Java API管理角色和許可權 {#managing-roles-and-permissions-using-the-java-api}

若要使用Authorization Manager Service API (Java)管理角色和許可權，請執行下列工作：

1. 包含專案檔案。

   在您的Java專案的類別路徑中包含使用者端JAR檔案，例如adobe-usermanager-client.jar。

1. 建立AuthorizationManagerService使用者端。

   建立 `AuthorizationManagerServiceClient` 物件，使用它的建構函式並傳遞 `ServiceClientFactory` 包含連線屬性的物件。

1. 叫用適當的角色或許可權作業。

   若要將角色指派給主體，請叫用 `AuthorizationManagerServiceClient` 物件的 `assignRole` 方法並傳遞下列值：

   * A `java.lang.String` 包含角色識別碼的物件
   * 陣列 `java.lang.String` 包含主要識別碼的物件。

   若要從主體中移除角色，請叫用 `AuthorizationManagerServiceClient` 物件的 `unassignRole` 方法並傳遞下列值：

   * A `java.lang.String` 包含角色識別碼的物件。
   * 陣列 `java.lang.String` 包含主要識別碼的物件。


**另请参阅**

[步驟摘要](users.md#summary-of-steps)

[快速入門（SOAP模式）：使用Java API管理角色和許可權](/help/forms/developing/user-manager-java-api-quick.md#quick-start-soap-mode-managing-roles-and-permissions-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服務API管理角色和許可權 {#managing-roles-and-permissions-using-the-web-service-api}

使用授權管理員服務API （Web服務）管理角色和許可權：

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET專案。 請確定您使用下列WSDL定義： `http://localhost:8080/soap/services/AuthorizationManagerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Replace `localhost` 搭配裝載AEM Forms之伺服器的IP位址。

1. 建立AuthorizationManagerService使用者端。

   * 建立 `AuthorizationManagerServiceClient` 物件（使用其預設建構函式）。
   * 建立 `AuthorizationManagerServiceClient.Endpoint.Address` 物件，使用 `System.ServiceModel.EndpointAddress` 建構函式。 將指定WSDL的字串值傳遞至AEM Forms服務(例如， `http://localhost:8080/soap/services/AuthorizationManagerService?blob=mtom`.) 您不需要使用 `lc_version` 屬性。 當您建立服務參考時，會使用此屬性。
   * 建立 `System.ServiceModel.BasicHttpBinding` 物件，方法是取得 `AuthorizationManagerServiceClient.Endpoint.Binding` 欄位。 將傳回值轉換為 `BasicHttpBinding`.
   * 設定 `System.ServiceModel.BasicHttpBinding` 物件的 `MessageEncoding` 欄位至 `WSMessageEncoding.Mtom`. 此值可確保使用MTOM。
   * 執行下列工作來啟用基本HTTP驗證：

      * 將AEM表單使用者名稱指派給欄位 `AuthorizationManagerServiceClient.ClientCredentials.UserName.UserName`.
      * 將對應的密碼值指派給欄位 `AuthorizationManagerServiceClient.ClientCredentials.UserName.Password`.
      * 指派常數值 `HttpClientCredentialType.Basic` 至欄位 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * 指派常數值 `BasicHttpSecurityMode.TransportCredentialOnly` 至欄位 `BasicHttpBindingSecurity.Security.Mode`.

1. 叫用適當的角色或許可權作業。

   若要將角色指派給主體，請叫用 `AuthorizationManagerServiceClient` 物件的 `assignRole` 方法並傳遞下列值：

   * A `string` 包含角色識別碼的物件
   * A `MyArrayOf_xsd_string` 包含主要識別碼的物件。

   若要從主體中移除角色，請叫用 `AuthorizationManagerServiceService` 物件的 `unassignRole` 方法並傳遞下列值：

   * A `string` 包含角色識別碼的物件。
   * 陣列 `string` 包含主要識別碼的物件。


**另请参阅**

[步驟摘要](users.md#summary-of-steps)

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

## 驗證使用者 {#authenticating-users}

本主題說明如何使用Authentication Manager Service API (Java)讓您的使用者端應用程式以程式設計方式驗證使用者。

可能需要使用者驗證，才能與儲存安全資料的企業資料庫或其他企業儲存區域互動。

例如，假設使用者在網頁中輸入使用者名稱和密碼，並將值提交至託管Forms的J2EE應用程式伺服器。 Forms自訂應用程式可以使用Authentication Manager服務驗證使用者。

如果驗證成功，應用程式會存取安全的企業資料庫。 否則，會傳送訊息給使用者，指出該使用者不是授權使用者。

下圖顯示應用程式的邏輯流程。

![au_au_umauth_process](assets/au_au_umauth_process.png)

下表說明此圖表中的步驟

<table>
 <thead>
  <tr>
   <th><p>步骤</p></th>
   <th><p>描述</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>1</p></td>
   <td><p>使用者存取網站並指定使用者名稱和密碼。 此資訊會提交至裝載AEM Forms的J2EE應用程式伺服器。</p></td>
  </tr>
  <tr>
   <td><p>2</p></td>
   <td><p>使用者認證由Authentication Manager服務驗證。 如果使用者認證有效，則工作流程會繼續進行步驟3。 否則，會傳送訊息給使用者，指出該使用者不是授權使用者。</p></td>
  </tr>
  <tr>
   <td><p>3</p></td>
   <td><p>使用者資訊和表單設計是從安全的企業資料庫中擷取。 </p></td>
  </tr>
  <tr>
   <td><p>4</p></td>
   <td><p>使用者資訊會與表單設計合併，且表單會呈現給使用者。 </p></td>
  </tr>
 </tbody>
</table>

### 步驟摘要 {#summary_of_steps-5}

若要以程式設計方式驗證使用者，請執行下列步驟：

1. 包含專案檔案。
1. 建立AuthenticationManagerService使用者端。
1. 叫用驗證作業。
1. 如有必要，請擷取內容，以便使用者端應用程式可將其轉送至其他AEM Forms服務以進行驗證。

**包含專案檔案**

在您的開發專案中包含必要的檔案。 如果您使用Java建立使用者端應用程式，請包含必要的JAR檔案。 如果您使用Web服務，請務必包含Proxy檔案。

**建立AuthenticationManagerService使用者端**

您必須先建立AuthenticationManagerService使用者端，才能以程式設計方式驗證使用者。 使用Java API時，建立 `AuthenticationManagerServiceClient` 物件。

**叫用驗證作業**

建立服務使用者端後，您就可以叫用驗證作業。 此作業需要有關使用者的資訊，例如使用者名稱和密碼。 如果使用者未驗證，則會擲回例外狀況。

**擷取驗證內容**

在驗證使用者後，您可以根據已驗證的使用者建立內容。 然後，您可以使用內容來叫用其他AEM Forms服務。 例如，您可以使用前後關聯來建立 `EncryptionServiceClient` 並使用密碼加密PDF檔案。 確保已驗證的使用者具有名為的角色 `Services User` 呼叫AEM Forms服務所需的專案。

**另请参阅**

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[使用者管理員API快速入門](/help/forms/developing/user-manager-java-api-quick.md#user-manager-java-api-quick-start-soap)

[使用密碼加密PDF檔案](/help/forms/developing/encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password)

### 使用Java API驗證使用者 {#authenticate-a-user-using-the-java-api}

使用Authentication Manager Service API (Java)驗證使用者：

1. 包含專案檔案。

   在您的Java專案的類別路徑中包含使用者端JAR檔案，例如adobe-usermanager-client.jar。

1. 建立AuthenticationManagerServices使用者端。

   建立 `AuthenticationManagerServiceClient` 物件，使用它的建構函式並傳遞 `ServiceClientFactory` 包含連線屬性的物件。

1. 叫用驗證作業。

   叫用 `AuthenticationManagerServiceClient` 物件的 `authenticate` 方法並傳遞下列值：

   * A `java.lang.String` 包含使用者名稱的物件。
   * 位元組陣列(a `byte[]` 物件)，其中包含使用者的密碼。 您可以取得 `byte[]` 物件(透過叫用 `java.lang.String` 物件的 `getBytes` 方法。

   驗證方法傳回 `AuthResult` 物件，其中包含已驗證使用者的相關資訊。

1. 擷取驗證內容。

   叫用 `ServiceClientFactory` 物件的 `getContext` 方法，會傳回 `Context` 物件。

   然後叫用 `Context` 物件的 `initPrincipal` 方法並傳遞 `AuthResult`.

### 使用Web服務API驗證使用者 {#authenticate-a-user-using-the-web-service-api}

使用Authentication Manager服務API （Web服務）驗證使用者：

1. 包含專案檔案。

   * 建立使用Authentication Manager WSDL的Microsoft .NET使用者端元件。 (請參閱 [使用Base64編碼叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding).)
   * 參考Microsoft .NET使用者端元件。 (請參閱中的「參照.NET使用者端元件」 [使用Base64編碼叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding).)

1. 建立AuthenticationManagerService使用者端。

   建立 `AuthenticationManagerServiceService` 物件。

1. 叫用驗證作業。

   叫用 `AuthenticationManagerServiceClient` 物件的 `authenticate` 方法並傳遞下列值：

   * A `string` 包含使用者名稱的物件
   * 位元組陣列(a `byte[]` 物件)，其中包含使用者的密碼。 您可以取得 `byte[]` 物件，透過轉換 `string` 包含密碼的物件 `byte[]` 陣列，使用下列範例中顯示的邏輯。
   * 傳回值將為 `AuthResult` 物件，可用於擷取有關使用者的資訊。 在以下範例中，會先取得 `AuthResult` 物件的 `authenticatedUser` 欄位並隨後取得結果 `User` 物件的 `canonicalName` 和 `domainName` 欄位。

**另请参阅**

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 以程式設計方式同步使用者 {#programmatically-synchronizing-users}

您可以使用使用者管理API，以程式設計方式同步使用者。 同步使用者時，您會使用位於使用者存放庫中的使用者資料來更新AEM Forms。 例如，假設您將新使用者新增至使用者存放庫。 執行同步化作業後，新使用者會成為AEM Forms使用者。 此外，您使用者存放庫中已不再存在的使用者也會從AEM Forms中移除。

下圖顯示AEM Forms與使用者存放庫同步處理。

![ps_ps_umauth_sync](assets/ps_ps_umauth_sync.png)

下表說明此圖表中的步驟

<table>
 <thead>
  <tr>
   <th><p>步骤</p></th>
   <th><p>描述</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>1</p></td>
   <td><p>使用者端應用程式要求AEM Forms執行同步作業。</p></td>
  </tr>
  <tr>
   <td><p>2</p></td>
   <td><p>AEM Forms會執行同步作業。</p></td>
  </tr>
  <tr>
   <td><p>3</p></td>
   <td><p>使用者資訊已更新。</p></td>
  </tr>
  <tr>
   <td><p>4</p></td>
   <td><p>使用者可以檢視更新的使用者資訊。 </p></td>
  </tr>
 </tbody>
</table>

### 步驟摘要 {#summary_of_steps-6}

若要以程式設計方式同步使用者，請執行下列步驟：

1. 包含專案檔案。
1. 建立UserManagerUtilServiceClient使用者端。
1. 指定企業網域。
1. 叫用驗證作業。
1. 判斷同步化作業是否完成

**包含專案檔案**

在您的開發專案中包含必要的檔案。 如果您使用Java建立使用者端應用程式，請包含必要的JAR檔案。 如果您使用Web服務，請務必包含Proxy檔案。

**建立UserManagerUtilServiceClientclient**

您必須先建立「 」，才能以程式設計方式同步使用者 `UserManagerUtilServiceClient` 物件。

**指定企業網域**

在使用「使用者管理API」執行同步化作業之前，請先指定使用者所屬的企業網域。 您可以指定一或多個企業網域。 您必須先使用「管理主控台」設定企業網域，才能以程式設計方式執行同步化作業。 (請參閱 [管理說明](https://www.adobe.com/go/learn_aemforms_admin_63).)

**叫用同步作業**

指定一或多個企業網域後，即可執行同步化作業。 執行此作業所需的時間取決於使用者存放庫中的使用者記錄數量。

**判斷同步化作業是否完成**

以程式設計方式執行同步化作業之後，您可以判斷作業是否已完成。

**另请参阅**

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[使用者管理員API快速入門](/help/forms/developing/user-manager-java-api-quick.md#user-manager-java-api-quick-start-soap)

[使用密碼加密PDF檔案](/help/forms/developing/encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password)

### 使用Java API以程式設計方式同步使用者 {#programmatically-synchronizing-users-using-the-java-api}

使用使用者管理API (Java)同步使用者：

1. 包含專案檔案。

   在您的Java專案的類別路徑中包含使用者端JAR檔案，例如adobe-usermanager-client.jar和adobe-usermanager-util-client.jar。

1. 建立UserManagerUtilServiceClient使用者端。

   建立 `UserManagerUtilServiceClient` 物件，使用它的建構函式並傳遞 `ServiceClientFactory` 包含連線屬性的物件。

1. 指定企業網域。

   * 叫用 `UserManagerUtilServiceClient` 物件的 `scheduleSynchronization` 啟動使用者同步作業的方法。
   * 建立 `java.util.Set` 使用執行個體 `HashSet` 建構函式。 請務必指定 `String` 作為資料型別。 此 `Java.util.Set` 執行個體會儲存套用同步化操作的網域名稱。
   * 對於要新增的每個網域名稱，叫用 `java.util.Set` 物件的add方法並傳遞網域名稱。

1. 叫用同步作業。

   叫用 `ServiceClientFactory` 物件的 `getContext` 方法，會傳回 `Context` 物件。

   然後叫用 `Context` 物件的 `initPrincipal` 方法並傳遞 `AuthResult`.

**另请参阅**

[以程式設計方式同步使用者](users.md#programmatically-synchronizing-users)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)
