---
title: 使用原則保護檔案
seo-title: Protecting Documents with Policies
description: 使用Document Security服務來動態套用機密性設定至Adobe PDF檔案，並保持對檔案的控制。 Document Security服務也可讓使用者控制收件人如何使用受原則保護的PDF檔案。
seo-description: Use the Document Security service to dynamically apply confidentiality settings to Adobe PDF documents and to maintain control over the documents. The Document Security service also enables the users to maintain control over how recipients use the policy-protected PDF document.
uuid: 6feb69ef-7b61-4d0b-8c87-d65d98bae9b5
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 9b1d2bf3-f28c-41b2-9026-1f3311556422
role: Developer
exl-id: ff42579e-6aaf-433d-8b5d-9e9dd0957250
source-git-commit: 135f50cc80f8bb449b2f1621db5e2564f5075968
workflow-type: tm+mt
source-wordcount: '15514'
ht-degree: 0%

---

# 使用原則保護檔案 {#protecting-documents-with-policies}

**本檔案中的範例和範例僅適用於JEE環境上的AEM Forms 。**

**關於Document Security Service**

Document Security服務可讓使用者動態地將機密性設定套用至Adobe PDF檔案，並保持對檔案的控制，無論檔案分佈得多廣泛。

Document Security服務可讓使用者持續控制受原則保護的PDF檔案接收者的使用方式，以防止資訊擴散到使用者觸及的範圍之外。 使用者可以指定誰可以開啟檔案、限制他們使用檔案的方式，並在檔案分發後監視檔案。 使用者也可以動態控制對受原則保護檔案的存取權，甚至可以動態撤銷對檔案的存取權。

Document Security服務也會保護其他檔案型別，例如Microsoft Word檔案（DOC檔案）。 您可以使用Document Security使用者端API來操作這些檔案型別。 支援下列版本：

* Microsoft Office 2003檔案（DOC、XLS、PPT檔案）
* Microsoft Office 2007檔案（DOCX、XLSX、PPTX檔案）
* PTC Pro/E檔案

為清楚起見，以下兩節討論如何使用Word檔案：

* [將原則套用至Word檔案](protecting-documents-policies.md#applying-policies-to-word-documents)
* [從Word檔案移除原則](protecting-documents-policies.md#removing-policies-from-word-documents)

您可以使用Document Security服務完成這些工作：

* 建立原則。 如需詳細資訊，請參閱 [建立原則](protecting-documents-policies.md#creating-policies).
* 修改原則。 如需詳細資訊，請參閱 [修改原則](protecting-documents-policies.md#modifying-policies).
* 刪除原則。 如需詳細資訊，請參閱 [刪除原則](protecting-documents-policies.md#deleting-policies).
* 套用原則至PDF檔案。 如需詳細資訊，請參閱 [套用原則至PDF檔案](protecting-documents-policies.md#applying-policies-to-pdf-documents).
* 從PDF檔案中移除原則。 如需詳細資訊，請參閱 [從PDF檔案中移除原則](protecting-documents-policies.md#removing-policies-from-pdf-documents).
* Inspect受原則保護的檔案。 如需詳細資訊，請參閱 [檢查受原則保護的PDF檔案](protecting-documents-policies.md#inspecting-policy-protected-pdf-documents).
* 撤銷PDF檔案的存取權。 如需詳細資訊，請參閱 [撤銷對檔案的存取權](protecting-documents-policies.md#revoking-access-to-documents).
* 恢復對已撤銷檔案的存取權。 如需詳細資訊，請參閱 [恢復對已撤銷檔案的存取](protecting-documents-policies.md#reinstating-access-to-revoked-documents).
* 建立浮水印。 如需詳細資訊，請參閱 [建立浮水印](protecting-documents-policies.md#creating-watermarks).
* 搜尋事件。 如需詳細資訊，請參閱 [搜尋事件](protecting-documents-policies.md#searching-for-events).

>[!NOTE]
>
>如需Document Security服務的詳細資訊，請參閱 [AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63).

## 建立原則 {#creating-policies}

您可以使用Document Security Java API或Web服務API，以程式設計方式建立原則。 A *原則* 是包含Document Security設定、授權使用者和使用許可權的資訊集合。 您可以使用適用於不同情況和使用者的安全性設定，建立並儲存任意數量的原則。

原則可讓您執行下列工作：

* 指定可以開啟檔案的個人。 收件者可以屬於或屬於您的組織。
* 指定收件者如何使用檔案。 您可以限制存取不同的Acrobat和Adobe Reader功能。 這些功能包括列印和複製文字、新增簽名以及在檔案中新增註解的功能。
* 隨時變更存取權及安全性設定，即使在您散發受原則保護的檔案後亦然。
* 在您分發檔案後監視檔案的使用。 您可以檢視檔案的使用方式以及誰正在使用它。 例如，您可以找出何時有人開啟了檔案。

### 使用Web服務建立原則 {#creating-a-policy-using-web-services}

使用Web服務API建立原則時，請參考說明原則的現有Portable Document Rights Language (PDRL) XML檔案。 原則許可權和主體在PDRL檔案中定義。 下列XML檔案是PDRL檔案的範例。

```xml
 <?xml version="1.0" encoding="UTF-8" standalone="yes"?>
 <Policy PolicyInstanceVersion="1" PolicyID="5DA3F847-DE76-F9CC-63EA-49A8D59154DE" PolicyCreationTime="2004-08-30T00:02:28.294+00:00" PolicyType="1" PolicySchemaVersion="1.0" PolicyName="SDK Test Policy -4344050357301573237" PolicyDescription="An SDK Test policy" xmlns="https://www.adobe.com/schema/1.0/pdrl">
       <PolicyEntry>
          <ns1:Permission PermissionName="com.adobe.aps.onlineOpen" Access="ALLOW" xmlns:ns1="https://www.adobe.com/schema/1.0/pdrl" xmlns="https://www.adobe.com/schema/1.0/pdrl-ex" />
 
          <ns2:Permission PermissionName="com.adobe.aps.offlineOpen" Access="ALLOW" xmlns:ns2="https://www.adobe.com/schema/1.0/pdrl" xmlns="https://www.adobe.com/schema/1.0/pdrl-ex" />
 
          <ns3:Permission PermissionName="com.adobe.aps.pdf.editNotes" Access="ALLOW" xmlns:ns3="https://www.adobe.com/schema/1.0/pdrl" xmlns="https://www.adobe.com/schema/1.0/pdrl-ex" />
 
          <ns4:Permission PermissionName="com.adobe.aps.pdf.fillAndSign" Access="ALLOW" xmlns:ns4="https://www.adobe.com/schema/1.0/pdrl" xmlns="https://www.adobe.com/schema/1.0/pdrl-ex" />
          <Principal PrincipalNameType="SYSTEM">
             <PrincipalDomain>EDC_SPECIAL</PrincipalDomain>
 
             <PrincipalName>all_internal_users</PrincipalName>
          </Principal>
       </PolicyEntry>
       <PolicyEntry>
          <ns5:Permission PermissionName="com.adobe.aps.onlineOpen" Access="ALLOW" xmlns:ns5="https://www.adobe.com/schema/1.0/pdrl" xmlns="https://www.adobe.com/schema/1.0/pdrl-ex" />
 
          <ns6:Permission PermissionName="com.adobe.aps.offlineOpen" Access="ALLOW" xmlns:ns6="https://www.adobe.com/schema/1.0/pdrl" xmlns="https://www.adobe.com/schema/1.0/pdrl-ex" />
 
          <ns7:Permission PermissionName="com.adobe.aps.pdf.copy" Access="ALLOW" xmlns:ns7="https://www.adobe.com/schema/1.0/pdrl" xmlns="https://www.adobe.com/schema/1.0/pdrl-ex" />
 
          <ns8:Permission PermissionName="com.adobe.aps.pdf.printLow" Access="ALLOW" xmlns="https://www.adobe.com/schema/1.0/pdrl-ex" xmlns:ns8="https://www.adobe.com/schema/1.0/pdrl" />
 
          <ns9:Permission PermissionName="com.adobe.aps.policySwitch" Access="ALLOW" xmlns:ns9="https://www.adobe.com/schema/1.0/pdrl" xmlns="https://www.adobe.com/schema/1.0/pdrl-ex" />
 
          <ns10:Permission PermissionName="com.adobe.aps.revoke" Access="ALLOW" xmlns="https://www.adobe.com/schema/1.0/pdrl-ex" xmlns:ns10="https://www.adobe.com/schema/1.0/pdrl" />
 
          <ns11:Permission PermissionName="com.adobe.aps.pdf.edit" Access="ALLOW" xmlns:ns11="https://www.adobe.com/schema/1.0/pdrl" xmlns="https://www.adobe.com/schema/1.0/pdrl-ex" />
 
          <ns12:Permission PermissionName="com.adobe.aps.pdf.editNotes" Access="ALLOW" xmlns:ns12="https://www.adobe.com/schema/1.0/pdrl" xmlns="https://www.adobe.com/schema/1.0/pdrl-ex" />
 
          <ns13:Permission PermissionName="com.adobe.aps.pdf.fillAndSign" Access="ALLOW" xmlns:ns13="https://www.adobe.com/schema/1.0/pdrl" xmlns="https://www.adobe.com/schema/1.0/pdrl-ex" />
 
          <ns14:Permission PermissionName="com.adobe.aps.pdf.printHigh" Access="ALLOW" xmlns:ns14="https://www.adobe.com/schema/1.0/pdrl" xmlns="https://www.adobe.com/schema/1.0/pdrl-ex" />
 
          <Principal PrincipalNameType="SYSTEM">
             <PrincipalDomain>EDC_SPECIAL</PrincipalDomain>
 
             <PrincipalName>publisher</PrincipalName>
          </Principal>
       </PolicyEntry>
 
       <OfflineLeasePeriod>
          <Duration>P31D</Duration>
       </OfflineLeasePeriod>
 
       <AuditSettings isTracked="true" />
 
       <PolicyValidityPeriod isAbsoluteTime="false">
          <ValidityPeriodRelative>
             <NotBeforeRelative>PT0S</NotBeforeRelative>
 
             <NotAfterRelative>P20D</NotAfterRelative>
          </ValidityPeriodRelative>
       </PolicyValidityPeriod>
 </Policy>
 
```

>[!NOTE]
>
>如需Document Security服務的詳細資訊，請參閱 [AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63).

### 步驟摘要 {#summary-of-steps}

若要建立原則，請執行下列步驟：

1. 包含專案檔案。
1. 建立Document Security使用者端API物件。
1. 設定原則的屬性。
1. 建立原則專案。
1. 註冊原則。

**包含專案檔案**

將必要的檔案納入您的開發專案中。 如果您使用Java建立使用者端應用程式，請包含必要的JAR檔案。 如果您使用Web服務，請務必包含Proxy檔案。

下列JAR檔案必須新增到專案的類別路徑中：

* adobe-rightsmanagement-client.jar
* namespace.jar (如果AEM Forms部署在JBoss上)
* jaxb-api.jar (如果AEM Forms部署在JBoss上)
* jaxb-impl.jar (如果AEM Forms部署在JBoss上)
* jaxb-libs.jar (如果AEM Forms部署在JBoss上)
* jaxb-xjc.jar (如果AEM Forms部署在JBoss上)
* relaxngDatatype.jar (如果AEM Forms部署在JBoss上)
* xsdlib.jar (如果AEM Forms部署在JBoss上)
* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar
* jbossall-client.jar (如果AEM Forms未部署在JBoss上，請使用其他JAR檔案)

有關這些JAR檔案位置的資訊，請參見 [包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**建立Document Security使用者端API物件**

以程式設計方式執行Document Security服務操作之前，請先建立Document Security服務使用者端物件。

**設定原則的屬性**

若要建立原則，請設定原則屬性。 強制屬性是原則名稱。 每個原則集的原則名稱必須是唯一的。 原則集只是原則的集合。 如果原則屬於不同的原則集，則可能有兩個同名原則。 但是，單一原則集內的兩個原則不能有相同的原則名稱。

另一個要設定的實用屬性是有效期。 有效期間是指獲授權的收件者可存取受原則保護檔案的時段。 如果您未設定此屬性，則原則一律有效。

有效期可以設定為下列選項之一：

* 從檔案發佈之日開始可存取檔案的設定天數
* 無法存取檔案的結束日期
* 可存取檔案的特定日期範圍
* 一律有效

您可以只指定開始日期，這會導致原則在開始日期之後有效。 如果您只指定結束日期，則原則在結束日期之前有效。 但是，如果未定義開始日期和結束日期，則會擲回例外狀況。

設定屬於原則的屬性時，您也可以設定加密設定。 這些加密設定會在原則套用至檔案時生效。 您可以指定下列加密值：

* **AES256**：代表使用256位元金鑰的AES加密演演算法。
* **AES128**：代表使用128位元金鑰的AES加密演演算法。
* **NoEncryption：** 表示沒有加密。

指定 `NoEncryption` 選項，則無法設定 `PlaintextMetadata` 選項至 `false`. 如果您嘗試這麼做，則會擲回例外狀況。

>[!NOTE]
>
>如需可設定的其他屬性的相關資訊，請參閱 `Policy` 中的介面說明 [AEM Forms API參考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

**建立原則專案**

原則專案會附加主體（群組和使用者）以及原則的許可權。 原則必須至少有一個原則專案。 例如，假設您執行下列工作：

* 建立並註冊原則專案，讓群組僅能線上上時檢視檔案，並禁止收件者複製檔案。
* 將原則專案附加至原則。
* 使用Acrobat以原則保護檔案。

這些動作會導致收件者僅能線上上檢視檔案，而無法複製檔案。 檔案會保持安全狀態，直到安全性從其中移除為止。

**註冊原則**

必須先註冊新原則，才能使用。 註冊原則之後，您可以使用它來保護檔案。

### 使用Java API建立原則 {#create-a-policy-using-the-java-api}

使用Document Security API (Java)建立原則：

1. 包含專案檔案。

   在您的Java專案的類別路徑中包含使用者端JAR檔案，例如adobe-rightsmanagement-client.jar。

1. 建立Document Security使用者端API物件。

   * 建立 `ServiceClientFactory` 包含連線屬性的物件。
   * 建立 `DocumentSecurityClient` 物件，使用它的建構函式並傳遞 `ServiceClientFactory` 物件。

1. 設定原則的屬性。

   * 建立 `Policy` 物件(透過叫用 `InfomodelObjectFactory` 物件的靜態 `createPolicy` 方法。 此方法會傳回 `Policy` 物件。
   * 透過叫用 `Policy` 物件的 `setName` 並傳遞指定原則名稱的字串值。
   * 透過叫用 `Policy` 物件的 `setDescription` 並傳遞指定原則說明的字串值。
   * 透過叫用「 」設定新原則所屬的原則集 `Policy` 物件的 `setPolicySetName` 方法並傳遞指定原則集名稱的字串值。 (您可以指定 `null` ，此引數值會導致原則新增至 *我的原則* 原則集)。
   * 透過叫用「 」來建立原則的有效期。 `InfomodelObjectFactory` 物件的靜態 `createValidityPeriod` 方法。 此方法會傳回 `ValidityPeriod` 物件。
   * 設定受原則保護檔案可存取的天數，方法是叫用 `ValidityPeriod` 物件的 `setRelativeExpirationDays` 方法，並傳遞指定天數的整數值。
   * 透過叫用 `Policy` 物件的 `setValidityPeriod` 方法和傳遞 `ValidityPeriod` 物件。

1. 建立原則專案。

   * 透過叫用原則專案來建立原則專案 `InfomodelObjectFactory` 物件的靜態 `createPolicyEntry` 方法。 此方法會傳回 `PolicyEntry` 物件。
   * 透過叫用指定原則的許可權 `InfomodelObjectFactory` 物件的靜態 `createPermission` 方法。 傳遞屬於的靜態資料成員 `Permission` 代表許可權的介面。 此方法會傳回 `Permission` 物件。 例如，若要新增允許使用者從受原則保護的PDF檔案複製資料的許可權，請傳遞 `Permission.COPY`. （對每個要新增的許可權重複此步驟）。
   * 透過叫用 `PolicyEntry` 物件的 `addPermission` 方法和傳遞 `Permission` 物件。 (針對每個重複此步驟 `Permission` 您所建立的物件)。
   * 透過叫用原則主體 `InfomodelObjectFactory` 物件的靜態 `createSpecialPrincipal` 方法。 傳遞屬於下列專案的資料成員： `InfomodelObjectFactory` 代表主體的物件。 此方法會傳回 `Principal` 物件。 例如，若要新增檔案的發行者作為主體，請傳遞 `InfomodelObjectFactory.PUBLISHER_PRINCIPAL`.
   * 透過叫用 `PolicyEntry` 物件的 `setPrincipal`方法和傳遞 `Principal` 物件。
   * 透過叫用「 」將原則專案新增到原則中 `Policy` 物件的 `addPolicyEntry` 方法和傳遞 `PolicyEntry` 物件。

1. 註冊原則。

   * 建立 `PolicyManager` 物件(透過叫用 `DocumentSecurityClient` 物件的 `getPolicyManager` 方法。
   * 透過叫用原則來註冊原則 `PolicyManager` 物件的 `registerPolicy` 並傳遞下列值：

      * 此 `Policy` 代表要註冊之原則的物件。
   * 字串值，代表原則所屬的原則集。

   如果您在連線設定中使用AEM表單管理員帳戶來建立 `DocumentSecurityClient` 物件，然後在您叫用時指定原則集名稱 `registerPolicy` 方法。 如果您傳入 `null` 值，則會在管理員中建立原則 *我的原則* 原則集。

   如果您在連線設定中使用Document Security使用者，則可以叫用多載 `registerPolicy` 僅接受原則的方法。 也就是說，您不需要指定原則集名稱。 但是，會將原則新增至名為的原則集 *我的原則*. 如果您不想將新原則新增至這個原則集，請在叫用時指定原則集名稱 `registerPolicy` 方法。

   >[!NOTE]
   >
   >建立原則時，請參考現有的原則集。 如果您指定的原則集不存在，則會擲回例外狀況。

如需使用Document Security服務的程式碼範例，請參閱以下內容：

* 「快速入門（SOAP模式）：使用Java API建立原則」

### 使用Web服務API建立原則 {#create-a-policy-using-the-web-service-api}

使用Document Security API （Web服務）建立原則：

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET專案。 請確定您使用下列WSDL定義： `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Replace `localhost` 搭配裝載AEM Forms之伺服器的IP位址。

1. 建立Document Security使用者端API物件。

   * 建立 `DocumentSecurityServiceClient` 物件（使用其預設建構函式）。
   * 建立 `DocumentSecurityServiceClient.Endpoint.Address` 物件，使用 `System.ServiceModel.EndpointAddress` 建構函式。 將指定WSDL的字串值傳遞至AEM Forms服務(例如， `http://localhost:8080/soap/services/RightsManagementService?WSDL`.) 您不需要使用 `lc_version` 屬性。 當您建立服務參考時，會使用此屬性。)
   * 建立 `System.ServiceModel.BasicHttpBinding` 物件，方法是取得 `RightsManagementServiceClient.Endpoint.Binding` 欄位。 將傳回值轉換為 `BasicHttpBinding`.
   * 設定 `System.ServiceModel.BasicHttpBinding` 物件的 `MessageEncoding` 欄位至 `WSMessageEncoding.Mtom`. 此值可確保使用MTOM。
   * 執行下列工作來啟用基本HTTP驗證：

      * 將AEM表單使用者名稱指派給欄位 `RightsManagementServiceClient.ClientCredentials.UserName.UserName`.
      * 將對應的密碼值指派給欄位 `RightsManagementServiceClient.ClientCredentials.UserName.Password`.
      * 指派常數值 `HttpClientCredentialType.Basic` 至欄位 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * 指派常數值 `BasicHttpSecurityMode.TransportCredentialOnly` 至欄位 `BasicHttpBindingSecurity.Security.Mode`.


1. 設定原則的屬性。

   * 建立 `PolicySpec` 物件（使用其建構函式）。
   * 將字串值指派給，以設定原則的名稱 `PolicySpec` 物件的 `name` 資料成員。
   * 將字串值指派給，以設定原則的描述 `PolicySpec` 物件的 `description` 資料成員。
   * 將字串值指派給，以設定原則將屬於的原則集 `PolicySpec` 物件的 `policySetName` 資料成員。 您必須指定現有的原則集名稱。 (您可以指定 `null` ，此引數值會導致原則被新增至 *我的原則*.)
   * 將整數值指派給，以設定原則的離線租期 `PolicySpec` 物件的 `offlineLeasePeriod` 資料成員。
   * 設定 `PolicySpec` 物件的 `policyXml` 具有代表PDRL XML資料的字串值的資料成員。 若要執行此工作，請建立.NET `StreamReader` 物件（使用其建構函式）。 將代表原則的PDRL XML檔案位置傳遞給 `StreamReader` 建構函式。 接下來，叫用 `StreamReader` 物件的 `ReadLine` 方法將傳回值指派給字串變數。 循環瀏覽 `StreamReader` 物件，直到 `ReadLine` 方法傳回null。 將字串變數指派給 `PolicySpec` 物件的 `policyXml` 資料成員。

1. 建立原則專案。

   使用Document Security Web服務API建立原則時，不需要建立原則專案。 原則專案是在PDRL檔案中定義的。

1. 註冊原則。

   透過叫用原則來註冊原則 `DocumentSecurityServiceClient` 物件的 `registerPolicy` 並傳遞下列值：

   * 此 `PolicySpec` 代表要註冊之原則的物件。
   * 字串值，代表原則所屬的原則集。 您可以指定 `null` 將原則新增至的值 *MyPolicy* 原則集。

   如果您在連線設定中使用AEM表單管理員帳戶來建立 `DocumentSecurityClient` 物件時，請指定原則集名稱。 `registerPolicy` 方法。

   如果您在連線設定中使用Document SecurityDocument Security使用者，則可以叫用多載 `registerPolicy` 僅接受原則的方法。 也就是說，您不需要指定原則集名稱。 但是，會將原則新增至名為的原則集 *我的原則*. 如果您不想將新原則新增至這個原則集，請在叫用時指定原則集名稱 `registerPolicy` 方法。

   >[!NOTE]
   >
   >建立原則並指定原則集時，請確定您指定現有的原則集。 如果您指定的原則集不存在，則會擲回例外狀況。

如需使用Document Security服務的程式碼範例，請參閱下列快速入門：

* 「快速入門(MTOM)：使用Web服務API建立原則」
* 「快速入門(SwaRef)：使用網站服務API建立原則」

## 修改原則 {#modifying-policies}

您可以使用Document Security Java API或Web服務API修改現有原則。 若要變更現有原則，您可以擷取並修改該原則，然後在伺服器上更新該原則。 例如，假設您擷取現有原則並延長其有效期。 在變更生效之前，您必須更新原則。

當業務需求變更且原則不再反映這些需求時，您可以修改原則。 您可以直接更新現有原則，而不用建立新原則。

若要使用Web服務（例如，使用以JAX-WS建立的Java Proxy類別）修改原則屬性，您必須確保該原則已向Document Security服務註冊。 然後，您可以使用 `PolicySpec.getPolicyXml` 方法，並使用適用方法修改原則屬性。 例如，您可以透過叫用 `PolicySpec.setOfflineLeasePeriod` 方法。

>[!NOTE]
>
>如需Document Security服務的詳細資訊，請參閱 [AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63).

### 步驟摘要 {#summary_of_steps-1}

若要修改現有原則，請執行下列步驟：

1. 包含專案檔案。
1. 建立Document Security使用者端API物件。
1. 擷取現有原則。
1. 變更原則屬性。
1. 更新原則。

**包含專案檔案**

將必要的檔案納入您的開發專案中。 如果您使用Java建立使用者端應用程式，請包含必要的JAR檔案。 如果您使用Web服務，請務必包含Proxy檔案。

**建立Document Security使用者端API物件**

您必須先建立Document Security服務使用者端物件，才能以程式設計方式執行Document Security服務操作。 如果您使用Java API，請建立 `RightsManagementClient` 物件。 如果您使用Document Security Web服務API，請建立 `RightsManagementServiceService` 物件。

**擷取現有原則**

您必須擷取現有原則才能進行修改。 若要擷取原則，請指定原則名稱和原則所屬的原則集。 如果您指定 `null` 值作為原則集名稱，此原則是從 *我的原則* 原則集。

**設定原則的屬性**

若要修改原則，請修改原則屬性的值。 唯一不能變更的原則屬性是name屬性。 例如，若要變更原則的離線租期，您可以修改原則的離線租期屬性的值。

使用Web服務修改原則的離線租期時， `offlineLeasePeriod` 欄位 `PolicySpec` 已忽略介面。 若要更新離線租期，請修改 `OfflineLeasePeriod` PDRL XML檔案中的元素。 然後使用參照更新的PDRL XML檔案 `PolicySpec` 介面的 `policyXML` 資料成員。

>[!NOTE]
>
>如需可設定的其他屬性的相關資訊，請參閱 `Policy` 中的介面說明 [AEM Forms API參考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

**更新原則**

在您對原則進行的變更生效之前，必須使用Document Security服務更新該原則。 保護檔案的原則變更會在下次受原則保護的檔案與Document Security服務同步時更新。

### 使用Java API修改現有原則 {#modify-existing-policies-using-the-java-api}

使用Document Security API (Java)修改現有原則：

1. 包含專案檔案。

   在您的Java專案的類別路徑中包含使用者端JAR檔案，例如adobe-rightsmanagement-client.jar。

1. 建立Document Security使用者端API物件。

   * 建立 `ServiceClientFactory` 包含連線屬性的物件。
   * 建立 `RightsManagementClient` 物件，使用它的建構函式並傳遞 `ServiceClientFactory` 物件。

1. 擷取現有原則。

   * 建立 `PolicyManager` 物件(透過叫用 `RightsManagementClient` 物件的 `getPolicyManager` 方法。
   * 建立 `Policy` 代表要更新之原則的物件(透過叫用 `PolicyManager` 物件的 `getPolicy` 並傳遞下列值」

      * 字串值，代表原則所屬的原則集名稱。 您可以指定 `null` 這會導致 `MyPolicies` 正在使用的原則集。
      * 代表原則名稱的字串值。

1. 設定原則的屬性。

   變更原則的屬性以符合您的業務需求。 例如，若要變更原則的離線租期，請叫用 `Policy` 物件的 `setOfflineLeasePeriod` 方法。

1. 更新原則。

   透過叫用更新原則 `PolicyManager` 物件的 `updatePolicy` 方法。 傳遞 `Policy` 代表要更新之原則的物件。

**程式碼範例**

如需使用Document Security服務的程式碼範例，請參閱快速入門（SOAP模式）：使用Java API修改原則一節。

### 使用Web服務API修改現有原則 {#modify-existing-policies-using-the-web-service-api}

使用Document Security API （Web服務）修改現有原則：

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET專案。 請確定您使用下列WSDL定義： `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Replace `localhost` 搭配裝載AEM Forms之伺服器的IP位址。

1. 建立Document Security使用者端API物件。

   * 建立 `RightsManagementServiceClient` 物件（使用其預設建構函式）。
   * 建立 `RightsManagementServiceClient.Endpoint.Address` 物件，使用 `System.ServiceModel.EndpointAddress` 建構函式。 將指定WSDL的字串值傳遞至AEM Forms服務(例如， `http://localhost:8080/soap/services/RightsManagementService?WSDL`.) 您不需要使用 `lc_version` 屬性。 當您建立服務參考時，會使用此屬性。)
   * 建立 `System.ServiceModel.BasicHttpBinding` 物件，方法是取得 `RightsManagementServiceClient.Endpoint.Binding` 欄位。 將傳回值轉換為 `BasicHttpBinding`.
   * 設定 `System.ServiceModel.BasicHttpBinding` 物件的 `MessageEncoding` 欄位至 `WSMessageEncoding.Mtom`. 此值可確保使用MTOM。
   * 執行下列工作來啟用基本HTTP驗證：

      * 將AEM表單使用者名稱指派給欄位 `RightsManagementServiceClient.ClientCredentials.UserName.UserName`.
      * 將對應的密碼值指派給欄位 `RightsManagementServiceClient.ClientCredentials.UserName.Password`.
      * 指派常數值 `HttpClientCredentialType.Basic` 至欄位 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * 指派常數值 `BasicHttpSecurityMode.TransportCredentialOnly` 至欄位 `BasicHttpBindingSecurity.Security.Mode`.


1. 擷取現有原則。

   建立 `PolicySpec` 代表要修改之原則的物件，方法是叫用 `RightsManagementServiceClient` 物件的 `getPolicy` 並傳遞下列值：

   * 字串值，指定原則所屬的原則集名稱。 您可以指定 `null` 這會導致 `MyPolicies` 正在使用的原則集。
   * 字串值，指定原則的名稱。

1. 設定原則的屬性。

   變更原則的屬性以符合您的業務需求。

1. 更新原則。

   透過叫用 `RightsManagementServiceClient` 物件的 `updatePolicyFromSDK` 方法和傳遞 `PolicySpec` 代表要更新之原則的物件。

**程式碼範例**

如需使用Document Security服務的程式碼範例，請參閱下列快速入門：

* 「快速入門(MTOM)：使用Web服務API修改原則」
* 「快速入門(SwaRef)：使用Web服務API修改原則」

## 刪除原則 {#deleting-policies}

您可以使用Document Security Java API或Web服務API刪除現有原則。 刪除原則後，就無法再用來保護檔案。 不過，使用原則的現有受原則保護檔案仍受保護。 您可以在有較新原則可用時刪除原則。

>[!NOTE]
>
>如需Document Security服務的詳細資訊，請參閱 [AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63).

### 步驟摘要 {#summary_of_steps-2}

若要刪除現有原則，請執行下列步驟：

1. 包含專案檔案
1. 建立Document Security使用者端API物件。
1. 刪除原則。

**包含專案檔案**

將必要的檔案納入您的開發專案中。 如果您使用Java建立使用者端應用程式，請包含必要的JAR檔案。 如果您使用Web服務，請務必包含Proxy檔案。

**建立Document Security使用者端API物件**

您必須先建立Document Security服務使用者端物件，才能以程式設計方式執行Document Security服務操作。 如果您使用Java API，請建立 `RightsManagementClient` 物件。 如果您使用Document Security Web服務API，請建立 `RightsManagementServiceService` 物件。

**刪除原則**

若要刪除原則，您可以指定要刪除的原則以及該原則所屬的原則集。 其設定用於叫用AEM Forms的使用者必須擁有刪除原則的許可權；否則會發生例外狀況。 同樣地，如果您嘗試刪除不存在的原則，則會發生例外狀況。

### 使用Java API刪除原則 {#delete-policies-using-the-java-api}

使用Document Security API (Java)刪除原則：

1. 包含專案檔案。

   在您的Java專案的類別路徑中包含使用者端JAR檔案，例如adobe-rightsmanagement-client.jar。

1. 建立Document Security使用者端API物件。

   * 建立 `ServiceClientFactory` 包含連線屬性的物件。
   * 建立 `RightsManagementClient` 物件，使用它的建構函式並傳遞 `ServiceClientFactory` 物件。

1. 刪除原則。

   * 建立 `PolicyManager` 物件(透過叫用 `RightsManagementClient` 物件的 `getPolicyManager` 方法。
   * 透過叫用原則來刪除原則 `PolicyManager` 物件的 `deletePolicy` 並傳遞下列值：

      * 字串值，指定原則所屬的原則集名稱。 您可以指定 `null` 這會導致 `MyPolicies` 正在使用的原則集。
      * 字串值，指定要刪除之原則的名稱。

**程式碼範例**

如需使用Document Security服務的程式碼範例，請參閱下列快速入門：

* 「快速入門（SOAP模式）：使用Java API刪除原則」

### 使用Web服務API刪除原則 {#delete-policies-using-the-web-service-api}

使用Document Security API （Web服務）刪除原則：

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET專案。 請確定您使用下列WSDL定義： `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Replace `localhost` 搭配裝載AEM Forms之伺服器的IP位址。

1. 建立Document Security使用者端API物件。

   * 建立 `RightsManagementServiceClient` 物件（使用其預設建構函式）。
   * 建立 `RightsManagementServiceClient.Endpoint.Address` 物件，使用 `System.ServiceModel.EndpointAddress` 建構函式。 將指定WSDL的字串值傳遞至AEM Forms服務(例如， `http://localhost:8080/soap/services/RightsManagementService?WSDL`.) 您不需要使用 `lc_version` 屬性。 當您建立服務參考時，會使用此屬性。)
   * 建立 `System.ServiceModel.BasicHttpBinding` 物件，方法是取得 `RightsManagementServiceClient.Endpoint.Binding` 欄位。 將傳回值轉換為 `BasicHttpBinding`.
   * 設定 `System.ServiceModel.BasicHttpBinding` 物件的 `MessageEncoding` 欄位至 `WSMessageEncoding.Mtom`. 此值可確保使用MTOM。
   * 執行下列工作來啟用基本HTTP驗證：

      * 將AEM表單使用者名稱指派給欄位 `RightsManagementServiceClient.ClientCredentials.UserName.UserName`.
      * 將對應的密碼值指派給欄位 `RightsManagementServiceClient.ClientCredentials.UserName.Password`.
      * 指派常數值 `HttpClientCredentialType.Basic` 至欄位 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * 指派常數值 `BasicHttpSecurityMode.TransportCredentialOnly` 至欄位 `BasicHttpBindingSecurity.Security.Mode`.


1. 刪除原則。

   透過叫用原則來刪除原則 `RightsManagementServiceClient` 物件的 `deletePolicy` 並傳遞下列值：

   * 字串值，指定原則所屬的原則集名稱。 您可以指定 `null` 這會導致 `MyPolicies` 正在使用的原則集。
   * 字串值，指定要刪除之原則的名稱。

**程式碼範例**

如需使用Document Security服務的程式碼範例，請參閱下列快速入門：

* 「快速入門(MTOM)：使用Web服務API刪除原則」
* 「快速入門(SwaRef)：使用網站服務API刪除原則」

## 套用原則至PDF檔案 {#applying-policies-to-pdf-documents}

您可以將原則套用至PDF檔案，以保護檔案。 透過將原則套用到PDF檔案，您可以限制對檔案的存取。 如果檔案已受原則保護，則無法將原則套用至檔案。

檔案開啟時，您也可以限制對Acrobat和Adobe Reader功能的存取，包括列印和複製文字、進行變更以及將簽名和註解新增到檔案的功能。 此外，當您不再希望使用者存取受原則保護的PDF檔案時，也可以撤銷該檔案。

您可以在分發受原則保護的檔案後，監視該檔案的使用。 也就是說，您可以看到檔案的使用方式以及誰在使用檔案。 例如，您可以找出何時有人開啟了檔案。

>[!NOTE]
>
>如需Document Security服務的詳細資訊，請參閱 [AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63).

### 步驟摘要 {#summary_of_steps-3}

若要將原則套用至PDF檔案，請執行下列步驟：

1. 包含專案檔案。
1. 建立Document Security使用者端API物件。
1. 擷取套用了原則的PDF檔案。
1. 將現有原則套用至PDF檔案。
1. 儲存受原則保護的PDF檔案。

**包含專案檔案**

將必要的檔案納入您的開發專案中。 如果您使用Java建立使用者端應用程式，請包含必要的JAR檔案。 如果您使用Web服務，請務必包含Proxy檔案。

**建立Document Security使用者端API物件**

以程式設計方式執行Document Security服務操作之前，請先建立Document Security服務使用者端物件。 如果您使用Java API，請建立 `DocumentSecurityClient` 物件。 如果您使用Document Security Web服務API，請建立 `DocumentSecurityServiceService` 物件。

**擷取PDF檔案**

您可以擷取PDF檔案以套用原則。 將原則套用至PDF檔案後，使用者使用檔案時會受到限制。 例如，如果原則未允許在離線時開啟檔案，則使用者必須線上上才能開啟檔案。

**將現有原則套用至PDF檔案**

若要將原則套用至PDF檔案，請參照現有原則並指定該原則所屬的原則集。 設定連線屬性的使用者必須擁有指定原則的存取權。 如果沒有，會發生例外狀況。

**儲存PDF檔案**

在Document Security服務將原則套用至PDF檔案後，您可以將受原則保護的PDF檔案儲存為PDF檔案。

**另请参阅**

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[撤銷對檔案的存取權](protecting-documents-policies.md#revoking-access-to-documents)

### 使用Java API將原則套用至PDF檔案 {#apply-a-policy-to-a-pdf-document-using-the-java-api}

使用Document Security API (Java)將原則套用至PDF檔案：

1. 包含專案檔案。

   在您的Java專案的類別路徑中包含使用者端JAR檔案，例如adobe-rightsmanagement-client.jar。

1. 建立Document Security使用者端API物件。

   * 建立 `ServiceClientFactory` 包含連線屬性的物件。
   * 建立 `RightsManagementClient` 物件，使用它的建構函式並傳遞 `ServiceClientFactory` 物件。

1. 擷取PDF檔案。

   * 建立 `java.io.FileInputStream` 物件，使用它的建構函式代表PDF檔案。 傳遞字串值，指定PDF檔案的位置。
   * 建立 `com.adobe.idp.Document` 物件，使用它的建構函式並傳遞 `java.io.FileInputStream` 物件。

1. 將現有原則套用至PDF檔案。

   * 建立 `DocumentManager` 物件(透過叫用 `RightsManagementClient` 物件的 `getDocumentManager` 方法。
   * 透過叫用「 」，將原則套用到PDF檔案 `DocumentManager` 物件的 `protectDocument` 並傳遞下列值：

      * 此 `com.adobe.idp.Document` 包含套用原則之PDF檔案的物件。
      * 字串值，指定檔案的名稱。
      * 字串值，指定原則所屬的原則集名稱。 您可以指定 `null` 導致下列專案的值： `MyPolicies` 正在使用的原則集。
      * 字串值，指定原則名稱。
      * 字串值，代表檔案發行者使用者的使用者管理員網域名稱。 此引數值為選用值，可為Null （若此引數為Null，則下一個引數值必須為Null）。
      * 字串值，代表作為檔案發行者的使用者管理員使用者的正式名稱名稱。 此引數值為選用值，可以是 `null` (如果此引數為null，則先前的引數值必須是 `null`)。
      * A `com.adobe.livecycle.rightsmanagement.Locale` 代表用於選取MS Office範本的地區設定。 此引數值為選用值，不用於PDF檔案。 若要保護PDF檔案，請指定 `null`.

      此 `protectDocument` 方法傳回 `RMSecureDocumentResult` 包含受原則保護的PDF檔案的物件。


1. 儲存PDF檔案。

   * 叫用 `RMSecureDocumentResult` 物件的 `getProtectedDoc` 取得受原則保護的PDF檔案的方法。 此方法會傳回 `com.adobe.idp.Document` 物件。
   * 建立 `java.io.File` 物件，並確認副檔名為PDF。
   * 叫用 `com.adobe.idp.Document` 物件的 `copyToFile` 複製目錄內容的方法 `Document` 物件放入檔案(請確定您使用 `Document` 物件，由 `getProtectedDoc` 方法)。

**程式碼範例**

如需使用Document Security服務的程式碼範例，請參閱下列快速入門：

* 「快速入門（EJB模式）：使用Java API將原則套用至PDF檔案」
* 「快速入門（SOAP模式）：使用Java API將原則套用至PDF檔案」

**另请参阅**

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服務API將原則套用至PDF檔案 {#apply-a-policy-to-a-pdf-document-using-the-web-service-api}

使用Document Security API （Web服務）將原則套用至PDF檔案：

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET專案。 請確定您使用下列WSDL定義： `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Replace `localhost` 搭配裝載AEM Forms之伺服器的IP位址。

1. 建立Document Security使用者端API物件。

   * 建立 `RightsManagementServiceClient` 物件（使用其預設建構函式）。
   * 建立 `RightsManagementServiceClient.Endpoint.Address` 物件，使用 `System.ServiceModel.EndpointAddress` 建構函式。 將指定WSDL的字串值傳遞至Forms服務(例如， `http://localhost:8080/soap/services/RightsManagementService?WSDL`.) 您不需要使用 `lc_version` 屬性。 當您建立服務參考時，會使用此屬性。)
   * 建立 `System.ServiceModel.BasicHttpBinding` 物件，方法是取得 `RightsManagementServiceClient.Endpoint.Binding` 欄位。 將傳回值轉換為 `BasicHttpBinding`.
   * 設定 `System.ServiceModel.BasicHttpBinding` 物件的 `MessageEncoding` 欄位至 `WSMessageEncoding.Mtom`. 此值可確保使用MTOM。
   * 執行下列工作來啟用基本HTTP驗證：

      * 將AEM表單使用者名稱指派給欄位 `RightsManagementServiceClient.ClientCredentials.UserName.UserName`.
      * 將對應的密碼值指派給欄位 `RightsManagementServiceClient.ClientCredentials.UserName.Password`.
      * 指派常數值 `HttpClientCredentialType.Basic` 至欄位 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * 指派常數值 `BasicHttpSecurityMode.TransportCredentialOnly` 至欄位 `BasicHttpBindingSecurity.Security.Mode`.


1. 擷取PDF檔案。

   * 建立 `BLOB` 物件（使用其建構函式）。 此 `BLOB` 物件是用來儲存套用原則的PDF檔案。
   * 建立 `System.IO.FileStream` 物件，方法是叫用其建構函式，並傳遞代表PDF檔案的檔案位置和開啟檔案的模式的字串值。
   * 建立位元組陣列，儲存 `System.IO.FileStream` 物件。 透過取得 `System.IO.FileStream` 物件的 `Length` 屬性。
   * 叫用 `System.IO.FileStream` 物件的 `Read` 方法。 傳遞位元組陣列、起始位置以及要讀取的資料流長度。
   * 填入 `BLOB` 物件，透過指派其 `MTOM` 包含位元組陣列內容的欄位。

1. 將現有原則套用至PDF檔案。

   透過叫用「 」，將原則套用到PDF檔案 `RightsManagementServiceClient` 物件的 `protectDocument` 並傳遞下列值：

   * 此 `BLOB` 包含套用原則之PDF檔案的物件。
   * 字串值，指定檔案的名稱。
   * 字串值，指定原則所屬的原則集名稱。 您可以指定 `null` 導致下列專案的值： `MyPolicies` 正在使用的原則集。
   * 字串值，指定原則名稱。
   * 字串值，代表檔案發行者使用者的使用者管理員網域名稱。 此引數值為選用值，可為Null (若此引數為Null，則下一個引數值必須為 `null`)。
   * 字串值，代表作為檔案發行者的使用者管理員使用者的正式名稱名稱。 此引數值為選用值，可為Null (若此引數為Null，則前一個引數值必須為 `null`)。
   * A `RMLocale` 指定地區設定值的值(例如， `RMLocale.en`)。
   * 用來儲存原則識別碼值的字串輸出引數。
   * 字串輸出引數，用來儲存受原則保護的識別碼值。
   * 用來儲存MIME型別的字串輸出引數(例如， `application/pdf`)。

   此 `protectDocument` 方法傳回 `BLOB` 包含受原則保護的PDF檔案的物件。

1. 儲存PDF檔案。

   * 建立 `System.IO.FileStream` 物件，方法是叫用其建構函式，並傳遞代表受原則保護之PDF檔案的檔案位置的字串值。
   * 建立位元組陣列，儲存 `BLOB` 物件，由 `protectDocument` 方法。 透過取得 `BLOB` 物件的 `MTOM` 資料成員。
   * 建立 `System.IO.BinaryWriter` 物件，方法是叫用其建構函式並傳遞 `System.IO.FileStream` 物件。
   * PDF透過叫用 `System.IO.BinaryWriter` 物件的 `Write` 方法並傳遞位元組陣列。

**程式碼範例**

如需使用Document Security服務的程式碼範例，請參閱下列快速入門：

* 「快速入門(MTOM)：使用Web服務API將原則套用至PDF檔案」
* 「快速入門(SwaRef)：使用網站服務API將原則套用至PDF檔案」

## 從PDF檔案中移除原則 {#removing-policies-from-pdf-documents}

您可以從受原則保護的檔案中移除原則，以便從檔案中移除安全性。 亦即，如果您不再希望檔案受原則保護。 如果您想要使用較新的原則更新受原則保護的檔案，那麼與移除原則並新增更新的原則不同，切換原則會更有效率。

>[!NOTE]
>
>如需Document Security服務的詳細資訊，請參閱 [AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63).

### 步驟摘要 {#summary_of_steps-4}

若要從受原則保護的PDF檔案中移除原則，請執行下列步驟：

1. 包含專案檔案
1. 建立Document Security使用者端API物件。
1. 擷取受原則保護的PDF檔案。
1. 從PDF檔案中移除原則。
1. 儲存不安全的PDF檔案。

**包含專案檔案**

將必要的檔案納入您的開發專案中。 如果您使用Java建立使用者端應用程式，請包含必要的JAR檔案。 如果您使用Web服務，請務必包含Proxy檔案。

**建立Document Security使用者端API物件**

以程式設計方式執行Document Security服務操作之前，請先建立Document Security服務使用者端物件。

**擷取受原則保護的PDF檔案**

您可以擷取受原則保護的PDF檔案，以移除原則。 如果您嘗試從不受原則保護的PDF檔案中移除原則，則會造成例外狀況。

**從PDF檔案中移除原則**

只要連線設定中指定了管理員，您就可以從受原則保護的PDF檔案中移除原則。 如果沒有，則用來保護檔案的原則必須包含 `SWITCH_POLICY` 以從PDF檔案中移除原則的許可權。 此外，AEM Forms連線設定中指定的使用者也必須具有該許可權。 否則，會擲回例外狀況。

**儲存不安全的PDF檔案**

在Document Security服務從PDF檔案中移除原則後，您可以將不安全的PDF檔案儲存為PDF檔案。

**另请参阅**

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[套用原則至PDF檔案](protecting-documents-policies.md#applying-policies-to-pdf-documents)

### 使用Java API從PDF檔案中移除原則 {#remove-a-policy-from-a-pdf-document-using-the-java-api}

使用Document Security API (Java)從受原則保護的PDF檔案中移除原則：

1. 包含專案檔案。

   在您的Java專案的類別路徑中包含使用者端JAR檔案，例如adobe-rightsmanagement-client.jar。

1. 建立Document Security使用者端API物件。

   * 建立 `ServiceClientFactory` 包含連線屬性的物件。
   * 建立 `DocumentSecurityClient` 物件，使用它的建構函式並傳遞 `ServiceClientFactory` 物件。

1. 擷取受原則保護的PDF檔案。

   * 建立 `java.io.FileInputStream` 物件，使用原則保護的PDF檔案的建構函式，並傳遞字串值，指定PDF檔案的位置。
   * 建立 `com.adobe.idp.Document` 物件，使用它的建構函式並傳遞 `java.io.FileInputStream` 物件。

1. 從PDF檔案中移除原則。

   * 建立 `DocumentManager` 物件(透過叫用 `DocumentSecurityClient` 物件的 `getDocumentManager` 方法。
   * 叫用「 」，從PDF檔案中移除原則 `DocumentManager` 物件的 `removeSecurity` 方法和傳遞 `com.adobe.idp.Document` 包含受原則保護的PDF檔案的物件。 此方法會傳回 `com.adobe.idp.Document` 包含不安全PDF檔案的物件。

1. 儲存不安全的PDF檔案。

   * 建立 `java.io.File` 物件，並確認副檔名為PDF。
   * 叫用 `Document` 物件的 `copyToFile` 複製目錄內容的方法 `Document` 物件放入檔案(請確定您使用 `Document` 物件，由 `removeSecurity` 方法)。

**程式碼範例**

如需使用Document Security服務的程式碼範例，請參閱下列快速入門：

* 「快速入門（SOAP模式）：使用Java API從PDF檔案中移除原則」

### 使用Web服務API移除原則 {#remove-a-policy-using-the-web-service-api}

使用Document Security API （Web服務）從受原則保護的PDF檔案中移除原則：

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET專案。 請確定您使用下列WSDL定義： `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Replace `localhost` 搭配裝載AEM Forms之伺服器的IP位址。

1. 建立Document Security使用者端API物件。

   * 建立 `DocumentSecurityServiceClient` 物件（使用其預設建構函式）。
   * 建立 `DocumentSecurityServiceClient.Endpoint.Address` 物件，使用 `System.ServiceModel.EndpointAddress` 建構函式。 將指定WSDL的字串值傳遞至AEM Forms服務(例如， `http://localhost:8080/soap/services/RightsManagementService?WSDL`.) 您不需要使用 `lc_version` 屬性。 當您建立服務參考時，會使用此屬性。)
   * 建立 `System.ServiceModel.BasicHttpBinding` 物件，方法是取得 `DocumentSecurityServiceClient.Endpoint.Binding` 欄位。 將傳回值轉換為 `BasicHttpBinding`.
   * 設定 `System.ServiceModel.BasicHttpBinding` 物件的 `MessageEncoding` 欄位至 `WSMessageEncoding.Mtom`. 此值可確保使用MTOM。
   * 執行下列工作來啟用基本HTTP驗證：

      * 將AEM表單使用者名稱指派給欄位 `DocumentSecurityServiceClient.ClientCredentials.UserName.UserName`.
      * 將對應的密碼值指派給欄位 `DocumentSecurityServiceClient.ClientCredentials.UserName.Password`.
      * 指派常數值 `HttpClientCredentialType.Basic` 至欄位 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * 指派常數值 `BasicHttpSecurityMode.TransportCredentialOnly` 至欄位 `BasicHttpBindingSecurity.Security.Mode`.


1. 擷取受原則保護的PDF檔案。

   * 建立 `BLOB` 物件（使用其建構函式）。 此 `BLOB` 物件是用來儲存受原則保護的PDF檔案，原則會從中移除。
   * 建立 `System.IO.FileStream` 物件，方法是叫用其建構函式，並傳遞代表PDF檔案的檔案位置和開啟檔案的模式的字串值。
   * 建立位元組陣列，儲存 `System.IO.FileStream` 物件。 您可以取得 `System.IO.FileStream` 物件的 `Length` 屬性。
   * 叫用 `System.IO.FileStream` 物件的 `Read` 方法，並傳遞位元組陣列、起始位置以及要讀取的資料流長度。
   * 填入 `BLOB` 物件，透過指派其 `MTOM` 包含位元組陣列內容的欄位。

1. 從PDF檔案中移除原則。

   叫用「 」，從PDF檔案中移除原則 `DocumentSecurityServiceClient` 物件的 `removePolicySecurity` 方法和傳遞 `BLOB` 包含受原則保護的PDF檔案的物件。 此方法會傳回 `BLOB` 包含不安全PDF檔案的物件。

1. 儲存不安全的PDF檔案。

   * 建立 `System.IO.FileStream` 物件，方法是叫用其建構函式，並傳遞代表不安全PDF檔案檔案位置的字串值。
   * 建立位元組陣列，儲存 `BLOB` 物件，由 `removePolicySecurity` 方法。 透過取得 `BLOB` 物件的 `MTOM` 欄位。
   * 建立 `System.IO.BinaryWriter` 物件，方法是叫用其建構函式並傳遞 `System.IO.FileStream` 物件。

**程式碼範例**

如需使用Document Security服務的程式碼範例，請參閱下列快速入門：

* 「快速入門(MTOM)：使用網站服務API從PDF檔案中移除原則」
* 「快速入門(SwaRef)：使用網站服務API從PDF檔案中移除原則」

**另请参阅**

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 撤銷對檔案的存取權 {#revoking-access-to-documents}

您可以撤銷受原則保護之PDF檔案的存取權，導致使用者無法存取該檔案的所有復本。 當使用者嘗試開啟撤銷的PDF檔案時，他們被重新導向到指定的URL，可以在其中檢視修訂的檔案。 必須以程式設計方式指定要將使用者重新導向到的URL。 當您撤銷對檔案的存取權時，變更會在使用者下次透過線上開啟受原則保護的檔案與Document Security服務同步時生效。

撤銷檔案存取權的功能提供額外的安全性。 例如，假設有較新版本的檔案可用，而您不再希望任何人檢視過時的版本。 在此情況下，對舊檔案的存取權可能會被撤銷，除非恢復存取權，否則任何人都無法檢視該檔案。

>[!NOTE]
>
>如需Document Security服務的詳細資訊，請參閱 [AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63).

### 步驟摘要 {#summary_of_steps-5}

若要撤銷受原則保護的檔案，請執行下列步驟：

1. 包含專案檔案。
1. 建立Document Security使用者端API物件。
1. 擷取受原則保護的PDF檔案。
1. 撤銷受原則保護的檔案。

**包含專案檔案**

將必要的檔案納入您的開發專案中。 如果您使用Java建立使用者端應用程式，請包含必要的JAR檔案。 如果您使用Web服務，請務必包含Proxy檔案。

**建立Document Security使用者端API物件**

您必須先建立Document Security服務使用者端物件，才能以程式設計方式執行Document Security服務操作。

**擷取受原則保護的PDF檔案**

您必須擷取受原則保護的PDF檔案，才能將其撤銷。 您無法撤銷已撤銷或不是受原則保護檔案的檔案。

如果您知道受原則保護檔案的授權識別碼值，則不必擷取受原則保護的PDF檔案。 但在大多數情況下，您需要擷取PDF檔案才能取得授權識別碼值。

**撤銷受原則保護的檔案**

若要撤銷受原則保護檔案，請指定受原則保護檔案的授權識別碼。 此外，您可以指定當使用者嘗試開啟撤銷的檔案時，使用者可以檢視的檔案URL。 也就是說，假設過時檔案被撤銷。 當使用者嘗試開啟已撤銷的檔案時，他們將看到更新檔案，而不是已撤銷的檔案。

>[!NOTE]
>
>如果您嘗試撤銷已撤銷的檔案，則會擲回例外狀況。

**另请参阅**

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[套用原則至PDF檔案](protecting-documents-policies.md#applying-policies-to-pdf-documents)

[恢復對已撤銷檔案的存取](protecting-documents-policies.md#reinstating-access-to-revoked-documents)

### 使用Java API撤銷對檔案的存取權 {#revoke-access-to-documents-using-the-java-api}

使用Document Security API (Java)撤銷受原則保護的PDF檔案的存取權：

1. 包含專案檔案

   在您的Java專案的類別路徑中包含使用者端JAR檔案，例如adobe-rightsmanagement-client.jar。

1. 建立Document Security使用者端API物件

   * 建立 `ServiceClientFactory` 包含連線屬性的物件。
   * 建立 `DocumentSecurityClient` 物件，使用它的建構函式並傳遞 `ServiceClientFactory` 物件。

1. 擷取受原則保護的PDF檔案

   * 建立 `java.io.FileInputStream` 物件，使用受原則保護的PDF檔案的建構函式，並傳遞字串值(指定PDF檔案的位置)來表示該檔案。
   * 建立 `com.adobe.idp.Document` 物件，使用它的建構函式並傳遞 `java.io.FileInputStream` 物件。

1. 撤銷受原則保護的檔案

   * 建立 `DocumentManager` 物件(透過叫用 `DocumentSecurityClient` 物件的 `getDocumentManager` 方法。
   * 透過叫用受原則保護檔案的授權識別碼值 `DocumentManager` 物件的 `getLicenseId` 方法。 傳遞 `com.adobe.idp.Document` 代表受原則保護檔案的物件。 此方法會傳回代表授權識別碼值的字串值。
   * 建立 `LicenseManager` 物件(透過叫用 `DocumentSecurityClient` 物件的 `getLicenseManager` 方法。
   * 叫用受原則保護的檔案 `LicenseManager` 物件的 `revokeLicense` 並傳遞下列值：

      * 字串值，指定受原則保護檔案的授權識別碼值(指定 `DocumentManager` 物件的 `getLicenseId` 方法)。
      * 的靜態資料成員 `License` 指定撤銷檔案原因的介面。 例如，您可以指定 `License.DOCUMENT_REVISED`.
      * A `java.net.URL` 指定修訂檔案所在位置的值。 如果您不想將使用者重新導向至其他URL，則可以傳遞 `null`.

**程式碼範例**

如需使用Document Security服務的程式碼範例，請參閱下列快速入門：

* 「快速入門（SOAP模式）：使用Java API撤銷檔案」

### 使用Web服務API撤銷檔案的存取權 {#revoke-access-to-documents-using-the-web-service-api}

使用Document Security API （Web服務）撤銷受原則保護的PDF檔案的存取權：

1. 包含專案檔案

   建立使用MTOM的Microsoft .NET專案。 請確定您使用下列WSDL定義： `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Replace `localhost` 搭配裝載AEM Forms之伺服器的IP位址。

1. 建立Document Security使用者端API物件

   * 建立 `DocumentSecurityServiceClient` 物件（使用其預設建構函式）。
   * 建立 `DocumentSecurityServiceClient.Endpoint.Address` 物件，使用 `System.ServiceModel.EndpointAddress` 建構函式。 將指定WSDL的字串值傳遞至AEM Forms服務(例如， `http://localhost:8080/soap/services/RightsManagementService?WSDL`.) 您不需要使用 `lc_version` 屬性。 當您建立服務參考時，會使用此屬性。)
   * 建立 `System.ServiceModel.BasicHttpBinding` 物件，方法是取得 `DocumentSecurityServiceClient.Endpoint.Binding` 欄位。 將傳回值轉換為 `BasicHttpBinding`.
   * 設定 `System.ServiceModel.BasicHttpBinding` 物件的 `MessageEncoding` 欄位至 `WSMessageEncoding.Mtom`. 此值可確保使用MTOM。
   * 執行下列工作來啟用基本HTTP驗證：

      * 將AEM表單使用者名稱指派給欄位 `DocumentSecurityServiceClient.ClientCredentials.UserName.UserName`.
      * 將對應的密碼值指派給欄位 `DocumentSecurityServiceClient.ClientCredentials.UserName.Password`.
      * 指派常數值 `HttpClientCredentialType.Basic` 至欄位 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * 指派常數值 `BasicHttpSecurityMode.TransportCredentialOnly` 至欄位 `BasicHttpBindingSecurity.Security.Mode`.


1. 擷取受原則保護的PDF檔案

   * 建立 `BLOB` 物件（使用其建構函式）。 此 `BLOB` 物件是用來儲存已撤銷的受原則PDF檔案。
   * 建立 `System.IO.FileStream` 物件，方法是叫用其建構函式，並傳遞代表要撤銷之受原則保護之PDF檔案的檔案位置，以及開啟檔案的模式的字串值。
   * 建立位元組陣列，儲存 `System.IO.FileStream` 物件。 您可以取得 `System.IO.FileStream` 物件的 `Length` 屬性。
   * 叫用 `System.IO.FileStream` 物件的 `Read` 方法，並傳遞位元組陣列、起始位置以及要讀取的資料流長度。
   * 填入 `BLOB` 物件，透過指派其 `MTOM` 包含位元組陣列內容的欄位。

1. 撤銷受原則保護的檔案

   * 透過叫用受原則保護檔案的授權識別碼值 `DocumentSecurityServiceClient` 物件的 `getLicenseID` 方法和傳遞 `BLOB` 代表受原則保護檔案的物件。 此方法會傳回代表授權識別碼的字串值。
   * 叫用受原則保護的檔案 `DocumentSecurityServiceClient` 物件的 `revokeLicense` 並傳遞下列值：

      * 字串值，指定受原則保護檔案的授權識別碼值(指定 `DocumentSecurityServiceService` 物件的 `getLicenseId` 方法)。
      * 的靜態資料成員 `Reason` 列舉指定撤銷檔案的原因。 例如，您可以指定 `Reason.DOCUMENT_REVISED`.
      * A `string` 指定修訂檔案所在的URL位置的值。 如果您不想將使用者重新導向至其他URL，則可以傳遞 `null`.

**程式碼範例**

如需使用Document Security服務的程式碼範例，請參閱下列快速入門：

* 「快速入門(MTOM)：使用網站服務API撤銷檔案」
* 「快速入門(SwaRef)：使用網站服務API撤銷檔案」

**另请参阅**

[從Word檔案移除原則](protecting-documents-policies.md#removing-policies-from-word-documents)

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 恢復對已撤銷檔案的存取 {#reinstating-access-to-revoked-documents}

您可以恢復對已撤銷PDF檔案的存取權，讓使用者能夠存取已撤銷檔案的所有復本。 當使用者開啟已撤銷的恢復檔案時，使用者能夠檢視檔案。

>[!NOTE]
>
>如需Document Security服務的詳細資訊，請參閱 [AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63).

### 步驟摘要 {#summary_of_steps-6}

若要恢復對已撤銷PDF檔案的存取權，請執行下列步驟：

1. 包含專案檔案。
1. 建立Document Security使用者端API物件。
1. 擷取已撤銷PDF檔案的授權識別碼。
1. 恢復對已撤銷PDF檔案的存取權。

**包含專案檔案**

將必要的檔案納入您的開發專案中。 如果您使用Java建立使用者端應用程式，請包含必要的JAR檔案。 如果您使用Web服務，請務必包含Proxy檔案。

**建立Document Security使用者端API物件**

您必須先建立Document Security服務使用者端物件，才能以程式設計方式執行Document Security服務操作。 如果您使用Java API，請建立 `DocumentSecurityClient` 物件。 如果您使用Document Security Web服務API，請建立 `DocumentSecurityServiceService` 物件。

**擷取已撤銷PDF檔案的授權識別碼**

您必須擷取已撤銷PDF檔案的授權識別碼，才能恢復已撤銷PDF檔案。 取得授權識別碼值後，即可恢復已撤銷的檔案。 如果您嘗試恢復未撤銷的檔案，則會造成例外狀況。

**恢復對已撤銷PDF檔案的存取權**

若要恢復對已撤銷PDF檔案的存取權，您必須指定已撤銷檔案的授權識別碼。 如果您嘗試恢復未撤銷之PDF檔案的存取權，則會造成例外狀況。

**另请参阅**

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[套用原則至PDF檔案](protecting-documents-policies.md#applying-policies-to-pdf-documents)

[撤銷對檔案的存取權](protecting-documents-policies.md#revoking-access-to-documents)

### 使用Java API恢復對已撤銷檔案的存取 {#reinstate-access-to-revoked-documents-using-the-java-api}

使用Document Security API (Java)恢復對已撤銷檔案的存取：

1. 包含專案檔案。

   在您的Java專案的類別路徑中包含使用者端JAR檔案，例如adobe-rightsmanagement-client.jar。

1. 建立Document Security使用者端API物件。

   * 建立 `ServiceClientFactory` 包含連線屬性的物件。
   * 建立 `DocumentSecurityClient` 物件，使用它的建構函式並傳遞 `ServiceClientFactory` 物件。

1. 擷取已撤銷PDF檔案的授權識別碼。

   * 建立 `java.io.FileInputStream` 物件，使用它的建構函式並傳遞字串值(指定PDF檔案的位置)來代表已撤銷的PDF檔案。
   * 建立 `com.adobe.idp.Document` 物件，使用它的建構函式並傳遞 `java.io.FileInputStream` 物件。
   * 建立 `DocumentManager` 物件(透過叫用 `DocumentSecurityClient` 物件的 `getDocumentManager` 方法。
   * 透過叫用來擷取已撤銷檔案的授權識別碼值 `DocumentManager` 物件的 `getLicenseId` 方法和傳遞 `com.adobe.idp.Document` 代表已撤銷檔案的物件。 此方法會傳回代表授權識別碼的字串值。

1. 恢復對已撤銷PDF檔案的存取權。

   * 建立 `LicenseManager` 物件(透過叫用 `DocumentSecurityClient` 物件的 `getLicenseManager` 方法。
   * 透過叫用以恢復對已撤銷PDF檔案的存取 `LicenseManager` 物件的 `unrevokeLicense` 方法並傳遞已撤銷檔案的授權識別碼值。

**程式碼範例**

如需使用Document Security服務的程式碼範例，請參閱下列快速入門：

* 「快速入門（SOAP模式）：使用網站服務API恢復對已撤銷檔案的存取權」

### 使用Web服務API恢復對已撤銷檔案的存取 {#reinstate-access-to-revoked-documents-using-the-web-service-api}

使用Document Security API （Web服務）恢復對已撤銷檔案的存取：

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET專案。 請確定您使用下列WSDL定義： `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Replace `localhost` 搭配裝載AEM Forms之伺服器的IP位址。

1. 建立Document Security使用者端API物件。

   * 建立 `DocumentSecurityServiceClient` 物件（使用其預設建構函式）。
   * 建立 `DocumentSecurityServiceClient.Endpoint.Address` 物件，使用 `System.ServiceModel.EndpointAddress` 建構函式。 將指定WSDL的字串值傳遞至AEM Forms服務(例如， `http://localhost:8080/soap/services/RightsManagementService?WSDL`.) 您不需要使用 `lc_version` 屬性。 當您建立服務參考時，會使用此屬性。)
   * 建立 `System.ServiceModel.BasicHttpBinding` 物件，方法是取得 `DocumentSecurityServiceClient.Endpoint.Binding` 欄位。 將傳回值轉換為 `BasicHttpBinding`.
   * 設定 `System.ServiceModel.BasicHttpBinding` 物件的 `MessageEncoding` 欄位至 `WSMessageEncoding.Mtom`. 此值可確保使用MTOM。
   * 執行下列工作來啟用基本HTTP驗證：

      * 將AEM表單使用者名稱指派給欄位 `DocumentSecurityServiceClient.ClientCredentials.UserName.UserName`.
      * 將對應的密碼值指派給欄位 `DocumentSecurityServiceClient.ClientCredentials.UserName.Password`.
      * 指派常數值 `HttpClientCredentialType.Basic` 至欄位 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * 指派常數值 `BasicHttpSecurityMode.TransportCredentialOnly` 至欄位 `BasicHttpBindingSecurity.Security.Mode`.


1. 擷取已撤銷PDF檔案的授權識別碼。

   * 建立 `BLOB` 物件（使用其建構函式）。 此 `BLOB` 物件可用來儲存已撤銷的PDF檔案，存取權將恢復到該檔案。
   * 建立 `System.IO.FileStream` 物件，方法是叫用其建構函式，並傳遞代表已撤銷PDF檔案的檔案位置和開啟檔案的模式的字串值。
   * 建立位元組陣列，儲存 `System.IO.FileStream` 物件。 您可以取得 `System.IO.FileStream` 物件的 `Length` 屬性。
   * 叫用 `System.IO.FileStream` 物件的 `Read` 方法，並傳遞位元組陣列、起始位置以及要讀取的資料流長度。
   * 填入 `BLOB` 物件，透過指派其 `MTOM` 包含位元組陣列內容的欄位。

1. 恢復對已撤銷PDF檔案的存取權。

   * 透過叫用來擷取已撤銷檔案的授權識別碼值 `DocumentSecurityServiceClient` 物件的 `getLicenseID` 方法和傳遞 `BLOB` 代表已撤銷檔案的物件。 此方法會傳回代表授權識別碼的字串值。
   * 透過叫用以恢復對已撤銷PDF檔案的存取 `DocumentSecurityServiceClient` 物件的 `unrevokeLicense` 方法並傳遞字串值，該值指定已撤銷PDF檔案的授權識別碼值(傳遞的傳回值 `DocumentSecurityServiceClient` 物件的 `getLicenseId` 方法)。

**程式碼範例**

如需使用Document Security服務的程式碼範例，請參閱下列快速入門：

* 「快速入門(MTOM)：使用網站服務API恢復對已撤銷檔案的存取」
* 「快速入門(SwaRef)：使用網站服務API恢復對已撤銷檔案的存取」

**另请参阅**

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 檢查受原則保護的PDF檔案 {#inspecting-policy-protected-pdf-documents}

您可以使用Document Security Service API （Java和Web服務）來檢查受原則保護的PDF檔案。 檢查受原則保護的PDF檔案會傳回受原則保護的PDF檔案的相關資訊。 例如，您可以決定用來保護檔案的原則以及保護檔案的日期。

如果您的LiveCycle版本是8.x或較舊的版本，則無法執行此工作。 AEM Forms已新增檢查受原則保護檔案的支援。 如果您嘗試使用LiveCycle8.x （或更早版本）來檢查受原則保護的檔案，則會擲回例外狀況。

>[!NOTE]
>
>如需Document Security服務的詳細資訊，請參閱 [AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63).

### 步驟摘要 {#summary_of_steps-7}

若要檢查受原則保護的PDF檔案，請執行下列步驟：

1. 包含專案檔案。
1. 建立Document Security使用者端API物件。
1. 擷取受原則保護的檔案以進行檢查。
1. 取得受原則保護檔案的相關資訊。

**包含專案檔案**

將必要的檔案納入您的開發專案中。 如果您使用Java建立使用者端應用程式，請包含必要的JAR檔案。 如果您使用Web服務，請務必包含Proxy檔案。

**建立Document Security使用者端API物件**

以程式設計方式執行Document Security服務操作之前，請先建立Document Security服務使用者端物件。 如果您使用Java API，請建立 `RightsManagementClient` 物件。 如果您使用Document Security Web服務API，請建立 `RightsManagementServiceService` 物件。

**擷取受原則保護的檔案以檢查**

若要檢查受原則保護的檔案，請擷取該檔案。 如果您嘗試檢查未受原則保護或已撤銷的檔案，則會擲回例外狀況。

**Inspect檔案**

擷取受原則保護的檔案後，您可以檢查該檔案。

**取得受原則保護檔案的相關資訊**

檢查受原則保護的PDF檔案後，您可以取得相關資訊。 例如，您可以決定用來保護檔案的原則。

如果您使用屬於「我的原則」的原則來保護檔案，然後呼叫 `RMInspectResult.getPolicysetName` 或 `RMInspectResult.getPolicysetId`，會傳回null。

如果檔案是使用包含在原則集（除了「我的原則」）中的原則進行保護，則 `RMInspectResult.getPolicysetName` 和 `RMInspectResult.getPolicysetId` 傳回有效字串。

**另请参阅**

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Java API的Inspect受原則保護的PDF檔案 {#inspect-policy-protected-pdf-documents-using-the-java-api}

使用Document Security Service API (Java)，Inspect受原則保護的PDF檔案：

1. 包含專案檔案。

   在您的Java專案的類別路徑中包含使用者端JAR檔案，例如adobe-rightsmanagement-client.jar。 如需有關這些檔案位置的資訊，請參閱 [包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

1. 建立Document Security使用者端API物件。

   * 建立 `ServiceClientFactory` 包含連線屬性的物件。 (請參閱 [設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).)
   * 建立 `RightsManagementClient` 物件，使用它的建構函式並傳遞 `ServiceClientFactory` 物件。

1. 擷取受原則保護的檔案以進行檢查。

   * 建立 `java.io.FileInputStream` 物件，使用它的建構函式代表受原則保護的PDF檔案。 傳遞字串值，指定PDF檔案的位置。
   * 建立 `com.adobe.idp.Document` 物件，使用它的建構函式並傳遞 `java.io.FileInputStream` 物件。

1. Inspect檔案。

   * 建立 `DocumentManager` 物件(透過叫用 `RightsManagementClient` 物件的 `getDocumentManager` 方法。
   * 叫用Inspect受原則保護的檔案 `LicenseManager` 物件的 `inspectDocument` 方法。 傳遞 `com.adobe.idp.Document` 包含受原則保護的PDF檔案的物件。 此方法會傳回 `RMInspectResult` 包含受原則保護檔案相關資訊的物件。

1. 取得受原則保護檔案的相關資訊。

   若要取得受原則保護檔案的相關資訊，請叫用屬於的適當方法 `RMInspectResult` 物件。 例如，若要擷取原則名稱，請叫用 `RMInspectResult` 物件的 `getPolicyName` 方法。

**程式碼範例**

如需使用Document Security服務的程式碼範例，請參閱下列快速入門：

* 「快速入門（SOAP模式）：使用Java API檢查受原則保護的PDF檔案」

### 使用Web服務API的Inspect受原則保護的PDF檔案 {#inspect-policy-protected-pdf-documents-using-the-web-service-api}

使用Document Security Service API （Web服務），Inspect受原則保護的PDF檔案：

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET專案。 請確定您使用下列WSDL定義： `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Replace `localhost` 搭配裝載AEM Forms之伺服器的IP位址。

1. 建立Document Security使用者端API物件。

   * 建立 `RightsManagementServiceClient` 物件（使用其預設建構函式）。
   * 建立 `RightsManagementServiceClient.Endpoint.Address` 物件，使用 `System.ServiceModel.EndpointAddress` 建構函式。 將指定WSDL的字串值傳遞至AEM Forms服務(例如， `http://localhost:8080/soap/services/RightsManagementService?WSDL`.) 您不需要使用 `lc_version` 屬性。 當您建立服務參考時，會使用此屬性。)
   * 建立 `System.ServiceModel.BasicHttpBinding` 物件，方法是取得 `RightsManagementServiceClient.Endpoint.Binding` 欄位。 將傳回值轉換為 `BasicHttpBinding`.
   * 設定 `System.ServiceModel.BasicHttpBinding` 物件的 `MessageEncoding` 欄位至 `WSMessageEncoding.Mtom`. 此值可確保使用MTOM。
   * 執行下列工作來啟用基本HTTP驗證：

      * 將AEM表單使用者名稱指派給欄位 `RightsManagementServiceClient.ClientCredentials.UserName.UserName`.
      * 將對應的密碼值指派給欄位 `RightsManagementServiceClient.ClientCredentials.UserName.Password`.
      * 指派常數值 `HttpClientCredentialType.Basic` 至欄位 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * 指派常數值 `BasicHttpSecurityMode.TransportCredentialOnly` 至欄位 `BasicHttpBindingSecurity.Security.Mode`.


1. 擷取受原則保護的檔案以進行檢查。

   * 建立 `BLOB` 物件（使用其建構函式）。 此 `BLOB` 物件可用來儲存要檢查的PDF檔案。
   * 建立 `System.IO.FileStream` 物件（透過叫用其建構函式）。 傳遞代表PDF檔案檔案位置的字串值，以及用來開啟檔案的模式。
   * 建立位元組陣列，儲存 `System.IO.FileStream` 物件。 您可以取得 `System.IO.FileStream` 物件的 `Length` 屬性。
   * 叫用 `System.IO.FileStream` 物件的 `Read` 方法。 傳遞位元組陣列、起始位置和串流長度以讀取。
   * 填入 `BLOB` 物件，透過指派其 `MTOM` 包含位元組陣列內容的欄位。

1. Inspect檔案。

   叫用Inspect受原則保護的檔案 `RightsManagementServiceClient` 物件的 `inspectDocument` 方法。 傳遞 `BLOB` 包含受原則保護的PDF檔案的物件。 此方法會傳回 `RMInspectResult` 包含受原則保護檔案相關資訊的物件。

1. 取得受原則保護檔案的相關資訊。

   若要取得受原則保護檔案的相關資訊，請取得屬於的適當欄位的值 `RMInspectResult` 物件。 例如，若要擷取原則名稱，請取得 `RMInspectResult` 物件的 `policyName` 欄位。

**程式碼範例**

如需使用Document Security服務的程式碼範例，請參閱下列快速入門：

* 「快速入門(MTOM)：使用網站服務API檢查受原則保護的PDF檔案」
* 「快速入門(SwaRef)：使用網站服務API檢查受原則保護的PDF檔案」

**另请参阅**

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 建立浮水印 {#creating-watermarks}

浮水印可唯一識別檔案並控制侵犯版權，以協助確保檔案的安全性。 例如，您可以建立並放置浮水印，在檔案的所有頁面上顯示「機密」。 建立浮水印後，您可以將其納入原則中。 也就是說，您可以使用新建立的浮水印來設定原則的浮水印屬性。 將包含浮水印的原則套用至檔案後，浮水印會出現在受原則保護的檔案中。

>[!NOTE]
>
>只有具有Document Security管理許可權的使用者才能建立浮水印。 也就是說，在定義建立Document Security服務使用者端物件所需的連線設定時，您必須指定這類使用者。

>[!NOTE]
>
>如需Document Security服務的詳細資訊，請參閱 [AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63).

### 步驟摘要 {#summary_of_steps-8}

若要建立浮水印，請執行下列步驟：

1. 包含專案檔案。
1. 建立Document Security使用者端API物件。
1. 設定浮水印屬性。
1. 向Document Security服務註冊浮水印。

**包含專案檔案**

將必要的檔案納入您的開發專案中。 如果您使用Java建立使用者端應用程式，請包含必要的JAR檔案。 如果您使用Web服務，請務必包含Proxy檔案。

**建立Document Security使用者端API物件**

您必須先建立Document Security服務使用者端物件，才能以程式設計方式執行Document Security服務操作。 如果您使用Java API，請建立 `RightsManagementClient` 物件。 如果您使用Document Security Web服務API，請建立 `RightsManagementServiceService` 物件。

**設定浮水印屬性**

若要建立新的浮水印，您必須設定浮水印屬性。 必須一律定義名稱屬性。 除了name屬性之外，您至少必須設定下列其中一個屬性：

* 自定义文本
* DateInclude
* UserIdInclude
* UserNameInclude

下表列出使用Web服務建立浮水印時所需的索引鍵和值組。

<table>
 <thead>
  <tr>
   <th><p>键名</p></th>
   <th><p>描述</p></th>
   <th><p>价值</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p><code>WaterBackCmd:IS_USERNAME_ENABLED</code></p></td>
   <td><p>指定開啟檔案之使用者的使用者名稱是否為浮水印的一部分。</p></td>
   <td><p>True或False</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:IS_USERID_ENABLED</code></p></td>
   <td><p>指定開啟檔案的使用者識別碼是否為浮水印的一部分。</p></td>
   <td><p>True或False</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:IS_CURRENTDATE_ENABLED</code></p></td>
   <td><p>指定目前日期是否為浮水印的一部分。</p></td>
   <td><p>True或False</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:IS_CUSTOMTEXT_ENABLED</code></p></td>
   <td><p>如果此值為true，則必須使用指定自訂文字的值 <code>WaterBackCmd:SRCTEXT</code>.</p></td>
   <td><p>True或False</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:OPACITY</code></p></td>
   <td><p>指定浮水印的不透明度。 若未指定，則預設值為0.5。</p></td>
   <td><p>介於0.0和1.0之間的值。</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:ROTATION</code></p></td>
   <td><p>指定浮水印的旋轉。 預設值為0度。</p></td>
   <td><p>介於0到359之間的值。</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:SCALE</code></p></td>
   <td><p>若指定此值，則 <code>WaterBackCmd:IS_SIZE_ENABLED</code> 必須存在且值必須為true。 如果未指定此屬性，預設行為會符合頁面。</p></td>
   <td><p>大於0.0且小於或等於1.0的值。</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:HORIZ_ALIGN</code></p></td>
   <td><p>指定浮水印的水準對齊方式。 預設值為center。</p></td>
   <td><p>左、中或右</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:VERT_ALIGN</code></p></td>
   <td><p>指定浮水印的垂直對齊方式。 預設值為center。</p></td>
   <td><p>上、中或下</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:IS_USE_BACKGROUND</code></p></td>
   <td><p>指定浮水印是否為背景。 預設值為false。</p></td>
   <td><p>True或False</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:IS_SIZE_ENABLED</code></p></td>
   <td><p>如果指定了自訂比例，則為True。 如果此值為true，則必須指定SCALE。 如果此值為false，則預設為適合頁面。</p></td>
   <td><p>True或False</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:SRCTEXT</code></p></td>
   <td><p>指定浮水印的自訂文字。 如果此值存在，則 <code>WaterBackCmd:IS_CUSTOMTEXT_ENABLED</code> 也必須存在並設定為true。</p></td>
   <td><p>True或False</p></td>
  </tr>
 </tbody>
</table>

所有浮水印都必須已定義下列其中一個屬性：

* `WaterBackCmd:IS_USERNAME_ENABLED`
* `WaterBackCmd:IS_USERID_ENABLED`
* `WaterBackCmd:IS_CURRENTDATE_ENABLED`
* `WaterBackCmd:IS_CUSTOMTEXT_ENABLED`

所有其他屬性都是選擇性的。

**註冊浮水印**

新浮水印必須先向Document Security服務註冊，然後才能使用。 註冊浮水印後，您可以在原則內使用它。

**另请参阅**

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[套用原則至PDF檔案](protecting-documents-policies.md#applying-policies-to-pdf-documents)

### 使用Java API建立浮水印 {#create-watermarks-using-the-java-api}

使用Document Security API (Java)建立浮水印：

1. 包含專案檔案。

   包含使用者端JAR檔案，例如 `adobe-rightsmanagement-client.jar`，位於Java專案的類別路徑中。

1. 建立Document Security使用者端API物件。

   * 建立 `ServiceClientFactory` 包含連線屬性的物件。
   * 建立 `RightsManagementClient` 物件，使用它的建構函式並傳遞 `ServiceClientFactory` 物件。

1. 設定浮水印屬性

   * 建立 `Watermark` 物件(透過叫用 `InfomodelObjectFactory` 物件的靜態 `createWatermark` 方法。 此方法會傳回 `Watermark` 物件。
   * 透過叫用設定浮水印的名稱屬性 `Watermark` 物件的 `setName` 並傳遞指定原則名稱的字串值。
   * 透過叫用設定浮水印的背景屬性 `Watermark` 物件的 `setBackground` 方法與傳遞 `true`. 透過設定此屬性，浮水印會出現在檔案的背景中。
   * 透過叫用「 」，設定浮水印的自訂文字屬性 `Watermark` 物件的 `setCustomText` 並傳遞代表浮水印文字的字串值。
   * 透過叫用 `Watermark` 物件的 `setOpacity` 方法，並傳遞指定不透明度等級的整數值。 值100表示浮水印完全不透明，值0表示浮水印完全透明。

1. 註冊浮水印。

   * 建立 `WatermarkManager` 物件(透過叫用 `RightsManagementClient` 物件的 `getWatermarkManager` 方法。 此方法會傳回 `WatermarkManager` 物件。
   * 透過叫用浮水印 `WatermarkManager` 物件的 `registerWatermark` 方法和傳遞 `Watermark` 代表要註冊之浮水印的物件。 此方法會傳回代表浮水印識別值的字串值。

**程式碼範例**

如需使用Document Security服務的程式碼範例，請參閱下列快速入門：

* 「快速入門（SOAP模式）：使用Java API建立浮水印」

### 使用網站服務API建立浮水印 {#create-watermarks-using-the-web-service-api}

使用Document Security API （Web服務）建立浮水印：

1. 建立Document Security使用者端API物件。

   建立使用MTOM的Microsoft .NET專案。 請確定您使用下列WSDL定義： `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Replace `localhost` 搭配裝載AEM Forms之伺服器的IP位址。

1. 建立Document Security使用者端API物件。

   * 建立 `RightsManagementServiceClient` 物件（使用其預設建構函式）。
   * 建立 `RightsManagementServiceClient.Endpoint.Address` 物件，使用 `System.ServiceModel.EndpointAddress` 建構函式。 將指定WSDL的字串值傳遞至AEM Forms服務(例如， `http://localhost:8080/soap/services/RightsManagementService?WSDL`.) 您不需要使用 `lc_version` 屬性。 當您建立服務參考時，會使用此屬性。)
   * 建立 `System.ServiceModel.BasicHttpBinding` 物件，方法是取得 `RightsManagementServiceClient.Endpoint.Binding` 欄位。 將傳回值轉換為 `BasicHttpBinding`.
   * 設定 `System.ServiceModel.BasicHttpBinding` 物件的 `MessageEncoding` 欄位至 `WSMessageEncoding.Mtom`. 此值可確保使用MTOM。
   * 執行下列工作來啟用基本HTTP驗證：

      * 將AEM表單使用者名稱指派給欄位 `RightsManagementServiceClient.ClientCredentials.UserName.UserName`.
      * 將對應的密碼值指派給欄位 `RightsManagementServiceClient.ClientCredentials.UserName.Password`.
      * 指派常數值 `HttpClientCredentialType.Basic` 至欄位 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * 指派常數值 `BasicHttpSecurityMode.TransportCredentialOnly` 至欄位 `BasicHttpBindingSecurity.Security.Mode`.


1. 設定浮水印屬性。

   * 建立 `WatermarkSpec` 物件(透過叫用 `WatermarkSpec` 建構函式。
   * 將字串值指派給，以設定浮水印的名稱 `WatermarkSpec` 物件的 `name` 資料成員。
   * 設定浮水印 `id` 屬性，方法是將字串值指派給 `WatermarkSpec` 物件的 `id` 資料成員。
   * 對於要設定的每個浮水印屬性，建立一個單獨的 `MyMapOf_xsd_string_To_xsd_anyType_Item` 物件。
   * 將值指派給以設定索引鍵值 `MyMapOf_xsd_string_To_xsd_anyType_Item` 物件的 `key` 資料成員(例如， `WaterBackCmd:OPACITY)`.
   * 將值指派給 `MyMapOf_xsd_string_To_xsd_anyType_Item` 物件的 `value` 資料成員(例如， `.25`)。
   * 建立 `MyArrayOf_xsd_anyType` 物件。 針對每個 `MyMapOf_xsd_string_To_xsd_anyType_Item` 物件，叫用 `MyArrayOf_xsd_anyType` 物件的 `Add` 方法。 傳遞 `MyMapOf_xsd_string_To_xsd_anyType_Item` 物件。
   * 指派 `MyArrayOf_xsd_anyType` 物件至 `WatermarkSpec` 物件的 `values` 資料成員。

1. 註冊浮水印。

   透過叫用浮水印 `RightsManagementServiceClient` 物件的 `registerWatermark` 方法和傳遞 `WatermarkSpec` 代表要註冊之浮水印的物件。

**程式碼範例**

如需使用Document Security服務的程式碼範例，請參閱下列快速入門：

* 「快速入門(MTOM)：使用網站服務API建立浮水印」
* 「快速入門(SwaRef)：使用網站服務API建立浮水印」

**另请参阅**

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 修改浮水印 {#modifying-watermarks}

您可以使用Document Security Java API或Web服務API修改現有的浮水印。 若要變更現有的浮水印，您可以擷取它、修改它的屬性，然後在伺服器上更新它。 例如，假設您擷取浮水印並修改其不透明度屬性。 在變更生效之前，您必須更新浮水印。

當您修改浮水印時，此變更會影響已套用浮水印的未來檔案。 也就是說，包含浮水印的現有PDF檔案不受影響。

>[!NOTE]
>
>只有具有Document Security管理許可權的使用者才能修改浮水印。 也就是說，在定義建立Document Security服務使用者端物件所需的連線設定時，您必須指定這類使用者。

>[!NOTE]
>
>如需Document Security服務的詳細資訊，請參閱 [AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63).

### 步驟摘要 {#summary_of_steps-9}

若要修改浮水印，請執行下列步驟：

1. 包含專案檔案。
1. 建立Document Security使用者端API物件。
1. 擷取要修改的浮水印。
1. 設定浮水印屬性。
1. 更新浮水印。

**包含專案檔案**

將必要的檔案納入您的開發專案中。 如果您使用Java建立使用者端應用程式，請包含必要的JAR檔案。 如果您使用Web服務，請務必包含Proxy檔案。

**建立Document Security使用者端API物件**

您必須先建立Document Security服務使用者端物件，才能以程式設計方式執行Document Security服務操作。 如果您使用Java API，請建立 `DocumentSecurityClient` 物件。 如果您使用Document Security Web服務API，請建立 `DocumentSecurityServiceService` 物件。

**擷取要修改的浮水印**

若要修改浮水印，您必須擷取現有的浮水印。 您可以指定浮水印名稱或指定其識別碼值來擷取浮水印。

**設定浮水印屬性**

若要修改現有的浮水印，請變更一或多個浮水印屬性的值。 使用Web服務以程式設計方式更新浮水印時，您必須設定最初設定的所有屬性，即使值未變更亦然。 例如，假設已設定下列浮水印屬性： `WaterBackCmd:IS_USERID_ENABLED`， `WaterBackCmd:IS_CUSTOMTEXT_ENABLED`， `WaterBackCmd:OPACITY`、和 `WaterBackCmd:SRCTEXT`. 雖然您唯一想要修改的屬性是 `WaterBackCmd:OPACITY`，您必須將其他值設定為well。

>[!NOTE]
>
>使用Java API修改浮水印時，您不需要指定所有屬性。 設定您要修改的浮水印屬性。

>[!NOTE]
>
>如需有關浮水印屬性名稱的資訊，請參閱 [建立浮水印](protecting-documents-policies.md#creating-watermarks).

**更新浮水印**

修改浮水印的屬性後，您必須更新浮水印。

**另请参阅**

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[建立浮水印](protecting-documents-policies.md#creating-watermarks)

### 使用Java API修改浮水印 {#modify-watermarks-using-the-java-api}

使用Document Security API (Java)修改浮水印：

1. 包含專案檔案。

   在您的Java專案的類別路徑中包含使用者端JAR檔案，例如adobe-rightsmanagement-client.jar。

1. 建立Document Security使用者端API物件。

   * 建立 `ServiceClientFactory` 包含連線屬性的物件。
   * 建立 `DocumentSecurityClient` 物件，使用它的建構函式並傳遞 `ServiceClientFactory` 物件。

1. 擷取要修改的浮水印。

   建立 `WatermarkManager` 物件(透過叫用 `DocumentSecurityClient` 物件的 `getWatermarkManager` 方法，並傳遞指定浮水印名稱的字串值。 此方法會傳回 `Watermark` 代表要修改之浮水印的物件。

1. 設定浮水印屬性。

   透過叫用 `Watermark` 物件的 `setOpacity` 方法，並傳遞指定不透明度等級的整數值。 值100表示浮水印完全不透明，值0表示浮水印完全透明。

   >[!NOTE]
   >
   >此範例只會修改不透明度屬性。

1. 更新浮水印。

   * 透過叫用來更新浮水印 `WatermarkManager` 物件的 `updateWatermark` 方法並傳遞 `Watermark` 修改其屬性的物件。

**程式碼範例**

如需使用Document Security服務的程式碼範例，請參閱快速入門（SOAP模式）：使用Java API修改浮水印一節。

### 使用網站服務API修改浮水印 {#modify-watermarks-using-the-web-service-api}

使用Document Security API （Web服務）修改浮水印：

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET專案。 請確定您使用下列WSDL定義： `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Replace `localhost` 搭配裝載AEM Forms之伺服器的IP位址。

1. 建立Document Security使用者端API物件。

   * 建立 `DocumentSecurityServiceClient` 物件（使用其預設建構函式）。
   * 建立 `RightsManagementServiceClient.Endpoint.Address` 物件，使用 `System.ServiceModel.EndpointAddress` 建構函式。 將指定WSDL的字串值傳遞至AEM Forms服務(例如， `http://localhost:8080/soap/services/DocumentSecurityService?WSDL`.) 您不需要使用 `lc_version` 屬性。 當您建立服務參考時，會使用此屬性。)
   * 建立 `System.ServiceModel.BasicHttpBinding` 物件，方法是取得 `DocumentSecurityServiceClient.Endpoint.Binding` 欄位。 將傳回值轉換為 `BasicHttpBinding`.
   * 設定 `System.ServiceModel.BasicHttpBinding` 物件的 `MessageEncoding` 欄位至 `WSMessageEncoding.Mtom`. 此值可確保使用MTOM。
   * 執行下列工作來啟用基本HTTP驗證：

      * 將AEM表單使用者名稱指派給欄位 `DocumentSecurityServiceClient.ClientCredentials.UserName.UserName`.
      * 將對應的密碼值指派給欄位 `DocumentSecurityServiceClient.ClientCredentials.UserName.Password`.
      * 指派常數值 `HttpClientCredentialType.Basic` 至欄位 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * 指派常數值 `BasicHttpSecurityMode.TransportCredentialOnly` 至欄位 `BasicHttpBindingSecurity.Security.Mode`.


1. 擷取要修改的浮水印。

   擷取浮水印，以透過叫用 `DocumentSecurityServiceClient` 物件的 `getWatermarkByName` 方法。 傳遞指定浮水印名稱的字串值。 此方法會傳回 `WatermarkSpec` 代表要修改之浮水印的物件。

1. 設定浮水印屬性。

   * 若要更新每個浮水印屬性，請建立個別的 `MyMapOf_xsd_string_To_xsd_anyType_Item` 物件。
   * 將值指派給以設定索引鍵值 `MyMapOf_xsd_string_To_xsd_anyType_Item` 物件的 `key` 資料成員(例如， `WaterBackCmd:OPACITY)`.
   * 將值指派給 `MyMapOf_xsd_string_To_xsd_anyType_Item` 物件的 `value` 資料成員(例如， `.50`)。
   * 建立 `MyArrayOf_xsd_anyType` 物件。 針對每個 `MyMapOf_xsd_string_To_xsd_anyType_Item` 物件，叫用 `MyArrayOf_xsd_anyType` 物件的 `Add` 方法。 傳遞 `MyMapOf_xsd_string_To_xsd_anyType_Item` 物件。
   * 指派 `MyArrayOf_xsd_anyType` 物件至 `WatermarkSpec` 物件的 `values` 資料成員。

1. 更新浮水印。

   透過叫用來更新浮水印 `DocumentSecurityServiceClient` 物件的 `updateWatermark` 方法和傳遞 `WatermarkSpec` 代表要修改之浮水印的物件。

**程式碼範例**

如需使用Document Security服務的程式碼範例，請參閱以下快速入門：

* 「快速入門(MTOM)：使用網站服務API修改浮水印」

## 搜尋事件 {#searching-for-events}

Rights Management服務會在特定動作發生時加以追蹤，例如將原則套用至檔案、開啟受原則保護的檔案，以及撤銷對檔案的存取權。 必須為Rights Management服務啟用事件稽核，否則不會追蹤事件。

事件會分為下列其中一個類別：

* 管理員事件是與管理員相關的動作，例如建立新的管理員帳戶。
* 檔案事件是與檔案相關的動作，例如關閉受原則保護的檔案。
* 原則事件是與原則相關的動作，例如建立新原則。
* 服務事件是與Rights Management服務相關的動作，例如與使用者目錄同步。

您可以使用Rights ManagementJava API或Web服務API來搜尋指定事件。 透過搜尋事件，您可以執行工作，例如建立特定事件的記錄檔。

>[!NOTE]
>
>如需Rights Management服務的詳細資訊，請參閱 [AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63).

### 步驟摘要 {#summary_of_steps-10}

若要搜尋Rights Management事件，請執行下列步驟：

1. 包含專案檔案。
1. 建立Rights Management使用者端API物件。
1. 指定要搜尋的事件。
1. 搜尋事件。

**包含專案檔案**

將必要的檔案納入您的開發專案中。 如果您使用Java建立使用者端應用程式，請包含必要的JAR檔案。 如果您使用Web服務，請務必包含Proxy檔案。

**建立Rights Management使用者端API物件**

您必須先建立Rights Management服務使用者端物件，才能以程式設計方式執行Rights Management服務作業。 如果您使用Java API，請建立 `DocumentSecurityClient` 物件。 如果您使用Rights ManagementWeb服務API，請建立 `DocumentSecurityServiceService` 物件。

**指定要搜尋的事件**

您必須指定要搜尋的事件。 例如，您可以搜尋原則建立事件，在建立新原則時會發生此事件。

**搜尋事件**

指定要搜尋的事件後，您可以使用Rights ManagementJava API或Rights ManagementWeb服務API來搜尋事件。

**另请参阅**

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Java API搜尋事件 {#search-for-events-using-the-java-api}

使用Rights ManagementAPI (Java)搜尋事件：

1. 包含專案檔案

   在您的Java專案的類別路徑中包含使用者端JAR檔案，例如adobe-rightsmanagement-client.jar。

1. 建立Rights Management使用者端API物件

   建立 `DocumentSecurityClient` 物件，使用它的建構函式並傳遞 `ServiceClientFactory` 包含連線屬性的物件。

1. 指定要搜尋的事件

   * 建立 `EventManager` 物件(透過叫用 `DocumentSecurityClient` 物件的 `getEventManager` 方法。 此方法會傳回 `EventManager` 物件。
   * 建立 `EventSearchFilter` 物件（透過叫用其建構函式）。
   * 透過叫用「 」指定要搜尋的事件 `EventSearchFilter` 物件的 `setEventCode` 方法並傳遞屬於的靜態資料成員 `EventManager` 代表要搜尋之事件的類別。 例如，若要搜尋原則建立事件，請傳遞 `EventManager.POLICY_CREATE_EVENT`.

   >[!NOTE]
   >
   >您可以透過叫用來定義其他搜尋條件 `EventSearchFilter` 物件方法。 例如，叫用 `setUserName` 指定與事件相關聯之使用者的方法。

1. 搜尋事件

   透過叫用搜尋事件 `EventManager` 物件的 `searchForEvents` 方法和傳遞 `EventSearchFilter` 定義事件搜尋條件的物件。 此方法傳回陣列 `Event` 物件。

**程式碼範例**

如需使用Rights Management服務的程式碼範例，請參閱下列快速入門：

* 「快速入門(SOAP)：使用Java API搜尋事件」

### 使用Web服務API搜尋事件 {#search-for-events-using-the-web-service-api}

使用Rights ManagementAPI （網站服務）搜尋事件：

1. 包含專案檔案

   建立使用MTOM的Microsoft .NET專案。 請確定您使用下列WSDL定義： `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Replace `localhost` 搭配裝載AEM Forms之伺服器的IP位址。

1. 建立Rights Management使用者端API物件

   * 建立 `DocumentSecurityServiceClient` 物件（使用其預設建構函式）。
   * 建立 `DocumentSecurityServiceClient.Endpoint.Address` 物件，使用 `System.ServiceModel.EndpointAddress` 建構函式。 將指定WSDL的字串值傳遞至AEM Forms服務(例如， `http://localhost:8080/soap/services/RightsManagementService?WSDL`.) 您不需要使用 `lc_version` 屬性。 當您建立服務參考時，會使用此屬性。)
   * 建立 `System.ServiceModel.BasicHttpBinding` 物件，方法是取得 `DocumentSecurityServiceClient.Endpoint.Binding` 欄位。 將傳回值轉換為 `BasicHttpBinding`.
   * 設定 `System.ServiceModel.BasicHttpBinding` 物件的 `MessageEncoding` 欄位至 `WSMessageEncoding.Mtom`. 此值可確保使用MTOM。
   * 執行下列工作來啟用基本HTTP驗證：

      * 將AEM表單使用者名稱指派給欄位 `DocumentSecurityServiceClient.ClientCredentials.UserName.UserName`.
      * 將對應的密碼值指派給欄位 `DocumentSecurityServiceClient.ClientCredentials.UserName.Password`.
      * 指派常數值 `HttpClientCredentialType.Basic` 至欄位 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * 指派常數值 `BasicHttpSecurityMode.TransportCredentialOnly` 至欄位 `BasicHttpBindingSecurity.Security.Mode`.


1. 指定要搜尋的事件

   * 建立 `EventSpec` 物件（使用其建構函式）。
   * 透過設定「 」，指定事件發生的時段的開始 `EventSpec` 物件的 `firstTime.date` 資料成員具有 `DataTime` 代表事件發生時日期範圍開始的例項。
   * 指派值 `true` 至 `EventSpec` 物件的 `firstTime.dateSpecified` 資料成員。
   * 透過設定「 」，指定事件發生的時段的結束 `EventSpec` 物件的 `lastTime.date` 資料成員具有 `DataTime` 代表事件發生時日期範圍結束的例項。
   * 指派值 `true` 至 `EventSpec` 物件的 `lastTime.dateSpecified` 資料成員。
   * 將字串值指派給，以設定要搜尋的事件 `EventSpec` 物件的 `eventCode` 資料成員。 下表列出您可以指派給此屬性的數值：

   <table>
    <thead>
    <tr>
    <th><p>事件型別</p></th>
    <th><p>价值</p></th>
    </tr>
    </thead>
    <tbody>
    <tr>
    <td><p><code>ALL_EVENTS</code></p></td>
    <td><p>999</p></td>
    </tr>
    <tr>
    <td><p><code>USER_CHANGE_PASSWORD_EVENT</code></p></td>
    <td><p>1000</p></td>
    </tr>
    <tr>
    <td><p><code>USER_REGISTER_EVENT</code></p></td>
    <td><p>1001</p></td>
    </tr>
    <tr>
    <td><p><code>USER_PREREGISTER_EVENT</code></p></td>
    <td><p>1002</p></td>
    </tr>
    <tr>
    <td><p><code>USER_ACTIVATE_EVENT</code></p></td>
    <td><p>1003</p></td>
    </tr>
    <tr>
    <td><p><code>USER_DEACTIVATE_EVENT</code></p></td>
    <td><p>1004</p></td>
    </tr>
    <tr>
    <td><p><code>USER_AUTHENTICATE_EVENT</code></p></td>
    <td><p>1005</p></td>
    </tr>
    <tr>
    <td><p><code>USER_AUTHENTICATE_DENY_EVENT </code></p></td>
    <td><p>1006</p></td>
    </tr>
    <tr>
    <td><p><code>USER_ACCOUNT_LOCK_EVENT</code></p></td>
    <td><p>1007</p></td>
    </tr>
    <tr>
    <td><p><code>USER_DELETE_EVENT </code></p></td>
    <td><p>1008</p></td>
    </tr>
    <tr>
    <td><p><code>USER_UPDATE_PROFILE_EVENT </code></p></td>
    <td><p>1009</p></td>
    </tr>
    <tr>
    <td><p><code>DOCUMENT_VIEW_EVENT </code></p></td>
    <td><p>2000</p></td>
    </tr>
    <tr>
    <td><p><code>DOCUMENT_PRINT_LOW_EVENT </code></p></td>
    <td><p>2001</p></td>
    </tr>
    <tr>
    <td><p><code>DOCUMENT_PRINT_HIGH_EVENT </code></p></td>
    <td><p>2002</p></td>
    </tr>
    <tr>
    <td><p><code>DOCUMENT_SIGN_EVENT </code></p></td>
    <td><p>2003</p></td>
    </tr>
    <tr>
    <td><p><code>DOCUMENT_ADD_ANNOTATION_EVENT </code></p></td>
    <td><p>2004</p></td>
    </tr>
    <tr>
    <td><p><code>DOCUMENT_FORM_FILL_EVENT </code></p></td>
    <td><p>2005</p></td>
    </tr>
    <tr>
    <td><p><code>DOCUMENT_CLOSE_EVENT </code></p></td>
    <td><p>2006</p></td>
    </tr>
    <tr>
    <td><p><code>DOCUMENT_MODIFY_EVENT </code></p></td>
    <td><p>2007</p></td>
    </tr>
    <tr>
    <td><p><code>DOCUMENT_CHANGE_SECURITY_HANDLER_EVENT </code></p></td>
    <td><p>2008</p></td>
    </tr>
    <tr>
    <td><p><code>DOCUMENT_SWITCH_POLICY_EVENT </code></p></td>
    <td><p>2009</p></td>
    </tr>
    <tr>
    <td><p><code>DOCUMENT_REVOKE_EVENT </code></p></td>
    <td><p>2010</p></td>
    </tr>
    <tr>
    <td><p><code>$1</code></p></td>
    <td><p>2011</p></td>
    </tr>
    <tr>
    <td><p><code>DOCUMENT_SECURE_EVENT </code></p></td>
    <td><p>2012</p></td>
    </tr>
    <tr>
    <td><p><code>DOCUMENT_UNKNOWN_CLIENT_EVENT </code></p></td>
    <td><p>2013</p></td>
    </tr>
    <tr>
    <td><p><code>DOCUMENT_CHANGE_REVOKE_URL_EVENT </code></p></td>
    <td><p>2014</p></td>
    </tr>
    <tr>
    <td><p><code>POLICY_CHANGE_EVENT </code></p></td>
    <td><p>3000</p></td>
    </tr>
    <tr>
    <td><p><code>POLICY_ENABLE_EVENT </code></p></td>
    <td><p>3001</p></td>
    </tr>
    <tr>
    <td><p><code>POLICY_DISABLE_EVENT </code></p></td>
    <td><p>3002</p></td>
    </tr>
    <tr>
    <td><p><code>POLICY_CREATE_EVENT </code></p></td>
    <td><p>3003</p></td>
    </tr>
    <tr>
    <td><p><code>POLICY_DELETE_EVENT </code></p></td>
    <td><p>3004</p></td>
    </tr>
    <tr>
    <td><p><code>POLICY_CHANGE_OWNER_EVENT </code></p></td>
    <td><p>3005</p></td>
    </tr>
    <tr>
    <td><p><code>SERVER_CLIENT_SYNC_EVENT </code></p></td>
    <td><p>4000</p></td>
    </tr>
    <tr>
    <td><p><code>SERVER_SYNC_DIR_INFO_EVENT </code></p></td>
    <td><p>4001</p></td>
    </tr>
    <tr>
    <td><p><code>SERVER_SYNC_DIR_COMPLETE_EVENT </code></p></td>
    <td><p>4002</p></td>
    </tr>
    <tr>
    <td><p><code>SERVER_VERSION_MISMATCH_EVENT </code></p></td>
    <td><p>4003</p></td>
    </tr>
    <tr>
    <td><p><code>SERVER_CONFIG_CHANGE_EVENT </code></p></td>
    <td><p>4004</p></td>
    </tr>
    <tr>
    <td><p><code>SERVER_ENABLE_OFFLINE_ACCESS_EVENT </code></p></td>
    <td><p>4005</p></td>
    </tr>
    <tr>
    <td><p><code>ADMIN_ADD_EVENT </code></p></td>
    <td><p>5000</p></td>
    </tr>
    <tr>
    <td><p><code>ADMIN_DELETE_EVENT </code></p></td>
    <td><p>5001</p></td>
    </tr>
    <tr>
    <td><p><code>ADMIN_EDIT_EVENT </code></p></td>
    <td><p>5002</p></td>
    </tr>
    <tr>
    <td><p><code>ADMIN_ACTIVATE_EVENT </code></p></td>
    <td><p>5003</p></td>
    </tr>
    <tr>
    <td><p><code>ADMIN_DEACTIVATE_EVENT </code></p></td>
    <td><p>5004</p></td>
    </tr>
    <tr>
    <td><p><code>ERROR_DIRECTORY_SERVICE_EVENT </code></p></td>
    <td><p>6000</p></td>
    </tr>
    <tr>
    <td><p><code>CREATED_POLICYSET_EVENT</code></p></td>
    <td><p>7000</p></td>
    </tr>
    <tr>
    <td><p><code>DELETED_POLICYSET_EVENT</code></p></td>
    <td><p>7001</p></td>
    </tr>
    <tr>
    <td><p><code>MODIFIED_POLICYSET_EVENT</code></p></td>
    <td><p>7002</p></td>
    </tr>
    </tbody>
    </table>

1. 搜尋事件

   透過叫用搜尋事件 `DocumentSecurityServiceClient` 物件的 `searchForEvents` 方法和傳遞 `EventSpec` 物件，代表要搜尋的事件和結果數目上限。 此方法會傳回 `MyArrayOf_xsd_anyType` 每個元素為的集合 `AuditSpec` 執行個體。 使用 `AuditSpec` 例如，您可以取得事件的相關資訊，例如發生時間。 此 `AuditSpec` 執行個體包含 `timestamp` 指定此資訊的資料成員。

**程式碼範例**

如需使用Rights Management服務的程式碼範例，請參閱下列快速入門：

* 「快速入門(MTOM)：使用網站服務API搜尋事件」
* 「快速入門(SwaRef)：使用網站服務API搜尋事件」

**另请参阅**

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 將原則套用至Word檔案 {#applying-policies-to-word-documents}

除了PDF檔案之外，Rights Management服務還支援其他檔案格式，例如Microsoft Word檔案（DOC檔案）和其他Microsoft Office檔案格式。 例如，您可以將原則套用至Word檔案，以便保護它。 將原則套用至Word檔案後，您就可以限制對檔案的存取。 如果檔案已受原則保護，則無法將原則套用至檔案。

您可以在分發受原則保護的Word檔案後，監視其使用。 也就是說，您可以看到檔案的使用方式以及誰在使用檔案。 例如，您可以找出何時有人開啟了檔案。

>[!NOTE]
>
>如需Document Security服務的詳細資訊，請參閱 [AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63).

### 步驟摘要 {#summary_of_steps-11}

若要將原則套用至Word檔案，請執行下列步驟：

1. 包含專案檔案。
1. 建立Document Security使用者端API物件。
1. 擷取套用原則的Word檔案。
1. 將現有原則套用至Word檔案。
1. 儲存受原則保護的Word檔案。

**包含專案檔案**

將必要的檔案納入您的開發專案中。 如果您使用Java建立使用者端應用程式，請包含必要的JAR檔案。 如果您使用Web服務，請務必包含Proxy檔案。

**建立Document Security使用者端API物件**

您必須先建立Document Security服務使用者端物件，才能以程式設計方式執行Document Security服務操作。

**擷取Word檔案**

您必須擷取Word檔案才能套用原則。 將原則套用至Word檔案後，使用者使用檔案時會受到限制。 例如，如果原則未允許在離線時開啟檔案，則使用者必須線上上才能開啟檔案。

**將現有原則套用至Word檔案**

若要將原則套用至Word檔案，您必須參考現有原則並指定該原則所屬的原則集。 設定連線屬性的使用者必須擁有指定原則的存取權。 如果沒有，會發生例外狀況。

**儲存文字檔案**

Document Security服務將原則套用至Word檔案後，您可以將受原則保護的Word檔案儲存為DOC檔案。

**另请参阅**

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[撤銷對檔案的存取權](protecting-documents-policies.md#revoking-access-to-documents)

### 使用Java API將原則套用至Word檔案 {#apply-a-policy-to-a-word-document-using-the-java-api}

使用Document Security API (Java)將原則套用至Word檔案：

1. 包含專案檔案。

   在您的Java專案的類別路徑中包含使用者端JAR檔案，例如adobe-rightsmanagement-client.jar。

1. 建立Document Security使用者端API物件。

   * 建立 `ServiceClientFactory` 包含連線屬性的物件。
   * 建立 `DocumentSecurityClient` 物件，使用它的建構函式並傳遞 `ServiceClientFactory` 物件。

1. 擷取Word檔案。

   * 建立 `java.io.FileInputStream` 物件，使用它的建構函式並傳遞字串值來表示Word檔案，該字串值指定Word檔案的位置。
   * 建立 `com.adobe.idp.Document` 物件，使用它的建構函式並傳遞 `java.io.FileInputStream` 物件。

1. 將現有原則套用至Word檔案。

   * 建立 `DocumentManager` 物件(透過叫用 `DocumentSecurityClient` 物件的 `getDocumentManager` 方法。
   * 透過叫用「 」，將原則套用到Word檔案 `DocumentManager` 物件的 `protectDocument` 並傳遞下列值：

      * 此 `com.adobe.idp.Document` 包含套用原則之Word檔案的物件。
      * 字串值，指定檔案的名稱。
      * 字串值，指定原則所屬的原則集名稱。 您可以指定 `null` 導致下列專案的值： `MyPolicies` 正在使用的原則集。
      * 字串值，指定原則名稱。
      * 字串值，代表檔案發行者使用者的使用者管理員網域名稱。 此引數值為選用值，可為Null （若此引數為Null，則下一個引數值必須為Null）。
      * 字串值，代表作為檔案發行者的使用者管理員使用者的正式名稱。 此引數值為選用值，可以是 `null` (如果此引數為 `null`，則前一個引數值必須為 `null`)。
      * A `com.adobe.livecycle.rightsmanagement.Locale` 代表用於選取MS Office範本的地區設定。 此引數值為選用值，您可以指定 `null`.

      此 `protectDocument` 方法傳回 `RMSecureDocumentResult` 包含受原則保護的Word檔案的物件。


1. 儲存Word檔案。

   * 叫用 `RMSecureDocumentResult` 物件的 `getProtectedDoc` 取得受原則保護的Word檔案的方法。 此方法會傳回 `com.adobe.idp.Document` 物件。
   * 建立 `java.io.File` 物件並確保副檔名為DOC。
   * 叫用 `com.adobe.idp.Document` 物件的 `copyToFile` 複製目錄內容的方法 `Document` 物件放入檔案(請確定您使用 `Document` 物件，由 `getProtectedDoc` 方法)。

**程式碼範例**

如需使用Document Security服務的程式碼範例，請參閱以下快速入門：

* 「快速入門（SOAP模式）：使用Java API將原則套用至Word檔案」

### 使用Web服務API將原則套用至Word檔案 {#apply-a-policy-to-a-word-document-using-the-web-service-api}

使用Document Security API （Web服務）將原則套用至Word檔案：

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET專案。 請確定您使用下列WSDL定義： `http://localhost:8080/soap/services/DocumentSecurityService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Replace `localhost` 搭配裝載AEM Forms之伺服器的IP位址。

1. 建立Document Security使用者端API物件。

   * 建立 `DocumentSecurityServiceClient` 物件（使用其預設建構函式）。
   * 建立 `DocumentSecurityServiceClient.Endpoint.Address` 物件，使用 `System.ServiceModel.EndpointAddress` 建構函式。 將指定WSDL的字串值傳遞至AEM Forms服務(例如， `http://localhost:8080/soap/services/DocumentSecurityService?WSDL`.) 您不需要使用 `lc_version` 屬性。 當您建立服務參考時，會使用此屬性。)
   * 建立 `System.ServiceModel.BasicHttpBinding` 物件，方法是取得 `DocumentSecurityServiceClient.Endpoint.Binding` 欄位。 將傳回值轉換為 `BasicHttpBinding`.
   * 設定 `System.ServiceModel.BasicHttpBinding` 物件的 `MessageEncoding` 欄位至 `WSMessageEncoding.Mtom`. 此值可確保使用MTOM。
   * 執行下列工作來啟用基本HTTP驗證：

      * 將AEM表單使用者名稱指派給欄位 `DocumentSecurityServiceClient.ClientCredentials.UserName.UserName`.
      * 將對應的密碼值指派給欄位 `DocumentSecurityServiceClient.ClientCredentials.UserName.Password`.
      * 指派常數值 `HttpClientCredentialType.Basic` 至欄位 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * 指派常數值 `BasicHttpSecurityMode.TransportCredentialOnly` 至欄位 `BasicHttpBindingSecurity.Security.Mode`.


1. 擷取Word檔案。

   * 建立 `BLOB` 物件（使用其建構函式）。 此 `BLOB` 物件是用來儲存已套用原則的Word檔案。
   * 建立 `System.IO.FileStream` 物件，方法是叫用其建構函式，並傳遞代表Word檔案檔案位置和開啟檔案的模式的字串值。
   * 建立位元組陣列，儲存 `System.IO.FileStream` 物件。 透過取得 `System.IO.FileStream` 物件的 `Length` 屬性。
   * 叫用 `System.IO.FileStream` 物件的 `Read` 方法。 傳遞位元組陣列、起始位置以及要讀取的資料流長度。
   * 填入 `BLOB` 物件，透過指派其 `MTOM` 包含位元組陣列內容的欄位。

1. 將現有原則套用至Word檔案。

   透過叫用「 」，將原則套用到Word檔案 `DocumentSecurityServiceClient` 物件的 `protectDocument` 並傳遞下列值：

   * 此 `BLOB` 包含套用原則之Word檔案的物件。
   * 字串值，指定檔案的名稱。
   * 字串值，指定原則所屬的原則集名稱。 您可以指定 `null` 導致下列專案的值： `MyPolicies` 正在使用的原則集。
   * 字串值，指定原則名稱。
   * 字串值，代表檔案發行者使用者的使用者管理員網域名稱。 此引數值為選用值，可為Null (若此引數為Null，則下一個引數值必須為 `null`)。
   * 字串值，代表作為檔案發行者的使用者管理員使用者的正式名稱名稱。 此引數值為選用值，可為Null (若此引數為Null，則前一個引數值必須為 `null`)。
   * A `RMLocale` 指定地區設定值的值(例如， `RMLocale.en`)。
   * 用來儲存原則識別碼值的字串輸出引數。
   * 字串輸出引數，用來儲存受原則保護的識別碼值。
   * 用來儲存MIME型別的字串輸出引數(例如， `application/doc`)。

   此 `protectDocument` 方法傳回 `BLOB` 包含受原則保護的Word檔案的物件。

1. 儲存Word檔案。

   * 建立 `System.IO.FileStream` 物件，方法是叫用其建構函式，並傳遞代表受原則保護之Word檔案的檔案位置的字串值。
   * 建立位元組陣列，儲存 `BLOB` 物件，由 `protectDocument` 方法。 透過取得 `BLOB` 物件的 `MTOM` 資料成員。
   * 建立 `System.IO.BinaryWriter` 物件，方法是叫用其建構函式並傳遞 `System.IO.FileStream` 物件。
   * 透過叫用 `System.IO.BinaryWriter` 物件的 `Write` 方法並傳遞位元組陣列。

**程式碼範例**

如需使用Document Security服務的程式碼範例，請參閱以下快速入門：

* 「快速入門(MTOM)：使用網站服務API將原則套用至Word檔案」

## 從Word檔案移除原則 {#removing-policies-from-word-documents}

您可以從受原則保護的Word檔案中移除原則，以便從檔案中移除安全性。 亦即，如果您不再希望檔案受原則保護。 如果您想要使用更新的原則更新受原則保護的Word檔案，那麼與其移除原則並新增更新的原則，切換原則會更有效率。

>[!NOTE]
>
>如需Document Security服務的詳細資訊，請參閱 [AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63).

### 步驟摘要 {#summary_of_steps-12}

若要從受原則保護的Word檔案中移除原則，請執行下列步驟：

1. 包含專案檔案
1. 建立Document Security使用者端API物件。
1. 擷取受原則保護的Word檔案。
1. 從Word檔案中移除原則。
1. 儲存不安全的Word檔案。

**包含專案檔案**

將必要的檔案納入您的開發專案中。 如果您使用Java建立使用者端應用程式，請包含必要的JAR檔案。 如果您使用Web服務，請務必包含Proxy檔案。

**建立Document Security使用者端API物件**

以程式設計方式執行Document Security服務操作之前，請先建立Document Security服務使用者端物件。

**擷取受原則保護的Word檔案**

您必須擷取受原則保護的Word檔案，才能移除原則。 如果您嘗試從不受原則保護的Word檔案中移除原則，將會造成例外狀況。

**從Word檔案中移除原則**

只要連線設定中指定了管理員，您就可以從受原則保護的Word檔案中移除原則。 如果沒有，則用來保護檔案的原則必須包含 `SWITCH_POLICY` 以從Word檔案中移除原則的許可權。 此外，AEM Forms連線設定中指定的使用者也必須具有該許可權。 否則，會擲回例外狀況。

**儲存不安全的Word檔案**

在Document Security服務從Word檔案中移除原則後，您可以將不安全的Word檔案儲存為DOC檔案。

**另请参阅**

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[將原則套用至Word檔案](protecting-documents-policies.md#applying-policies-to-word-documents)

### 使用Java API從Word檔案中移除原則 {#remove-a-policy-from-a-word-document-using-the-java-api}

使用Document Security API (Java)從受原則保護的Word檔案中移除原則：

1. 包含專案檔案

   在您的Java專案的類別路徑中包含使用者端JAR檔案，例如adobe-rightsmanagement-client.jar。

1. 建立Document Security使用者端API物件

   * 建立 `ServiceClientFactory` 包含連線屬性的物件。
   * 建立 `RightsManagementClient` 物件，使用它的建構函式並傳遞 `ServiceClientFactory` 物件。

1. 擷取受原則保護的Word檔案

   * 建立 `java.io.FileInputStream` 物件，使用受原則保護的Word檔案的建構函式，並傳遞字串值，指定Word檔案的位置。
   * 建立 `com.adobe.idp.Document` 物件，使用它的建構函式並傳遞 `java.io.FileInputStream` 物件。

1. 從Word檔案中移除原則

   * 建立 `DocumentManager` 物件(透過叫用 `RightsManagementClient` 物件的 `getDocumentManager` 方法。
   * 透過叫用 `DocumentManager` 物件的 `removeSecurity` 方法和傳遞 `com.adobe.idp.Document` 包含受原則保護的Word檔案的物件。 此方法會傳回 `com.adobe.idp.Document` 包含不安全Word檔案的物件。

1. 儲存不安全的Word檔案

   * 建立 `java.io.File` 物件並確保副檔名為DOC。
   * 叫用 `Document` 物件的 `copyToFile` 複製目錄內容的方法 `Document` 物件放入檔案(請確定您使用 `Document` 物件，由 `removeSecurity` 方法)。

**程式碼範例**

如需使用Document Security服務的程式碼範例，請參閱以下快速入門：

* 「快速入門（SOAP模式）：使用Java API從Word檔案中移除原則」

### 使用Web服務API從Word檔案中移除原則 {#remove-a-policy-from-a-word-document-using-the-web-service-api}

使用Document Security API （Web服務）從受原則保護的Word檔案中移除原則：

1. 包含專案檔案

   建立使用MTOM的Microsoft .NET專案。 請確定您使用下列WSDL定義： `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Replace `localhost` 搭配裝載AEM Forms之伺服器的IP位址。

1. 建立Document Security使用者端API物件

   * 建立 `RightsManagementServiceClient` 物件（使用其預設建構函式）。
   * 建立 `RightsManagementServiceClient.Endpoint.Address` 物件，使用 `System.ServiceModel.EndpointAddress` 建構函式。 將指定WSDL的字串值傳遞至AEM Forms服務(例如， `http://localhost:8080/soap/services/RightsManagementService?WSDL`.) 您不需要使用 `lc_version` 屬性。 當您建立服務參考時，會使用此屬性。)
   * 建立 `System.ServiceModel.BasicHttpBinding` 物件，方法是取得 `RightsManagementServiceClient.Endpoint.Binding` 欄位。 將傳回值轉換為 `BasicHttpBinding`.
   * 設定 `System.ServiceModel.BasicHttpBinding` 物件的 `MessageEncoding` 欄位至 `WSMessageEncoding.Mtom`. 此值可確保使用MTOM。
   * 執行下列工作來啟用基本HTTP驗證：

      * 將AEM表單使用者名稱指派給欄位 `RightsManagementServiceClient.ClientCredentials.UserName.UserName`.
      * 將對應的密碼值指派給欄位 `RightsManagementServiceClient.ClientCredentials.UserName.Password`.
      * 指派常數值 `HttpClientCredentialType.Basic` 至欄位 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * 指派常數值 `BasicHttpSecurityMode.TransportCredentialOnly` 至欄位 `BasicHttpBindingSecurity.Security.Mode`.


1. 擷取受原則保護的Word檔案

   * 建立 `BLOB` 物件（使用其建構函式）。 此 `BLOB` 物件可用來儲存受原則保護的Word檔案，而原則會從中移除。
   * 建立 `System.IO.FileStream` 物件，方法是叫用其建構函式，並傳遞代表Word檔案檔案位置和開啟檔案的模式的字串值。
   * 建立位元組陣列，儲存 `System.IO.FileStream` 物件。 您可以取得 `System.IO.FileStream` 物件的 `Length` 屬性。
   * 叫用 `System.IO.FileStream` 物件的 `Read` 方法，並傳遞位元組陣列、起始位置以及要讀取的資料流長度。
   * 填入 `BLOB` 物件，透過指派其 `MTOM` 包含位元組陣列內容的欄位。

1. 從Word檔案中移除原則

   透過叫用 `RightsManagementServiceClient` 物件的 `removePolicySecurity` 方法和傳遞 `BLOB` 包含受原則保護的Word檔案的物件。 此方法會傳回 `BLOB` 包含不安全Word檔案的物件。

1. 儲存不安全的Word檔案

   * 建立 `System.IO.FileStream` 物件，方法是叫用其建構函式，並傳遞代表不安全Word檔案檔案位置的字串值。
   * 建立位元組陣列，儲存 `BLOB` 物件，由 `removePolicySecurity` 方法。 透過取得 `BLOB` 物件的 `MTOM` 欄位。
   * 建立 `System.IO.BinaryWriter` 物件，方法是叫用其建構函式並傳遞 `System.IO.FileStream` 物件。

**程式碼範例**

如需使用Document Security服務的程式碼範例，請參閱以下快速入門：

* 「快速入門(MTOM)：使用網站服務API從Word檔案中移除原則」

**另请参阅**

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
