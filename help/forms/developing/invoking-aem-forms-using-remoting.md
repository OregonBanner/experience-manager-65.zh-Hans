---
title: 使用远程调用AEM Forms
seo-title: Invoking AEM Forms using Remoting
description: 使用远程调用AEM Forms进程以调用在Workbench中创建的进程。 您可以从使用Flex构建的客户端应用程序中调用AEM Forms进程。
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

# 使用远程调用AEM Forms {#invoking-aem-forms-using-remoting}

**本文档中的示例和示例仅适用于JEE环境中的AEM Forms。**

在Workbench中创建的进程可以使用远程调用来调用。 也就是说，您可以从使用Flex构建的客户端应用程序中调用AEM Forms进程。 此功能基于数据服务。

>[!NOTE]
>
>使用远程处理时，建议您调用在Workbench中创建的进程，而不是AEM Forms服务。 但是，可以直接调用AEM Forms服务。 (请参阅位于AEM Forms开发人员中心的使用远程处理加密PDF文档。)

>[!NOTE]
>
>如果AEM Forms服务未配置为允许匿名访问，则来自Flex客户端的请求会导致Web浏览器出现问题。 用户必须输入用户名和密码凭据。

以下AEM Forms短暂的过程，已命名 `MyApplication/EncryptDocument`，可以使用远程调用。 (有关此流程的信息（如其输入和输出值），请参阅 [短暂的流程示例](/help/forms/developing/aem-forms-processes.md).)

![iu_iu_encryptdocumentprocess2](assets/iu_iu_encryptdocumentprocess2.png)

>[!NOTE]
>
>要使用Flex应用程序调用AEM Forms进程，请确保已启用远程处理端点。 默认情况下，在部署进程时会启用远程处理端点。

调用此过程时，会执行以下操作：

1. 获取作为输入值传递的不安全PDF文档。 此操作基于 `SetValue` 操作。 输入参数的名称为 `inDoc` 其数据类型为 `document`. ( `document` 数据类型是Workbench中的可用数据类型。)
1. 使用密码加密PDF文档。 此操作基于 `PasswordEncryptPDF` 操作。 此进程的输出值的名称为 `outDoc` 和表示密码加密的PDF文档。 outDoc的数据类型为 `document`.
1. 将密码加密的PDF文档作为PDF文件保存到本地文件系统。 此操作基于 `WriteDocument` 操作。

>[!NOTE]
>
>的 `MyApplication/EncryptDocument` 进程不基于现有的AEM Forms进程。 要遵循代码示例，请创建一个名为 `MyApplication/EncryptDocument` 使用Workbench。

>[!NOTE]
>
>有关使用远程调用长生命周期进程的信息，请参阅 [调用以人为中心的长寿过程](/help/forms/developing/invoking-human-centric-long-lived.md#invoking-human-centric-long-lived-processes).

**另请参阅**

[包含AEM Forms Flex库文件](invoking-aem-forms-using-remoting.md#including-the-aem-forms-flex-library-file)

[处理文档时使用(AEM表单已弃用)AEM Forms Remoting](invoking-aem-forms-using-remoting.md#handling-documents-with-remoting)

[通过使用(AEM表单已弃用)AEM Forms Remoting传递不安全的文档来调用短暂的进程](invoking-aem-forms-using-remoting.md#invoking-a-short-lived-process-by-passing-an-unsecure-document-using-remoting)

[验证使用Flex构建的客户端应用程序](invoking-aem-forms-using-remoting.md#authenticating-client-applications-built-with-flex)

[使用远程处理传递安全文档以调用进程](invoking-aem-forms-using-remoting.md#passing-secure-documents-to-invoke-processes-using-remoting)

[使用远程调用自定义组件服务](invoking-aem-forms-using-remoting.md#invoking-custom-component-services-using-remoting)

[创建使用Flex构建的客户端应用程序，该应用程序会调用以人为中心的长寿过程](/help/forms/developing/invoking-human-centric-long-lived.md#creating-a-client-application-built-with-flex-that-invokes-a-human-centric-long-lived-process)

[创建使用HTTP令牌执行SSO身份验证的Flash Builder应用程序](/help/forms/developing/creating-flash-builder-applications-perform.md#creating-flash-builder-applications-that-perform-sso-authentication-using-http-tokens)

<!-- For information on how to display process data in a Flex graph control, see [Displaying AEM Forms process data in Flex graphs](https://www.adobe.com/devnet/livecycle/articles/populating_flexcontrols.html). This URL is 404. No suitable replacement URL was found after a search. Do not make this link live if it is dead! -->

>[!NOTE]
>
>*请务必将crossdomain.xml文件放置到正确的位置。 例如，假定您在JBoss上部署了AEM Forms，请将此文件放置在以下位置： &lt;install_directory>\Adobe_Experience_Manager_forms\jboss\server\lc_turnkey\deploy\jboss-web.deployer\ROOT.war。*

## 包含AEM Forms Flex库文件 {#including-the-aem-forms-flex-library-file}

要使用Remoting以编程方式调用AEM Forms进程，请将adobe-remoting-provider.swc文件添加到Flex项目的类路径中。 此SWC文件位于以下位置：

* *&lt;install_directory>\Adobe_Experience_Manager_forms\sdk\misc\DataServices\Client-Libraries*

   where &lt;*install_directory*>是安装AEM Forms的目录。

**另请参阅**

[使用调用AEM Forms(AEM表单已弃用)AEM Forms Remoting](invoking-aem-forms-using-remoting.md#invoking-aem-forms-using-remoting)

[处理文档时使用(AEM表单已弃用)AEM Forms Remoting](invoking-aem-forms-using-remoting.md#handling-documents-with-remoting)

[通过使用(AEM表单已弃用)AEM Forms Remoting传递不安全的文档来调用短暂的进程](invoking-aem-forms-using-remoting.md#invoking-a-short-lived-process-by-passing-an-unsecure-document-using-remoting)

[验证使用Flex构建的客户端应用程序](invoking-aem-forms-using-remoting.md#authenticating-client-applications-built-with-flex)

## 使用远程处理文档 {#handling-documents-with-remoting}

AEM Forms中使用的最重要的非原始Java™类型之一是 `com.adobe.idp.Document` 类。 通常需要文档才能调用AEM Forms操作。 它主要是PDF文档，但可以包含其他文档类型，如SWF、HTML、XML或DOC文件。 (请参阅 [使用Java API将数据传递到AEM Forms服务](/help/forms/developing/invoking-aem-forms-using-java.md#passing-data-to-aem-forms-services-using-the-java-api).)

使用Flex构建的客户端应用程序无法直接请求文档。 例如，您无法启动Adobe Reader以请求生成PDF文件的URL。 文档类型(如PDF和Microsoft® Word文档)的请求将返回一个URL结果。 客户负责显示URL的内容。 文档管理服务可帮助生成URL和内容类型信息。 对XML文档的请求将返回结果中的完整XML文档。

### 将文档作为输入参数传递 {#passing-a-document-as-an-input-parameter}

使用Flex构建的客户端应用程序无法将文档直接传递到AEM Forms进程。 客户端应用程序而是使用 `mx.rpc.livecycle.DocumentReference` ActionScript类，用于将输入参数传递到 `com.adobe.idp.Document` 实例。 Flex客户端应用程序具有多个选项，用于设置 `DocumentReference` 对象：

* 当文档在服务器上且其文件位置已知时，将DocumentReference对象的referenceType属性设置为REF_TYPE_FILE。 将fileRef属性设置为文件的位置，如以下示例所示：

```java
 ... var docRef: DocumentReference = new DocumentReference(); 
 docRef.referenceType = DocumentReference.REF_TYPE_FILE; 
 docRef.fileRef = "C:/install/adobe/cs2/How to Uninstall.pdf"; ...
```

* 当文档在服务器上并且您知道其URL时，将DocumentReference对象的referenceType属性设置为REF_TYPE_URL。 将url属性设置为URL，如以下示例所示：

```java
... var docRef: DocumentReference = new DocumentReference(); 
docRef.referenceType = DocumentReference.REF_TYPE_URL; 
docRef.url = "https://companyserver:8080/DocumentManager/116/7855"; ...
```

* 要从客户端应用程序中的文本字符串创建DocumentReference对象，请将DocumentReference对象的referenceType属性设置为REF_TYPE_INLINE。 将text属性设置为要包含在对象中的文本，如以下示例所示：

```java
... var docRef: DocumentReference = new DocumentReference(); 
docRef.referenceType = DocumentReference.REF_TYPE_INLINE; 
docRef.text = "Text for my document";  // Optionally, you can override the server's default character set  // if necessary:  // docRef.charsetName=CharacterSetName  ...
```

* 当文档不在服务器上时，使用远程上传servlet将文档上传到AEM Forms。 AEM Forms的新增功能是上传安全文档。 在上传安全文档时，您必须使用 *文档上传应用程序用户* 角色。 如果没有此角色，用户将无法上载安全文档。 建议您使用单点登录上传安全文档。 (请参阅 [使用远程处理传递安全文档以调用进程](invoking-aem-forms-using-remoting.md#passing-secure-documents-to-invoke-processes-using-remoting).)

>[!NOTE]
如果将AEM Forms配置为允许上载不安全的文档，则可以使用没有“文档上载应用程序用户”角色的用户来上载文档。 用户还可以具有“文档上传”权限。 但是，如果将AEM Forms配置为仅允许安全文档，请确保用户具有“文档上传应用程序用户”角色或“文档上传”权限。 (请参阅 [配置AEM Forms以接受安全和不安全的文档](invoking-aem-forms-using-remoting.md#configuring-aem-forms-to-accept-secure-and-unsecure-documents).

您对指定的上传URL使用标准Flash上传功能： `https://SERVER:PORT/remoting/lcfileupload`. 然后，您可以使用 `DocumentReference` 对象类型的输入参数 `Document` 预期
` private function startUpload():void  {  fileRef.addEventListener(Event.SELECT, selectHandler);  fileRef.addEventListener("uploadCompleteData", completeHandler);  try  {   var success:Boolean = fileRef.browse();  }    catch (error:Error)  {   trace("Unable to browse for files.");  }  }      private function selectHandler(event:Event):void {  var request:URLRequest = new  URLRequest("https://SERVER:PORT/remoting/lcfileupload")  try   {   fileRef.upload(request);   }    catch (error:Error)   {   trace("Unable to upload file.");   }  }    private function completeHandler(event:DataEvent):void  {   var params:Object = new Object();   var docRef:DocumentReference = new DocumentReference();   docRef.url = event.data as String;   docRef.referenceType = DocumentReference.REF_TYPE_URL;  }`远程上传快速入门使用远程上传servlet将PDF文件传递到 `MyApplication/EncryptDocument`进程。 (请参阅 [通过使用(AEM表单已弃用)AEM Forms Remoting传递不安全的文档来调用短暂的进程](invoking-aem-forms-using-remoting.md#invoking-a-short-lived-process-by-passing-an-unsecure-document-using-remoting).)

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

远程上传快速入门使用远程上传servlet将PDF文件传递到 `MyApplication/EncryptDocument`进程。 (请参阅 [通过使用(AEM表单已弃用)AEM Forms Remoting传递不安全的文档来调用短暂的进程](invoking-aem-forms-using-remoting.md#invoking-a-short-lived-process-by-passing-an-unsecure-document-using-remoting).)

### 将文档传回客户端应用程序 {#passing-a-document-back-to-a-client-application}

客户端应用程序接收类型的对象 `mx.rpc.livecycle.DocumentReference` 返回 `com.adobe.idp.Document` 实例作为输出参数。 由于客户端应用程序处理的是ActionScript对象而不是Java，因此您无法将基于Java的文档对象传递回Flex客户端。 服务器而是会为文档生成一个URL，并将该URL传递回客户端。 的 `DocumentReference` 对象 `referenceType` 属性指定内容是否在 `DocumentReference` 对象或必须从 `DocumentReference.url` 属性。 的 `DocumentReference.contentType` 属性指定文档的类型。

**另请参阅**

[使用调用AEM Forms(AEM表单已弃用)AEM Forms Remoting](invoking-aem-forms-using-remoting.md#invoking-aem-forms-using-remoting)

[包含AEM Forms Flex库文件](invoking-aem-forms-using-remoting.md#including-the-aem-forms-flex-library-file)

[通过使用(AEM表单已弃用)AEM Forms Remoting传递不安全的文档来调用短暂的进程](invoking-aem-forms-using-remoting.md#invoking-a-short-lived-process-by-passing-an-unsecure-document-using-remoting)

[验证使用Flex构建的客户端应用程序](invoking-aem-forms-using-remoting.md#authenticating-client-applications-built-with-flex)

[使用远程处理传递安全文档以调用进程](invoking-aem-forms-using-remoting.md#passing-secure-documents-to-invoke-processes-using-remoting)

## 通过使用远程处理传递不安全的文档来调用短暂的进程 {#invoking-a-short-lived-process-by-passing-an-unsecure-document-using-remoting}

要从使用Flex构建的应用程序中调用AEM Forms进程，请执行以下任务：

1. 创建 `mx:RemoteObject` 实例。
1. 创建 `ChannelSet` 实例。
1. 传递所需的输入值。
1. 处理返回值。

>[!NOTE]
本节讨论在将AEM Forms配置为上传不安全文档时如何调用AEM Forms进程并上传文档。 有关如何调用AEM Forms进程和上传安全文档以及如何配置AEM Forms以接受安全和不安全文档的信息，请参阅 [使用远程处理传递安全文档以调用进程](invoking-aem-forms-using-remoting.md#passing-secure-documents-to-invoke-processes-using-remoting).

**创建mx:RemoteObject实例**

您可以创建 `mx:RemoteObject` 用于调用在Workbench中创建的AEM Forms进程的实例。 创建 `mx:RemoteObject` 实例中，指定以下值：

* **id:** 的名称 `mx:RemoteObject` 表示要调用的进程的实例。
* **目标：** 要调用的AEM Forms进程的名称。 例如，调用 `MyApplication/EncryptDocument` 进程，指定 `MyApplication/EncryptDocument`.
* **结果：** 处理结果的Flex方法的名称。

在 `mx:RemoteObject` 标记，指定 `<mx:method>` 用于指定进程调用方法名称的标记。 通常，Forms调用方法的名称为 `invoke`.

以下代码示例将创建 `mx:RemoteObject` 调用的实例 `MyApplication/EncryptDocument` 进程。

```java
 <mx:RemoteObject id="EncryptDocument" destination="MyApplication/EncryptDocument" result="resultHandler(event);">
          <mx:method name="invoke" result="handleExecuteInvoke(event)"/>
      </mx:RemoteObject>
```

**创建到AEM Forms的渠道**

客户端应用程序可以通过在MXML或ActionScript中指定渠道来调用AEM Forms，如以下ActionScript示例所示。 渠道必须为 `AMFChannel`, `SecureAMFChannel`, `HTTPChannel`或 `SecureHTTPChannel`.

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

分配 `ChannelSet` 实例 `mx:RemoteObject` 实例 `channelSet` 字段（如上一个代码示例中所示）。 通常，在import语句中导入channel类，而不是在调用 `ChannelSet.addChannel` 方法。

**传递输入值**

在Workbench中创建的进程可采用零个或多个输入参数并返回输出值。 客户端应用程序在 `ActionScript` 对象，其字段与属于AEM Forms进程的参数相对应。 这个短暂的过程，名为 `MyApplication/EncryptDocument`，需要一个名为的输入参数 `inDoc`. 流程公开的操作的名称为 `invoke` （短暂流程的默认名称）。 (请参阅 [使用调用AEM Forms(AEM表单已弃用)AEM Forms Remoting](invoking-aem-forms-using-remoting.md#invoking-aem-forms-using-remoting).)

以下代码示例将PDF文档传递到 `MyApplication/EncryptDocument` 进程：

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

在此代码示例中， `pdfDocument` 是 `DocumentReference` 包含不安全的PDF文档的实例。 有关 `DocumentReference`，请参阅 [处理文档时使用(AEM表单已弃用)AEM Forms Remoting](invoking-aem-forms-using-remoting.md#handling-documents-with-remoting).

**调用服务的特定版本**

您可以使用 `_version` 参数。 例如，调用 `MyApplication/EncryptDocument` 服务：

```java
 var params:Object = new Object();
 params["inDoc"] = pdfDocument;
 params["_version"] = "1.2"
 var token:AsyncToken = echoService.echoString(params);
```

的 `version` 参数必须是包含单个句点的字符串。 句点的左、主版本和右、副版本的值必须是整数。 如果未指定此参数，则会调用头活动版本。

**处理返回值**

AEM Forms进程输出参数被反序列化为ActionScript对象，客户端应用程序从这些对象中按名称提取特定参数，如以下示例所示。 ( `MyApplication/EncryptDocument` 进程已命名 `outDoc`.)

```java
     ...
     var res:Object = event.result;
     var docRef:DocumentReference = res["outDoc"] as DocumentReference;
     ...
```

**调用MyApplication/EncryptDocument进程**

您可以调用 `MyApplication/EncryptDocument` 流程：

1. 创建 `mx:RemoteObject` 实例(通过ActionScript或MXML)。 请参阅创建mx:RemoteObject实例。
1. 设置 `ChannelSet` 与AEM Forms通信，并将其与 `mx:RemoteObject` 实例。 请参阅创建到AEM Forms的渠道。
1. 调用ChannelSet的 `login` 方法或服务 `setCredentials` 方法来指定用户标识符值和密码。 (请参阅 [使用单点登录](invoking-aem-forms-using-remoting.md#using-single-sign-on).)
1. 填充 `mx.rpc.livecycle.DocumentReference` 实例，其中包含一个不安全的PDF文档，以传递到 `MyApplication/EncryptDocument` 进程。 (请参阅 [将文档作为输入参数传递](invoking-aem-forms-using-remoting.md#passing-a-document-as-an-input-parameter).)
1. 通过调用 `mx:RemoteObject` 实例 `invoke` 方法。 传递 `Object` 中包含输入参数(这是不安全的PDF文档)。 请参阅传递输入值。
1. 检索从进程返回的密码加密PDF文档。 请参阅处理返回值。

[快速入门：通过使用(AEM表单已弃用)AEM Forms Remoting传递不安全的文档来调用短暂的进程](/help/forms/developing/invocation-api-quick-starts.md#quick-start-invoking-a-short-lived-process-by-passing-an-unsecure-document-using-deprecated-for-aem-forms-aem-forms-remoting)

## 验证使用Flex构建的客户端应用程序 {#authenticating-client-applications-built-with-flex}

AEM Forms用户管理器可通过多种方式来验证来自Flex应用程序的远程处理请求，包括通过中央登录服务进行AEM Forms单点登录、基本身份验证和自定义身份验证。 如果未启用单点登录和匿名访问，则远程处理请求将导致基本身份验证（默认）或自定义身份验证。

基本身份验证依赖于Web应用程序容器中的标准J2EE基本身份验证。 对于基本身份验证，HTTP 401错误会导致浏览器出现问题。 这意味着当您尝试使用RemoteObject连接到Forms应用程序，但尚未从Flex应用程序登录时，浏览器会提示您输入用户名和密码。

对于自定义身份验证，服务器会向客户端发送错误，以指示需要进行身份验证。

>[!NOTE]
有关使用HTTP令牌执行身份验证的信息，请参阅 [创建使用HTTP令牌执行SSO身份验证的Flash Builder应用程序](/help/forms/developing/creating-flash-builder-applications-perform.md#creating-flash-builder-applications-that-perform-sso-authentication-using-http-tokens).

### 使用自定义身份验证 {#using-custom-authentication}

在管理控制台中，可通过在远程处理端点上将身份验证方法从“基本”更改为“自定义”，来启用自定义身份验证。 如果您使用自定义身份验证，则客户端应用程序会调用 `ChannelSet.login` 登录方法和 `ChannelSet.logout` 方法注销。

>[!NOTE]
在上一版本的AEM Forms中，您通过调用 `RemoteObject.setCredentials` 方法。 的 `setCredentials` 方法直到组件首次尝试连接到服务器时才实际将凭据传递到服务器。 因此，如果组件发出了故障事件，则无法确定是由于身份验证错误或其他原因导致了故障。 的 `ChannelSet.login` 方法在调用时会连接到服务器，以便您可以立即处理身份验证问题。 尽管您可以继续使用 `setCredentials` 方法，建议您使用 `ChannelSet.login` 方法。

由于多个目标可以使用相同的渠道和相应的ChannelSet对象，因此登录到一个目标会将用户登录到使用相同渠道或渠道的任何其他目标。 如果两个组件将不同的凭据应用到同一ChannelSet对象，则会使用最后应用的凭据。 如果多个组件使用相同的经过身份验证的ChannelSet对象，则调用 `logout` 方法从目标中记录所有组件。

以下示例使用 `ChannelSet.login` 和 `ChannelSet.logout` 方法。 此应用程序会执行以下操作：

* 创建 `ChannelSet` 对象 `creationComplete` 表示 `RemoteObject` 组件
* 通过调用 `ROLogin` 响应按钮点击事件的函数
* 使用RemoteObject组件向服务器发送字符串以响应Button点击事件。 服务器将相同的字符串返回到RemoteObject组件
* 使用RemoteObject组件的结果事件在TextArea控件中显示字符串
* 通过调用 `ROLogout` 响应按钮点击事件的函数

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

的 `login` 和 `logout` 方法会返回AsyncToken对象。 将事件处理程序分配给AsyncToken对象，以便结果事件处理成功调用，并将错误事件分配给处理失败。

### 使用单点登录 {#using-single-sign-on}

AEM forms用户可以连接到多个AEM Forms web应用程序以执行任务。 当用户从一个Web应用程序移动到另一个Web应用程序时，要求他们单独登录到每个Web应用程序是不高效的。 AEM Forms单点登录机制允许用户登录一次，然后访问任何AEM Forms Web应用程序。 由于AEM Forms开发人员可以创建客户端应用程序以与AEM Forms一起使用，因此他们还必须能够利用单点登录机制。

每个AEM Forms Web应用程序都打包在其自己的Web存档(WAR)文件中，然后将该文件打包为企业存档(EAR)文件的一部分。 由于应用程序服务器不允许在不同的Web应用程序之间共享会话数据，因此AEM Forms使用HTTP Cookie存储身份验证信息。 身份验证Cookie使用户能够登录到Forms应用程序，然后连接到其他AEM Forms Web应用程序。 此技术称为单点登录。

AEM Forms开发人员编写客户端应用程序以扩展表单指南（已弃用）的功能并自定义工作区。 例如，工作区应用程序可以启动一个流程。 然后，客户端应用程序使用远程处理端点从Forms服务中检索数据。

使用(AEM表单已弃用)AEM Forms Remoting调用AEM Forms服务时，客户端应用程序会在请求中传递身份验证Cookie。 由于用户已经进行了身份验证，因此无需再进行登录即可从客户端应用程序连接到AEM Forms服务。

>[!NOTE]
如果Cookie无效或缺失，则不存在到登录页面的隐式重定向。 因此，您仍然可以调用匿名服务。

您可以通过编写一个自行登录和注销的客户端应用程序来绕过AEM Forms单点登录机制。 如果您绕过单点登录机制，则可以对应用程序使用基本或自定义身份验证。

由于此机制不使用AEM Forms单点登录机制，因此不会向客户端写入身份验证Cookie。 登录凭据存储在 `ChannelSet` 对象。 因此， `RemoteObject` 你发出的呼叫与 `ChannelSet` 是在这些全权证书的背景下作出的。

### 在AEM Forms中设置单点登录 {#setting-up-single-sign-on-in-aem-forms}

要在AEM Forms中使用单点登录，请安装表单工作流组件，该组件包括集中登录服务。 用户成功登录后，集中登录服务会向用户返回身份验证Cookie。 对Forms Web应用程序的后续每个请求都包含Cookie。 如果Cookie有效，则用户将被视为已通过身份验证，因此无需再次登录。

### 编写使用单点登录的客户端应用程序 {#writing-a-client-application-that-uses-single-sign-on}

使用单点登录机制时，您希望用户在启动客户端应用程序之前使用集中登录服务登录。 也就是说，客户端应用程序不会通过浏览器或通过调用 `ChannelSet.login` 方法。

如果您使用AEM Forms单点登录机制，请将远程处理端点配置为使用自定义身份验证，而不是基本身份验证。 否则，在使用基本身份验证时，身份验证错误会导致浏览器出现问题，您不希望用户看到这些问题。 您的应用程序会检测到身份验证错误，然后显示一条消息，指示用户使用集中登录服务登录。

客户端应用程序使用 `RemoteObject` 组件，如以下示例所示。

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

**在Flex应用程序仍在运行时以新用户身份登录**

使用Flex构建的应用程序包含对AEM Forms服务的每个请求所包含的身份验证Cookie。 出于性能原因，AEM Forms不会在每个请求中验证Cookie。 但是，AEM Forms会检测身份验证Cookie何时被其他身份验证Cookie替换。

例如，启动客户端应用程序，当应用程序处于活动状态时，使用集中登录服务注销。 接下来，您可以以其他用户的身份登录。 以其他用户身份登录，会将现有的身份验证Cookie替换为新用户的身份验证Cookie。

在客户端应用程序发出下一个请求时，AEM Forms会检测到Cookie已发生更改，并注销用户。 因此，Cookie更改后的第一个请求失败。 所有后续请求都会在新Cookie的上下文中发出并成功。

**注销**

要从AEM Forms注销并使会话失效，必须从客户端的计算机中删除身份验证Cookie。 由于单点登录的目的是允许用户登录一次，因此您不希望客户端应用程序删除该Cookie。 此操作会有效地注销用户。

因此，请调用 `RemoteObject.logout` 客户端应用程序中的方法在客户端上生成一条错误消息，指定会话未注销。 用户可以使用集中式登录服务注销和删除身份验证Cookie。

**在Flex应用程序仍在运行时注销**

您可以启动使用Flex构建的客户端应用程序，并使用集中登录服务注销。 在注销过程中，会删除身份验证Cookie。 如果远程请求在没有Cookie的情况下发出，或者Cookie无效，则用户会话将失效。 此操作实际上是注销。 下次客户端应用程序尝试连接到AEM Forms服务时，将请求用户登录。

**另请参阅**

[使用调用AEM Forms(AEM表单已弃用)AEM Forms Remoting](invoking-aem-forms-using-remoting.md#invoking-aem-forms-using-remoting)

[处理文档时使用(AEM表单已弃用)AEM Forms Remoting](invoking-aem-forms-using-remoting.md#handling-documents-with-remoting)

[包含AEM Forms Flex库文件](invoking-aem-forms-using-remoting.md#including-the-aem-forms-flex-library-file)

[通过使用(AEM表单已弃用)AEM Forms Remoting传递不安全的文档来调用短暂的进程](invoking-aem-forms-using-remoting.md#invoking-a-short-lived-process-by-passing-an-unsecure-document-using-remoting)

[使用远程处理传递安全文档以调用进程](invoking-aem-forms-using-remoting.md#passing-secure-documents-to-invoke-processes-using-remoting)

## 使用远程处理传递安全文档以调用进程 {#passing-secure-documents-to-invoke-processes-using-remoting}

调用需要一个或多个文档的进程时，您可以将安全文档传递到AEM Forms。 通过传递安全文档，您可以保护业务信息和机密文档。 在这种情况下，文档可以是PDF文档、XML文档、Word文档等。 将AEM Forms配置为允许安全文档时，需要将安全文档从在Flex中编写的客户端应用程序传递到AEM Forms。 (请参阅 [配置AEM Forms以接受安全和不安全的文档](invoking-aem-forms-using-remoting.md#configuring-aem-forms-to-accept-secure-and-unsecure-documents).)

在传递安全文档时，请使用单点登录，并指定具有 *文档上传应用程序用户* 角色。 如果没有此角色，用户将无法上载安全文档。 您可以以编程方式为用户分配角色。 (请参阅 [管理角色和权限](/help/forms/developing/users.md#managing-roles-and-permissions).)

>[!NOTE]
创建新角色并希望该角色的成员上传安全文档时，请确保指定“文档上传”权限。

AEM Forms支持名为 `getFileUploadToken` 会返回传递到上载servlet的令牌。 的 `DocumentReference.constructRequestForUpload` 方法需要指向AEM Forms的URL以及 `LC.FileUploadAuthenticator.getFileUploadToken` 方法。 此方法将返回 `URLRequest` 在对上载servlet的调用中使用的对象。 以下代码演示了此应用程序逻辑。

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

### 配置AEM Forms以接受安全和不安全的文档 {#configuring-aem-forms-to-accept-secure-and-unsecure-documents}

您可以使用管理控制台指定在将文档从Flex客户端应用程序传递到AEM Forms进程时，文档是否安全。 默认情况下，AEM Forms配置为接受安全文档。 您可以通过执行以下步骤将AEM Forms配置为接受安全文档：

1. 登录到管理控制台。
1. 单击 **设置**.
1. 单击 **核心系统设置。**
1. 单击配置。
1. 确保取消选择允许从Flex应用程序上传非安全文档选项。

>[!NOTE]
要将AEM Forms配置为接受非安全文档，请选择允许从Flex应用程序上传非安全文档选项。 然后，重新启动应用程序或服务，以确保该设置生效。

### 快速入门：使用Remoting通过传递安全文档来调用短暂的进程 {#quick-start-invoking-a-short-lived-process-by-passing-a-secure-document-using-remoting}

以下代码示例将调用 `MyApplication/EncryptDocument.`用户必须登录才能单击“选择文件”按钮，该按钮用于上传PDF文件并调用该过程。 即，用户进行身份验证后，“选择文件”按钮即会启用。 下图显示了用户进行身份验证后的Flex客户端应用程序。 请注意，已启用“已验证”复选框。

![iu_iu_secureremotelogin](assets/iu_iu_secureremotelogin.png)

如果AEM Forms配置为仅允许上载安全文档，且用户没有 *文档上传应用程序用户* 角色，则会引发异常。 如果用户确实具有此角色，则会上传文件并调用该过程。

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

[使用调用AEM Forms(AEM表单已弃用)AEM Forms Remoting](invoking-aem-forms-using-remoting.md#invoking-aem-forms-using-remoting)

[处理文档时使用(AEM表单已弃用)AEM Forms Remoting](invoking-aem-forms-using-remoting.md#handling-documents-with-remoting)

[包含AEM Forms Flex库文件](invoking-aem-forms-using-remoting.md#including-the-aem-forms-flex-library-file)

[通过使用(AEM表单已弃用)AEM Forms Remoting传递不安全的文档来调用短暂的进程](invoking-aem-forms-using-remoting.md#invoking-a-short-lived-process-by-passing-an-unsecure-document-using-remoting)

[验证使用Flex构建的客户端应用程序](invoking-aem-forms-using-remoting.md#authenticating-client-applications-built-with-flex)

## 使用远程调用自定义组件服务 {#invoking-custom-component-services-using-remoting}

您可以使用远程处理调用位于自定义组件中的服务。 例如，请考虑包含客户服务的银行组件。 您可以使用在Flex中编写的客户端应用程序调用属于客户服务的操作。 在执行与此部分关联的快速启动之前，必须创建银行自定义组件。

客户服务公开了名为 `createCustomer`. 本讨论介绍如何创建调用客户服务并创建客户的Flex客户端应用程序。 此操作需要类型复杂的对象 `com.adobe.livecycle.sample.customer.Customer` 代表新客户。 下图显示了调用客户服务并创建新客户的客户端应用程序。 的 `createCustomer` 操作会返回客户标识符值。 标识符值显示在“客户标识符”文本框中。

![iu_iu_flexnewcust](assets/iu_iu_flexnewcust.png)

下表列出了属于此客户端应用程序的控件。

<table>
 <thead>
  <tr>
   <th><p>控件名称</p></th>
   <th><p>描述</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>txtFirst</p></td>
   <td><p>指定客户的名字。 </p></td>
  </tr>
  <tr>
   <td><p>txtLast</p></td>
   <td><p>指定客户的姓氏。 </p></td>
  </tr>
  <tr>
   <td><p>txtPhone</p></td>
   <td><p>指定客户的电话号码。</p></td>
  </tr>
  <tr>
   <td><p>txtStreet</p></td>
   <td><p>指定客户的街道名称。</p></td>
  </tr>
  <tr>
   <td><p>txtState</p></td>
   <td><p>指定客户的状态。 </p></td>
  </tr>
  <tr>
   <td><p>txtZIP</p></td>
   <td><p>指定客户的邮政编码。 </p></td>
  </tr>
  <tr>
   <td><p>txtCity</p></td>
   <td><p>指定客户的城市。</p></td>
  </tr>
  <tr>
   <td><p>txtCustId</p></td>
   <td><p>指定新帐户所属的客户标识符值。 此文本框由客户服务的返回值填充 <code>createCustomer</code> 操作。 </p></td>
  </tr>
 </tbody>
</table>

### 映射AEM Forms复杂数据类型 {#mapping-aem-forms-complex-data-types}

某些AEM Forms操作需要复杂的数据类型作为输入值。 这些复杂数据类型定义操作使用的运行时值。 例如，客户服务的 `createCustomer` 操作需要 `Customer` 包含服务所需的运行时值的实例。 如果没有复杂类型，客户服务将引发异常，并且不执行操作。

调用AEM Forms服务时，请创建映射到所需AEM Forms复杂类型的ActionScript对象。 对于操作所需的每个复杂数据类型，请创建一个单独的ActionScript对象。

在ActionScript类中，使用 `RemoteClass` 映射到AEM Forms复杂类型的元数据标记。 例如，在调用 `createCustomer` 操作，创建映射到的ActionScript类 `com.adobe.livecycle.sample.customer.Customer` 数据类型。

以下名为Customer的ActionScript类显示了如何映射到AEM Forms数据类型 `com.adobe.livecycle.sample.customer.Customer`.

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

AEM Forms复杂类型的完全限定数据类型已分配给别名标记。

ActionScript类的字段与属于AEM Forms复杂类型的字段匹配。 位于客户ActionScript类中的六个字段与属于 `com.adobe.livecycle.sample.customer.Customer`.

>[!NOTE]
确定属于Forms复杂类型的字段名称的一种好方法是在Web浏览器中查看服务的WSDL。 WSDL指定服务的复杂类型和相应的数据成员。 以下WSDL用于客户服务： `https://[yourServer]:[yourPort]/soap/services/CustomerService?wsdl.`

客户ActionScript类属于名为customer的包。 建议您将映射到复杂AEM Forms数据类型的所有ActionScript类都放置到其自己的包中。 在Flex项目的src文件夹中创建一个文件夹，并将ActionScript文件放在该文件夹中，如下图所示。

![iu_iu_customeras](assets/iu_iu_customeras.png)

### 快速入门：使用远程调用客户自定义服务 {#quick-start-invoking-the-customer-custom-service-using-remoting}

以下代码示例调用客户服务并创建客户。 运行此代码示例时，请确保填写所有文本框。 另外，请确保创建映射到 `com.adobe.livecycle.sample.customer.Customer`.

>[!NOTE]
在执行此快速启动之前，您必须创建并部署银行自定义组件。

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

**样式表**

此快速入门包含一个名为 *bank.css*. 以下代码表示使用的样式表。

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

[使用调用AEM Forms(AEM表单已弃用)AEM Forms Remoting](invoking-aem-forms-using-remoting.md#invoking-aem-forms-using-remoting)

[处理文档时使用(AEM表单已弃用)AEM Forms Remoting](invoking-aem-forms-using-remoting.md#handling-documents-with-remoting)

[包含AEM Forms Flex库文件](invoking-aem-forms-using-remoting.md#including-the-aem-forms-flex-library-file)

[通过使用(AEM表单已弃用)AEM Forms Remoting传递不安全的文档来调用短暂的进程](invoking-aem-forms-using-remoting.md#invoking-a-short-lived-process-by-passing-an-unsecure-document-using-remoting)

[验证使用Flex构建的客户端应用程序](invoking-aem-forms-using-remoting.md#authenticating-client-applications-built-with-flex)

[使用远程处理传递安全文档以调用进程](invoking-aem-forms-using-remoting.md#passing-secure-documents-to-invoke-processes-using-remoting)
