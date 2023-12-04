---
title: Reader使用可移植保护库扩展受策略保护的PDF文档
seo-title: Reader extending policy-protected PDF documents using Portable Protection Library
description: Reader扩展通过Acrobat Reader启用Adobe PDF文档中的交互功能。 您可以使用Portable Protection Library (PPL)来读取器扩展受DRM保护的PDF文档。
seo-description: Reader extensions enable interactive features in Adobe PDF documents through Acrobat Reader. You can use the Portable Protection Library (PPL) to reader extend the DRM protected PDF documents.
uuid: 0da17641-d24c-43c2-b918-8b5abe1e5473
contentOwner: khsingh
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: document_services
discoiquuid: 83ca522e-d16e-4196-9aa7-84f85de8dee2
feature: Document Security
exl-id: fe5d83e8-5e36-4146-a20a-dab2213055e2
source-git-commit: 10b370fd8f855f71c6d7d791c272137bb5e04d97
workflow-type: tm+mt
source-wordcount: '783'
ht-degree: 1%

---

# Reader使用可移植保护库扩展受策略保护的PDF文档 {#reader-extending-policy-protected-pdf-documents-using-portable-protection-library}

熟悉Document Security、Reader Extension和Java编程语言的概念，以便对Document Security受策略保护的PDF文档进行Reader扩展。

您可以使用Document Security限制仅授权用户访问特定PDF文档。 您还可以确定收件人如何使用受保护的文档。 例如，您可以指定收件人是否可以打印、复制或编辑受Document Security策略保护的文档的文本。 要了解有关Document Security的更多信息，请参阅 [关于document security](/help/forms/using/admin-help/document-security.md).

您可以使用Reader Extensions通过Acrobat Reader在Adobe PDF文档中启用交互式功能。 这些交互功能通常只能通过Adobe Acrobat Professional和Standard使用。 要了解Reader扩展可以启用的交互功能，请参阅 [Adobe Experience Manager Forms DocAssurance服务&#x200B;](/help/forms/using/overview-aem-document-services.md)**.**

您可以使用便携式保护库对文档应用策略，而无需通过网络传输文档。 只有安全凭据和保护策略详细信息会通过网络传递。 实际文档永远不会离开客户端，并且保护策略将在客户端本地应用。

## Reader扩展document security受策略保护的PDF文档 {#reader-extending-document-security-policy-protected-pdf-documents}

受策略保护的文档是加密的文档。 您无法使用标准reader-extension API来应用、删除和检索受策略保护的PDF文档的使用权限。 只有Portable Protection Library的Reader扩展服务提供API来应用、删除和检索受Document Security策略保护的PDF文档的使用权限。

### Reader扩展服务 {#reader-extensions-service}

reader扩展服务向受策略保护的PDF文档添加使用权限，以激活在使用Adobe Acrobat Reader打开PDF文档时通常不可用的功能。 它还具有用于移除和检索受策略保护文档的使用权限的API。

Reader扩展服务完全支持基于PDF标准1.6及更高版本的PDF文档。 除了Acrobat Reader之外，第三方用户不需要任何其他软件或插件即可使用受策略保护的PDF文档。

您可以使用Reader扩展服务完成以下任务：

* 将使用权限应用到受策略保护的PDF文档。
* 删除受策略保护的PDF文档的使用权限。
* 检索应用于受策略保护的PDF文档的使用权限。

### 对受Document Security策略保护的PDF文档应用使用权限 {#apply-usage-rights-to-a-document-security-policy-protected-pdf-document}

您可以使用 `applyUsageRights`用于向受策略保护的PDF文档应用使用权限的Java API。 使用权限与Acrobat中默认提供的功能有关，但在Adobe Reader中不可用，例如向表单添加注释或填写表单字段并保存表单的功能。 已应用使用权限的PDF文档称为启用权限的文档。 在Adobe Reader中打开启用了权限的文档的用户可以执行为该特定文档启用的操作。

**语法：** `InputStream applyUsageRights(InputStream inputFile, File certFile, String credentialPassword, UsageRights usageRights)`

<table>
 <tbody>
  <tr>
   <td><p><strong>参数</strong></p> </td>
   <td><p><strong>描述</strong></p> </td>
  </tr>
  <tr>
   <td><p>输入文件</p> </td>
   <td><p>指定表示要应用使用权限的PDF文档的InputStream。 您可以使用LiveCycleRights Management或AEM Forms Document Security保护的文档。</p> </td>
  </tr>
  <tr>
   <td><p>certFile</p> </td>
   <td><p>指定表示.jks文件的文件对象。 .jks文件是密钥库文件。 它指向授予使用权限的证书。</p> </td>
  </tr>
  <tr>
   <td><p>credentialPassword</p> </td>
   <td><p>指定密钥库的密码。 </p> </td>
  </tr>
  <tr>
   <td><p>usageRights</p> </td>
   <td><p>指定类型的对象 <a href="https://help.adobe.com/en_US/livecycle/11.0/ProgramLC/javadoc/com/adobe/livecycle/readerextensions/client/UsageRights.html" target="_blank">使用权限</a>. usageRights对象表示可应用于受策略保护的PDF文档的单个权限。</p> </td>
  </tr>
 </tbody>
</table>

### 检索应用于受策略保护的PDF文档的使用权限。   {#retrieve-usage-rights-applied-to-a-policy-protected-pdf-document-nbsp}

您可以使用 `getDocumentUsageRights`Java API用于检索应用于受策略保护的PDF文档的Reader扩展使用权限。 通过检索有关使用权限的信息，您可以了解为受策略保护的PDF文档启用的Reader扩展功能。

**语法：** `public GetUsageRightsResult getDocumentUsageRights(InputStream inDoc)`

<table>
 <tbody>
  <tr>
   <td><p><strong>参数</strong></p> </td>
   <td><p><strong>描述</strong></p> </td>
  </tr>
  <tr>
   <td><p>inDoc</p> </td>
   <td><p>指定表示从中检索使用权限的PDF文档的InputStream。 您可以使用LiveCycleRights Management或AEM Forms Document Security保护的文档。</p> </td>
  </tr>
 </tbody>
</table>

#### 代码示例 {#code-sample}

```java
//Create a ServiceClientFactory instance
ServiceClientFactory factory = ServiceClientFactory.createInstance(connectionProps);
//Create a RightsManagementClient object
RightsManagementClient2 rmClient2= new RightsManagementClient2(factory);

String inputFileName = "C:\\Sample\\protected.pdf"; //Input file can be RM protected or unprotected pdf file
File certFile = new File("C:\\Sample\\cert.jks"); //RE certificate file
String password = "password"; //password for RE certificate
UsageRights usageRights = getUsageRights(true,true,false,false,true,true,false,false,false,false,true);

//RE rights to be applied on the file : FormFillIn, FormDataImportExport, SubmitStandalone, OnlineForms, DynamicFormField, DynamicFormPages, BarcodeDecoding, DigitalSignatures, Comments, CommentsOnline, EmbeddedFiles

InputStream inputFileStream = new FileInputStream(inputFileName);
InputStream output = rmClient2.getRightsManagementReaderExtensionService().applyUsageRights(inputFileStream, certFile, credentialPassword, rights);

String outputFileName = "C:\\Sample\\ReAdded.pdf";
//Save the PDF document
File myFile = new File(outputFileName);
FileOutputStream outputStream = new FileOutputStream(myFile);

int read = 0;
byte[] bytes = new byte[1024];

while ((read = output.read(bytes)) != -1) {

    outputStream.write(bytes, 0, read);
}

System.out.println("UsageRights applied successfully to the document. ");
 outputStream.close();
inputFileStream.close();

//Get Usage Rights for the output pdf document
InputStream fileWithRe = new FileInputStream(myFile);

GetUsageRightsResult usageRights = rmClient2.getRightsManagementReaderExtensionService().getDocumentUsageRights(fileWithRe);

UsageRights rights = usageRights.getRights();
String right1 = rights1.toString();
System.out.println("RE rights for the file are :\n"+right1);
 fileWithRe.close();
```

### 删除受策略保护的PDF文档的使用权限 {#remove-usage-rights-of-a-policy-protected-pdf-document}

您可以使用 `removeUsageRights`Java API可从受策略保护的文档中删除使用权限。 从受策略保护的PDF文档中删除使用权限是对该文档执行其他AEM Forms操作所必需的。 例如，在设置使用权限之前，必须对PDF文档进行数字签名（或认证）。 因此，如果要对受策略保护的文档执行操作，必须从PDF文档中删除使用权限，执行其他操作，如对文档进行数字签名，然后重新将使用权限应用到文档。

**语法：** `InputStream removeUsageRights(InputStream inputFile)`

<table>
 <tbody>
  <tr>
   <td><p><strong>参数</strong></p> </td>
   <td><p><strong>描述</strong></p> </td>
  </tr>
  <tr>
   <td><p> </p> <p>输入文件</p> </td>
   <td>指定表示使用方式的PDF文档的InputStream<br /> 权限将被删除。 您可以使用LiveCycleRights Management或AEM Forms Document Security保护的文档。</td>
  </tr>
 </tbody>
</table>

#### 代码示例 {#code-sample-1}

```java
//Create a ServiceClientFactory instance
ServiceClientFactory factory = ServiceClientFactory.createInstance(connectionProps);
//Create a RightsManagementClient object
RightsManagementClient2 rmClient2= new RightsManagementClient2(factory);

String inputFileName = "C:\\Sample\\fileWithRe.pdf"; //Input file can be RM protected or unprotected pdf file
InputStream inputFileStream = new FileInputStream(inputFileName);

InputStream fileStream = rmClient2.getRightsManagementReaderExtensionService().removeUsageRights(inputFileStream);

String outputFileName = "C:\\Sample\\ReRemoveded.pdf";
//Save the PDF document
File myFile = new File(outputFileName);
FileOutputStream outputStream = new FileOutputStream(myFile);

int read = 0;
byte[] bytes = new byte[1024];

while ((read = fileStream.read(bytes)) != -1) {

    outputStream.write(bytes, 0, read);
}
System.out.println("RE rights removed successfully from the document.");
outputStream.close();
inputFileStream.close();
```
