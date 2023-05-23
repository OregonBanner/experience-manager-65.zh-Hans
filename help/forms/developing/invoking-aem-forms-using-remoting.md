---
title: 使用Remoting叫用AEM Forms
seo-title: Invoking AEM Forms using Remoting
description: 使用遠端處理來叫用AEM Forms程式，以叫用在Workbench中建立的程式。 您可以從使用AEM Forms建立的使用者端應用程式叫用Flex程式。
seo-description: Use Remoting to invoke an AEM Forms process to invoke processes created in Workbench. You can invoke a AEM Forms process from a client application built with Flex.
uuid: 592d1519-c38b-4b33-8cf3-61e2bff81501
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: coding
discoiquuid: 3d8bb2d3-b1f8-49e1-a529-b3e7a28da4bb
role: Developer
exl-id: 94a48776-f537-4b4e-8d71-51b08e463cba
source-git-commit: c47b4dcfd2fbdcb0b98ad815f5b04d8f593e4f64
workflow-type: tm+mt
source-wordcount: '4599'
ht-degree: 0%

---

# 使用Remoting叫用AEM Forms {#invoking-aem-forms-using-remoting}

**本檔案中的範例和範例僅適用於JEE環境上的AEM Forms 。**

在Workbench中建立的處理作業可使用遠端功能來叫用。 也就是說，您可以從使用AEM Forms建置的使用者端應用程式叫用Flex程式。 此功能以Data Services為基礎。

>[!NOTE]
>
>使用遠端處理時，建議您叫用在Workbench中建立的程式，而非AEM Forms服務。 不過，您可以直接叫用AEM Forms服務。 (請參閱AEM Forms開發人員中心的「使用遠端處理加密PDF檔案」。)

>[!NOTE]
>
>如果AEM Forms服務未設定為允許匿名存取，來自Flex使用者端的請求會導致網頁瀏覽器詢問。 使用者必須輸入使用者名稱和密碼認證。

下列AEM Forms短期程式，已命名 `MyApplication/EncryptDocument`，可使用Remoting叫用。 (如需有關此程式的資訊，例如其輸入和輸出值，請參閱 [短期程式範例](/help/forms/developing/aem-forms-processes.md).)

![iu_iu_encryptdocumentprocess2](assets/iu_iu_encryptdocumentprocess2.png)

>[!NOTE]
>
>若要使用Flex應用程式叫用AEM Forms程式，請確定已啟用遠端端點。 依預設，當您部署程式時會啟用遠端端點。

叫用此程式時，會執行下列動作：

1. 取得作為輸入值傳遞的不安全PDF檔案。 此動作是根據 `SetValue` 作業。 輸入引數的名稱為 `inDoc` 且其資料型別為 `document`. (此 `document` data type是Workbench中的可用資料型別。)
1. 使用密碼加密PDF檔案。 此動作是根據 `PasswordEncryptPDF` 作業。 此處理序的輸出值名稱是 `outDoc` 和代表以密碼加密的PDF檔案。 outDoc的資料型別為 `document`.
1. 將密碼加密的PDF檔案儲存為PDF檔案至本機檔案系統。 此動作是根據 `WriteDocument` 作業。

>[!NOTE]
>
>此 `MyApplication/EncryptDocument` 程式並非以現有AEM Forms程式為基礎。 若要跟隨程式碼範例，請建立名為的程式 `MyApplication/EncryptDocument` 使用Workbench。

>[!NOTE]
>
>如需使用遠端處理來叫用長效處理程式的詳細資訊，請參閱 [叫用以人為中心的長期流程](/help/forms/developing/invoking-human-centric-long-lived.md#invoking-human-centric-long-lived-processes).

**另请参阅**

[包含AEM Forms Flex程式庫檔案](invoking-aem-forms-using-remoting.md#including-the-aem-forms-flex-library-file)

[使用(不建議用於AEM表單) AEM Forms Remoting處理檔案](invoking-aem-forms-using-remoting.md#handling-documents-with-remoting)

[透過使用(不建議用於AEM表單) AEM Forms Remoting傳遞不安全的檔案來叫用短暫的程式](invoking-aem-forms-using-remoting.md#invoking-a-short-lived-process-by-passing-an-unsecure-document-using-remoting)

[驗證使用Flex建置的使用者端應用程式](invoking-aem-forms-using-remoting.md#authenticating-client-applications-built-with-flex)

[傳遞安全檔案以使用遠端處理來叫用程式](invoking-aem-forms-using-remoting.md#passing-secure-documents-to-invoke-processes-using-remoting)

[使用Remoting叫用自訂元件服務](invoking-aem-forms-using-remoting.md#invoking-custom-component-services-using-remoting)

[使用Flex建立使用者端應用程式，叫用以人為中心的長期流程](/help/forms/developing/invoking-human-centric-long-lived.md#creating-a-client-application-built-with-flex-that-invokes-a-human-centric-long-lived-process)

[建立使用HTTP權杖執行SSO驗證的Flash Builder應用程式](/help/forms/developing/creating-flash-builder-applications-perform.md#creating-flash-builder-applications-that-perform-sso-authentication-using-http-tokens)

<!-- For information on how to display process data in a Flex graph control, see [Displaying AEM Forms process data in Flex graphs](https://www.adobe.com/devnet/livecycle/articles/populating_flexcontrols.html). This URL is 404. No suitable replacement URL was found after a search. Do not make this link live if it is dead! -->

>[!NOTE]
>
>*請務必將crossdomain.xml檔案放在正確的位置。 例如，假設您在JBoss上部署了AEM Forms，請將此檔案放在以下位置： &lt;install_directory>\Adobe_Experience_Manager_forms\jboss\server\lc_turnkey\deploy\jboss-web.deployer\ROOT.war.*

## 包含AEM Forms Flex程式庫檔案 {#including-the-aem-forms-flex-library-file}

若要以程式設計方式使用Remoting叫用AEM Forms程式，請將adobe-remoting-provider.swc檔案新增至Flex專案的類別路徑。 此SWC檔案位於下列位置：

* *&lt;install_directory>\Adobe_Experience_Manager_forms\sdk\misc\DataServices\Client-Libraries*

   其中&lt;*install_directory*>是安裝AEM Forms的目錄。

**另请参阅**

[使用AEM Forms叫用(AEM表單已棄用) AEM Forms Remoting](invoking-aem-forms-using-remoting.md#invoking-aem-forms-using-remoting)

[使用(不建議用於AEM表單) AEM Forms Remoting處理檔案](invoking-aem-forms-using-remoting.md#handling-documents-with-remoting)

[透過使用(不建議用於AEM表單) AEM Forms Remoting傳遞不安全的檔案來叫用短暫的程式](invoking-aem-forms-using-remoting.md#invoking-a-short-lived-process-by-passing-an-unsecure-document-using-remoting)

[驗證使用Flex建置的使用者端應用程式](invoking-aem-forms-using-remoting.md#authenticating-client-applications-built-with-flex)

## 使用遠端處理檔案 {#handling-documents-with-remoting}

AEM Forms中使用的最重要的非原始Java™型別之一是 `com.adobe.idp.Document` 類別。 叫用AEM Forms作業通常需要檔案。 它主要是PDF檔案，但可以包含其他檔案型別，例如SWF、HTML、XML或DOC檔案。 (請參閱 [使用Java API傳遞資料至AEM Forms服務](/help/forms/developing/invoking-aem-forms-using-java.md#passing-data-to-aem-forms-services-using-the-java-api).)

以Flex建置的使用者端應用程式無法直接要求檔案。 例如，您無法啟動Adobe Reader來請求產生PDF檔案的URL。 請求檔案型別(例如PDF和Microsoft® Word檔案)會傳回URL結果。 使用者端有責任顯示URL的內容。 Document Management服務可協助產生URL和內容型別資訊。 對XML檔案的請求會傳回結果中的完整XML檔案。

### 將檔案作為輸入引數傳遞 {#passing-a-document-as-an-input-parameter}

以Flex建置的使用者端應用程式無法直接將檔案傳遞至AEM Forms程式。 相反地，使用者端應用程式使用 `mx.rpc.livecycle.DocumentReference` ActionScript類別，用於將輸入引數傳遞至預期為下列值的作業： `com.adobe.idp.Document` 執行個體。 Flex使用者端應用程式有數個選項可設定 `DocumentReference` 物件：

* 當檔案在伺服器上且其檔案位置已知時，請將DocumentReference物件的referenceType屬性設定為REF_TYPE_FILE。 將fileRef屬性設定為檔案的位置，如下列範例所示：

```java
 ... var docRef: DocumentReference = new DocumentReference(); 
 docRef.referenceType = DocumentReference.REF_TYPE_FILE; 
 docRef.fileRef = "C:/install/adobe/cs2/How to Uninstall.pdf"; ...
```

* 當檔案位於伺服器上且您知道其URL時，請將DocumentReference物件的referenceType屬性設定為REF_TYPE_URL。 將url屬性設定為URL，如下列範例所示：

```java
... var docRef: DocumentReference = new DocumentReference(); 
docRef.referenceType = DocumentReference.REF_TYPE_URL; 
docRef.url = "https://companyserver:8080/DocumentManager/116/7855"; ...
```

* 若要從使用者端應用程式的文字字串建立DocumentReference物件，請將DocumentReference物件的referenceType屬性設定為REF_TYPE_INLINE。 將text屬性設定為要包含在物件中的文字，如下列範例所示：

```java
... var docRef: DocumentReference = new DocumentReference(); 
docRef.referenceType = DocumentReference.REF_TYPE_INLINE; 
docRef.text = "Text for my document";  // Optionally, you can override the server's default character set  // if necessary:  // docRef.charsetName=CharacterSetName  ...
```

* 當檔案不在伺服器上時，請使用遠端上傳servlet將檔案上傳到AEM Forms。 AEM Forms的新功能是上傳安全檔案。 上傳安全檔案時，您必須使用具有 *檔案上傳應用程式使用者* 角色。 若沒有此角色，使用者無法上傳安全檔案。 建議您使用單一登入來上傳安全檔案。 (請參閱 [傳遞安全檔案以使用遠端處理來叫用程式](invoking-aem-forms-using-remoting.md#passing-secure-documents-to-invoke-processes-using-remoting).)

>[!NOTE]
如果將AEM Forms設定為允許上傳不安全的檔案，您可以使用沒有檔案上傳應用程式使用者角色的使用者來上傳檔案。 使用者也可以擁有檔案上傳許可權。 不過，如果AEM Forms設定為僅允許安全檔案，則請確保使用者具有「檔案上傳應用程式」使用者角色或「檔案上傳」許可權。 (請參閱 [將AEM Forms設定為接受安全和不安全的檔案](invoking-aem-forms-using-remoting.md#configuring-aem-forms-to-accept-secure-and-unsecure-documents).

您可對指定的上傳URL使用標準Flash上傳功能： `https://SERVER:PORT/remoting/lcfileupload`. 然後，您可以使用 `DocumentReference` 任何型別的輸入引數所在的物件 `Document` 預期
` private function startUpload():void  {  fileRef.addEventListener(Event.SELECT, selectHandler);  fileRef.addEventListener("uploadCompleteData", completeHandler);  try  {   var success:Boolean = fileRef.browse();  }    catch (error:Error)  {   trace("Unable to browse for files.");  }  }      private function selectHandler(event:Event):void {  var request:URLRequest = new  URLRequest("https://SERVER:PORT/remoting/lcfileupload")  try   {   fileRef.upload(request);   }    catch (error:Error)   {   trace("Unable to upload file.");   }  }    private function completeHandler(event:DataEvent):void  {   var params:Object = new Object();   var docRef:DocumentReference = new DocumentReference();   docRef.url = event.data as String;   docRef.referenceType = DocumentReference.REF_TYPE_URL;  }`遠端快速入門使用遠端上傳servlet將PDF檔案傳遞至 `MyApplication/EncryptDocument`程式。 (請參閱 [透過使用(不建議用於AEM表單) AEM Forms Remoting傳遞不安全的檔案來叫用短暫的程式](invoking-aem-forms-using-remoting.md#invoking-a-short-lived-process-by-passing-an-unsecure-document-using-remoting).)

```java
 
private
function startUpload(): void  { 
 fileRef.addEventListener(Event.SELECT, selectHandler); 
 fileRef.addEventListener("uploadCompleteData", completeHandler); 
 try  { 
  var success: Boolean = fileRef.browse(); 
 }  
 catch (error: Error)  { 
  trace("Unable to browse for files."); 
 } 
}   
private
function selectHandler(event: Event): void { 
 var request: URLRequest = new  URLRequest("https://SERVER:PORT/remoting/lcfileupload")  try  { 
  fileRef.upload(request); 
 }  
 catch (error: Error)  { 
  trace("Unable to upload file."); 
 } 
}  
private
function completeHandler(event: DataEvent): void  { 
 var params: Object = new Object(); 
 var docRef: DocumentReference = new DocumentReference(); 
 docRef.url = event.data as String; 
 docRef.referenceType = DocumentReference.REF_TYPE_URL; 
}
```

遠端快速入門使用遠端上傳servlet將PDF檔案傳遞至 `MyApplication/EncryptDocument`程式。 (請參閱 [透過使用(不建議用於AEM表單) AEM Forms Remoting傳遞不安全的檔案來叫用短暫的程式](invoking-aem-forms-using-remoting.md#invoking-a-short-lived-process-by-passing-an-unsecure-document-using-remoting).)

### 將檔案傳回使用者端應用程式 {#passing-a-document-back-to-a-client-application}

使用者端應用程式接收型別物件 `mx.rpc.livecycle.DocumentReference` 針對傳回 `com.adobe.idp.Document` 執行個體作為輸出引數。 由於使用者端應用程式處理ActionScript物件而非Java，因此您無法將Java型Document物件傳回Flex使用者端。 相反地，伺服器會為檔案產生URL，並將URL傳回使用者端。 此 `DocumentReference` 物件的 `referenceType` 屬性指定內容是否位於 `DocumentReference` 物件或必須從以下位置的URL擷取： `DocumentReference.url` 屬性。 此 `DocumentReference.contentType` 屬性指定檔案的型別。

**另请参阅**

[使用AEM Forms叫用(AEM表單已棄用) AEM Forms Remoting](invoking-aem-forms-using-remoting.md#invoking-aem-forms-using-remoting)

[包含AEM Forms Flex程式庫檔案](invoking-aem-forms-using-remoting.md#including-the-aem-forms-flex-library-file)

[透過使用(不建議用於AEM表單) AEM Forms Remoting傳遞不安全的檔案來叫用短暫的程式](invoking-aem-forms-using-remoting.md#invoking-a-short-lived-process-by-passing-an-unsecure-document-using-remoting)

[驗證使用Flex建置的使用者端應用程式](invoking-aem-forms-using-remoting.md#authenticating-client-applications-built-with-flex)

[傳遞安全檔案以使用遠端處理來叫用程式](invoking-aem-forms-using-remoting.md#passing-secure-documents-to-invoke-processes-using-remoting)

## 透過使用Remoting傳遞不安全的檔案來叫用短暫的流程 {#invoking-a-short-lived-process-by-passing-an-unsecure-document-using-remoting}

若要從使用AEM Forms建立的應用程式叫用Flex程式，請執行下列工作：

1. 建立 `mx:RemoteObject` 執行個體。
1. 建立 `ChannelSet` 執行個體。
1. 傳遞必要的輸入值。
1. 處理傳回值。

>[!NOTE]
本節探討如何叫用AEM Forms程式，以及當AEM Forms設定為上傳不安全的檔案時如何上傳檔案。 如需如何叫用AEM Forms程式及上傳安全檔案，以及如何設定AEM Forms以接受安全和不安全檔案的詳細資訊，請參閱 [傳遞安全檔案以使用遠端處理來叫用程式](invoking-aem-forms-using-remoting.md#passing-secure-documents-to-invoke-processes-using-remoting).

**建立mx：RemoteObject執行個體**

您建立 `mx:RemoteObject` 執行個體，以叫用在Workbench中建立的AEM Forms程式。 若要建立 `mx:RemoteObject` 例項，請指定下列值：

* **id：** 的名稱 `mx:RemoteObject` 代表要呼叫之程式的例項。
* **目的地：** 要呼叫的AEM Forms程式名稱。 例如，若要叫用 `MyApplication/EncryptDocument` 程式，指定 `MyApplication/EncryptDocument`.
* **結果：** 處理結果的Flex方法名稱。

在內 `mx:RemoteObject` 標籤，指定 `<mx:method>` 標籤，指定處理序的呼叫方法名稱。 Forms叫用方法的名稱通常為 `invoke`.

下列程式碼範例會建立 `mx:RemoteObject` 叫用「 」的例項 `MyApplication/EncryptDocument` 程式。

```java
 <mx:RemoteObject id="EncryptDocument" destination="MyApplication/EncryptDocument" result="resultHandler(event);">
          <mx:method name="invoke" result="handleExecuteInvoke(event)"/>
      </mx:RemoteObject>
```

**建立AEM Forms的管道**

使用者端應用程式可透過在MXML或ActionScript中指定管道來叫用AEM Forms，如以下ActionScript範例所示。 管道必須是 `AMFChannel`， `SecureAMFChannel`， `HTTPChannel`，或 `SecureHTTPChannel`.

```java
     ...
     private function refresh():void{
         var cs:ChannelSet= new ChannelSet();
         cs.addChannel(new AMFChannel("my-amf",
             "https://yourlcserver:8080/remoting/messagebroker/amf"));
         EncryptDocument.setCredentials("administrator", "password");
         EncryptDocument.channelSet = cs;
     }
     ...
```

指派 `ChannelSet` 例項至 `mx:RemoteObject` 執行個體的 `channelSet` 欄位（如上一個程式碼範例所示）。 一般而言，您會在匯入陳述式中匯入channel類別，而不是在叫用時指定完整名稱 `ChannelSet.addChannel` 方法。

**傳遞輸入值**

在Workbench中建立的程式可以接受零個或多個輸入引數並傳回輸出值。 使用者端應用程式會將輸入引數傳入 `ActionScript` 物件，其欄位對應至屬於AEM Forms程式的引數。 短期程式，已命名 `MyApplication/EncryptDocument`，需要一個名為的輸入引數 `inDoc`. 處理公開的作業名稱是 `invoke` （短期流程的預設名稱）。 (請參閱 [使用AEM Forms叫用(AEM表單已棄用) AEM Forms Remoting](invoking-aem-forms-using-remoting.md#invoking-aem-forms-using-remoting).)

下列程式碼範例將PDF檔案傳遞至 `MyApplication/EncryptDocument` 程式：

```java
     ...
     var params:Object = new Object();
 
     //Document is an instance of DocumentReference
     //that store an unsecured PDF document
     params["inDoc"] = pdfDocument;
 
     // Invoke an operation synchronously:
     EncryptDocument.invoke(params);
     ...
```

在此程式碼範例中， `pdfDocument` 是 `DocumentReference` 包含不安全PDF檔案的執行個體。 如需關於的資訊 `DocumentReference`，請參閱 [使用(不建議用於AEM表單) AEM Forms Remoting處理檔案](invoking-aem-forms-using-remoting.md#handling-documents-with-remoting).

**叫用特定版本的服務**

您可以使用叫用特定版本的Forms服務 `_version` 引動引數對應中的引數。 例如，若要叫用版本1.2的 `MyApplication/EncryptDocument` 服務：

```java
 var params:Object = new Object();
 params["inDoc"] = pdfDocument;
 params["_version"] = "1.2"
 var token:AsyncToken = echoService.echoString(params);
```

此 `version` 引數必須是包含單一句號的字串。 句點左側（主要版本）和右側（次要版本）的值必須是整數。 如果未指定此引數，則會叫用head active版本。

**處理傳回值**

AEM Forms處理序輸出引數會還原序列化為ActionScript物件，使用者端應用程式會依名稱從中擷取特定引數，如下列範例所示。 (的輸出值 `MyApplication/EncryptDocument` 處理序已命名 `outDoc`.)

```java
     ...
     var res:Object = event.result;
     var docRef:DocumentReference = res["outDoc"] as DocumentReference;
     ...
```

**叫用MyApplication/EncryptDocument程式**

您可以叫用 `MyApplication/EncryptDocument` 透過執行以下步驟來處理：

1. 建立 `mx:RemoteObject` 透過ActionScript或MXML執行個體。 請參閱建立mx：RemoteObject執行個體。
1. 設定 `ChannelSet` 執行個體以與AEM Forms通訊，並將其與 `mx:RemoteObject` 執行個體。 請參閱建立AEM Forms管道。
1. 呼叫ChannelSet `login` 服務的方法或 `setCredentials` 指定使用者識別碼值和密碼的方法。 (請參閱 [使用單一登入](invoking-aem-forms-using-remoting.md#using-single-sign-on).)
1. 填入 `mx.rpc.livecycle.DocumentReference` 具有不安全PDF檔案的執行個體，以傳遞至 `MyApplication/EncryptDocument` 程式。 (請參閱 [將檔案作為輸入引數傳遞](invoking-aem-forms-using-remoting.md#passing-a-document-as-an-input-parameter).)
1. PDF透過呼叫 `mx:RemoteObject` 執行個體的 `invoke` 方法。 傳遞 `Object` 該檔案包含輸入引數(這是不安全的PDF檔案)。 請參閱傳遞輸入值。
1. 擷取從程式傳回的密碼加密PDF檔案。 請參閱處理傳回值。

[快速入門：透過使用(不建議用於AEM表單) AEM Forms Remoting傳遞不安全的檔案來叫用短暫的程式](/help/forms/developing/invocation-api-quick-starts.md#quick-start-invoking-a-short-lived-process-by-passing-an-unsecure-document-using-deprecated-for-aem-forms-aem-forms-remoting)

## 驗證使用Flex建置的使用者端應用程式 {#authenticating-client-applications-built-with-flex}

AEM Forms使用者管理員可透過數種方式，驗證來自Flex應用程式的遠端要求，包括透過中央登入服務的AEM Forms單一登入、基本驗證和自訂驗證。 當未啟用單一登入或匿名存取時，遠端請求會導致基本驗證（預設）或自訂驗證。

基本驗證仰賴Web應用程式容器的標準J2EE基本驗證。 對於基本驗證，HTTP 401錯誤會導致瀏覽器挑戰。 這表示當您嘗試使用RemoteObject連線至Forms應用程式，但尚未從Flex應用程式登入時，瀏覽器會提示您輸入使用者名稱和密碼。

對於自訂驗證，伺服器會傳送錯誤給使用者端，以指出需要驗證。

>[!NOTE]
如需使用HTTP權杖執行驗證的詳細資訊，請參閱 [建立使用HTTP權杖執行SSO驗證的Flash Builder應用程式](/help/forms/developing/creating-flash-builder-applications-perform.md#creating-flash-builder-applications-that-perform-sso-authentication-using-http-tokens).

### 使用自訂驗證 {#using-custom-authentication}

您可以在管理主控台中啟用自訂驗證，方法是從遠端端點上的驗證方法從基本變更為自訂。 如果您使用自訂驗證，使用者端應用程式會呼叫 `ChannelSet.login` 登入方法和 `ChannelSet.logout` 登出的方法。

>[!NOTE]
在舊版AEM Forms中，您藉由呼叫 `RemoteObject.setCredentials` 方法。 此 `setCredentials` 在元件第一次嘗試連線至伺服器之前，方法實際上並未將認證傳遞至伺服器。 因此，如果元件發出錯誤事件，您就無法確定錯誤是否是因為驗證錯誤或其他原因而發生。 此 `ChannelSet.login` 方法會在您呼叫伺服器時連線至伺服器，以便您可以立即處理驗證問題。 雖然您可以繼續使用 `setCredentials` 方法，建議您使用 `ChannelSet.login` 方法。

由於多個目的地可以使用相同的頻道和相應的ChannelSet物件，因此登入一個目的地會將使用者登入使用相同頻道或頻道的任何其他目的地。 如果兩個元件對相同的ChannelSet物件套用不同的認證，則會使用最後套用的認證。 如果有多個元件使用相同的已驗證ChannelSet物件，請呼叫 `logout` 方法會將所有元件登出目的地。

以下範例使用 `ChannelSet.login` 和 `ChannelSet.logout` 方法與RemoteObject控制。 此應用程式會執行下列動作：

* 建立 `ChannelSet` 中的物件 `creationComplete` 代表所使用的管道的處理常式 `RemoteObject` 元件
* 透過呼叫 `ROLogin` 函式來回應按鈕點選事件
* 使用RemoteObject元件傳送字串至伺服器，以回應Button點選事件。 伺服器將相同的字串傳回RemoteObject元件
* 使用RemoteObject元件的結果事件來顯示TextArea控制項中的字串
* 透過呼叫 `ROLogout` 函式來回應按鈕點選事件

```java
 <?xml version="1.0"?>
 <!-- security/SecurityConstraintCustom.mxml -->
 <mx:Application xmlns:mx="https://www.adobe.com/2006/mxml" width="100%"
     height="100%" creationComplete="creationCompleteHandler();">
 
     <mx:Script>
         <![CDATA[
             import mx.controls.Alert;
             import mx.messaging.config.ServerConfig;
             import mx.rpc.AsyncToken;
             import mx.rpc.AsyncResponder;
             import mx.rpc.events.FaultEvent;
             import mx.rpc.events.ResultEvent;
             import mx.messaging.ChannelSet;
 
             // Define a ChannelSet object.
             public var cs:ChannelSet;
 
             // Define an AsyncToken object.
             public var token:AsyncToken;
 
             // Initialize ChannelSet object based on the
             // destination of the RemoteObject component.
             private function creationCompleteHandler():void {
                 if (cs == null)
                 cs = ServerConfig.getChannelSet(remoteObject.destination);
             }
 
             // Login and handle authentication success or failure.
             private function ROLogin():void {
                 // Make sure that the user is not already logged in.
                 if (cs.authenticated == false) {
                     token = cs.login("sampleuser", "samplepassword");
                     // Add result and fault handlers.
                     token.addResponder(new AsyncResponder(LoginResultEvent,
                     LoginFaultEvent));
                 }
             }
 
             // Handle successful login.
             private function LoginResultEvent(event:ResultEvent,
                 token:Object=null):void  {
                     switch(event.result) {
                         case "success":
                             authenticatedCB.selected = true;
                             break;
                             default:
                     }
                 }
 
                 // Handle login failure.
                 private function LoginFaultEvent(event:FaultEvent,
                     token:Object=null):void {
                         switch(event.fault.faultCode) {
                             case "Client.Authentication":
                                 default:
                                 authenticatedCB.selected = false;
                                 Alert.show("Login failure: " + event.fault.faultString);
                     }
                 }
 
                 // Logout and handle success or failure.
                 private function ROLogout():void {
                     // Add result and fault handlers.
                     token = cs.logout();
                     token.addResponder(new
                         AsyncResponder(LogoutResultEvent,LogoutFaultEvent));
                 }
 
                 // Handle successful logout.
                 private function LogoutResultEvent(event:ResultEvent,
                     token:Object=null):void {
                         switch (event.result) {
                             case "success":
                                 authenticatedCB.selected = false;
                                 break;
                                 default:
                     }
                 }
 
                 // Handle logout failure.
                 private function LogoutFaultEvent(event:FaultEvent,
                     token:Object=null):void {
                         Alert.show("Logout failure: " + event.fault.faultString);
                 }
                 // Handle message recevied by RemoteObject component.
                 private function resultHandler(event:ResultEvent):void {
                     ta.text += "Server responded: "+ event.result + "\n";
                 }
 
                 // Handle fault from RemoteObject component.
                 private function faultHandler(event:FaultEvent):void {
                     ta.text += "Received fault: " + event.fault + "\n";
                 }
             ]]>
     </mx:Script>
     <mx:HBox>
         <mx:Label text="Enter a text for the server to echo"/>
         <mx:TextInput id="ti" text="Hello World!"/>
         <mx:Button label="Login"
             click="ROLogin();"/>
         <mx:Button label="Echo"
             enabled="{authenticatedCB.selected}"
             click="remoteObject.echo(ti.text);"/>
         <mx:Button label="Logout"
             click="ROLogout();"/>
         <mx:CheckBox id="authenticatedCB"
             label="Authenticated?"
             enabled="false"/>
     </mx:HBox>
     <mx:TextArea id="ta" width="100%" height="100%"/>
 
     <mx:RemoteObject id="remoteObject"
         destination="myDest"
         result="resultHandler(event);"
         fault="faultHandler(event);"/>
 </mx:Application>
```

此 `login` 和 `logout` 方法會傳回AsyncToken物件。 將事件處理常式指派給AsyncToken物件，讓結果事件處理成功的呼叫，並讓錯誤事件處理失敗。

### 使用單一登入 {#using-single-sign-on}

AEM forms使用者可以連線至多個AEM Forms網頁應用程式以執行工作。 當使用者從一個Web應用程式移動到另一個Web應用程式時，要求他們分別登入每個Web應用程式並不有效率。 AEM Forms單一登入機制可讓使用者登入一次，然後存取任何AEM Forms Web應用程式。 由於AEM Forms開發人員可建立使用者端應用程式以與AEM Forms搭配使用，因此他們也必須能夠利用單一登入機制。

每個AEM Forms Web應用程式都會封裝在自己的Web Archive (WAR)檔案中，然後封裝為Enterprise Archive (EAR)檔案的一部分。 由於應用程式伺服器不允許跨不同的Web應用程式共用工作階段資料，因此AEM Forms會使用HTTP Cookie來儲存驗證資訊。 驗證Cookie可讓使用者登入Forms應用程式，然後連線至其他AEM Forms網頁應用程式。 此技術稱為單一登入。

AEM Forms開發人員撰寫使用者端應用程式以擴充表單指南（已棄用）的功能及自訂工作區。 例如，Workspace應用程式可以啟動程式。 然後，使用者端應用程式會使用遠端端點，從Forms服務擷取資料。

使用(不適用於AEM表單) AEM Forms Remoting叫用AEM Forms服務時，使用者端應用程式會傳遞驗證Cookie作為請求的一部分。 由於使用者已驗證，因此從使用者端應用程式連線至AEM Forms服務不需要額外登入。

>[!NOTE]
如果Cookie無效或遺失，則不會隱含重新導向至登入頁面。 因此，您仍然可以呼叫匿名服務。

您可以撰寫自行登入和登出的使用者端應用程式，略過AEM Forms單一登入機制。 如果您略過單一登入機制，則可以在應用程式中使用基本或自訂驗證。

由於此機制不使用AEM Forms單一登入機制，因此不會將驗證Cookie寫入使用者端。 登入憑證會儲存在 `ChannelSet` 物件。 因此，任何 `RemoteObject` 您透過相同方式進行的呼叫 `ChannelSet` 會以這些認證的內容建立。

### 在AEM Forms中設定單一登入 {#setting-up-single-sign-on-in-aem-forms}

若要在AEM Forms中使用單一登入，請安裝表單工作流程元件，其中包括集中式登入服務。 使用者成功登入後，集中式登入服務會傳回驗證Cookie給使用者。 對Forms網頁應用程式的每個後續請求都包含Cookie。 如果Cookie有效，系統會將使用者視為已驗證，且無需再次登入。

### 撰寫使用單一登入的使用者端應用程式 {#writing-a-client-application-that-uses-single-sign-on}

當您利用單一登入機制時，您預期使用者在啟動使用者端應用程式之前，會先使用集中式登入服務登入。 也就是說，使用者端應用程式不會透過瀏覽器或呼叫 `ChannelSet.login` 方法。

如果您使用AEM Forms單一登入機制，請設定遠端端點使用自訂驗證，而非基本驗證。 否則，在使用基本驗證時，驗證錯誤會導致瀏覽器質詢，您不希望使用者看到。 反之，您的應用程式會偵測驗證錯誤，然後顯示一則訊息，指示使用者使用集中式登入服務登入。

使用者端應用程式透過遠端端點存取AEM Forms，方法是使用 `RemoteObject` 元件，如下列範例所示。

```java
 <?xml version="1.0"?>
 <mx:Application
        backgroundColor="#FFFFFF">
 
       <mx:Script>
          <![CDATA[
 
            import mx.controls.Alert;
            import mx.rpc.events.FaultEvent;
 
            // Prompt user to login on a fault.
            private function faultHandler(event:FaultEvent):void
            {
             if(event.fault.faultCode=="Client.Authentication")
             {
                 Alert.show(
                     event.fault.faultString + "\n" +
                     event.fault.faultCode + "\n" +
                     "Please login to continue.");
             }
         }
          ]]>
       </mx:Script>
 
       <mx:RemoteObject id="srv"
           destination="product"
           fault="faultHandler(event);"/>
 
       <mx:DataGrid
           width="100%" height="100%"
           dataProvider="{srv.getProducts.lastResult}"/>
 
       <mx:Button label="Get Data"
           click="srv.getProducts();"/>
 
 </mx:Application>
```

**在Flex應用程式仍在執行時，以新使用者身分登入**

以Flex建立的應用程式包含驗證Cookie，以及向AEM Forms服務提出的每個請求。 基於效能考量，AEM Forms不會驗證每個請求的Cookie。 不過，AEM Forms會在驗證Cookie被其他驗證Cookie取代時偵測到。

例如，您啟動使用者端應用程式，當應用程式作用中時，您可使用集中式登入服務登出。 接下來，您可以以其他使用者的身分登入。 以其他使用者身分登入會以新使用者的驗證Cookie取代現有的驗證Cookie。

在來自使用者端應用程式的下一個請求中，AEM Forms會偵測Cookie已變更，並將使用者登出。 因此，Cookie變更後的第一個要求會失敗。 所有後續請求都會在新Cookie的上下文中提出，而且會成功。

**登出**

若要登出AEM Forms並讓工作階段失效，必須從使用者端電腦刪除驗證Cookie。 由於單一登入的目的是允許使用者登入一次，因此您不希望使用者端應用程式刪除Cookie。 此動作會有效地將使用者登出。

因此，呼叫 `RemoteObject.logout` 使用者端應用程式中的方法會在使用者端上產生錯誤訊息，指定工作階段未登出。 使用者可以使用集中式登入服務來登出並刪除驗證Cookie。

**Flex應用程式仍在執行時登出**

您可以啟動以Flex建置的使用者端應用程式，並使用集中式登入服務登出。 在登出程式中，會刪除驗證Cookie。 如果在沒有Cookie或使用了無效Cookie的情況下提出遠端請求，則使用者工作階段會失效。 此動作實際上是登出。 下次使用者端應用程式嘗試連線至AEM Forms服務時，系統會要求使用者登入。

**另请参阅**

[使用AEM Forms叫用(AEM表單已棄用) AEM Forms Remoting](invoking-aem-forms-using-remoting.md#invoking-aem-forms-using-remoting)

[使用(不建議用於AEM表單) AEM Forms Remoting處理檔案](invoking-aem-forms-using-remoting.md#handling-documents-with-remoting)

[包含AEM Forms Flex程式庫檔案](invoking-aem-forms-using-remoting.md#including-the-aem-forms-flex-library-file)

[透過使用(不建議用於AEM表單) AEM Forms Remoting傳遞不安全的檔案來叫用短暫的程式](invoking-aem-forms-using-remoting.md#invoking-a-short-lived-process-by-passing-an-unsecure-document-using-remoting)

[傳遞安全檔案以使用遠端處理來叫用程式](invoking-aem-forms-using-remoting.md#passing-secure-documents-to-invoke-processes-using-remoting)

## 傳遞安全檔案以使用遠端處理來叫用程式 {#passing-secure-documents-to-invoke-processes-using-remoting}

當叫用需要一個或多個檔案的程式時，您可以將安全檔案傳遞到AEM Forms。 透過傳遞安全檔案，您就能保護商業資訊和機密檔案。 在這種情況下，檔案可以指PDF檔案、XML檔案、Word檔案等等。 將AEM Forms設定為允許安全檔案時，需要從寫入Flex的使用者端應用程式傳遞安全檔案至AEM Forms。 (請參閱 [將AEM Forms設定為接受安全和不安全的檔案](invoking-aem-forms-using-remoting.md#configuring-aem-forms-to-accept-secure-and-unsecure-documents).)

AEM傳遞安全檔案時，請使用單一登入，並指定擁有 *檔案上傳應用程式使用者* 角色。 若沒有此角色，使用者無法上傳安全檔案。 您可以以程式設計方式將角色指派給使用者。 (請參閱 [管理角色和許可權](/help/forms/developing/users.md#managing-roles-and-permissions).)

>[!NOTE]
當您建立新角色並希望該角色的成員上傳安全檔案時，請確保您指定檔案上傳許可權。

AEM Forms支援名為的操作 `getFileUploadToken` 會傳回傳遞至上傳servlet的Token。 此 `DocumentReference.constructRequestForUpload` 方法需要AEM Forms的URL以及傳回的權杖 `LC.FileUploadAuthenticator.getFileUploadToken` 方法。 此方法會傳回 `URLRequest` 用於叫用上傳servlet的物件。 下列程式碼會示範此應用程式邏輯。

```java
     ...
         private function startUpload():void
         {
             fileRef.addEventListener(Event.SELECT, selectHandler);
             fileRef.addEventListener("uploadCompleteData", completeHandler);
             try
             {
         var success:Boolean = fileRef.browse();
             }
             catch (error:Error)
             {
                 trace("Unable to browse for files.");
             }
 
         }
 
          private function selectHandler(event:Event):void
             {
             var authTokenService:RemoteObject = new RemoteObject("LC.FileUploadAuthenticator");
             authTokenService.addEventListener("result", authTokenReceived);
             authTokenService.channelSet = cs;
             authTokenService.getFileUploadToken();
             }
 
         private function authTokenReceived(event:ResultEvent):void
             {
             var token:String = event.result as String;
             var request:URLRequest = DocumentReference.constructRequestForUpload("http://localhost:8080", token);
 
             try
             {
           fileRef.upload(request);
             }
             catch (error:Error)
             {
             trace("Unable to upload file.");
             }
             }
 
         private function completeHandler(event:DataEvent):void
         {
 
             var params:Object = new Object();
             var docRef:DocumentReference = new DocumentReference();
             docRef.url = event.data as String;
             docRef.referenceType = DocumentReference.REF_TYPE_URL;
         }
         ...
```

）

### 將AEM Forms設定為接受安全和不安全的檔案 {#configuring-aem-forms-to-accept-secure-and-unsecure-documents}

您可以將檔案從Flex使用者端應用程式傳遞至AEM Forms程式時，使用管理主控台來指定檔案是否安全。 依預設，AEM Forms會設定為接受安全檔案。 您可以透過執行以下步驟來設定AEM Forms以接受安全檔案：

1. 登入管理主控台。
1. 按一下 **設定**.
1. 按一下 **核心系統設定。**
1. 按一下「組態」。
1. 確保取消選取「允許從Flex應用程式上傳不安全的檔案」選項。

>[!NOTE]
若要設定AEM Forms以接受不安全的檔案，請選取允許從Flex應用程式上傳不安全的檔案選項。 然後重新啟動應用程式或服務，確保設定生效。

### 快速入門：透過使用Remoting傳遞安全檔案來叫用短期程式 {#quick-start-invoking-a-short-lived-process-by-passing-a-secure-document-using-remoting}

下列程式碼範例會叫用 `MyApplication/EncryptDocument.`使用者必須登入才能按一下選取檔案按鈕，該按鈕用於上傳PDF檔案並叫用程式。 也就是說，一旦使用者通過驗證，就會啟用「選取檔案」按鈕。 下圖顯示使用者通過驗證後的Flex使用者端應用程式。 請注意，已驗證的CheckBox已啟用。

![iu_iu_securemotelogin](assets/iu_iu_secureremotelogin.png)

如果將AEM Forms設定為只允許上傳安全檔案，而使用者沒有 *檔案上傳應用程式使用者* 角色，則會擲回例外狀況。 如果使用者確實有此角色，則會上傳檔案並叫用程式。

```java
 <?xml version="1.0" encoding="utf-8"?>
 <mx:Application  xmlns="*"
      creationComplete="initializeChannelSet();">
        <mx:Script>
        <![CDATA[
      import mx.rpc.livecycle.DocumentReference;
      import flash.net.FileReference;
      import flash.net.URLRequest;
      import flash.events.Event;
      import flash.events.DataEvent;
      import mx.messaging.ChannelSet;
      import mx.messaging.channels.AMFChannel;
      import mx.rpc.events.ResultEvent;
      import mx.collections.ArrayCollection;
      import mx.rpc.AsyncToken;
      import mx.controls.Alert;
      import mx.rpc.events.FaultEvent;
      import mx.rpc.AsyncResponder;
 
      // Classes used in file retrieval
      private var fileRef:FileReference = new FileReference();
      private var docRef:DocumentReference = new DocumentReference();
      private var parentResourcePath:String = "/";
      private var now1:Date;
      private var serverPort:String = "hiro-xp:8080";
 
      // Define a ChannelSet object.
      public var cs:ChannelSet;
 
      // Define an AsyncToken object.
      public var token:AsyncToken;
 
       // Holds information returned from AEM Forms
      [Bindable]
      public var progressList:ArrayCollection = new ArrayCollection();
 
 
      // Handles a successful login
     private function LoginResultEvent(event:ResultEvent,
         token:Object=null):void  {
             switch(event.result) {
                 case "success":
                     authenticatedCB.selected = true;
                     btnFile.enabled = true;
                     btnLogout.enabled = true;
                     btnLogin.enabled = false;
                         break;
                     default:
                 }
             }
 
 
 // Handle login failure.
 private function LoginFaultEvent(event:FaultEvent,
     token:Object=null):void {
     switch(event.fault.faultCode) {
                 case "Client.Authentication":
                         default:
                         authenticatedCB.selected = false;
                         Alert.show("Login failure: " + event.fault.faultString);
                 }
             }
 
 
      // Set up channel set to invoke AEM Forms
      private function initializeChannelSet():void {
        cs = new ChannelSet();
        cs.addChannel(new AMFChannel("remoting-amf", "https://" + serverPort + "/remoting/messagebroker/amf"));
        EncryptDocument2.channelSet = cs;
      }
 
     // Call this method to upload the file.
      // This creates a file picker and lets the user select a PDF file to pass to the EncryptDocument process.
      private function uploadFile():void {
        fileRef.addEventListener(Event.SELECT, selectHandler);
        fileRef.addEventListener(DataEvent.UPLOAD_COMPLETE_DATA,completeHandler);
        fileRef.browse();
      }
 
      // Gets called for selected file. Does the actual upload via the file upload servlet.
      private function selectHandler(event:Event):void {
              var authTokenService:RemoteObject = new RemoteObject("LC.FileUploadAuthenticator");
         authTokenService.addEventListener("result", authTokenReceived);
         authTokenService.channelSet = cs;
         authTokenService.getFileUploadToken();
      }
 
     private function authTokenReceived(event:ResultEvent):void
     {
     var token:String = event.result as String;
     var request:URLRequest = DocumentReference.constructRequestForUpload("https://hiro-xp:8080", token);
 
     try
     {
           fileRef.upload(request);
     }
     catch (error:Error)
     {
         trace("Unable to upload file.");
     }
 }
 
      // Called once the file is completely uploaded.
      private function completeHandler(event:DataEvent):void {
 
        // Set the docRef's url and referenceType parameters
        docRef.url = event.data as String;
        docRef.referenceType=DocumentReference.REF_TYPE_URL;
        executeInvokeProcess();
      }
 
     //This method invokes the EncryptDocument process
      public function executeInvokeProcess():void {
         //Create an Object to store the input value for the EncryptDocument process
           now1 = new Date();
 
         var params:Object = new Object();
         params["inDoc"]=docRef;
 
         // Invoke the EncryptDocument process
         var token:AsyncToken;
         token = EncryptDocument2.invoke(params);
         token.name = name;
      }
 
      // AEM Forms  login method
      private function ROLogin():void {
         // Make sure that the user is not already logged in.
 
         //Get the User and Password
         var userName:String = txtUser.text;
         var pass:String = txtPassword.text;
 
        if (cs.authenticated == false) {
             token = cs.login(userName, pass);
 
         // Add result and fault handlers.
         token.addResponder(new AsyncResponder(LoginResultEvent,    LoginFaultEvent));
                 }
             }
 
      // This method handles a successful process invocation
      public function handleResult(event:ResultEvent):void
      {
            //Retrieve information returned from the service invocation
          var token:AsyncToken = event.token;
          var res:Object = event.result;
          var dr:DocumentReference = res["outDoc"] as DocumentReference;
          var now2:Date = new Date();
 
           // These fields map to columns in the DataGrid
          var progObject:Object = new Object();
          progObject.filename = token.name;
          progObject.timing = (now2.time - now1.time).toString();
          progObject.state = "Success";
          progObject.link = "<a href='" + dr.url + "'> open </a>";
          progressList.addItem(progObject);
      }
 
      // Prompt user to login on a fault.
       private function faultHandler(event:FaultEvent):void
            {
             if(event.fault.faultCode=="Client.Authentication")
             {
                 Alert.show(
                     event.fault.faultString + "\n" +
                     event.fault.faultCode + "\n" +
                     "Please login to continue.");
             }
            }
 
       // AEM Forms  logout method
     private function ROLogout():void {
         // Add result and fault handlers.
         token = cs.logout();
         token.addResponder(new AsyncResponder(LogoutResultEvent,LogoutFaultEvent));
     }
 
     // Handle successful logout.
     private function LogoutResultEvent(event:ResultEvent,
         token:Object=null):void {
         switch (event.result) {
         case "success":
                 authenticatedCB.selected = false;
                 btnFile.enabled = false;
                 btnLogout.enabled = false;
                 btnLogin.enabled = true;
                 break;
                 default:
             }
     }
 
     // Handle logout failure.
     private function LogoutFaultEvent(event:FaultEvent,
             token:Object=null):void {
             Alert.show("Logout failure: " + event.fault.faultString);
     }
 
          private function resultHandler(event:ResultEvent):void {
          // Do anything else here.
          }
        ]]>
 
      </mx:Script>
      <mx:RemoteObject id="EncryptDocument" destination="MyApplication/EncryptDocument" result="resultHandler(event);">
          <mx:method name="invoke" result="handleResult(event)"/>
      </mx:RemoteObject>
 
       <!--//This consists of what is displayed on the webpage-->
      <mx:Panel id="lcPanel" title="EncryptDocument  (Deprecated for AEM forms) AEM Forms Remoting Example"
           height="25%" width="25%" paddingTop="10" paddingLeft="10" paddingRight="10"
           paddingBottom="10">
         <mx:Label width="100%" color="blue"
                text="Select a PDF file to pass to the EncryptDocument process"/>
        <mx:DataGrid x="10" y="0" width="500" id="idProgress" editable="false"
           dataProvider="{progressList}" height="231" selectable="false" >
          <mx:columns>
            <mx:DataGridColumn headerText="Filename" width="200" dataField="filename" editable="false"/>
            <mx:DataGridColumn headerText="State" width="75" dataField="state" editable="false"/>
            <mx:DataGridColumn headerText="Timing" width="75" dataField="timing" editable="false"/>
            <mx:DataGridColumn headerText="Click to Open" dataField="link" editable="false" >
             <mx:itemRenderer>
                <mx:Component>
                   <mx:Text x="0" y="0" width="100%" htmlText="{data.link}"/>
                </mx:Component>
             </mx:itemRenderer>
            </mx:DataGridColumn>
          </mx:columns>
        </mx:DataGrid>
        <mx:Button label="Select File" click="uploadFile()"  id="btnFile" enabled="false"/>
        <mx:Button label="Login" click="ROLogin();" id="btnLogin"/>
        <mx:Button label="LogOut" click="ROLogout();" enabled="false" id="btnLogout"/>
        <mx:HBox>
         <mx:Label text="User:"/>
         <mx:TextInput id="txtUser" text=""/>
         <mx:Label text="Password:"/>
         <mx:TextInput id="txtPassword" text="" displayAsPassword="true"/>
         <mx:CheckBox id="authenticatedCB"
             label="Authenticated?"
             enabled="false"/>
     </mx:HBox>
      </mx:Panel>
 </mx:Application>
```

**另请参阅**

[使用AEM Forms叫用(AEM表單已棄用) AEM Forms Remoting](invoking-aem-forms-using-remoting.md#invoking-aem-forms-using-remoting)

[使用(不建議用於AEM表單) AEM Forms Remoting處理檔案](invoking-aem-forms-using-remoting.md#handling-documents-with-remoting)

[包含AEM Forms Flex程式庫檔案](invoking-aem-forms-using-remoting.md#including-the-aem-forms-flex-library-file)

[透過使用(不建議用於AEM表單) AEM Forms Remoting傳遞不安全的檔案來叫用短暫的程式](invoking-aem-forms-using-remoting.md#invoking-a-short-lived-process-by-passing-an-unsecure-document-using-remoting)

[驗證使用Flex建置的使用者端應用程式](invoking-aem-forms-using-remoting.md#authenticating-client-applications-built-with-flex)

## 使用Remoting叫用自訂元件服務 {#invoking-custom-component-services-using-remoting}

您可以使用Remoting叫用位於自訂元件中的服務。 例如，考慮包含客戶服務的Bank元件。 您可以使用在Flex中編寫的使用者端應用程式來叫用屬於客戶服務的操作。 您必須先建立Bank自訂元件，才能執行與此區段關聯的快速入門。

客戶服務會公開名為的作業 `createCustomer`. 本討論說明如何建立叫用客戶服務並建立客戶的Flex使用者端應用程式。 此作業需要型別複雜的物件 `com.adobe.livecycle.sample.customer.Customer` 代表新客戶。 下圖顯示叫用客戶服務並建立新客戶的使用者端應用程式。 此 `createCustomer` operation會傳回客戶識別碼值。 識別碼值會顯示在「客戶識別碼」文字方塊中。

![iu_iu_flexnewcust](assets/iu_iu_flexnewcust.png)

下表列出屬於此使用者端應用程式的控制項。

<table>
 <thead>
  <tr>
   <th><p>控制項名稱</p></th>
   <th><p>描述</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>txtFirst</p></td>
   <td><p>指定客戶的名字。 </p></td>
  </tr>
  <tr>
   <td><p>txtLast</p></td>
   <td><p>指定客戶的姓氏。 </p></td>
  </tr>
  <tr>
   <td><p>txtPhone</p></td>
   <td><p>指定客戶的電話號碼。</p></td>
  </tr>
  <tr>
   <td><p>txtStreet</p></td>
   <td><p>指定客戶的街道名稱。</p></td>
  </tr>
  <tr>
   <td><p>txtState</p></td>
   <td><p>指定客戶的狀態。 </p></td>
  </tr>
  <tr>
   <td><p>txtZIP</p></td>
   <td><p>指定客戶的郵遞區號。 </p></td>
  </tr>
  <tr>
   <td><p>txtCity</p></td>
   <td><p>指定客戶的城市。</p></td>
  </tr>
  <tr>
   <td><p>txtCustId</p></td>
   <td><p>指定新帳戶所屬的客戶識別碼值。 此文字方塊由客戶服務的 <code>createCustomer</code> 作業。 </p></td>
  </tr>
 </tbody>
</table>

### 對應AEM Forms複雜資料型別 {#mapping-aem-forms-complex-data-types}

有些AEM Forms作業會以複雜的資料型別作為輸入值。 這些複雜的資料型別會定義作業所使用的執行階段值。 例如，客戶服務的 `createCustomer` 作業需要 `Customer` 包含服務所需的執行階段值的執行個體。 若沒有複雜型別，客戶服務會擲回例外狀況，且不會執行作業。

叫用AEM Forms服務時，請建立對應到所需AEM Forms複雜型別的ActionScript物件。 針對作業所需的每個複雜資料型別，建立個別的ActionScript物件。

在ActionScript類別中，使用 `RemoteClass` 對應至AEM Forms複雜型別的中繼資料標籤。 例如，叫用客戶服務的 `createCustomer` 作業，建立對應至的ActionScript類別 `com.adobe.livecycle.sample.customer.Customer` 資料型別。

下列名為「客戶」的ActionScript類別說明如何對應至AEM Forms資料型別 `com.adobe.livecycle.sample.customer.Customer`.

```java
 package customer
 
 {
     [RemoteClass(alias="com.adobe.livecycle.sample.customer.Customer")]
     public class Customer
     {
            public var name:String;
            public var street:String;
            public var city:String;
            public var state:String;
            public var phone:String;
            public var zip:int;
        }
 }
```

AEM Forms複雜型別的完整資料型別會指派給別名標籤。

ActionScript類別的欄位與屬於AEM Forms複雜型別的欄位相符。 位於客戶ActionScript類別中的六個欄位與屬於的欄位相符 `com.adobe.livecycle.sample.customer.Customer`.

>[!NOTE]
判斷屬於Forms複雜型別的欄位名稱的一個好方法是在Web瀏覽器中檢視服務的WSDL。 WSDL會指定服務的複雜型別和對應的資料成員。 客戶服務使用下列WSDL： `https://[yourServer]:[yourPort]/soap/services/CustomerService?wsdl.`

CustomerActionScript類別屬於名為customer的套件。 建議您將對應到複雜AEM Forms資料型別的所有ActionScript類別放在自己的套件中。 在Flex專案的src資料夾中建立一個資料夾，並將ActionScript檔案放在資料夾中，如下圖所示。

![iu_iu_customeras](assets/iu_iu_customeras.png)

### 快速入門：使用Remoting叫用客戶自訂服務 {#quick-start-invoking-the-customer-custom-service-using-remoting}

下列程式碼範例會叫用客戶服務並建立客戶。 執行此程式碼範例時，請確定您填寫所有文字方塊。 此外，請確定您建立了對應至下列專案的Customer.as檔案： `com.adobe.livecycle.sample.customer.Customer`.

>[!NOTE]
您必須先建立並部署Bank自訂元件，才能執行此快速入門。

```java
 <?xml version="1.0" encoding="utf-8"?>
 <mx:Application  layout="absolute" backgroundColor="#B1ABAB">
 
 <mx:Script>
            <![CDATA[
 
      import flash.net.FileReference;
      import flash.net.URLRequest;
      import flash.events.Event;
      import flash.events.DataEvent;
      import mx.messaging.ChannelSet;
      import mx.messaging.channels.AMFChannel;
      import mx.rpc.events.ResultEvent;
      import mx.collections.ArrayCollection;
      import mx.rpc.AsyncToken;
      import mx.managers.CursorManager;
      import mx.rpc.remoting.mxml.RemoteObject;
 
 
      // Custom class that corresponds to an input to the
      // AEM Forms encryption method
      import customer.Customer;
 
      // Classes used in file retrieval
      private var fileRef:FileReference = new FileReference();
      private var parentResourcePath:String = "/";
      private var serverPort:String = "hiro-xp:8080";
      private var now1:Date;
      private var fileName:String;
 
      // Prepares parameters for encryptPDFUsingPassword method call
      public function executeCreateCustomer():void
      {
 
        var cs:ChannelSet= new ChannelSet();
     cs.addChannel(new AMFChannel("remoting-amf", "https://" + serverPort + "/remoting/messagebroker/amf"));
 
     customerService.setCredentials("administrator", "password");
     customerService.channelSet = cs;
 
     //Create a Customer object required to invoke the Customer service's
     //createCustomer operation
     var myCust:Customer = new Customer();
 
     //Get values from the user of the Flex application
     var fullName:String = txtFirst.text +" "+txtLast.text ;
     var Phone:String = txtPhone.text;
     var Street:String = txtStreet.text;
     var State:String = txtState.text;
     var Zip:int = parseInt(txtZIP.text);
     var City:String = txtCity.text;
 
     //Populate Customer fields
     myCust.name = fullName;
     myCust.phone = Phone;
     myCust.street= Street;
     myCust.state= State;
     myCust.zip = Zip;
     myCust.city = City;
 
     //Invoke the Customer service's createCustomer operation
     var params:Object = new Object();
        params["inCustomer"]=myCust;
     var token:AsyncToken;
        token = customerService.createCustomer(params);
        token.name = name;
      }
 
      private function handleResult(event:ResultEvent):void
      {
          // Retrieve the information returned from the service invocation
          var token:AsyncToken = event.token;
          var res:Object = event.result;
          var custId:String = res["CustomerId"] as String;
 
          //Assign to the custId to the text box
          txtCustId.text = custId;
      }
 
 
      private function resultHandler(event:ResultEvent):void
      {
 
      }
            ]]>
 </mx:Script>
 <mx:RemoteObject id="customerService" destination="CustomerService" result="resultHandler(event);">
 <mx:method name="createCustomer" result="handleResult(event)"/>
 </mx:RemoteObject>
 
 
 <mx:Style source="../bank.css"/>
     <mx:Grid>
                     <mx:GridRow width="100%" height="100%">
                         <mx:GridItem width="100%" height="100%">
                             <mx:Label text="New Customer" fontSize="16" fontWeight="bold"/>
                         </mx:GridItem>
                         <mx:GridItem width="100%" height="100%">
                         </mx:GridItem>
                         <mx:GridItem width="100%" height="100%">
                         </mx:GridItem>
                     </mx:GridRow>
                     <mx:GridRow width="100%" height="100%">
                         <mx:GridItem width="100%" height="100%">
                             <mx:Label text="First Name:" fontSize="12" fontWeight="bold"/>
                         </mx:GridItem>
                         <mx:GridItem width="100%" height="100%">
                             <mx:TextInput styleName="textField" id="txtFirst"/>
                         </mx:GridItem>
                         <mx:GridItem width="100%" height="100%">
                             <mx:Button label="Create Customer" id="btnCreateCustomer" click="executeCreateCustomer()"/>
                         </mx:GridItem>
                     </mx:GridRow>
                     <mx:GridRow width="100%" height="100%">
                         <mx:GridItem width="100%" height="100%">
                             <mx:Label text="Last Name" fontSize="12" fontWeight="bold"/>
                         </mx:GridItem>
                         <mx:GridItem width="100%" height="100%">
                             <mx:TextInput styleName="textField" id="txtLast"/>
                         </mx:GridItem>
                         <mx:GridItem width="100%" height="100%">
                         </mx:GridItem>
                     </mx:GridRow>
                     <mx:GridRow width="100%" height="100%">
                         <mx:GridItem width="100%" height="100%">
                             <mx:Label text="Phone" fontSize="12" fontWeight="bold"/>
                         </mx:GridItem>
                         <mx:GridItem width="100%" height="100%">
                             <mx:TextInput styleName="textField" id="txtPhone"/>
                         </mx:GridItem>
                         <mx:GridItem width="100%" height="100%">
                         </mx:GridItem>
                     </mx:GridRow>
                     <mx:GridRow width="100%" height="100%">
                         <mx:GridItem width="100%" height="100%">
                             <mx:Label text="Street" fontSize="12" fontWeight="bold"/>
                         </mx:GridItem>
                         <mx:GridItem width="100%" height="100%">
                             <mx:TextInput styleName="textField" id="txtStreet"/>
                         </mx:GridItem>
                         <mx:GridItem width="100%" height="100%">
                         </mx:GridItem>
                     </mx:GridRow>
                     <mx:GridRow width="100%" height="100%">
                         <mx:GridItem width="100%" height="100%">
                             <mx:Label text="State" fontSize="12" fontWeight="bold"/>
                         </mx:GridItem>
                         <mx:GridItem width="100%" height="100%">
                             <mx:TextInput styleName="textField" id="txtState"/>
                         </mx:GridItem>
                         <mx:GridItem width="100%" height="100%">
                         </mx:GridItem>
                     </mx:GridRow>
                     <mx:GridRow width="100%" height="100%">
                         <mx:GridItem width="100%" height="100%">
                             <mx:Label text="ZIP" fontSize="12" fontWeight="bold"/>
                         </mx:GridItem>
                         <mx:GridItem width="100%" height="100%">
                             <mx:TextInput styleName="textField" id="txtZIP"/>
                         </mx:GridItem>
                         <mx:GridItem width="100%" height="100%">
                         </mx:GridItem>
                     </mx:GridRow>
                     <mx:GridRow width="100%" height="100%">
                         <mx:GridItem width="100%" height="100%">
                             <mx:Label text="City" fontSize="12" fontWeight="bold"/>
                         </mx:GridItem>
                         <mx:GridItem width="100%" height="100%">
                             <mx:TextInput styleName="textField" id="txtCity"/>
                         </mx:GridItem>
                         <mx:GridItem width="100%" height="100%">
                         </mx:GridItem>
                     </mx:GridRow>
                             <mx:GridRow width="100%" height="100%">
                         <mx:GridItem width="100%" height="100%">
                             <mx:Label text="Customer Identifier" fontSize="12" fontWeight="bold"/>
                         </mx:GridItem>
                         <mx:GridItem width="100%" height="100%">
                             <mx:TextInput styleName="textField" id="txtCustId" editable="false"/>
                         </mx:GridItem>
                         <mx:GridItem width="100%" height="100%">
                         </mx:GridItem>
                     </mx:GridRow>
                 </mx:Grid>
 </mx:Application>
 
```

**樣式表**

此快速入門包含名為的樣式表 *bank.css*. 下列程式碼代表使用的樣式表。

```css
 /* CSS file */
 global
 {
          backgroundGradientAlphas: 1.0, 1.0;
          backgroundGradientColors: #525152,#525152;
          borderColor: #424444;
          verticalAlign: middle;
          color: #FFFFFF;
          font-size:12;
          font-weight:normal;
 }
 
 ApplicationControlBar
 {
          fillAlphas: 1.0, 1.0;
          fillColors: #393839, #393839;
 }
 
 .textField
 {
          backgroundColor: #393839;
          background-disabled-color: #636563;
 }
 
 
 .button
 {
          fillColors: #636563, #424242;
 }
 
 .dropdownMenu
 {
          backgroundColor: #DDDDDD;
          fillColors: #636563, #393839;
          alternatingItemColors: #888888, #999999;
 }
 
 .questionLabel
 {
 
 }
 
 ToolTip
 {
        backgroundColor: black;
        backgroundAlpha: 1.0;
        cornerRadius: 0;
        color: white;
 }
 
 DateChooser
 {
        cornerRadius: 0; /* pixels */
        headerColors: black, black;
        borderColor: black;
        themeColor: black;
        todayColor: red;
        todayStyleName: myTodayStyleName;
        headerStyleName: myHeaderStyleName;
        weekDayStyleName: myWeekDayStyleName;
        dropShadowEnabled: true;
 }
 
 .myTodayStyleName
 {
        color: white;
 }
 
 .myWeekDayStyleName
 {
        fontWeight: normal;
 }
 
 .myHeaderStyleName
 {
        color: red;
        fontSize: 16;
        fontWeight: bold;
 }
```

**另请参阅**

[使用AEM Forms叫用(AEM表單已棄用) AEM Forms Remoting](invoking-aem-forms-using-remoting.md#invoking-aem-forms-using-remoting)

[使用(不建議用於AEM表單) AEM Forms Remoting處理檔案](invoking-aem-forms-using-remoting.md#handling-documents-with-remoting)

[包含AEM Forms Flex程式庫檔案](invoking-aem-forms-using-remoting.md#including-the-aem-forms-flex-library-file)

[透過使用(不建議用於AEM表單) AEM Forms Remoting傳遞不安全的檔案來叫用短暫的程式](invoking-aem-forms-using-remoting.md#invoking-a-short-lived-process-by-passing-an-unsecure-document-using-remoting)

[驗證使用Flex建置的使用者端應用程式](invoking-aem-forms-using-remoting.md#authenticating-client-applications-built-with-flex)

[傳遞安全檔案以使用遠端處理來叫用程式](invoking-aem-forms-using-remoting.md#passing-secure-documents-to-invoke-processes-using-remoting)
