---
title: 建立使用HTTP權杖執行SSO驗證的Flash Builder應用程式
seo-title: Creating Flash Builder applicationsthat perform SSO authentication using HTTP tokens
description: 使用Flash Builder建立使用者端應用程式，該應用程式會使用HTTP權杖執行單一登入(SSO)驗證。 對某個操作驗證一次使用者，然後使用該驗證執行多個AEM Forms操作。
seo-description: Create a client application using Flash Builder that performs single-sign on (SSO) authentication using HTTP tokens. Authenticate a user for an operation once and use that authentication to perform multiple AEM Forms operations.
uuid: 273db00a-a665-4e52-88fa-4fca06d05f8c
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: coding
discoiquuid: 0ff30df7-b3ad-4c34-9644-87c689acc294
role: Developer
exl-id: 7f1f49e6-028c-47b6-a24d-a83bed40242e
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1796'
ht-degree: 0%

---

# 建立使用HTTP權杖執行SSO驗證的Flash Builder應用程式 {#creating-flash-builder-applicationsthat-perform-sso-authentication-using-http-tokens}

**本檔案中的範例和範例僅適用於JEE環境上的AEM Forms 。**

您可以使用Flash Builder建立使用者端應用程式，該應用程式會使用HTTP權杖執行單一登入(SSO)驗證。 例如，假設您使用Flash Builder建立網頁型應用程式。 接下來，假設應用程式包含不同的檢視，每個檢視會叫用不同的AEM Forms操作。 您可以建立登入頁面，讓使用者驗證一次，而不需驗證每個Forms作業的使用者。 一旦驗證，使用者就可以叫用多個操作，而無需再次驗證。 例如，如果使用者已登入工作區(或其他Forms應用程式)，則使用者不需要再次驗證。

雖然使用者端應用程式包含執行SSO驗證所需的應用程式邏輯，但AEM Forms使用者管理會執行實際的使用者驗證。 若要使用HTTP權杖驗證使用者，使用者端應用程式會叫用Authentication Manager服務的 `authenticateWithHTTPToken` 作業。 「使用者管理」能使用HTTP權杖驗證使用者。 對於後續對AEM Forms的遠端處理或Web服務呼叫，您不必傳遞認證以進行驗證。

>[!NOTE]
>
>在閱讀本節之前，建議您先熟悉使用遠端功能叫用AEM Forms 。 (請參閱 [使用AEM Forms Remoting叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-remoting.md#invoking-aem-forms-using-remoting).)

下列AEM Forms短期程式，已命名 `MyApplication/EncryptDocument`，會在使用者使用SSO驗證後叫用。 (如需有關此程式的資訊，例如其輸入和輸出值，請參閱 [短期程式範例](/help/forms/developing/aem-forms-processes.md).)

![cf_cf_encryptdocumentprocess2](assets/cf_cf_encryptdocumentprocess2.png)

>[!NOTE]
>
>此程式並非以現有AEM Forms程式為基礎。 若要與討論如何呼叫此程式的程式碼範例一起遵循，請建立名為的程式 `MyApplication/EncryptDocument` 使用workbench。 (請參閱 [使用Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63).)

使用Flash Builder建置的使用者端應用程式會與設定在「 」的User Manager安全性servlet互動 `/um/login` 和 `/um/logout`. 也就是說，使用者端應用程式會將要求傳送至 `/um/login` 啟動期間的URL，用於判斷使用者的狀態。 然後User Manager會以使用者狀態回應。 使用者端應用程式和使用者管理員安全性servlet使用HTTP通訊。

**請求格式**

安全性servlet需要下列輸入變數：

* `um_no_redirect`  — 此值必須為 `true`. 此變數會與對使用者管理員安全性servlet提出的所有請求一併提供。 它還有助於安全性servlet區分來自Flex使用者端或其他Web應用程式的傳入請求。
* `j_username`  — 此值是使用者在登入表單中提供的登入識別碼值。
* `j_password`  — 此值是使用者在登入表單中提供的對應密碼。

此 `j_password` 只有認證請求才需要值。 如果未指定密碼值，則安全性servlet會檢查以判斷您使用的帳戶是否已驗證。 如果是，您可以繼續；但是，安全性servlet不會再次驗證您。

>[!NOTE]
>
>若要正確處理i18n，請確定這些值採用POST形式。

**回應格式**

安全性servlet設定於 `/um/login` 使用回應 `URLVariables` 格式。 在此格式中，內容型別的輸出為text/plain。 輸出包含以&amp;字元分隔的名稱值組。 回應包含下列變數：

* `authenticated`  — 值是 `true` 或 `false`.
* `authstate`  — 此值可包含下列其中一個值：

   * `CREDENTIAL_CHALLENGE`  — 此狀態表示使用者管理員無法透過任何方法判斷使用者的身分。 為了進行驗證，需要使用者的使用者名稱和密碼。
   * `SPNEGO_CHALLENGE` — 此狀態的處理方式與 `CREDENTIAL_CHALLENGE`.
   * `COMPLETE`  — 此狀態表示使用者管理員能夠驗證使用者。
   * `FAILED`  — 此狀態表示使用者管理員無法驗證使用者。 作為對此狀態的回應，Flex使用者端可以向使用者顯示錯誤訊息。
   * `LOGGED_OUT`  — 此狀態表示使用者已成功登出。

* `assertionid`  — 如果狀態為 `COMPLETE` 然後包含使用者的 `assertionId` 值。 使用者端應用程式可取得 `AuthResult` （使用者）。

**登入程式**

POST當使用者端應用程式啟動時，您可以向 `/um/login` 安全性servlet。 例如， `https://<your_serverhost>:<your_port>/um/login?um_no_redirect=true`. 當請求到達User Manager安全性servlet時，它會執行以下步驟：

1. 它會尋找名為的Cookie `lcAuthToken`. 如果使用者已登入另一個Forms應用程式，則此Cookie會出現。 如果找到Cookie，則會驗證其內容。
1. 如果啟用以標頭為基礎的SSO，則servlet會尋找已設定的標頭以確定使用者的身分。
1. 如果已啟用SPNEGO，則servlet會嘗試啟動SPNEGO並嘗試判斷使用者的身分。

如果安全性servlet找到符合使用者的有效Token，安全性servlet可讓您繼續操作，並以回應 `authstate=COMPLETE`. 否則，安全性servlet會回應 `authstate=CREDENTIAL_CHALLENGE`. 下列清單說明這些值：

* `Case authstate=COMPLETE`：指出使用者已驗證，且 `assertionid` 值包含使用者的判斷提示識別碼。 在此階段，使用者端應用程式可以連線至AEM Forms。 為該URL設定的servlet可以取得 `AuthResult` 對於使用者，方法是叫用 `AuthenticationManager.authenticate(HttpRequestToken)` 方法。 此 `AuthResult` 執行個體可以建立使用者管理員內容，並將其儲存在工作階段中。
* `Case authstate=CREDENTIAL_CHALLENGE`：指出安全性servlet需要使用者的認證。 作為回應，使用者端應用程式可以向使用者顯示登入畫面，並將取得的認證傳送給安全性servlet (例如， `https://<your_serverhost>:<your_port>/um/login?um_no_redirect=true&j_username=administrator&j_password=password)`. 如果驗證成功，則安全性servlet會以回應 `authstate=COMPLETE`.

如果驗證仍然失敗，則安全性servlet會以回應 `authstate=FAILED`. 若要回應此值，使用者端應用程式可以顯示訊息，再次取得認證。

>[!NOTE]
>
>當 `authstate=CREDENTIAL_CHALLENGE`，建議使用者端將取得的認證以POST表單傳送至安全性servlet。

**登出程式**

當使用者端應用程式登出時，您可以傳送請求至下列URL：

`https://<your_serverhost>:<your_port>/um/logout?um_no_redirect=true`

收到此請求後，使用者管理員安全性servlet會刪除 `lcAuthToken` Cookie和回應 `authstate=LOGGED_OUT`. 使用者端應用程式收到這個值之後，應用程式就可以執行清除工作。

## 建立使用SSO驗證AEM表單使用者的使用者端應用程式 {#creating-a-client-application-that-authenticates-aem-forms-users-using-sso}

為了示範如何建立執行SSO驗證的使用者端應用程式，建立了使用者端應用程式範例。 下圖顯示使用者端應用程式使用SSO驗證使用者的步驟。

![cf_cf_flexsso](assets/cf_cf_flexsso.png)

上圖說明使用者端應用程式啟動時發生的應用程式流程。

1. 使用者端應用程式會觸發 `applicationComplete` 事件。
1. 對的呼叫 `ISSOManager.singleSignOn` 已製作。 使用者端應用程式會傳送要求給使用者管理員安全性servlet。
1. 如果安全性servlet驗證使用者，則 `ISSOManager` dispatches `SSOEvent.AUTHENTICATION_SUCCESS`. 使用者端應用程式會回應顯示首頁面。 在此範例中，首頁面會叫用名為MyApplication/EncryptDocument的AEM Forms短期程式。
1. 如果安全性servlet無法判斷使用者是否有效，則應用程式會再次要求使用者認證。 此 `ISSOManager` 類別會傳送 `SSOEvent.AUTHENTICATION_REQUIRED` 事件。 使用者端應用程式會顯示登入頁面。
1. 登入頁面中提供的憑證會傳送至 `ISSOManager.login` 方法。 如果驗證成功，則會導向步驟3。 否則 `SSOEvent.AUTHENTICATION_FAILED` 事件已觸發。 使用者端應用程式會顯示登入頁面和適當的錯誤訊息。

### 建立使用者端應用程式 {#creating-the-client-application}

使用者端應用程式包含下列檔案：

* `SSOStandalone.mxml`：代表使用者端應用程式的主要MXML檔案。 (請參閱 [建立SSOStandalone.mxml檔案](creating-flash-builder-applications-perform.md#creating-the-ssostandalone-mxml-file).)
* `um/ISSOManager.as`：公開與單一登入(SSO)相關的作業。 (請參閱 [建立ISSOManager.as檔案](creating-flash-builder-applications-perform.md#creating-the-issomanager-as-file).)
* `um/SSOEvent.as`：此 `SSOEvent` 會為SSO相關事件傳送。 (請參閱 [建立SSOEvent.as檔案](creating-flash-builder-applications-perform.md#creating-the-ssoevent-as-file).)
* `um/SSOManager.as`：管理SSO相關作業並傳送適當事件。 (請參閱 [建立SSOManager.as檔案](creating-flash-builder-applications-perform.md#creating-the-ssomanager-as-file).)
* `um/UserManager.as`：包含使用其WSDL叫用Authentication Manager服務的應用程式邏輯。 (請參閱 [建立UserManager.as檔案](creating-flash-builder-applications-perform.md#creating-the-usermanager-as-file).)
* `views/login.mxml`：代表登入畫面。 (請參閱 [建立login.mxml檔案](creating-flash-builder-applications-perform.md#creating-the-login-mxml-file).)
* `views/logout.mxml`：代表登出畫面。 (請參閱 [建立logout.mxml檔案](creating-flash-builder-applications-perform.md#creating-the-logout-mxml-file).)
* `views/progress.mxml`：代表進度檢視。 (請參閱 [建立progress.mxml檔案](creating-flash-builder-applications-perform.md#creating-the-progress-mxml-file).)
* `views/remoting.mxml`：代表使用遠端處理叫用名為MyApplication/EncryptDocument的AEM Forms短期處理序的檢視。 (請參閱 [建立remoting.mxml檔案](creating-flash-builder-applications-perform.md#creating-the-remoting-mxml-file).)

下圖提供使用者端應用程式的視覺化表示。

![cf_cf_sso_project](assets/cf_cf_sso_project.png)

>[!NOTE]
>
>請注意，有兩個名為um和views的套件。 建立使用者端應用程式時，請確定您將檔案放在適當的套件中。 此外，請確定您將adobe-remoting-provider.swc檔案新增至專案的類別路徑。 (請參閱 [包含AEM Forms Flex程式庫檔案](/help/forms/developing/invoking-aem-forms-using-remoting.md#including-the-aem-forms-flex-library-file).)

### 建立SSOStandalone.mxml檔案 {#creating-the-ssostandalone-mxml-file}

下列程式碼代表SSOStandalone.mxml檔案。

```xml
 <?xml version="1.0" encoding="utf-8"?>
 <mx:Application
                 layout="absolute"
                 applicationComplete="initApp()"
                 height="400" width="550"
                 xmlns:v="views.*"
                 backgroundColor="#EDE8F0" viewSourceURL="srcview/index.html">
     <mx:Script>
         <![CDATA[
             import mx.utils.URLUtil;
             import um.SSOEvent;
             import mx.core.UIComponent;
             import um.SSOManager;
             import mx.rpc.events.ResultEvent;
             import mx.utils.ObjectUtil;
             import mx.controls.Alert;
 
             [Bindable]
             private var _serverURL:String;
 
             private var _ssoManager:SSOManager;
 
             private var _progress:UIComponent;
 
             private var _loginPage:UIComponent;
 
             private function initApp():void{
                 _serverURL = determineServerUrl();
                 _ssoManager = new SSOManager(_serverURL);
 
                 _ssoManager.addEventListener(SSOEvent.AUTHENTICATION_FAILED,loginHandler);
                 _ssoManager.addEventListener(SSOEvent.AUTHENTICATION_SUCCESS,loginHandler);
                 _ssoManager.addEventListener(SSOEvent.AUTHENTICATION_REQUIRED,loginHandler);
                 _ssoManager.addEventListener(SSOEvent.LOGOUT_COMPLETE,loginHandler);
                 _ssoManager.addEventListener(SSOEvent.AUTHENTICATION_FAULT,loginHandler);
 
                 trace("[Main] Add the required event handlers for authentication");
                 _ssoManager.singleSignOn();
 
                 showBusy();
             }
 
             private function determineServerUrl():String
             {
                 var s:String ;
                 var appUrl:String = Application.application.url;
                 var givenUrl:String  = ExternalInterface.call("serverUrl.toString");
                 trace("[Main] Application url ["+appUrl+"] Given url ["+givenUrl+"]");
                 if(appUrl != null && appUrl.search("^http") != -1){
                     s = appUrl;
                 }
                 if(s == null){
                     s = givenUrl;
                 }
                 if(s== null){
                     s = "https://hiro-xp:8080/";
                 }
                 s = URLUtil.getFullURL(s,"/");
                 trace("[Main] Would be using ["+s+"] as serverUrl");
                 return s;
             }
 
             private function loginHandler(event:SSOEvent):void
             {
                 trace("[Main] Handling event "+event.type);
                 switch(event.type)
                 {
                     case SSOEvent.AUTHENTICATION_FAILED:
                         viewContent.selectedChild = login;
                         login.showLoginFailed();
                         break;
                     case SSOEvent.AUTHENTICATION_SUCCESS:
                         viewContent.selectedChild = remoting;
                         break;
                     case SSOEvent.AUTHENTICATION_REQUIRED:
                         viewContent.selectedChild = login;
                         break;
                     case SSOEvent.LOGOUT_COMPLETE:
                         viewContent.selectedChild = logout;
                         break;
                     case SSOEvent.AUTHENTICATION_FAULT:
                         Alert.show("Error doing authentication. Root error ["+event.rootEvent+"]","Authentication Fault",Alert.OK);
                 }
             }
 
             public function get ssoManager():SSOManager
             {
                 return _ssoManager;
             }
 
             public function showBusy():void
             {
                 viewContent.selectedChild = progress;
             }
 
             public function get serverUrl():String
             {
                 return _serverURL;
             }
 
         ]]>
     </mx:Script>
     <mx:ViewStack x="0" y="0" id="viewContent" >
         <v:login id="login" />
         <v:remoting id="remoting"  />
         <v:progress id="progress" />
         <v:logout id="logout"/>
     </mx:ViewStack>
 </mx:Application>
 
```

### 建立ISSOManager.as檔案 {#creating-the-issomanager-as-file}

下列程式碼代表ISSOManager.as檔案。

```java
 package um
 {
     import flash.events.IEventDispatcher;
 
     /**
      * The <code>ISSOManager</code> expose operations related to Single Sign On (SSO) in AEM Forms
      * environment. The application should register appropriate <code>SSOEvent</code> handlers prior
      * to calling any of the following operations
      */
     public interface ISSOManager extends IEventDispatcher
     {
         /**
          * Tries to validate whether the user has an already existing session or not (SSO Scenarios). The application
          * may call this method during the initialization. In general this call would lead to one of the
          * following events getting dispatched
          * <ul>
          * <li>SSOEvent.AUTHENTICATION_SUCCESS - If a SSO session was found and valid
          * <li>SSOEvent.AUTHENTICATION_REQUIRED - No SSO session was found and as such authentication is required in
          * the form of username and password.
          * <li>SSOEvent.AUTHENTICATION_FAULT - Some error has occured while connecting to the server
          * </ul>
          */
         function singleSignOn():void;
 
         /**
          * Authenticates the user using username and password. It may lead to one of the following events
          * <ul>
          * <li>SSOEvent.AUTHENTICATION_SUCCESS - The authentication is successful and a session is established
          * <li>SSOEvent.AUTHENTICATION_FAILED - Authentication has failed
          * </ul>
          */
         function login(username:String, password:String):void;
 
         /**
          * Terminates the current session and logs out the user.
          */
         function logout():void;
 
         /**
          * Get the assertionId for the logged in user
          */
         function get assertionId():String;
     }
 }
```

### 建立SSOEvent.as檔案 {#creating-the-ssoevent-as-file}

下列程式碼代表SSOEvent.as檔案。

```java
 package um
 {
     import flash.events.Event;
 
     /**
      * The <code>SSOEvent</code> is dispatched for SSO related events
      */
     public class SSOEvent extends Event
     {
         /**
          * This type of event would be dispatched when the Authentication process is successful. Authentication
          * might have been done with SSO or username and password. As a response to this event the application
          * can show the welcome page to the user
          * The application may want to perform specific check for permission/role so as to verify the user is allowed.
          * So as a response to this event the application would do those checks and then only show the welcome page
          */
         public static const AUTHENTICATION_SUCCESS:String = "authenticationSuccess";
 
         /**
          * This type of event would be dispatched when authentication fails using the username, password.
          * As a response to this type of event an application can show an error message to the user.
          * This event would only happen when authentication is done using username and password and NOT in
          * SSO case.
          */
         public static const AUTHENTICATION_FAILED:String = "authenticationFailed";
 
         /**
          * This type of event would be dispatched when authentication using SSO is not achieved. And due to
          * that we require the user's username and password for authentication. As a response to this event
          * the application can show the login page to the user.
          */
         public static const AUTHENTICATION_REQUIRED:String = "authenticationRequired";
 
         /**
          * This type of event would be dispatched when logout is complete. As a response to this event the
          * application may show a logout page informing the user that he has been logged out. Or the application
          * can take the user back to login page
          */
         public static const LOGOUT_COMPLETE:String = "logoutComplete";
 
         /**
          * This type of event would be dispatched when ever there is a problem in doing Authentication. The root cause
          * can be obtained from the <code>rootEvent</code>.
          */
         public static const AUTHENTICATION_FAULT:String = "authenticationFault";
 
         private var _rootEvent:Event;
 
         public function SSOEvent(type:String, rootEvent:Event=null)
         {
             super(type,true,false);
             _rootEvent = rootEvent;
         }
 
         /**
          * The root event. If current event type is <code>AUTHENTICATION_FAULT</code> then it would be an
          * <code>IOErrorEvent</code> in other cases it would be complete event. Its basic use is to extract the root
          * cause in case of an authentication fault.
          */
         public function get rootEvent():Event
         {
             return _rootEvent;
         }
     }
 }
```

### 建立SSOManager.as檔案 {#creating-the-ssomanager-as-file}

下列程式碼代表SSOManager.as檔案。

```java
 package um
 {
     import flash.events.Event;
     import flash.events.EventDispatcher;
     import flash.events.IOErrorEvent;
     import flash.external.ExternalInterface;
     import flash.net.URLLoader;
     import flash.net.URLLoaderDataFormat;
     import flash.net.URLRequest;
     import flash.net.URLVariables;
 
     import mx.utils.ObjectUtil;
 
     /**
      * Manages the SSO related operations and dispatches appropriate events. It would connect to the UM Filter/Servlet
      * at <code>um/login</code> The UM response would be of form of url encoded variables. It would look for
      * <code>authstate</code> value in the response and depending on that it would proceed.
      *
      * <p>If there is an IO_Error while initial attempt to UM then it would assume it as a 401 response. And it would
      * be assumed that SPNEGO based authenticatin is not working and therefore user would be shown a login page.
      */
     public class SSOManager extends EventDispatcher implements ISSOManager
     {
         private static const SSO_URL:String = "um/login";
         private static const SSO_LOGOUT_URL:String = "um/logout";
         private static const AUTH_COOKIE_NAME:String = "lcAuthToken";
 
         private var _serverUrl:String;
         private var _assertionId:String;
 
         /**
          * Constructs an SSOManager with the given server url.
          *
          * @param serverUrl - The uri of the server to connect to. it must be without any context path e.g
          * http://localhost:8080/. The SSOManager would directly append the path of UM exposed SSO url to it
          * for its operations
          */
         public function SSOManager(serverUrl:String)
         {
             _serverUrl = serverUrl;
         }
 
         public function singleSignOn():void
         {
             sendRequest(SSO_URL,true);
         }
 
         public function login(username:String, password:String):void
         {
             sendRequest(SSO_URL,false,
                 function(request:URLRequest,vars:URLVariables):void
                 {
                     vars.j_username = username;
                     vars.j_password = password;
                 }
             );
         }
 
         public function logout():void
         {
             sendRequest(SSO_LOGOUT_URL);
         }
 
         public function get assertionId():String
         {
             return _assertionId;
         }
 
 
 
         /**
          * Connects to the UM security service.
          */
         private function sendRequest(relativeUrl:String,authenticationRequest:Boolean=false, requestProcessor:Function=null):void
         {
             var loader:URLLoader = new URLLoader();
             loader.dataFormat = URLLoaderDataFormat.VARIABLES;
             var request:URLRequest = new URLRequest(_serverUrl + relativeUrl);
             trace("[SSOmanager] Contacting ["+request.url+"]");
             var vars:URLVariables = new URLVariables();
             vars.um_no_redirect = "true";
             request.data = vars;
             if(requestProcessor != null){
                 requestProcessor(request,vars);
             }
 
             loader.addEventListener(Event.COMPLETE,authHandler);
             //if its an authentication request then only treat io error as a possible 401
             //for others treat them as faults
             if(authenticationRequest){
                 loader.addEventListener(IOErrorEvent.IO_ERROR,httpAuthenticationHandler);
             }else{
                 loader.addEventListener(IOErrorEvent.IO_ERROR,authFaultHandler);
             }
             trace("[SSOmanager] Sending request "+ ObjectUtil.toString(request));
             loader.load(request);
         }
 
         private function authHandler(event:Event):void
         {
             var loader:URLLoader = URLLoader(event.target);
             var response:URLVariables = URLVariables(loader.data);
             trace("[SSOmanager] Processing response ["+ObjectUtil.toString(response)+"]");
             handleAuthResult(response["authstate"],response);
         }
 
         /**
          * Handles the IOErrorEvent. Flash would dispatch IOEvent in response to HTTP 401.
          * There is no way to distinguish it from the genuine IOError.
          */
         private function httpAuthenticationHandler(event:IOErrorEvent):void
         {
             trace("[SSOmanager] Processing IOErrorEvent ["+ObjectUtil.toString(event)+"]");
             handleAuthResult("CREDENTIAL_CHALLENGE");
 
         }
 
         /**
          * Dispatches appropriate <code>SSOEvent</code> on the basis of the <code>authstate</code>
          * value of the response.
          * The response is url encoded in for of
          * <pre>
          * authenticated=false&authstate=SPNEGO_CHALLENGE
          * </pre>
          * Depending on <code>authstate</code> the SSOEvent is dispatched
          */
         private function handleAuthResult(authState:String,response:URLVariables = null):void
         {
             trace("[SSOmanager] processing state "+authState);
             switch(authState)
             {
                 case "FAILED"  :
                     dispatchEvent(new SSOEvent(SSOEvent.AUTHENTICATION_FAILED));
                     break;
                 case "COMPLETE" :
                     _assertionId = response ? response["assertionid"] : null;
                     dispatchEvent(new SSOEvent(SSOEvent.AUTHENTICATION_SUCCESS));
                     break;
                 case "CREDENTIAL_CHALLENGE" :
                     dispatchEvent(new SSOEvent(SSOEvent.AUTHENTICATION_REQUIRED));
                     break;
                 case "LOGGED_OUT" :
                     dispatchEvent(new SSOEvent(SSOEvent.LOGOUT_COMPLETE));
                     break;
                 default:
                     dispatchEvent(new SSOEvent(SSOEvent.AUTHENTICATION_REQUIRED));
                     break;
             }
         }
 
         private function authFaultHandler(event:Event):void
         {
             dispatchEvent(new SSOEvent(SSOEvent.AUTHENTICATION_FAULT,event));
         }
 
     }
 }
```

### 建立UserManager.as檔案 {#creating-the-usermanager-as-file}

下列程式碼代表UserManager.as檔案。

```java
 package um
 {
     import flash.events.Event;
     import mx.rpc.soap.WebService;
     import mx.rpc.soap.Operation;
     import mx.rpc.IResponder;
     import mx.rpc.events.FaultEvent;
     import mx.rpc.events.ResultEvent;
     import mx.rpc.soap.LoadEvent;
 
     public class UserManager
     {
         private var _ssoManager:ISSOManager;
         private var _serverUrl:String;
 
         public function UserManager(ssoManager:ISSOManager,serverUrl:String)
         {
             _serverUrl = serverUrl;
             _ssoManager = ssoManager;
         }
 
         public function retrieveAssertion(responder:IResponder):String
         {
             var assertionId:String = _ssoManager.assertionId;
             if(!assertionId)
             {
                 trace("[UserManager] AssertionId not found");
                 return null;
             }
 
             var ws:WebService = new WebService();
             var wsdl:String = _serverUrl+'soap/services/AuthenticationManagerService?wsdl&lc_version=8.2.1';
             ws.loadWSDL(wsdl);
             ws.addEventListener(LoadEvent.LOAD,
                 function(event:Event):void
                 {
                     trace("[UserManager] WSDL loaded");
                     var authenticate:Operation = ws.authenticateWithHttpToken as Operation;
                     authenticate.resultFormat = "e4x";
                     authenticate.addEventListener(ResultEvent.RESULT,
                         function(event:Event):void
                         {
                             responder.result(event);
                         }
                     );
                     authenticate.send({assertionId:assertionId});
                 }
             );
 
             ws.addEventListener(FaultEvent.FAULT,
                 function(event:Event):void
                 {
                     responder.fault(event);
                 }
             );
             return null;
         }
     }
 }
```

### 建立login.mxml檔案 {#creating-the-login-mxml-file}

下列程式碼代表login.mxml檔案。

```xml
 <?xml version="1.0" encoding="utf-8"?>
 <mx:Canvas  width="500" height="400">
     <mx:Script>
         <![CDATA[
             import mx.core.Application;
             public function showLoginFailed():void
             {
                 loginMessage.text = "Username or Password incorrect";
             }
 
             private function doLogin():void
             {
                 Application.application.ssoManager.login(j_username.text,j_password.text);
                 Application.application.showBusy();
             }
 
         ]]>
     </mx:Script>
 
     <mx:VBox height="113" width="244" x="128" y="144" horizontalAlign="center" verticalGap="10">
         <mx:HBox width="100%">
             <mx:HBox width="100%" verticalAlign="middle" horizontalAlign="center" height="32">
                 <mx:Label text="Username" fontWeight="bold"/>
                 <mx:TextInput id="j_username"/>
             </mx:HBox>
         </mx:HBox>
         <mx:HBox width="100%" height="33" horizontalAlign="center" horizontalGap="10" verticalAlign="middle">
             <mx:Label text="Password" fontWeight="bold"/>
             <mx:TextInput displayAsPassword="true" id="j_password"/>
         </mx:HBox>
         <mx:Button label="Login" click="doLogin()"/>
     </mx:VBox>
     <mx:Text x="128" y="122" id="loginMessage" width="230" height="14"/>
     <mx:Label x="154" y="65" text="AEM Forms SSO Demo" fontFamily="Georgia" fontSize="20" color="#0A0A0A"/>
 </mx:Canvas>
 
```

### 建立logout.mxml檔案 {#creating-the-logout-mxml-file}

下列程式碼代表logout.mxml檔案。

```xml
 <?xml version="1.0" encoding="utf-8"?>
 <mx:Canvas  width="500" height="400">
     <mx:Label x="97" y="188" text="You have successfully logged out from the application"/>
 
 </mx:Canvas>
 
```

### 建立progress.mxml檔案 {#creating-the-progress-mxml-file}

下列程式碼代表progress.mxml檔案。

```xml
 <?xml version="1.0" encoding="utf-8"?>
 <mx:Canvas >
     <mx:Label x="151" y="141" text="Wait...."/>
     <mx:SWFLoader source="LoadingCircle.swf" width="50" height="50" horizontalCenter="0" verticalCenter="0"/>
 </mx:Canvas>
```

### 建立remoting.mxml檔案 {#creating-the-remoting-mxml-file}

下列程式碼代表叫用 `MyApplication/EncryptDocument` 程式。 由於檔案會傳遞至程式，因此負責將安全檔案傳遞至AEM Forms的應用程式邏輯會位於此檔案中。 (請參閱 [傳遞安全檔案以使用遠端處理來叫用程式](/help/forms/developing/invoking-aem-forms-using-remoting.md#passing-secure-documents-to-invoke-processes-using-remoting).)

```xml
 <?xml version="1.0" encoding="utf-8"?>
 <mx:Canvas  width="664" height="400" creationComplete="initializeChannelSet()" xmlns:views="views.*">
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
             import um.UserManager;
             import mx.rpc.events.ResultEvent;
             import mx.rpc.events.FaultEvent;
             import mx.core.Application;
             import mx.rpc.Responder;
             import mx.utils.ObjectUtil;
 
             // Classes used in file retrieval
             private var fileRef:FileReference = new FileReference();
             private var docRef:DocumentReference = new DocumentReference();
             private var parentResourcePath:String = "/";
             //private var serverPort:String = "'[server]:[port]'";
             private var serverPort:String = "'[server]:[port]'";
             private var now1:Date;
             private var userManager:UserManager;
 
             // Define a ChannelSet object.
             public var cs:ChannelSet;
 
             // Holds information returned from AEM Forms
             [Bindable]
             public var progressList:ArrayCollection = new ArrayCollection();
 
 
             // Set up channel set to invoke AEM Forms.
             // This must be done before calling any service or process, but only
             // once for the entire application.
             private function initializeChannelSet():void {
                 cs = new ChannelSet();
                 cs.addChannel(new AMFChannel("remoting-amf", "https://" + serverPort + "/remoting/messagebroker/amf"));
                 EncryptDocument.channelSet = cs;
 
             //Get the user that is authenticated
             userManager = new UserManager(Application.application.ssoManager,Application.application.serverUrl);
             userManager.retrieveAssertion(
                     new mx.rpc.Responder(
                         function(event:ResultEvent):void
                         {
                             var name:String = XML(event.currentTarget.lastResult)..*::authenticatedUser.*::userid.text();
                             username.text = "Welcome "+name;
                         },
                         function(event:FaultEvent):void
                         {
                             mx.controls.Alert.show(event.fault.faultString,'Error')
                         }
                     )
                 );
 
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
 
                 // Set the docRefs url and referenceType parameters
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
                 token = EncryptDocument.invoke(params);
                 token.name = name;
             }
 
 
             // This method handles a successful conversion invocation
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
 
 
             private function resultHandler(event:ResultEvent):void {
             // Do anything else here.
 
             }
 
             private function logout():void
             {
                 Application.application.ssoManager.logout();
                 Application.application.showBusy();
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
                   id="username"/>
 
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
     <mx:Button label="Select File" click="uploadFile()" />
     <mx:Button label="Logout"  click="logout()" />
     </mx:Panel>
 </mx:Canvas>
 
 
```

### 附加信息 {#additional-information}

以下段落提供其他詳細資訊，說明使用者端應用程式和「使用者管理員」安全性servlet之間的通訊。

### 發生新驗證 {#a-new-authentication-occurs}

在此情況下，使用者會首次嘗試從使用者端應用程式登入AEM Forms。 （與使用者相關的先前工作階段不存在。） 在 `applicationComplete` 事件， `SSOManager.singleSignOn` 叫用方法以傳送要求給使用者管理員。

`GET /um/login?um%5Fno%5Fredirect=true HTTP/1.1`

User Manager安全性servlet會提供下列值當作回應：

`HTTP/1.1 200 OK`

`authenticated=false&authstate=CREDENTIAL_CHALLENGE`

對於此值的回應， `SSOEvent.AUTHENTICATION_REQUIRED` 值已傳送。 因此，使用者端應用程式會向使用者顯示登入畫面。 認證會提交回使用者管理員安全性servlet。

`GET /um/login?um%5Fno%5Fredirect=true&j%5Fusername=administrator&j%5Fpassword=password HTTP/1.1`

User Manager安全性servlet會提供下列值當作回應：

```verilog
 HTTP/1.1 200 OK
 Set-Cookie: lcAuthToken=53630BC8-F6D4-F588-5D5B-4668EFB2EC7A; Path=/
 authenticated=true&authstate=COMPLETE&assertionid=53630BC8-F6D4-F588-5D5B-4668EFB2EC7A
```

因此， `authstate=COMPLETE the SSOEvent.AUTHENTICATION_SUCCESS` 「 」已傳送。 必要時，使用者端應用程式可執行進一步處理。 例如，可以建立追蹤使用者已驗證日期和時間的記錄。

### 使用者已驗證 {#the-user-is-already-authenticated}

在此情況下，使用者已登入AEM Forms，然後導覽至使用者端應用程式。 使用者端應用程式會在啟動期間連線到User Manager安全性servlet。

```verilog
 GET /um/login?um%5Fno%5Fredirect=true HTTP/1.1
 Cookie: JSESSIONID=A4E0BCC2DD4BCCD3167C45FA350BD72A; lcAuthToken=53630BC8-F6D4-F588-5D5B-4668EFB2EC7A
```

由於使用者已經過驗證，因此使用者管理員Cookie會出現，並傳送至使用者管理員安全性servlet。 然後servlet取得 `assertionId` 值並驗證其是否有效。 如果有效，則 `authstate=COMPLETE` 會傳回。 否則 `authstate=CREDENTIAL_CHALLENGE` 會傳回。 以下是典型的回應：

```verilog
 HTTP/1.1 200 OK
        authenticated=true&authstate=COMPLETE&assertionid=53630BC8-F6D4-F588-5D5B-4668EFB2EC7A
```

在此情況下，使用者不會看到登入畫面，而是直接進入歡迎畫面。
