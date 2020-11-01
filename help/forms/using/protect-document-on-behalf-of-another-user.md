---
title: Protect代表其他用户创建文档
seo-title: Protect代表其他用户创建文档
description: Protect代表其他用户创建文档
uuid: 76f4b30b-6d0c-4cae-98b3-334efdbf27bb
geptopics: SG_AEMFORMS/categories/working_with_document_security
discoiquuid: 7cb8140d-dd62-4659-8cc7-21361bd5d3f6
translation-type: tm+mt
source-git-commit: a873cf3e7efd3bc9cd4744bf09078d9040efcdda
workflow-type: tm+mt
source-wordcount: '376'
ht-degree: 0%

---


# Protect代表其他用户创建文档 {#protect-a-document-on-behalf-of-another-user}

AEM Forms文档安全Java SDK提供API，允许用户帐户代表其他用户保护文档，而不获得编辑文档的权限。 您可以在工作流程中使用API，也可以通过编程方式将其用作文档服务。 新API包括：

* **protectDocument** 使用ProtectDocument API代表文档将策略应用到

   另一个用户帐户。 用于应用策略的用户帐户的权限仍限于保护文档。 它没有获得开放和视图文档的权利。 RMSecureDocumentResult protectDocument(文档inDoc、字符串documentName、字符串策略集名称、字符串策略名称、RMLocale区域设置、布尔bExactMatchForNames)

* **createLicense** 使用CreateLicense API代表其他用户帐户为策略创建许可证。 PublishLicenseDTO createLicense(String policyId, String documentName, boolean logSecureDocEvent)
* **protectDocumentWithCoverPage使用** ProtectDocumentWithCoverPage API应用策略并代表其他用户向文档添加封面。 用于应用策略的用户帐户的权限仍限于保护文档。 它没有获得开放和视图文档的权利。 RMSecureDocumentResult保护DocumentWithCoverPage(文档inDoc、String documentName、String policySetName、String policyName、文档coverDoc、布尔bExactMatchForNames)

## 使用API代表其他用户保护文档 {#using-the-apis-to-protect-a-document-on-behalf-of-another-user}

执行以下步骤以代表其他用户保护文档，而不获得编辑文档的权限：

1. 创建策略集。 例如，PolicySet1。
1. 在新创建的策略集中创建策略。 例如，PolicySet1中的Policy1。
1. 创建具有角色Rights Management最终用户的用户。 例如，User1。 为新创建的用户提供使用Policy1保护的视图文档的权限。
1. 创建新角色。 例如，Role1。 为新创建的角色提供服务调用权限。 创建具有新创建角色的用户。 例如，User2.您可以使用User2或管理员创建SDK连接并调用protectDocument服务。

   现在，您可以运行以下示例代码以保护文档，而无需向保护文档的用户提供编辑文档的权限：

   ```java
   import java.io.File;
   import java.io.FileInputStream;
   import java.io.FileNotFoundException;
   import java.io.FileOutputStream;
   import java.io.IOException;
   import java.io.InputStream;
   import java.util.Properties;
   
   import com.adobe.edc.common.dto.PublishLicenseDTO;
   import com.adobe.edc.sdk.SDKException;
   import com.adobe.idp.Document;
   import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
   import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
   import com.adobe.livecycle.rightsmanagement.RMSecureDocumentResult;
   import com.adobe.livecycle.rightsmanagement.client.DocumentManager;
   import com.adobe.livecycle.rightsmanagement.client.RightsManagementClient;
   import com.adobe.livecycle.rightsmanagement.client.RightsManagementClient2;
   
   public class PublishAsProtectAPI {
   
   private static final String unprotectedFileName = "C:\\unprotected.pdf";
   private static final String protectedFileName = "C:\\protect.pdf";
   private static final String coverFileName = "C:\\CoverPage.pdf";
   private static final String POLICY_ID = "2EF66008-5E2D-1034-9B06-00000A292C18"; 
   
   public static void main(String[] args) {
   
   try {
   
   Properties connectionProps = new Properties();
   connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT,"http://localhost:8080");
   connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
   connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
   connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME,"administrator");
   connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD,"password");
   
   // Create a ServiceClientFactory instance
   ServiceClientFactory factory = ServiceClientFactory.createInstance(connectionProps);
   testProtectDocument(factory);
   testProtectDocumentWithCoverPage(factory);
   testProtectDocumentJavaPPL(factory);
   
   } 
   catch (Exception ex) {
   ex.printStackTrace(); }
   }
   
   private static void testProtectDocument(ServiceClientFactory factory) throws FileNotFoundException, SDKException {
   // Create a RightsManagementClient object
   RightsManagementClient rmClient = new RightsManagementClient(factory);
   // Create a Document Manager object
   DocumentManager documentManager = rmClient.getDocumentManager();
   //Reference a policy-protected PDF document from which to remove a policy
   FileInputStream is = new FileInputStream(unprotectedFileName);
   Document inPDF = new Document(is);
   long startTime = System.currentTimeMillis();
   //Remove a policy from the policy-protected PDF document
   RMSecureDocumentResult securePDF = documentManager.protectDocument(inPDF, "test", "newPolicySet", "latest", "DefaultDom", "administrator", null, true);
   System.out.println("Total Time taken for protectDocument = " + (System.currentTimeMillis() - startTime));
   //Save the unsecured PDF document
   File myFile = new File(protectedFileName);
   securePDF.getProtectedDoc().copyToFile(myFile);
   }
   
   private static void testProtectDocumentWithCoverPage(ServiceClientFactory factory) throws FileNotFoundException, SDKException {
   // Create a RightsManagementClient object
   RightsManagementClient rmClient = new RightsManagementClient(factory);
   // Create a Document Manager object
   DocumentManager documentManager = rmClient.getDocumentManager();
   //Reference a policy-protected PDF document from which to remove a policy
   FileInputStream is = new FileInputStream(unprotectedFileName);
   Document inPDF = new Document(is);
   FileInputStream coverIS = new FileInputStream(coverFileName);
   Document inCoverPDF = new Document(coverIS);
   long startTime = System.currentTimeMillis();
   //Remove a policy from the policy-protected PDF document
   RMSecureDocumentResult securePDF = documentManager.protectDocumentWithCoverPage(inPDF, "test", "newPolicySet", "latestPolicy", inCoverPDF, true);
   System.out.println("Total Time taken for Page0ProtectDocument = " + (System.currentTimeMillis() - startTime));
   //Save the unsecured PDF document
   File myFile = new File(protectedFileName);
   securePDF.getProtectedDoc().copyToFile(myFile);
   }
   
   private static PublishLicenseDTO testProtectDocumentJavaPPL (ServiceClientFactory factory) throws SDKException, FileNotFoundException, IOException {
   // Create a RightsManagementClient object
   RightsManagementClient2 rmClient2 = new RightsManagementClient2(factory);
   // Create a Document Manager object
   DocumentManager documentManager = rmClient2.getDocumentManager();
   long startTime = System.currentTimeMillis();
   PublishLicenseDTO license = documentManager.createLicense(POLICY_ID, "Out.pdf", true);
   System.out.println("Create License totalTime = " + (System.currentTimeMillis() - startTime));
   startTime = System.currentTimeMillis();
   // Reference a PDF document to which a policy is applied
   InputStream inputFileStream = new FileInputStream(unprotectedFileName);
   // Apply a policy to the PDF document
   InputStream protectPDF = rmClient2.getRightsManagementEncryptionService().protectDocument(inputFileStream, license);
   // Save the policy-protected PDF document
   File myFile = new File(protectedFileName);
   // write the inputStream to a FileOutputStream
   FileOutputStream outputStream = new FileOutputStream(myFile);
   int read = 0;
   byte[] bytes = new byte[1024];
   while ((read = protectPDF.read(bytes)) != -1) {
   outputStream.write(bytes, 0, read);
   }
   System.out.println("protectPDFDocument totalTime = " + (System.currentTimeMillis() - startTime));
   outputStream.close();
   inputFileStream.close();
   System.out.println("Document Protected Successfully");
   return license;
   }
   }
   ```

