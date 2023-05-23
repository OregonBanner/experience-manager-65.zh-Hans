---
title: 組合器服務Java API快速入門(SOAP)
seo-title: Assembler Service Java API QuickStart(SOAP)
description: 組合器服務Java API快速入門(SOAP)
uuid: 33ad5f7a-4f4c-4e72-937d-85891498a80e
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: b7b17cf8-def5-4a77-a872-c1f286814881
role: Developer
exl-id: 306cd40b-1831-45aa-9f58-3ab1983a68c5
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1001'
ht-degree: 0%

---

# 組合器服務Java API快速入門(SOAP) {#assembler-service-java-api-quickstart-soap}

Java API快速入門(SOAP)適用於組合器服務

[快速入門（SOAP模式）：使用Java API組合PDF檔案](assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-a-pdf-document-using-the-java-api)

[快速入門（SOAP模式）：使用Java API分解PDF檔案](assembler-service-java-api-quick.md#quick-start-soap-mode-disassembling-a-pdf-document-using-the-java-api)

[快速入門（SOAP模式）：使用Java API組合已加密的PDF檔案](assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-an-encrypted-pdf-document-using-the-java-api)

[快速入門（SOAP模式）：使用Java API組合Bates編號的PDF檔案](assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-a-pdf-document-with-bates-numbering-using-the-java-api)

[快速入門（SOAP模式）：使用Java API組裝非互動式PDF檔案](assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-a-non-interactive-pdf-document-using-the-java-api)

[快速入門（SOAP模式）：使用Java API判斷檔案是否符合PDF/A標準](assembler-service-java-api-quick.md#quick-start-soap-mode-determining-whether-a-document-is-pdf-a-compliant-using-the-java-api)

[快速入門（SOAP模式）：使用Java API驗證DDX檔案](assembler-service-java-api-quick.md#quick-start-soap-mode-validating-ddx-documents-using-the-java-api)

[快速入門（SOAP模式）：使用Java API以書籤組合PDF檔案](assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-pdf-documents-with-bookmarks-using-the-java-api)

[快速入門（SOAP模式）：使用Java API動態建立DDX檔案](assembler-service-java-api-quick.md#quick-start-soap-mode-dynamically-creating-a-ddx-document-using-the-java-api)

[快速入門（SOAP模式）：使用Java API組合PDFPortfolio](assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-pdf-portfolios-using-the-java-api)

[快速入門（SOAP模式）：使用Java API組裝多個XDP片段](assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-multiple-xdp-fragments-using-the-java-api)

AEM Forms作業可使用AEM Forms強型別API執行，且連線模式應設定為SOAP。

>[!NOTE]
>
>「使用AEM Forms進行程式設計」中的「快速入門」是以部署在JBoss Application Server和Microsoft Windows作業系統上的Forms Server為基礎。 不過，如果您使用其他作業系統（例如UNIX），請以適用的作業系統支援的路徑取代Windows特定路徑。 同樣地，如果您使用其他J2EE應用程式伺服器，請務必指定有效的連線屬性。 另請參閱 [設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 快速入門（SOAP模式）：使用Java API組合PDF檔案 {#quick-start-soap-mode-assembling-a-pdf-document-using-the-java-api}

以下Java程式碼範例會合併兩個名為的PDF來原始檔 *map.pdf* 和 *directions.pdf* 放入單一PDF檔案中。 單一PDF檔案的名稱是 *AssemblerResultPDF.pdf*. DDX檔案的名稱為 *shell.xml*. (請參閱 [以程式設計方式組裝PDF檔案](/help/forms/developing/assembling-pdf-documents.md#programmatically-assembling-pdf-documents).)

```java
 /*
     * This Java Quick Start uses the SOAP mode and contains the following JAR files
     * in the class path:
     * 1. adobe-assembler-client.jar
     * 2. adobe-livecycle-client.jar
     * 3. adobe-usermanager-client.jar
     * 4. adobe-utilities.jar
     * 5. jboss-client.jar (use a different JAR file if the forms server is not deployed
     * on JBoss)
     * 6. activation.jar (required for SOAP mode)
     * 7. axis.jar (required for SOAP mode)
     * 8. commons-codec-1.3.jar (required for SOAP mode)
     * 9.  commons-collections-3.1.jar  (required for SOAP mode)
     * 10. commons-discovery.jar (required for SOAP mode)
     * 11. commons-logging.jar (required for SOAP mode)
     * 12. dom3-xml-apis-2.5.0.jar (required for SOAP mode)
     * 13. jaxen-1.1-beta-9.jar (required for SOAP mode)
     * 14. jaxrpc.jar (required for SOAP mode)
     * 15. log4j.jar (required for SOAP mode)
     * 16. mail.jar (required for SOAP mode)
     * 17. saaj.jar (required for SOAP mode)
     * 18. wsdl4j.jar (required for SOAP mode)
     * 19. xalan.jar (required for SOAP mode)
     * 20. xbean.jar (required for SOAP mode)
     * 21. xercesImpl.jar (required for SOAP mode)
     *
     * These JAR files are located in the following path:
     * <install directory>/sdk/client-libs/common
     *
     * The adobe-utilities.jar file is located in the following path:
     * <install directory>/sdk/client-libs/jboss
     *
     * The jboss-client.jar file is located in the following path:
     * <install directory>/jboss/bin/client
     *
     * SOAP required JAR files are located in the following path:
     * <install directory>/sdk/client-libs/thirdparty
     *
     * If you want to invoke a remote forms server instance and there is a
     * firewall between the client application and the server, then it is
     * recommended that you use the SOAP mode. When using the SOAP mode,
     * you have to include these additional JAR files
     *
     * For information about the SOAP
     * mode, see "Setting connection properties" in Programming
     * with AEM Forms
     *
     * The following XML represents the DDX document used in this quick start:
     * <?xml version="1.0" encoding="UTF-8"?>
     * <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
     * <PDF result="out.pdf">
     * <PDF source="map.pdf" />
     * <PDF source="directions.pdf" />
     * </PDF>
     *</DDX>
     */
 import com.adobe.livecycle.assembler.client.*;
 import java.util.*;
 import java.io.File;
 import java.io.FileInputStream;
 import com.adobe.idp.Document;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 
 public class InvokeAssemblerSOAP
 {
     public static void main(String[] args) {
         try{
             //Set connection properties required to invoke AEM Forms using SOAP mode
             Properties connectionProps = new Properties();
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 
             //Create a ServiceClientFactory instance
             ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
 
             //Create an AssemblerServiceClient object
             AssemblerServiceClient assemblerClient = new AssemblerServiceClient(myFactory);
 
             //Create a FileInputStream object based on an existing DDX file
             FileInputStream myDDXFile = new FileInputStream("C:\\shell.xml");
 
             //Create a Document object based on the DDX file
             Document myDDX = new Document(myDDXFile);
 
             //Create a Map object to store PDF source documents
             Map inputs = new HashMap();
             FileInputStream mySourceMap = new FileInputStream("C:\\map.pdf");
             FileInputStream mySourceOptions = new FileInputStream("C:\\directions.pdf");
 
             //Create a Document object based on the map.pdf source file
             Document myPDFMapSource = new Document(mySourceMap);
 
             //Create a Document object based on the directions.pdf source file
             Document myPDFOptionsSource = new Document(mySourceOptions);
 
             //Place two entries into the Map object
             inputs.put("map.pdf",myPDFMapSource);
             inputs.put("directions.pdf",myPDFOptionsSource);
 
             //Create an AssemblerOptionsSpec object
             AssemblerOptionSpec assemblerSpec = new AssemblerOptionSpec();
             assemblerSpec.setFailOnError(false);
 
             //Submit the job to Assembler service
             AssemblerResult jobResult = assemblerClient.invokeDDX(myDDX,inputs,assemblerSpec);
             java.util.Map allDocs = jobResult.getDocuments();
 
             //Retrieve the result PDF document from the Map object
             Document outDoc = null;
 
             //Iterate through the map object to retrieve the result PDF document
             for (Iterator i = allDocs.entrySet().iterator(); i.hasNext();) {
                 // Retrieve the Map object’s value
                 Map.Entry e = (Map.Entry)i.next();
 
                 //Get the key name as specified in the
                 //DDX document
                 String keyName = (String)e.getKey();
                 if (keyName.equalsIgnoreCase("out.pdf"))
                 {
                     Object o = e.getValue();
                     outDoc = (Document)o;
 
                     //Save the result PDF file
                     File myOutFile = new File("C:\\AssemblerResultPDF.pdf");
                     outDoc.copyToFile(myOutFile);
                 }
             }
         }catch (Exception e) {
             e.printStackTrace();
         }
     }
 }
```

## 快速入門（SOAP模式）：使用Java API分解PDF檔案 {#quick-start-soap-mode-disassembling-a-pdf-document-using-the-java-api}

以下Java程式碼範例將名為的PDF檔案分解 *AssemblerResultPDF.pdf*. 請注意，DDX檔案的名稱為 *shell_disassemble.xml*. 每個已拆解的PDF檔案都命名為 `ResultPDF[Number].pdf`. 亦即，第一個已拆解的PDF檔案已命名 *ResultPDF1.pdf。* 如需關於以下專案的資訊： *shell_disassemble.xml* 此程式碼範例中使用的DDX檔案，請參閱 [以程式設計方式分解PDF檔案](/help/forms/developing/assembling-pdf-documents.md#programmatically-disassembling-pdf-documents).

```java
 /*
     * This Java Quick Start uses the SOAP mode and contains the following JAR files
     * in the class path:
     * 1. adobe-assembler-client.jar
     * 2. adobe-livecycle-client.jar
     * 3. adobe-usermanager-client.jar
     * 4. adobe-utilities.jar
     * 5. jboss-client.jar (use a different JAR file if the forms server is not deployed
     * on JBoss)
     * 6. activation.jar (required for SOAP mode)
     * 7. axis.jar (required for SOAP mode)
     * 8. commons-codec-1.3.jar (required for SOAP mode)
     * 9.  commons-collections-3.1.jar  (required for SOAP mode)
     * 10. commons-discovery.jar (required for SOAP mode)
     * 11. commons-logging.jar (required for SOAP mode)
     * 12. dom3-xml-apis-2.5.0.jar (required for SOAP mode)
     * 13. jaxen-1.1-beta-9.jar (required for SOAP mode)
     * 14. jaxrpc.jar (required for SOAP mode)
     * 15. log4j.jar (required for SOAP mode)
     * 16. mail.jar (required for SOAP mode)
     * 17. saaj.jar (required for SOAP mode)
     * 18. wsdl4j.jar (required for SOAP mode)
     * 19. xalan.jar (required for SOAP mode)
     * 20. xbean.jar (required for SOAP mode)
     * 21. xercesImpl.jar (required for SOAP mode)
     *
     * These JAR files are located in the following path:
     * <install directory>/sdk/client-libs/common
     *
     * The adobe-utilities.jar file is located in the following path:
     * <install directory>/sdk/client-libs/jboss
     *
     * The jboss-client.jar file is located in the following path:
     * <install directory>/jboss/bin/client
     *
     * SOAP required JAR files are located in the following path:
     * <install directory>/sdk/client-libs/thirdparty
     *
     * If you want to invoke a remote forms server instance and there is a
     * firewall between the client application and the server, then it is
     * recommended that you use the SOAP mode. When using the SOAP mode,
     * you have to include these additional JAR files
     *
     * For information about the SOAP
     * mode, see "Setting connection properties" in Programming
     * with AEM Forms
     *
     * The following XML represents the DDX document used in this quick start:
     * <?xml version="1.0" encoding="UTF-8"?>
     *<DDX xmlns="https://ns.adobe.com/DDX/1.0/">
     * <PDFsFromBookmarks prefix="stmt">
     * <PDF source="AssemblerResultPDF.pdf"/>
     *</PDFsFromBookmarks>
     *</DDX>
     */
 import com.adobe.livecycle.assembler.client.*;
 import java.util.*;
 import java.io.File;
 import java.io.FileInputStream;
 import com.adobe.idp.Document;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 
 public class DisassemblePDFSOAP
 {
     public static void main(String[] args) {
         try{
             //Set connection properties required to invoke AEM Forms
             Properties connectionProps = new Properties();
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 
             //Create a ServiceClientFactory instance
             ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
 
             //Create an AssemblerServiceClient object
             AssemblerServiceClient assemblerClient = new AssemblerServiceClient(myFactory);
 
             //Create a FileInputStream object based on an existing DDX file
             FileInputStream myDDXFile = new FileInputStream("C:\\shell_disassemble.xml");
 
             //Create a Document object based on the DDX file
             Document myDDX = new Document(myDDXFile);
 
             //Create a Map object to store PDF source documents
             Map inputs = new HashMap();
             FileInputStream mySourceMap = new FileInputStream("C:\\AssemblerResultPDF.pdf");
 
             //Create a Document object based on the map.pdf source file
             Document myPDFSource = new Document(mySourceMap);
 
             //Place two entries into the Map object
             inputs.put("AssemblerResultPDF.pdf",myPDFSource);
 
             //Create an AssemblerOptionsSpec object
             AssemblerOptionSpec assemblerSpec = new AssemblerOptionSpec();
             assemblerSpec.setFailOnError(false);
 
             //Submit the job to the Assembler service
             AssemblerResult jobResult = assemblerClient.invokeDDX(myDDX,inputs,assemblerSpec);
             java.util.Map allDocs = jobResult.getDocuments();
 
             //Retrieve the result PDF documents from the Map object
             Document outDoc = null;
             int index = 0;
 
             //Iterate through the map object to retrieve the result PDF document
             for (Iterator i = allDocs.entrySet().iterator(); i.hasNext();) {
                 // Retrieve the Map object’s value
                 Map.Entry e = (Map.Entry)i.next();
                 Object o = e.getValue();
 
                 //Cast the Object to a Document
                 //and save to a file
                 outDoc = (Document)o;
                 File myOutFile = new File("C:\\ResultPDF"+index +".pdf");
                 outDoc.copyToFile(myOutFile);
                 index++;
             }
             if (index > 0)
                 System.out.println("The PDF document was disassembled into "+index+" PDF documents.");
             else
                 System.out.println("The PDF document was not disassembled.");
 
         }catch (Exception e) {
             System.out.println("Error OCCURRED: "+e.getMessage());
         }
     }
 }
```

## 快速入門（SOAP模式）：使用Java API組合已加密的PDF檔案 {#quick-start-soap-mode-assembling-an-encrypted-pdf-document-using-the-java-api}

以下Java程式碼範例會組合以密碼加密的PDF檔案。 未加密的PDF檔案已命名 *Loan.pdf*. 請注意，DDX檔案的名稱為 *shell_Encrypt.xml*. 已命名加密的PDF檔案 *AssemblerEncryptedPDF.pdf*. (請參閱 [組合已加密的PDF檔案](/help/forms/developing/assembling-pdf-documents.md#assembling-encrypted-pdf-documents).)

```java
 /*
     * This Java Quick Start uses the SOAP mode and contains the following JAR files
     * in the class path:
     * 1. adobe-assembler-client.jar
     * 2. adobe-livecycle-client.jar
     * 3. adobe-usermanager-client.jar
     * 4. adobe-utilities.jar
     * 5. jboss-client.jar (use a different JAR file if the forms server is not deployed
     * on JBoss)
     * 6. activation.jar (required for SOAP mode)
     * 7. axis.jar (required for SOAP mode)
     * 8. commons-codec-1.3.jar (required for SOAP mode)
     * 9.  commons-collections-3.1.jar  (required for SOAP mode)
     * 10. commons-discovery.jar (required for SOAP mode)
     * 11. commons-logging.jar (required for SOAP mode)
     * 12. dom3-xml-apis-2.5.0.jar (required for SOAP mode)
     * 13. jaxen-1.1-beta-9.jar (required for SOAP mode)
     * 14. jaxrpc.jar (required for SOAP mode)
     * 15. log4j.jar (required for SOAP mode)
     * 16. mail.jar (required for SOAP mode)
     * 17. saaj.jar (required for SOAP mode)
     * 18. wsdl4j.jar (required for SOAP mode)
     * 19. xalan.jar (required for SOAP mode)
     * 20. xbean.jar (required for SOAP mode)
     * 21. xercesImpl.jar (required for SOAP mode)
     *
     * These JAR files are located in the following path:
     * <install directory>/sdk/client-libs/common
     *
     * The adobe-utilities.jar file is located in the following path:
     * <install directory>/sdk/client-libs/jboss
     *
     * The jboss-client.jar file is located in the following path:
     * <install directory>/jboss/bin/client
     *
     * SOAP required JAR files are located in the following path:
     * <install directory>/sdk/client-libs/thirdparty
     *
     * If you want to invoke a remote forms server instance and there is a
     * firewall between the client application and the server, then it is
     * recommended that you use the SOAP mode. When using the SOAP mode,
     * you have to include these additional JAR files
     *
     * For information about the SOAP
     * mode, see "Setting connection properties" in Programming
     * with AEM Forms
     *
     * The following XML represents the DDX document used in this quick start:
     *<?xml version="1.0" encoding="UTF-8"?>
     * <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
     * <PDF result="EncryptLoan.pdf" encryption="userProtect">
     * <PDF source="inDoc" />
     * </PDF>
     * <PasswordEncryptionProfile name="userProtect" compatibilityLevel="Acrobat7">
     * <OpenPassword>AdobeOpen</OpenPassword>
     * </PasswordEncryptionProfile>
     * </DDX>
     */
 
 import com.adobe.livecycle.assembler.client.*;
 import java.util.*;
 import java.io.File;
 import java.io.FileInputStream;
 import com.adobe.idp.Document;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 
 public class AssembleEncryptedDocumentSOAP
 {
     public static void main(String[] args) {
         try{
             //Set connection properties required to invoke AEM Forms using SOAP mode
             Properties connectionProps = new Properties();
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 
             //Create a ServiceClientFactory instance
             ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
 
             //Create an AssemblerServiceClient object
             AssemblerServiceClient assemblerClient = new AssemblerServiceClient(myFactory);
 
             /*
              * Create a FileInputStream object based on an existing DDX file
              * This DDX document contains instructions to encrypt the PDF document
              */
             FileInputStream myDDXFile = new FileInputStream("C:\\shell_Encrypt.xml");
 
             //Create a Document object based on the DDX file
             Document myDDX = new Document(myDDXFile);
 
             //Reference an unsecured PDF document
             FileInputStream mySourceLoan = new FileInputStream("C:\\Loan.pdf");
 
             //Create a Document object based on the Loan.pdf source file
             Document myPDFLoanSource = new Document(mySourceLoan);
 
             //Create an AssemblerOptionsSpec object
             AssemblerOptionSpec assemblerSpec = new AssemblerOptionSpec();
             assemblerSpec.setFailOnError(false);
 
             //Submit the job to Assembler service
             Document jobResult = assemblerClient.invokeOneDocument(myDDX,myPDFLoanSource,assemblerSpec);
 
             //Create the output file
             File myOutFile = new File("C:\\AssemblerEncryptedPDF.pdf");
             jobResult.copyToFile(myOutFile);
 
         }catch (Exception e) {
             e.printStackTrace();
         }
     }
 }
```

## 快速入門（SOAP模式）：使用Java API組合Bates編號的PDF檔案 {#quick-start-soap-mode-assembling-a-pdf-document-with-bates-numbering-using-the-java-api}

以下Java程式碼範例會以唯一的頁面識別碼（bates編號）來組合PDF檔案。 請注意，DDX檔案的名稱為 *shell_Bates.xml*. 從組合器服務傳回的PDF檔案會儲存為名為的PDF檔案 *AssemblerResultBatesPDF.pdf*. (請參閱 [使用Bates編號組合檔案](/help/forms/developing/assembling-pdf-documents.md#assembling-documents-using-bates-numbering).)

```java
 /*
     * This Java Quick Start uses the SOAP mode and contains the following JAR files
     * in the class path:
     * 1. adobe-assembler-client.jar
     * 2. adobe-livecycle-client.jar
     * 3. adobe-usermanager-client.jar
     * 4. adobe-utilities.jar
     * 5. jboss-client.jar (use a different JAR file if the forms server is not deployed
     * on JBoss)
     * 6. activation.jar (required for SOAP mode)
     * 7. axis.jar (required for SOAP mode)
     * 8. commons-codec-1.3.jar (required for SOAP mode)
     * 9.  commons-collections-3.1.jar  (required for SOAP mode)
     * 10. commons-discovery.jar (required for SOAP mode)
     * 11. commons-logging.jar (required for SOAP mode)
     * 12. dom3-xml-apis-2.5.0.jar (required for SOAP mode)
     * 13. jaxen-1.1-beta-9.jar (required for SOAP mode)
     * 14. jaxrpc.jar (required for SOAP mode)
     * 15. log4j.jar (required for SOAP mode)
     * 16. mail.jar (required for SOAP mode)
     * 17. saaj.jar (required for SOAP mode)
     * 18. wsdl4j.jar (required for SOAP mode)
     * 19. xalan.jar (required for SOAP mode)
     * 20. xbean.jar (required for SOAP mode)
     * 21. xercesImpl.jar (required for SOAP mode)
     *
     * These JAR files are located in the following path:
     * <install directory>/sdk/client-libs/common
     *
     * The adobe-utilities.jar file is located in the following path:
     * <install directory>/sdk/client-libs/jboss
     *
     * The jboss-client.jar file is located in the following path:
     * <install directory>/jboss/bin/client
     *
     * SOAP required JAR files are located in the following path:
     * <install directory>/sdk/client-libs/thirdparty
     *
     * If you want to invoke a remote forms server instance and there is a
     * firewall between the client application and the server, then it is
     * recommended that you use the SOAP mode. When using the SOAP mode,
     * you have to include these additional JAR files
     *
     * For information about the SOAP
     * mode, see "Setting connection properties" in Programming
     * with AEM Forms
     *
     * The following XML represents the DDX document used in this quick start:
     * <?xml version="1.0" encoding="UTF-8"?>
     * <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
     * <PDF result="out.pdf">
     * <Header>
     * <Center>
     * <StyledText>
     * <p font-size="20pt"><BatesNumber/></p>
     * </StyledText>
     * </Center>
     * </Header>
     * <PDF source="map.pdf" />
     * <PDF source="directions.pdf" />
     * </PDF>
     * </DDX>
     */
 
 import com.adobe.livecycle.assembler.client.*;
 import java.util.*;
 import java.io.File;
 import java.io.FileInputStream;
 import com.adobe.idp.Document;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 
 
 public class AssembleBatesNumberDocumentSOAP
 {
     public static void main(String[] args) {
         try{
             //Set connection properties required to invoke AEM Forms using SOAP mode
             Properties connectionProps = new Properties();
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 
             //Create a ServiceClientFactory instance
             ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
 
             //Create an AssemblerServiceClient object
             AssemblerServiceClient assemblerClient = new AssemblerServiceClient(myFactory);
 
             //Create a FileInputStream object based on an existing DDX file
             FileInputStream myDDXFile = new FileInputStream("C:\\shell_Bates.xml");
 
             //Create a Document object based on the DDX file
             Document myDDX = new Document(myDDXFile);
 
             //Create a Map object to store PDF source documents
             Map<String, Object> inputs = new HashMap<String, Object>();
             FileInputStream mySourceMap = new FileInputStream("C:\\Adobe\map.pdf");
             FileInputStream mySourceOptions = new FileInputStream("C:\\Adobe\directions.pdf");
 
             //Create a Document object based on the map.pdf source file
             Document myPDFMapSource = new Document(mySourceMap);
 
             //Create a Document object based on the directions.pdf source file
             Document myPDFOptionsSource = new Document(mySourceOptions);
 
             //Place two entries into the Map object
             inputs.put("map.pdf",myPDFMapSource);
             inputs.put("directions.pdf",myPDFOptionsSource);
 
             //Create an AssemblerOptionsSpec object
             AssemblerOptionSpec assemblerSpec = new AssemblerOptionSpec();
             assemblerSpec.setFailOnError(false);
 
             //Set the initial number to 100
             assemblerSpec.setFirstBatesNumber(100);
 
             //Submit the job to Assembler service
             AssemblerResult jobResult = assemblerClient.invokeDDX(myDDX,inputs,assemblerSpec);
             java.util.Map allDocs = jobResult.getDocuments();
 
             //Retrieve the result PDF document from the Map object
             Document outDoc = null;
 
             //Iterate through the map object to retrieve the result PDF document
             for (Iterator i = allDocs.entrySet().iterator(); i.hasNext();) {
                 // Retrieve the Map object’s value
                 Map.Entry e = (Map.Entry)i.next();
 
                 //Get the key name as specified in the
                 //DDX document
                 String keyName = (String)e.getKey();
                 if (keyName.equalsIgnoreCase("out.pdf"))
                 {
                     //Cast the Object to a Document
                     Object o = e.getValue();
                     outDoc = (Document)o;
 
                     //Create the output file
                     File myOutFile = new File("C:\\AssemblerResultBatesPDF.pdf");
                     outDoc.copyToFile(myOutFile);
                 }
             }
             System.out.println("The PDF that contains Bates numbering was assembled.");
         }catch (Exception e) {
             e.printStackTrace();
         }
     }
 }
```

## 快速入門（SOAP模式）：使用Java API組裝非互動式PDF檔案 {#quick-start-soap-mode-assembling-a-non-interactive-pdf-document-using-the-java-api}

以下Java程式碼範例會組合非互動式PDF檔案。 傳遞至Assembler服務的互動式PDF檔案已命名 *Loan.pdf*. 請注意，DDX檔案的名稱為 *shell_XFA.xml*. 非互動式PDF檔案會儲存為名為的PDF檔案 *AssembleNonInteractivePDF.pdf*. (請參閱 [組合非互動式PDF檔案](/help/forms/developing/assembling-pdf-documents.md#assembling-non-interactive-pdf-documents).)

```java
 /*
     * This Java Quick Start uses the SOAP mode and contains the following JAR files
     * in the class path:
     * 1. adobe-assembler-client.jar
     * 2. adobe-livecycle-client.jar
     * 3. adobe-usermanager-client.jar
     * 4. adobe-utilities.jar
     * 5. jboss-client.jar (use a different JAR file if the forms server is not deployed
     * on JBoss)
     * 6. activation.jar (required for SOAP mode)
     * 7. axis.jar (required for SOAP mode)
     * 8. commons-codec-1.3.jar (required for SOAP mode)
     * 9.  commons-collections-3.1.jar  (required for SOAP mode)
     * 10. commons-discovery.jar (required for SOAP mode)
     * 11. commons-logging.jar (required for SOAP mode)
     * 12. dom3-xml-apis-2.5.0.jar (required for SOAP mode)
     * 13. jaxen-1.1-beta-9.jar (required for SOAP mode)
     * 14. jaxrpc.jar (required for SOAP mode)
     * 15. log4j.jar (required for SOAP mode)
     * 16. mail.jar (required for SOAP mode)
     * 17. saaj.jar (required for SOAP mode)
     * 18. wsdl4j.jar (required for SOAP mode)
     * 19. xalan.jar (required for SOAP mode)
     * 20. xbean.jar (required for SOAP mode)
     * 21. xercesImpl.jar (required for SOAP mode)
     *
     * These JAR files are located in the following path:
     * <install directory>/sdk/client-libs/common
     *
     * The adobe-utilities.jar file is located in the following path:
     * <install directory>/sdk/client-libs/jboss
     *
     * The jboss-client.jar file is located in the following path:
     * <install directory>/jboss/bin/client
     *
     * SOAP required JAR files are located in the following path:
     * <install directory>/sdk/client-libs/thirdparty
     *
     * If you want to invoke a remote forms server instance and there is a
     * firewall between the client application and the server, then it is
     * recommended that you use the SOAP mode. When using the SOAP mode,
     * you have to include these additional JAR files
     *
     * For information about the SOAP
     * mode, see "Setting connection properties" in Programming
     * with AEM Forms
     *
     * The following XML represents the DDX document used in this quick start:
     * <?xml version="1.0" encoding="UTF-8"?>
     * <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
     * <PDF result="out.pdf">
     * <PDF source="inDoc"/>
     * <NoXFA/>
     * </PDF>
     * </DDX>
     */
 import com.adobe.livecycle.assembler.client.*;
 import java.util.*;
 import java.io.File;
 import java.io.FileInputStream;
 import com.adobe.idp.Document;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 
 public class AssembleNonInteractiveSOAP
 {
     public static void main(String[] args) {
         try{
             //Set connection properties required to invoke AEM Forms
             Properties connectionProps = new Properties();
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 
             //Create a ServiceClientFactory instance
             ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
 
             //Create an AssemblerServiceClient object
             AssemblerServiceClient assemblerClient = new AssemblerServiceClient(myFactory);
 
             /*
              * Create a FileInputStream object based on an existing DDX file
              * This DDX document contains instructions to create
              * a non-interactive PDF document
              */
             FileInputStream myDDXFile = new FileInputStream("C:\\shell_XFA.xml");
 
             //Create a Document object based on the DDX file
             Document myDDX = new Document(myDDXFile);
 
             //Reference an interactive PDF document
             FileInputStream mySourceLoan = new FileInputStream("C:\\Adobe\Loan.pdf");
 
             //Create a Document object based on the Loan.pdf source file
             Document myPDFLoanSource = new Document(mySourceLoan);
 
             //Create an AssemblerOptionsSpec object
             AssemblerOptionSpec assemblerSpec = new AssemblerOptionSpec();
             assemblerSpec.setFailOnError(false);
 
             //Submit the job to Assembler service and get back a
             //non-interactive PDF document
             Document outDoc = assemblerClient.invokeOneDocument(myDDX,myPDFLoanSource,assemblerSpec);
 
             //Save the non-interactive PDF document
             File myOutFile = new File("C:\\AssembleNonInteractivePDF.pdf");
             outDoc.copyToFile(myOutFile);
 
         }catch (Exception e) {
             e.printStackTrace();
         }
     }
 }
 
 
```

## 快速入門（SOAP模式）：使用Java API判斷檔案是否符合PDF/A標準 {#quick-start-soap-mode-determining-whether-a-document-is-pdf-a-compliant-using-the-java-api}

以下Java程式碼範例會判斷輸入PDF檔案是否符合PDF/A規範。 傳遞至組合器服務的輸入PDF檔案已命名 *Loan.pdf*. DDX檔案的名稱為shell_PDFA.xml。 從Assembler服務傳回並指定輸入PDF檔案是否符合PDF/A的XML檔案會儲存為名為result.xml的XML檔案。 如需關於以下專案的資訊： *shell_PDFA.xml* 此程式碼範例中使用的DDX檔案，請參閱 [判斷檔案是否符合PDF/A規範](/help/forms/developing/assembling-pdf-documents.md#determining-whether-documents-are-pdf-a-compliant).

```java
 /*
     * This Java Quick Start uses the SOAP mode and contains the following JAR files
     * in the class path:
     * 1. adobe-assembler-client.jar
     * 2. adobe-livecycle-client.jar
     * 3. adobe-usermanager-client.jar
     * 4. adobe-utilities.jar
     * 5. jboss-client.jar (use a different JAR file if the forms server is not deployed
     * on JBoss)
     * 6. activation.jar (required for SOAP mode)
     * 7. axis.jar (required for SOAP mode)
     * 8. commons-codec-1.3.jar (required for SOAP mode)
     * 9.  commons-collections-3.1.jar  (required for SOAP mode)
     * 10. commons-discovery.jar (required for SOAP mode)
     * 11. commons-logging.jar (required for SOAP mode)
     * 12. dom3-xml-apis-2.5.0.jar (required for SOAP mode)
     * 13. jaxen-1.1-beta-9.jar (required for SOAP mode)
     * 14. jaxrpc.jar (required for SOAP mode)
     * 15. log4j.jar (required for SOAP mode)
     * 16. mail.jar (required for SOAP mode)
     * 17. saaj.jar (required for SOAP mode)
     * 18. wsdl4j.jar (required for SOAP mode)
     * 19. xalan.jar (required for SOAP mode)
     * 20. xbean.jar (required for SOAP mode)
     * 21. xercesImpl.jar (required for SOAP mode)
     *
     * These JAR files are located in the following path:
     * <install directory>/sdk/client-libs/common
     *
     * The adobe-utilities.jar file is located in the following path:
     * <install directory>/sdk/client-libs/jboss
     *
     * The jboss-client.jar file is located in the following path:
     * <install directory>/jboss/bin/client
     *
     * SOAP required JAR files are located in the following path:
     * <install directory>/sdk/client-libs/thirdparty
     *
     * If you want to invoke a remote forms server instance and there is a
     * firewall between the client application and the server, then it is
     * recommended that you use the SOAP mode. When using the SOAP mode,
     * you have to include these additional JAR files
     *
     * For information about the SOAP
     * mode, see "Setting connection properties" in Programming
     * with AEM Forms
     *
     * This quick start validates the following DDX document:
     *<?xml version="1.0" encoding="UTF-8"?>
     *<DDX xmlns="https://ns.adobe.com/DDX/1.0/">
     * <DocumentInformation source="Loan.pdf" result="Loan_result.xml">
     * <PDFAValidation compliance="PDF/A-1b" resultLevel="Detailed" ignoreUnusedResources="true" allowCertificationSignatures="true" />
     * </DocumentInformation>
     *</DDX>
     */
 
 import com.adobe.livecycle.assembler.client.*;
 import java.util.*;
 import java.io.File;
 import java.io.FileInputStream;
 import com.adobe.idp.Document;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 
 public class AssembleDeterminePDFASOAP
 {
     public static void main(String[] args) {
         try{
             //Set connection properties required to invoke AEM Forms using SOAP mode
             Properties connectionProps = new Properties();
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 
             //Create a ServiceClientFactory instance
             ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
 
             //Create an AssemblerServiceClient object
             AssemblerServiceClient assemblerClient = new AssemblerServiceClient(myFactory);
 
             //Create a FileInputStream object based on an existing DDX file
             FileInputStream myDDXFile = new FileInputStream("C:\\shell_PDFA.xml");
 
             //Create a Document object based on the DDX file
             Document myDDX = new Document(myDDXFile);
 
             //Create a Map object to store PDF source documents
             Map inputs = new HashMap();
             FileInputStream mySourceMap = new FileInputStream("C:\\Adobe\Loan.pdf");
 
             //Create a Document object based on the map.pdf source file
             Document myPDFMapSource = new Document(mySourceMap);
 
             //Place two entries into the Map object
             inputs.put("Loan.pdf",myPDFMapSource);
 
             //Create an AssemblerOptionsSpec object
             AssemblerOptionSpec assemblerSpec = new AssemblerOptionSpec();
             assemblerSpec.setFailOnError(false);
 
             //Submit the job to Assembler service
             AssemblerResult jobResult = assemblerClient.invokeDDX(myDDX,inputs,assemblerSpec);
             java.util.Map allDocs = jobResult.getDocuments();
 
             //Retrieve the result PDF document from the Map object
             Document outDoc = null;
 
             //Iterate through the map object to retrieve the result XML
             //document that specifies if the input document is
             //PDF/A compliant
             for (Iterator i = allDocs.entrySet().iterator(); i.hasNext();) {
                 // Retrieve the Map object’s value
                 Map.Entry e = (Map.Entry)i.next();
 
                 //Get the key name as specified in the
                 //DDX document
                 String keyName = (String)e.getKey();
                 if (keyName.equalsIgnoreCase("Loan_result.xml"))
                 {
                     //Get the element value
                     Object o = e.getValue();
 
                     //Cast the Object to a Document
                     outDoc = (Document)o;
 
                     //Save the XML file
                     File myMXLFile = new File("C:\\Adobe\result.xml");
                     outDoc.copyToFile(myMXLFile);
                      }
                 }
 
             System.out.println("The results are written to result.xml.");
         }catch (Exception e) {
             e.printStackTrace();
         }
     }
 }
```

## 快速入門（SOAP模式）：使用Java API驗證DDX檔案 {#quick-start-soap-mode-validating-ddx-documents-using-the-java-api}

以下Java程式碼範例會根據名為的檔案來驗證DDX檔案 *bookmarkDDX.xml*. (請參閱 [驗證DDX檔案](/help/forms/developing/assembling-pdf-documents.md#validating-ddx-documents).)

```java
 /*
     * This Java Quick Start uses the SOAP mode and contains the following JAR files
     * in the class path:
     * 1. adobe-assembler-client.jar
     * 2. adobe-livecycle-client.jar
     * 3. adobe-usermanager-client.jar
     * 4. adobe-utilities.jar
     * 5. jboss-client.jar (use a different JAR file if the forms server is not deployed
     * on JBoss)
     * 6. activation.jar (required for SOAP mode)
     * 7. axis.jar (required for SOAP mode)
     * 8. commons-codec-1.3.jar (required for SOAP mode)
     * 9.  commons-collections-3.1.jar  (required for SOAP mode)
     * 10. commons-discovery.jar (required for SOAP mode)
     * 11. commons-logging.jar (required for SOAP mode)
     * 12. dom3-xml-apis-2.5.0.jar (required for SOAP mode)
     * 13. jaxen-1.1-beta-9.jar (required for SOAP mode)
     * 14. jaxrpc.jar (required for SOAP mode)
     * 15. log4j.jar (required for SOAP mode)
     * 16. mail.jar (required for SOAP mode)
     * 17. saaj.jar (required for SOAP mode)
     * 18. wsdl4j.jar (required for SOAP mode)
     * 19. xalan.jar (required for SOAP mode)
     * 20. xbean.jar (required for SOAP mode)
     * 21. xercesImpl.jar (required for SOAP mode)
     *
     * These JAR files are located in the following path:
     * <install directory>/sdk/client-libs/common
     *
     * The adobe-utilities.jar file is located in the following path:
     * <install directory>/sdk/client-libs/jboss
     *
     * The jboss-client.jar file is located in the following path:
     * <install directory>/jboss/bin/client
     *
     * SOAP required JAR files are located in the following path:
     * <install directory>/sdk/client-libs/thirdparty
     *
     * If you want to invoke a remote forms server instance and there is a
     * firewall between the client application and the server, then it is
     * recommended that you use the SOAP mode. When using the SOAP mode,
     * you have to include these additional JAR files
     *
     * For information about the SOAP
     * mode, see "Setting connection properties" in Programming
     * with AEM Forms
     *
     * This quick start validates the following DDX document:
     *&<?xml version="1.0" encoding="UTF-8"?>
     * <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
     * <PDF result="out.pdf">
     * <PDF source="map.pdf" />
     * <PDF source="directions.pdf" />
     * </PDF>
     * </DDX>
     */
 import com.adobe.livecycle.assembler.client.*;
 import java.util.*;
 import java.io.File;
 import java.io.FileInputStream;
 import com.adobe.idp.Document;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 
 public class ValidateDDXSOAP
 {
     public static void main(String[] args) {
 
         boolean isValid = false;
            Document outLog = null;
 
         try{
             //Set connection properties required to invoke AEM Forms
             Properties connectionProps = new Properties();
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 
             //Create a ServiceClientFactory instance
             ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
 
             //Create an AssemblerServiceClient object
             AssemblerServiceClient assemblerClient = new AssemblerServiceClient(myFactory);
 
             //Create a FileInputStream object based on an existing DDX file
             FileInputStream myDDXFile = new FileInputStream("C:\\bookmarkDDX.xml");
 
             //Create a Document object based on the DDX file
             Document myDDX = new Document(myDDXFile);
 
             //Create an AssemblerOptionsSpec object
             AssemblerOptionSpec assemblerSpec = new AssemblerOptionSpec();
             assemblerSpec.setValidateOnly(true);
             assemblerSpec.setLogLevel("FINE");
             assemblerSpec.setFailOnError(false);
 
             //Validate the DDX document
             AssemblerResult jobResult = assemblerClient.invokeDDX(myDDX,null,assemblerSpec);
             outLog = jobResult.getJobLog();
             isValid = true;
 
         }catch (Exception e) {
              if (e instanceof OperationException) {
                     OperationException oe = (OperationException) e;
                     outLog = oe.getJobLog();
                     File myOutFile = new File("C:\\test.xml");
                     outLog.copyToFile(myOutFile);
                 }
              e.printStackTrace();
          } finally {
                if (outLog != null) {
                    File myOutFile = new File("C:\\test.xml");
                    outLog.copyToFile(myOutFile);
               }
           if (isValid) {
                 // do something
           } else {
                // do something else
              }
           }
     }
 }
```

## 快速入門（SOAP模式）：使用Java API以書籤組合PDF檔案 {#quick-start-soap-mode-assembling-pdf-documents-with-bookmarks-using-the-java-api}

以下Java程式碼範例會組合包含書籤的PDF檔案。 DDX檔案的名稱為 *bookmarkDDX.xml*. 書籤XML檔案的名稱是書籤.xml，說明要新增至PDF檔案的書籤。 結果PDF檔案會儲存為名為AssemblerResultBookmarks.pdf的PDF檔案。 (請參閱 [組合含書籤的PDF檔案](/help/forms/developing/assembling-pdf-documents.md#assembling-pdf-documents-with-bookmarks).)

```java
 /*
     * This Java Quick Start uses the SOAP mode and contains the following JAR files
     * in the class path:
     * 1. adobe-assembler-client.jar
     * 2. adobe-livecycle-client.jar
     * 3. adobe-usermanager-client.jar
     * 4. adobe-utilities.jar
     * 5. jboss-client.jar (use a different JAR file if the forms server is not deployed
     * on JBoss)
     * 6. activation.jar (required for SOAP mode)
     * 7. axis.jar (required for SOAP mode)
     * 8. commons-codec-1.3.jar (required for SOAP mode)
     * 9.  commons-collections-3.1.jar  (required for SOAP mode)
     * 10. commons-discovery.jar (required for SOAP mode)
     * 11. commons-logging.jar (required for SOAP mode)
     * 12. dom3-xml-apis-2.5.0.jar (required for SOAP mode)
     * 13. jaxen-1.1-beta-9.jar (required for SOAP mode)
     * 14. jaxrpc.jar (required for SOAP mode)
     * 15. log4j.jar (required for SOAP mode)
     * 16. mail.jar (required for SOAP mode)
     * 17. saaj.jar (required for SOAP mode)
     * 18. wsdl4j.jar (required for SOAP mode)
     * 19. xalan.jar (required for SOAP mode)
     * 20. xbean.jar (required for SOAP mode)
     * 21. xercesImpl.jar (required for SOAP mode)
     *
     * These JAR files are located in the following path:
     * <install directory>/sdk/client-libs/common
     *
     * The adobe-utilities.jar file is located in the following path:
     * <install directory>/sdk/client-libs/jboss
     *
     * The jboss-client.jar file is located in the following path:
     * <install directory>/jboss/bin/client
     *
     * SOAP required JAR files are located in the following path:
     * <install directory>/sdk/client-libs/thirdparty
     *
     * If you want to invoke a remote forms server instance and there is a
     * firewall between the client application and the server, then it is
     * recommended that you use the SOAP mode. When using the SOAP mode,
     * you have to include these additional JAR files
     *
     * For information about the SOAP
     * mode, see "Setting connection properties" in Programming
     * with AEM Forms
     *
     * * This quick start uses the following DDX document:
     * <?xml version="1.0" encoding="UTF-8"?>
     * <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
     * <PDF result="FinalDoc.pdf">
     * <PDF source="Loan.pdf">
     * <Bookmarks source="doc2" />
     * </PDF>
     * </PDF>
     * </DDX>
     *
     * This quick start also uses the following bookmarks XML
     * to assemble a PDF document containing bookmarks:
     * <?xml version="1.0" encoding="UTF-8"?>
     * <Bookmarks xmlns="https://ns.adobe.com/pdf/bookmarks" version="1.0">
     * <Bookmark>
     * <Action>
     * <Launch NewWindow="true">
     * <File Name="C:\Adobe\LoanDetails.pdf" />
     * </Launch>
     * </Action>
     * <Title>Open the Loan document</Title>
     * </Bookmark>
     * <Bookmark>
     * <Action>
     * <Launch>
     * <Win Name="C:\WINDOWS\notepad.exe" />
     * </Launch>
     * </Action>
     * <Title>Launch NotePad</Title>
     * </Bookmark>
     * </Bookmarks>
     *
     */
     import com.adobe.livecycle.assembler.client.*;
 import java.util.*;
 import java.io.File;
 import java.io.FileInputStream;
 import com.adobe.idp.Document;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 
 public class AssembleBookmarksSOAP
 {
     public static void main(String[] args) {
         try{
             //Set connection properties required to invoke AEM Forms using SOAP mode
             Properties connectionProps = new Properties();
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 
             //Create a ServiceClientFactory instance
             ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
 
             //Create an AssemblerServiceClient object
             AssemblerServiceClient assemblerClient = new AssemblerServiceClient(myFactory);
 
             //Create a FileInputStream object based on an existing DDX file
             FileInputStream myDDXFile = new FileInputStream("C:\\bookmarkDDX.xml");
 
             //Create a Document object based on the DDX file
             Document myDDX = new Document(myDDXFile);
 
             //Create a Map object to store an input PDF document and a Bookmark
             //XML document
             Map inputs = new HashMap();
             FileInputStream mySourceMap = new FileInputStream("C:\\Loan.pdf");
             FileInputStream bookmarkInfo = new FileInputStream("C:\\bookmarks.xml");
 
             //Create a Document object based on the Loan.pdf source file
             Document myPDFMapSource = new Document(mySourceMap);
 
             //Create a Document object based on the bookmarks.xml file
             Document myBookmarkXML= new Document(bookmarkInfo);
 
             //Place two entries into the Map object
             inputs.put("Loan.pdf",myPDFMapSource);
             inputs.put("doc2",myBookmarkXML);
 
             //Create an AssemblerOptionsSpec object
             AssemblerOptionSpec assemblerSpec = new AssemblerOptionSpec();
             assemblerSpec.setFailOnError(false);
 
             //Submit the job to Assembler service
             AssemblerResult jobResult = assemblerClient.invokeDDX(myDDX,inputs,assemblerSpec);
             java.util.Map allDocs = jobResult.getDocuments();
 
             //Retrieve the result PDF document from the Map object
             Document outDoc = null;
 
             //Iterate through the map object to retrieve the result PDF document
             for (Iterator i = allDocs.entrySet().iterator(); i.hasNext();) {
                 // Retrieve the Map object’s value
                 Map.Entry e = (Map.Entry)i.next();
 
                 //Get the key name as specified in the
                 //DDX document
                 String keyName = (String)e.getKey();
                 if (keyName.equalsIgnoreCase("FinalDoc.pdf"))
                 {
                     Object o = e.getValue();
                     outDoc = (Document)o;
 
                     //Save the result PDF file
                     File myOutFile = new File("C:\\Adobe\Assembler\Output\AssemblerResultBookmarks.pdf");
                     outDoc.copyToFile(myOutFile);
                 }
             }
         }catch (Exception e) {
             e.printStackTrace();
         }
     }
 }
 
```

## 快速入門（SOAP模式）：使用Java API動態建立DDX檔案 {#quick-start-soap-mode-dynamically-creating-a-ddx-document-using-the-java-api}

以下Java程式碼範例會動態建立可分解PDF檔案的DDX檔案。 系統會為輸入PDF檔案中的每個1級書籤建立新的PDF檔案。 此程式碼範例包含兩個使用者定義的方法：

* `createDDX`：建立 `org.w3c.dom.Document` 物件，代表傳送至Assembler服務的DDX檔案。 這個使用者定義的方法會傳回 `org.w3c.dom.Document` 物件。
* `convertDDX`：轉換 `org.w3c.dom.Document` 物件至 `com.adobe.idp.Document` 物件。 此方法接受 `org.w3c.dom.Document` 物件作為輸入引數並傳回 `com.adobe.idp.Document` 物件。

   這兩個方法都會在此快速入門中叫用。 (請參閱 [動態建立DDX檔案](/help/forms/developing/assembling-pdf-documents.md#dynamically-creating-ddx-documents).) 」

```java
/*
 * This Java Quick Start uses the SOAP mode and contains the following JAR files
 * in the class path:
 * 1. adobe-assembler-client.jar
 * 2. adobe-livecycle-client.jar
 * 3. adobe-usermanager-client.jar
 * 4. adobe-utilities.jar
 * 5. jboss-client.jar (use a different JAR file if the forms server is not deployed
 * on JBoss)
 * 6. activation.jar (required for SOAP mode)
 * 7. axis.jar (required for SOAP mode)
 * 8. commons-codec-1.3.jar (required for SOAP mode)
 * 9. commons-collections-3.1.jar (required for SOAP mode)
 * 10. commons-discovery.jar (required for SOAP mode)
 * 11. commons-logging.jar (required for SOAP mode)
 * 12. dom3-xml-apis-2.5.0.jar (required for SOAP mode)
 * 13. jaxen-1.1-beta-9.jar (required for SOAP mode)
 * 14. jaxrpc.jar (required for SOAP mode)
 * 15. log4j.jar (required for SOAP mode)
 * 16. mail.jar (required for SOAP mode)
 * 17. saaj.jar (required for SOAP mode)
 * 18. wsdl4j.jar (required for SOAP mode)
 * 19. xalan.jar (required for SOAP mode)
 * 20. xbean.jar (required for SOAP mode)
 * 21. xercesImpl.jar (required for SOAP mode)
 *
 * These JAR files are located in the following path:
 * <install directory>/sdk/client-libs/common
 *
 * The adobe-utilities.jar file is located in the following path:
 * <install directory>/sdk/client-libs/jboss
 *
 * The jboss-client.jar file is located in the following path:
 * <install directory>/jboss/bin/client
 *
 * SOAP required JAR files are located in the following path:
 * <install directory>/sdk/client-libs/thirdparty
 *
 * If you want to invoke a remote forms server instance and there is a
 * firewall between the client application and the server, then it is
 * recommended that you use the SOAP mode. When using the SOAP mode,
 * you have to include these additional JAR files
 *
 * For information about the SOAP
 * mode, see "Setting connection properties" in Programming
 * with AEM Forms
 *
 * The following XML represents the DDX document created in this quick start:
 * <?xml version="1.0" encoding="UTF-8"?>
 * <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
 * <PDF result="out.pdf">
 * <PDF source="inDoc"/>
 * <NoXFA/>
 * </PDF>
 * </DDX>
 */
import com.adobe.livecycle.assembler.client.*;
import java.util.*;
import java.io.ByteArrayOutputStream;
import java.io.File;
import java.io.FileInputStream;
import javax.xml.parsers.DocumentBuilder;
import javax.xml.parsers.DocumentBuilderFactory;
import javax.xml.transform.Transformer;
import javax.xml.transform.TransformerFactory;
import javax.xml.transform.dom.DOMSource;
import javax.xml.transform.stream.StreamResult;
import org.w3c.dom.Element;
import com.adobe.idp.Document;
import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
public class AssemblePDFWithDynamicDDXSOAP {
 public static void main(String[] args) {
   try {
    //Set connection properties required to invoke AEM Forms using SOAP mode
    Properties connectionProps = new Properties();
    connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT,
     "https://'[server]:[port]'");
    connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL, ServiceCl ientFactoryProperties.DSC_SOAP_PROTOCOL);
    connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE,
     "JBoss");
    connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME,
     "administrator");
    connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD,
     "password");
    //Create a ServiceClientFactory instance
    ServiceClientFactory myFactory =
     ServiceClientFactory.createInstance(connectionProps);
    //Create an AssemblerServiceClient object
    AssemblerServiceClient assemblerClient = new AssemblerServiceClient(myFactory);
    //Dynamically create a DDX document
    org.w3c.dom.Document myDDX = createDDX();
    //Covert the DDX document to a com.adobe.idp.Document instance
    com.adobe.idp.Document ddx = convertDDX(myDDX);
    //Create a Map object to store PDF source documents
    Map inputs = new HashMap();
    FileInputStream mySourceMap = new FileInputStream("C:\\AssemblerResultPDF.pdf");
    //Create a Document object based on the map.pdf source file
    Document myPDFSource = new Document(mySourceMap);
    //Place the entry into the Map object
    inputs.put("AssemblerResultPDF.pdf", myPDFSource);
    //Create an AssemblerOptionsSpec object
    AssemblerOptionSpec assemblerSpec = new AssemblerOptionSpec();
    assemblerSpec.setFailOnError(false);
    //Submit the job to Assembler service and use the dynamically created DDX document
    AssemblerResult jobResult = assemblerClient.invokeDDX(ddx, inputs, assemblerSpec);
    java.util.Map allDocs = jobResult.getDocuments();
    //Retrieve the result PDF document from the Map object
    Document outDoc = null;
    int index = 1;
    //Iterate through the map object to retrieve the result PDF documents
    for (Iterator i = allDocs.entrySet().iterator(); i.hasNext();) {
     // Retrieve the Map object's value
     Map.Entry e = (Map.Entry) i.next();
     Object o = e.getValue();
     //Cast the Object to a Document
     //and save to a file
     outDoc = (Document) o;
     File myOutFile = new File("C:\\ResultPDF" + index + ".pdf");
     outDoc.copyToFile(myOutFile);
     index++;
    }
   } catch (Exception e) {
    e.printStackTrace();
   }
  }
  //Creates a DDX document using an org.w3c.dom.Document object
 private static org.w3c.dom.Document createDDX() {
   org.w3c.dom.Document document = null;
   try {
    //Create DocumentBuilderFactory and DocumentBuilder objects
    DocumentBuilderFactory factory = DocumentBuilderFactory.newInstance();
    DocumentBuilder builder = factory.newDocumentBuilder();
    //Create a new Document object
    document = builder.newDocument();
    //Create the root element and append it to the XML DOM
    Element root = (Element) document.createElement("DDX");
    root.setAttribute("xmlns", "https://ns.adobe.com/DDX/1.0/");
    document.appendChild(root);
    //Create the PDFsFromBookmarks element
    Element PDFsFromBookmarks =
     (Element) document.createElement("PDFsFromBookmarks");
    PDFsFromBookmarks.setAttribute("prefix", "stmt");
    root.appendChild(PDFsFromBookmarks);
    //Create the PDF element
    Element PDF = (Element) document.createElement("PDF");
    PDF.setAttribute("source", "AssemblerResultPDF.pdf");
    PDFsFromBookmarks.appendChild(PDF);
   } catch (Exception e) {
    System.out.println("The following exception occurred: " + e.getMessage());
   }
   return document;
  }
  //Converts an org.w3c.dom.Document object to a
  //com.adobe.idp.Document object
 private static Document convertDDX(org.w3c.dom.Document myDOM) {
  byte[] mybytes = null;
  try {
   //Create a Java Transformer object
   TransformerFactory transFact = TransformerFactory.newInstance();
   Transformer transForm = transFact.newTransformer();
   //Create a Java ByteArrayOutputStream object
   ByteArrayOutputStream myOutStream = new ByteArrayOutputStream();
   //Create a Java Source object
   javax.xml.transform.dom.DOMSource myInput = new DOMSource(myDOM);
   //Create a Java Result object
   javax.xml.transform.stream.StreamResult myOutput = new StreamResult(myOutStream);
   //Populate the Java ByteArrayOutputStream object
   transForm.transform(myInput, myOutput);
   // Get the size of the ByteArrayOutputStream buffer
   int myByteSize = myOutStream.size();
   //Allocate myByteSize to the byte array
   mybytes = new byte[myByteSize];
   //Copy the content to the byte array
   mybytes = myOutStream.toByteArray();
  } catch (Exception e) {
   System.out.println("The following exception occurred: " + e.getMessage());
  }
  //Create a com.adobe.idp.Document object and copy the
  //contents of the byte array
  Document myDocument = new Document(mybytes);
  return myDocument;
 }
}
```

## 快速入門（SOAP模式）：使用Java API組合PDFPortfolio {#quick-start-soap-mode-assembling-pdf-portfolios-using-the-java-api}

以下Java程式碼範例會建立PDF投資組合。 PDF產品組合會儲存為名為的PDF檔案 *AssemblerResultPortfolio.pdf*. (請參閱 [組裝PDFPortfolio](/help/forms/developing/assembling-pdf-documents.md#assembling-pdf-portfolios).)

```java
 /*
     * This Java Quick Start uses the SOAP mode and contains the following JAR files
     * in the class path:
     * 1. adobe-assembler-client.jar
     * 2. adobe-livecycle-client.jar
     * 3. adobe-usermanager-client.jar
     * 4. adobe-utilities.jar
     * 5. jboss-client.jar (use a different JAR file if the forms server is not deployed
     * on JBoss)
     *
     * These JAR files are located in the following path:
     * <install directory>/sdk/client-libs/common
     *
     * The adobe-utilities.jar file is located in the following path:
     * <install directory>/sdk/client-libs/jboss
     *
     * The jboss-client.jar file is located in the following path:
     * <install directory>/jboss/bin/client
     *
     * SOAP required JAR files are located in the following path:
     * <install directory>/sdk/client-libs/thirdparty
     *
     * If you want to invoke a remote forms server instance and there is a
     * firewall between the client application and the server, then it is
     * recommended that you use the SOAP mode. When using the SOAP mode,
     * you have to include these additional JAR files
     *
     * For information about the SOAP
     * mode, see "Setting connection properties" in Programming
     * with AEM Forms
     *
     * This is the DDX file used to create a PDF portfolio:
     * <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
     * <PDF result="portfolio1.pdf">
     * <Portfolio>
     * <Navigator source="myNavigator">
     * <Resource name="navigator/image.xxx" source="myImage.png"/>
     * </Navigator>
     * </Portfolio>
     * <PackageFiles source="dog1"  >
     * <FieldData name="X">72</FieldData>
     * <FieldData name="Y">72</FieldData>
     * <File filename="saint_bernard.jpg" mimetype="image/jpeg"/>
     * </PackageFiles>
     * <PackageFiles source="dog2"  >
     * <FieldData name="X">120</FieldData>
     * <FieldData name="Y">216</FieldData>
     * <File filename="greyhound.pdf"/>
     * </PackageFiles>
     * </PDF>
     * </DDX>
     */
 import com.adobe.livecycle.assembler.client.*;
 
 import java.util.*;
 import java.io.File;
 import java.io.FileInputStream;
 import com.adobe.idp.Document;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 
 public class CreatePDFPortfolioSOAP {
     public static void main(String[] args) {
         try{
             //Set connection properties required to invoke AEM Forms
             Properties connectionProps = new Properties();
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 
             //Create a ServiceClientFactory instance
             ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
 
             //Create an AssemblerServiceClient object
             AssemblerServiceClient assemblerClient = new AssemblerServiceClient(myFactory);
 
             //Create a FileInputStream object based on an existing DDX file
             FileInputStream myDDXFile = new FileInputStream("C:\\Adobe\portfolioAssembly.xml");
             FileInputStream myNavFile = new FileInputStream("C:\\Adobe\AdobeOnImage.nav");
 
             //Create a Document object based on the DDX file
             Document myDDX = new Document(myDDXFile);
             Document myNav = new Document(myNavFile);
 
             //Create a Map object to store PDF source documents
             Map<String,Object> input = new HashMap<String, Object>();
             FileInputStream mySourceNavImage = new FileInputStream("C:\\Adobe\myImage.png");
             FileInputStream mySourceDog1 = new FileInputStream("C:\\Adobe\saint_bernard.jpg");
             FileInputStream mySourceDog2 = new FileInputStream("C:\\Adobe\greyhound.pdf");
 
             //Create a Document object based on the myImage.png source file
             Document myPDFNavImageSource = new Document(mySourceNavImage);
 
             //Create a Document object based on the MyFirstFile.pdf source file
             Document myPDFDog1Source = new Document(mySourceDog1);
 
             //Create a Document object based on the MySecondFile.txt source file
             Document myPDFDog2Source = new Document(mySourceDog2);
 
             //Place two entries into the Map object
             input.put("myNavigator", myNav);
             input.put("myImage.png",myPDFNavImageSource);
             input.put("dog1",myPDFDog1Source);
             input.put("dog2",myPDFDog2Source);
 
             //Create an AssemblerOptionsSpec object
             AssemblerOptionSpec assemblerSpec = new AssemblerOptionSpec();
             assemblerSpec.setFailOnError(false);
 
             //Submit the job to Assembler service
             AssemblerResult jobResult = assemblerClient.invokeDDX(myDDX,input,assemblerSpec);
             Map<String,Document> allDocs = jobResult.getDocuments();
 
             //Retrieve the result PDF document from the Map object
             Document outDoc = null;
 
             //Iterate through the map object to retrieve the result PDF document
             for (Iterator<Map.Entry<String,Document>> i = allDocs.entrySet().iterator(); i.hasNext();) {
                 // Retrieve the Map object?s value
                 Map.Entry<String,Document> e = (Map.Entry<String,Document>)i.next();
 
                 //Get the key name as specified in the
                 //DDX document
                 String keyName = (String)e.getKey();
                 if (keyName.equalsIgnoreCase("portfolio1.pdf"))
                 {
                     Object o = e.getValue();
                     outDoc = (Document)o;
 
                     //Save the result PDF file
                     File myOutFile = new File("C:\\Adobe\AssemblerResultPortfolio.pdf");
                     outDoc.copyToFile(myOutFile);
                 }
             }
 
         }catch (Exception e) {
             e.printStackTrace();
         }
     }
 }
 
 
```

## 快速入門（SOAP模式）：使用Java API組裝多個XDP片段 {#quick-start-soap-mode-assembling-multiple-xdp-fragments-using-the-java-api}

以下Java程式碼範例會組合以下列XDP檔案為基礎的XDP片段： *tuc018_template_flowed.xdp*， *tuc018_contact.xdp*，和* tuc018_patient.xdp*。 包含所有片段的組合XDP檔案會儲存為名為的XDP檔案 *AssemblerResultXDP.xdp*. (請參閱 [組合多個XDP片段](/help/forms/developing/assembling-pdf-documents.md#assembling-multiple-xdp-fragments).)

```java
 /*
     * This Java Quick Start uses the SOAP mode and contains the following JAR files
     * in the class path:
     * 1. adobe-assembler-client.jar
     * 2. adobe-livecycle-client.jar
     * 3. adobe-usermanager-client.jar
     * 4. adobe-utilities.jar
     * 5. jboss-client.jar (use a different JAR file if the forms server is not deployed
     * on JBoss)
     * 6. activation.jar (required for SOAP mode)
     * 7. axis.jar (required for SOAP mode)
     * 8. commons-codec-1.3.jar (required for SOAP mode)
     * 9.  commons-collections-3.1.jar  (required for SOAP mode)
     * 10. commons-discovery.jar (required for SOAP mode)
     * 11. commons-logging.jar (required for SOAP mode)
     * 12. dom3-xml-apis-2.5.0.jar (required for SOAP mode)
     * 13. jaxen-1.1-beta-9.jar (required for SOAP mode)
     * 14. jaxrpc.jar (required for SOAP mode)
     * 15. log4j.jar (required for SOAP mode)
     * 16. mail.jar (required for SOAP mode)
     * 17. saaj.jar (required for SOAP mode)
     * 18. wsdl4j.jar (required for SOAP mode)
     * 19. xalan.jar (required for SOAP mode)
     * 20. xbean.jar (required for SOAP mode)
     * 21. xercesImpl.jar (required for SOAP mode)
     *
     * These JAR files are located in the following path:
     * <install directory>/sdk/client-libs/common
     *
     * The adobe-utilities.jar file is located in the following path:
     * <install directory>/sdk/client-libs/jboss
     *
     * The jboss-client.jar file is located in the following path:
     * <install directory>/jboss/bin/client
     *
     * SOAP required JAR files are located in the following path:
     * <install directory>/sdk/client-libs/thirdparty
     *
     * If you want to invoke a remote forms server instance and there is a
     * firewall between the client application and the server, then it is
     * recommended that you use the SOAP mode. When using the SOAP mode,
     * you have to include these additional JAR files
     *
     * For information about the SOAP
     * mode, see "Setting connection properties" in Programming
     * with AEM Forms
     *
     * The following XML represents the DDX document used in this quick start:
     * <?xml version="1.0" encoding="UTF-8"?>
     * <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
     * <XDP result="tuc018result.xdp">
     * <XDP source="tuc018_template_flowed.xdp">
     * <XDPContent insertionPoint="ddx_fragment" source="tuc018_contact.xdp" fragment="subPatientContact" required="false"/>
     * <XDPContent insertionPoint="ddx_fragment" source="tuc018_patient.xdp" fragment="subPatientPhysical" required="false"/>
     * <XDPContent insertionPoint="ddx_fragment" source="tuc018_patient.xdp" fragment="subPatientHealth" required="false"/>
     * </XDP>
     * </XDP>
     * </DDX>
     */
 import com.adobe.livecycle.assembler.client.*;
 import java.util.*;
 import java.io.File;
 import java.io.FileInputStream;
 import com.adobe.idp.Document;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 
 public class AssembleFragmentsSOAP
 {
     public static void main(String[] args) {
         try{
             //Set connection properties required to invoke AEM Forms
             Properties connectionProps = new Properties();
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 
             //Create a ServiceClientFactory instance
             ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
 
             //Create an AssemblerServiceClient object
             AssemblerServiceClient assemblerClient = new AssemblerServiceClient(myFactory);
 
             //Create a FileInputStream object based on an existing DDX file
             FileInputStream myDDXFile = new FileInputStream("C:\\Adobe\fragmentDDX.xml");
 
             //Create a Document object based on the DDX file
             Document myDDX = new Document(myDDXFile);
 
             //Create a Map object to store the input XDP files
             Map inputs = new HashMap();
             FileInputStream inSource = new FileInputStream("C:\\Adobe\tuc018_template_flowed.xdp");
             FileInputStream inFragment1 = new FileInputStream("C:\\Adobe\tuc018_contact.xdp");
             FileInputStream inFragment2 = new FileInputStream("C:\\Adobe\tuc018_patient.xdp");
 
             //Create a Document object
             Document myMapSource = new Document(inSource);
 
             //Create a Document object
             Document inFragment1Doc = new Document(inFragment1);
 
             //Create a Document object
             Document inFragment2Doc = new Document(inFragment2);
 
             //Place all of the XDP files into the MAP
             inputs.put("tuc018_template_flowed.xdp",myMapSource);
             inputs.put("tuc018_contact.xdp",inFragment1Doc);
             inputs.put("tuc018_patient.xdp",inFragment2Doc);
 
 
             //Create an AssemblerOptionsSpec object
             AssemblerOptionSpec assemblerSpec = new AssemblerOptionSpec();
             assemblerSpec.setFailOnError(false);
 
             //Submit the job to Assembler service
             AssemblerResult jobResult = assemblerClient.invokeDDX(myDDX,inputs,assemblerSpec);
             java.util.Map allDocs = jobResult.getDocuments();
 
             //Retrieve the result PDF document from the Map object
             Document outDoc = null;
 
             //Iterate through the map object to retrieve the result XDP document
             for (Iterator i = allDocs.entrySet().iterator(); i.hasNext();) {
                 // Retrieve the Map object’s value
                 Map.Entry e = (Map.Entry)i.next();
 
                 //Get the key name as specified in the
                 //DDX document
                 String keyName = (String)e.getKey();
                 if (keyName.equalsIgnoreCase("tuc018result.xdp"))
                 {
                     Object o = e.getValue();
                     outDoc = (Document)o;
 
                     //Save the result XDP file
                     File myOutFile = new File("C:\\AssemblerResultXDP.xdp");
                     outDoc.copyToFile(myOutFile);
                 }
             }
         }catch (Exception e) {
             e.printStackTrace();
         }
     }
 }
```

## 快速入門（SOAP模式）：使用Java API編輯PDF檔案 {#quick-start-soap-mode-redacting-a-pdf-document-using-the-java-api}

下列程式碼範例會使用以下對PDF檔案進行編譯 `PDFUtility`.

>[!NOTE]
>
>`PDFUtility` 只能密文那些使用Acrobat標示為要密文的PDF。

```java
/*
 * This Java Quick Start uses the SOAP mode and contains the following JAR files
 * in the class path:
 * 1. adobe-pdfutility-client.jar
 * 2. adobe-livecycle-client.jar
 * 3. adobe-usermanager-client.jar
 * 4. adobe-utilities.jar
 * 5. jboss-client.jar (use a different JAR file if AEM Forms is not deployed
 * on JBoss)
 *
 * These JAR files are located in the following path:
 * <install directory>/Adobe/Adobe_Experience_Manager_forms/sdk/client-libs/common
 *
 * The adobe-utilities.jar file is located in the following path:
 * <install directory>/Adobe/Adobe_Experience_Manager_forms/sdk/client-libs/jboss
 *
 * The jboss-client.jar file is located in the following path:
 * <install directory>/Adobe/Adobe_Experience_Manager_forms/jboss/bin/client
 *
 * If you want to invoke a remote AEM Forms instance and there is a
 * firewall between the client application and AEM Forms, then it is
 * recommended that you use the SOAP mode. When using the SOAP mode,
 * you have to include additional JAR files located in the following
 * path
 * <install directory>/Adobe/Adobe_Experience_Manager_forms/sdk/client-libs/thirdparty
 *
 * For information about the SOAP
 * mode and the additional JAR files that need to be included,
 * see "Setting connection properties" in Programming
 * with AEM Forms
 *
 * For complete details about the location of the AEM Forms JAR files,
 * see "Including AEM Forms library files" in Programming
 * with AEM Forms
 */

import java.util.*;
import com.adobe.livecycle.pdfutility.client.*;
import java.io.*;
import com.adobe.idp.Document;
import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;

public class RedactPDF
{
    public static void main(String[] args)
    {
        try
        {
            //Set connection properties required to invoke AEM Forms
            Properties connectionProps = new Properties();
            connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
            connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
            connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
            connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
            connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");

            // Create a ServiceClientFactory object
            ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);

            // Create a PDF Utility client
            PDFUtilityServiceClient pdfUt = new PDFUtilityServiceClient(myFactory);

            // Specify a PDF document to Redact
            FileInputStream fileInputStream = new FileInputStream("C:\\Adobe\\RedactMarked.pdf");
            Document inDoc = new Document(fileInputStream);
            RedactionOptionSpec spec = new RedactionOptionSpec();

            // Convert the PDF document to redact
            RedactionResult redRes = pdfUt.redact(inDoc,spec);

            Document redactPDF = redRes.getDocument();

            //Save the returned Document object as an XDP file
            File redactedFile = new File("C:\\Adobe\\Redacted.pdf");
            redactPDF.copyToFile(redactedFile);
        }
        catch (Exception e)
        {
            e.printStackTrace();
        }
    }
}
```
