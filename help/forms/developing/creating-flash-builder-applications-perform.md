---
title: 创建使用HTTP令牌执行SSO身份验证的Flash Builder应用程序
seo-title: 创建使用HTTP令牌执行SSO身份验证的Flash Builder应用程序
description: 'null'
seo-description: 'null'
uuid: 273db00a-a665-4e52-88fa-4fca06d05f8c
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: coding
discoiquuid: 0ff30df7-b3ad-4c34-9644-87c689acc294
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '1761'
ht-degree: 0%

---


# 创建使用HTTP令牌{#creating-flash-builder-applicationsthat-perform-sso-authentication-using-http-tokens}执行SSO身份验证的Flash Builder应用程序

您可以使用Flash Builder创建客户端应用程序，该应用程序使用HTTP令牌执行单点登录(SSO)身份验证。 例如，假定您使用Flash Builder创建基于Web的应用程序。 接下来假设应用程序包含不同的视图，其中每个视图调用不同的AEM Forms操作。 您可以创建一个登录页面，让用户进行一次身份验证，而不是对每个Forms操作的用户进行身份验证。 一旦通过身份验证，用户就能够调用多个操作而无需再次进行身份验证。 例如，如果用户已登录Workspace(或另一个Forms应用程序)，则用户无需再次进行身份验证。

尽管客户端应用程序包含执行SSO身份验证所需的应用程序逻辑，AEM forms用户管理仍执行实际的用户身份验证。 要使用HTTP令牌对用户进行身份验证，客户端应用程序将调用Authentication Manager服务的`authenticateWithHTTPToken`操作。 用户管理可以使用HTTP令牌验证用户身份。 对于随后对AEM Forms的远程处理或Web服务调用，您无需传递身份验证凭据。

>[!NOTE]
>
>在阅读本节之前，建议您熟悉使用远程处理调用AEM Forms。 (请参阅[使用AEM Forms·雷莫廷调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-remoting.md#invoking-aem-forms-using-remoting)。)

使用SSO验证用户后，将调用以下名为`MyApplication/EncryptDocument`的AEM Forms短时进程。 （有关此进程的信息，如其输入值和输出值，请参见[短时进程示例](/help/forms/developing/aem-forms-processes.md)。）

![cf_cf_encryptdocumentprocess2](assets/cf_cf_encryptdocumentprocess2.png)

>[!NOTE]
>
>这一进程不是基于AEM Forms现有进程。 要跟随讨论如何调用此进程的代码示例，请使用Workbench创建一个名为`MyApplication/EncryptDocument`的进程。 （请参阅[使用Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63)。）

使用Flash Builder构建的客户端应用程序与在`/um/login`和`/um/logout`配置的用户管理器安全servlet进行交互。 即，客户端应用程序在启动过程中向`/um/login` URL发送请求，以确定用户的状态。 然后，用户管理器将用户状态做出响应。 客户端应用程序和用户管理器安全servlet使用HTTP进行通信。

**请求格式**

安全servlet需要以下输入变量：

* `um_no_redirect` -此值必须为 `true`。此变量随User Manager安全servlet发出的所有请求一起提供。 它还帮助安全servlet区分来自flex客户端或其他Web应用程序的传入请求。
* `j_username` -此值是登录表单中提供的用户的登录标识符值。
* `j_password` -此值是登录表单中提供的用户的相应口令。

`j_password`值仅对凭据请求是必需的。 如果未指定密码值，则安全servlet将检查确定您使用的帐户是否已通过身份验证。 如果是，您可以继续；但是，安全servlet不会再次验证您的身份。

>[!NOTE]
>
>要正确处理i18n，请确保这些值采用POST形式。

**响应格式**

在`/um/login`配置的安全servlet使用`URLVariables`格式做出响应。 在此格式中，内容类型的输出为text/plain。 输出包含由和号(&amp;)字符分隔的名称值对。 响应包含以下变量：

* `authenticated` -值为 `true` 或 `false`。
* `authstate` -此值可以包含以下值之一：

   * `CREDENTIAL_CHALLENGE` -此状态表示用户管理者无法通过任何方式确定用户的身份。要进行身份验证，需要用户的用户名和密码。
   * `SPNEGO_CHALLENGE`-此状态被视为相同 `CREDENTIAL_CHALLENGE`。
   * `COMPLETE` -此状态表示用户管理器能够验证用户身份。
   * `FAILED` -此状态表示用户管理器无法对用户进行身份验证。作为对此状态的响应，flex客户端可以向用户显示错误消息。
   * `LOGGED_OUT` -此状态表示用户已成功注销。

* `assertionid` -如果状态为， `COMPLETE` 则它包含用户的 `assertionId` 值。客户端应用程序可以获取用户的`AuthResult`。

**登录过程**

当客户端应用程序开始时，您可以向`/um/login`安全servlet发出POST请求。 例如，`https://<your_serverhost>:<your_port>/um/login?um_no_redirect=true`。 当请求到达User Manager安全servlet时，它执行以下步骤：

1. 它查找名为`lcAuthToken`的cookie。 如果用户已登录到另一个Forms应用程序，则此cookie存在。 如果找到Cookie，则验证其内容。
1. 如果启用了基于Header的SSO，则Servlet会查找已配置的标头以确定用户的标识。
1. 如果启用了SPNEGO，则servlet将尝试启动SPNEGO并尝试确定用户的标识。

如果安全servlet找到与用户匹配的有效令牌，则安全servlet允许您继续并使用`authstate=COMPLETE`做出响应。 否则，安全servlet将用`authstate=CREDENTIAL_CHALLENGE`做出响应。 以下列表解释这些值：

* `Case authstate=COMPLETE`:指示用户已通过身份验证， `assertionid` 且值包含用户的断言标识符。在此阶段，客户端应用程序可以连接到AEM Forms。 为该URL配置的Servlet可以通过调用`AuthenticationManager.authenticate(HttpRequestToken)`方法获得用户的`AuthResult`。 `AuthResult`实例可以创建用户管理器上下文并将其存储在会话中。
* `Case authstate=CREDENTIAL_CHALLENGE`:指示安全servlet需要用户的凭据。作为响应，客户端应用程序可以向用户显示登录屏幕，并将获得的凭据发送到安全servlet（例如`https://<your_serverhost>:<your_port>/um/login?um_no_redirect=true&j_username=administrator&j_password=password)`）。 如果身份验证成功，则安全servlet将用`authstate=COMPLETE`做出响应。

如果身份验证仍不成功，则安全servlet将用`authstate=FAILED`做出响应。 为响应此值，客户端应用程序可显示一条消息以再次获取凭据。

>[!NOTE]
>
>当`authstate=CREDENTIAL_CHALLENGE`时，建议客户端以POST形式将获取的凭据发送到安全servlet。

**注销过程**

当客户端应用程序注销时，您可以向以下URL发送请求：

`https://<your_serverhost>:<your_port>/um/logout?um_no_redirect=true`

收到此请求后，User Manager安全servlet将删除`lcAuthToken` cookie，并以`authstate=LOGGED_OUT`做出响应。 客户端应用程序收到此值后，该应用程序可以执行清除任务。

## 创建一个客户端应用程序，它使用SSO {#creating-a-client-application-that-authenticates-aem-forms-users-using-sso}验证AEM表单用户

要演示如何创建执行SSO身份验证的客户端应用程序，将创建一个示例客户端应用程序。 下图显示了客户端应用程序使用SSO验证用户身份时执行的步骤。

![cf_cf_flexsso](assets/cf_cf_flexsso.png)

上图描述了在客户端应用程序开始时发生的应用程序流。

1. 客户端应用程序触发`applicationComplete`事件。
1. 将调用`ISSOManager.singleSignOn`。 客户端应用程序向用户管理器安全servlet发送请求。
1. 如果安全servlet对用户进行身份验证，则`ISSOManager`将调度`SSOEvent.AUTHENTICATION_SUCCESS`。 作为响应，客户端应用程序显示主页。 在此示例中，主页调用名为MyApplication/EncryptDocument的AEM Forms短时进程。
1. 如果安全servlet无法确定用户是否有效，则应用程序将再次请求用户凭据。 `ISSOManager`类调度`SSOEvent.AUTHENTICATION_REQUIRED`事件。 客户端应用程序显示登录页面。
1. 登录页面中提供的凭据将发送到`ISSOManager.login`方法。 如果身份验证成功，则会导致步骤3。 否则，将触发`SSOEvent.AUTHENTICATION_FAILED`事件。 客户端应用程序显示登录页面和相应的错误消息。

### 创建客户端应用程序{#creating-the-client-application}

客户端应用程序由以下文件组成：

* `SSOStandalone.mxml`:表示客户端应用程序的主MXML文件。（请参阅[创建SSOStandalone.mxml文件](creating-flash-builder-applications-perform.md#creating-the-ssostandalone-mxml-file)。）
* `um/ISSOManager.as`:公开与单点登录(SSO)相关的操作。（请参阅[创建ISSOManager.as文件](creating-flash-builder-applications-perform.md#creating-the-issomanager-as-file)。）
* `um/SSOEvent.as`:将 `SSOEvent` 为SSO相关事件分派。（请参阅[创建SSOEvent.as文件](creating-flash-builder-applications-perform.md#creating-the-ssoevent-as-file)。）
* `um/SSOManager.as`:管理与SSO相关的操作并分派适当的事件。（请参阅[创建SSOManager.as文件](creating-flash-builder-applications-perform.md#creating-the-ssomanager-as-file)。）
* `um/UserManager.as`:包含使用WSDL调用身份验证管理器服务的应用程序逻辑。（请参阅[创建UserManager.as文件](creating-flash-builder-applications-perform.md#creating-the-usermanager-as-file)。）
* `views/login.mxml`:表示登录屏幕。（请参阅[创建login.mxml文件](creating-flash-builder-applications-perform.md#creating-the-login-mxml-file)。）
* `views/logout.mxml`:表示注销屏幕。（请参阅[创建logout.mxml文件](creating-flash-builder-applications-perform.md#creating-the-logout-mxml-file)。）
* `views/progress.mxml`:表示进度视图。（请参阅[创建progress.mxml文件](creating-flash-builder-applications-perform.md#creating-the-progress-mxml-file)。）
* `views/remoting.mxml`:表示使用远程处理调用名为MyApplication/EncryptDocument的AEM Forms短时进程的视图。（请参阅[创建remoting.mxml文件](creating-flash-builder-applications-perform.md#creating-the-remoting-mxml-file)。）

下图提供了客户端应用程序的可视表示。

![cf_cf_sso_project](assets/cf_cf_sso_project.png)

>[!NOTE]
>
>请注意，有两个名为um和视图的包。 创建客户端应用程序时，请确保将文件放在其正确的包中。 另外，请确保将adobe-remoting-provider.swc文件添加到项目的类路径中。 (请参阅[包括AEM FormsFlex库文件](/help/forms/developing/invoking-aem-forms-using-remoting.md#including-the-aem-forms-flex-library-file)。)

### 创建SSOStandalone.mxml文件{#creating-the-ssostandalone-mxml-file}

以下代码表示SSOStandalone.mxml文件。

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

### 创建ISSOManager.as文件{#creating-the-issomanager-as-file}

以下代码表示ISSOManager.as文件。

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

### 创建SSOEvent.as文件{#creating-the-ssoevent-as-file}

以下代码表示SSOEvent.as文件。

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

### 创建SSOManager.as文件{#creating-the-ssomanager-as-file}

以下代码表示SSOManager.as文件。

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

### 创建UserManager.as文件{#creating-the-usermanager-as-file}

以下代码表示UserManager.as文件。

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

### 创建login.mxml文件{#creating-the-login-mxml-file}

以下代码表示login.mxml文件。

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

### 创建logout.mxml文件{#creating-the-logout-mxml-file}

以下代码表示logout.mxml文件。

```xml
 <?xml version="1.0" encoding="utf-8"?>
 <mx:Canvas  width="500" height="400">
     <mx:Label x="97" y="188" text="You have successfully logged out from the application"/>
 
 </mx:Canvas>
 
```

### 创建progress.mxml文件{#creating-the-progress-mxml-file}

以下代码表示progress.mxml文件。

```xml
 <?xml version="1.0" encoding="utf-8"?>
 <mx:Canvas >
     <mx:Label x="151" y="141" text="Wait...."/>
     <mx:SWFLoader source="LoadingCircle.swf" width="50" height="50" horizontalCenter="0" verticalCenter="0"/>
 </mx:Canvas>
```

### 创建remoting.mxml文件{#creating-the-remoting-mxml-file}

以下代码表示调用`MyApplication/EncryptDocument`进程的remoting.mxml文件。 由于文档被传递到该进程，因此负责将安全文档传递到AEM Forms的应用程序逻辑位于该文件中。 (请参阅[使用Remoting](/help/forms/developing/invoking-aem-forms-using-remoting.md#passing-secure-documents-to-invoke-processes-using-remoting)传递安全文档以调用进程。)

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

以下各节提供了更多详细信息，用于描述客户端应用程序与用户管理器安全servlet之间的通信。

### 发生新身份验证{#a-new-authentication-occurs}

在这种情况下，用户首次尝试从客户端应用程序登录到AEM Forms。 （不存在与用户相关的以前会话。） 在`applicationComplete`事件中，将调用`SSOManager.singleSignOn`方法，向用户管理器发送请求。

`GET /um/login?um%5Fno%5Fredirect=true HTTP/1.1`

User Manager安全servlet用以下值做出响应：

`HTTP/1.1 200 OK`

`authenticated=false&authstate=CREDENTIAL_CHALLENGE`

作为对此值的响应，将调度`SSOEvent.AUTHENTICATION_REQUIRED`值。 结果，客户端应用程序显示用户的登录屏幕。 凭据将提交回User Manager安全servlet。

`GET /um/login?um%5Fno%5Fredirect=true&j%5Fusername=administrator&j%5Fpassword=password HTTP/1.1`

User Manager安全servlet用以下值做出响应：

```verilog
 HTTP/1.1 200 OK
 Set-Cookie: lcAuthToken=53630BC8-F6D4-F588-5D5B-4668EFB2EC7A; Path=/
 authenticated=true&authstate=COMPLETE&assertionid=53630BC8-F6D4-F588-5D5B-4668EFB2EC7A
```

因此，调度`authstate=COMPLETE the SSOEvent.AUTHENTICATION_SUCCESS`。 如果需要，客户端应用程序可以执行进一步处理。 例如，可以创建跟踪用户通过身份验证的日期和时间的日志。

### 用户已通过身份验证{#the-user-is-already-authenticated}

在这种情况下，用户已登录AEM Forms，然后导航到客户端应用程序。 在启动过程中，客户端应用程序连接到User Manager安全servlet。

```verilog
 GET /um/login?um%5Fno%5Fredirect=true HTTP/1.1
 Cookie: JSESSIONID=A4E0BCC2DD4BCCD3167C45FA350BD72A; lcAuthToken=53630BC8-F6D4-F588-5D5B-4668EFB2EC7A
```

由于用户已通过身份验证，因此User Manager Cookie存在并被发送到User Manager安全Servlet。 然后，servlet获取`assertionId`值并验证其是否有效。 如果有效，则返回`authstate=COMPLETE`。 否则，返回`authstate=CREDENTIAL_CHALLENGE`。 以下是典型响应：

```verilog
 HTTP/1.1 200 OK
        authenticated=true&authstate=COMPLETE&assertionid=53630BC8-F6D4-F588-5D5B-4668EFB2EC7A
```

在这种情况下，用户不会显示登录屏幕，而是直接转到欢迎屏幕。
