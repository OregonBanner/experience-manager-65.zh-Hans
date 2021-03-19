---
title: Reader使用可移植保护库扩展受策略保护的PDF文档
seo-title: Reader使用可移植保护库扩展受策略保护的PDF文档
description: Reader扩展通过Acrobat Reader在Adobe PDF文档中支持交互式功能。 您可以使用可移植保护库(PPL)来扩展受DRM保护的PDF文档。
seo-description: Reader扩展通过Acrobat Reader在Adobe PDF文档中支持交互式功能。 您可以使用可移植保护库(PPL)来扩展受DRM保护的PDF文档。
uuid: 0da17641-d24c-43c2-b918-8b5abe1e5473
contentOwner: khsingh
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: document_services
discoiquuid: 83ca522e-d16e-4196-9aa7-84f85de8dee2
feature: Document Security
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '835'
ht-degree: 0%

---


# Reader使用可移植保护库{#reader-extending-policy-protected-pdf-documents-using-portable-protection-library}扩展受策略保护的PDF文档

您必须熟悉文档安全性、读者扩展和Java编程语言的概念，才能对文档安全性受策略保护的PDF文档进行读者扩展。

您可以使用文档安全性将特定PDF文档的访问权限限制为仅限授权用户。 您还可以确定收件人如何使用受保护的文档。 例如，您可以指定收件人是否可以打印、复制或编辑受文档安全策略保护的文档的文本。 要了解有关文档安全性的更多信息，请参阅[关于文档安全](/help/forms/using/admin-help/document-security.md)。

您可以使用Reader扩展通过Acrobat Reader在Adobe PDF 文档中启用交互式功能。 这些交互功能通常仅通过Adobe Acrobat Professional和Standard提供。 要了解Reader扩展可启用的交互功能，请参阅[Adobe Experience Manager Forms DocAssurance服务&#x200B;](/help/forms/using/overview-aem-document-services.md)**。**

您可以使用便携式保护库对文档应用策略，而无需文档通过网络传输。 只有安全凭据和保护策略详细信息才能通过网络传输。 实际文档从不离开客户端，保护策略将在客户端本地应用。

## Reader扩展文档安全策略保护的PDF文档{#reader-extending-document-security-policy-protected-pdf-documents}

受策略保护的文档是加密文档。 不能使用标准Reader扩展API来应用、删除和检索受策略保护的PDF文档的使用权限。 只有可移植保护库的Reader扩展服务提供API来应用、删除和检索受文档安全策略保护的PDF文档的使用权限。

### Reader扩展服务{#reader-extensions-service}

Reader扩展服务将使用权限添加到受策略保护的PDF文档，激活在使用Adobe Acrobat Reader打开PDF文档时不正常可用的功能。 它还具有用于删除和检索受策略保护的文档的使用权限的API。

Reader扩展服务完全支持基于PDF标准1.6及更高版本的PDF文档。 除Acrobat Reader之外，第三方用户不需要任何其他软件或插件即可使用受策略保护的PDF文档。

您可以通过Reader扩展服务完成以下任务:

* 将使用权限应用于受策略保护的PDF文档。
* 删除受策略保护的PDF文档的使用权限。
* 检索应用于受策略保护的PDF文档的使用权限。

### 将使用权限应用于受文档安全策略保护的PDF文档{#apply-usage-rights-to-a-document-security-policy-protected-pdf-document}

可以使用`applyUsageRights`Java API将使用权限应用于受策略保护的PDF文档。 使用权限与默认在Acrobat中但在Adobe Reader中不可用的功能有关，例如向表单添加注释或填写表单字段并保存表单的功能。 对其应用了使用权限的PDF文档称为启用权限的文档。 在Adobe Reader中打开启用权限的文档的用户可以执行为该特定文档启用的操作。

**语法：** `InputStream applyUsageRights(InputStream inputFile, File certFile, String credentialPassword, UsageRights usageRights)`

<table>
 <tbody>
  <tr>
   <td><p><strong>参数</strong></p> </td>
   <td><p><strong>描述</strong></p> </td>
  </tr>
  <tr>
   <td><p>inputFile</p> </td>
   <td><p>指定表示要应用使用权限的PDF文档的InputStream。 您可以使用LiveCycleRights Management或AEM Forms 文档安全保护文档。</p> </td>
  </tr>
  <tr>
   <td><p>certFile</p> </td>
   <td><p>指定表示.jks文件的File对象。 .jks文件是keystore文件。 它指向授予使用权限的证书。</p> </td>
  </tr>
  <tr>
   <td><p>credentialPassword</p> </td>
   <td><p>指定密钥库的口令。 </p> </td>
  </tr>
  <tr>
   <td><p>usageRights</p> </td>
   <td><p>指定类型<a href="https://help.adobe.com/en_US/livecycle/11.0/ProgramLC/javadoc/com/adobe/livecycle/readerextensions/client/UsageRights.html" target="_blank">UsageRights</a>的对象。 usageRights对象表示可应用于受策略保护的PDF文档的个人权限。</p> </td>
  </tr>
 </tbody>
</table>

### 检索应用于受策略保护的PDF文档的使用权限。   {#retrieve-usage-rights-applied-to-a-policy-protected-pdf-document-nbsp}

可以使用`getDocumentUsageRights`Java API检索应用于受策略保护的PDF文档的Reader扩展使用权限。 通过检索有关使用权限的信息，您可以了解受策略保护的PDF文档中Reader扩展已启用的功能。

**语法：** `public GetUsageRightsResult getDocumentUsageRights(InputStream inDoc)`

<table>
 <tbody>
  <tr>
   <td><p><strong>参数</strong></p> </td>
   <td><p><strong>描述</strong></p> </td>
  </tr>
  <tr>
   <td><p>inDoc</p> </td>
   <td><p>指定表示要从中检索使用权限的PDF文档的InputStream。 您可以使用LiveCycleRights Management或AEM Forms 文档安全保护文档。</p> </td>
  </tr>
 </tbody>
</table>

#### 代码示例{#code-sample}

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

System.out.println("UsageRights applied successfully to the document. ”);
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

### 删除受策略保护的PDF文档{#remove-usage-rights-of-a-policy-protected-pdf-document}的使用权限

可以使用`removeUsageRights`Java API从受策略保护的文档中删除使用权限。 要对文档执行其他AEM Forms操作，必须从受策略保护的PDF文档中删除使用权限。 例如，在设置使用权限之前，您必须对PDF文档进行数字签名（或验证）。 因此，如果要对受策略保护的文档执行操作，则必须从PDF文档中删除使用权限，执行其他操作(如对文档进行数字签名)，然后对文档重新应用使用权限。

**语法：** `InputStream removeUsageRights(InputStream inputFile)`

<table>
 <tbody>
  <tr>
   <td><p><strong>参数</strong></p> </td>
   <td><p><strong>描述</strong></p> </td>
  </tr>
  <tr>
   <td><p> </p> <p>inputFile</p> </td>
   <td>指定表示要从中删除使用<br />权限的PDF文档的InputStream。 您可以使用LiveCycleRights Management或AEM Forms 文档安全保护文档。</td>
  </tr>
 </tbody>
</table>

#### 代码示例{#code-sample-1}

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
System.out.println("RE rights removed successfully from the document.”);
outputStream.close();
inputFileStream.close();
```

