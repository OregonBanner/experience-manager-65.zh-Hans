---
title: PDF公用程式服務Java API快速啟動(SOAP)
seo-title: PDF Utilities Service Java APIQuick Start(SOAP)
description: 使用「PDF公用程式」服務將PDF檔案轉換為XDP檔案、將XDP檔案轉換為PDF檔案、擷取PDF檔案屬性、設定PDF檔案的儲存樣式，以及整理PDF檔案。
seo-description: Use the PDF Utilities service to convert a PDF document to an XDP document, convert an XDP document to a PDF document, retrieve PDF document properties, setting the save style for a PDF document, and sanitize PDF documents.
uuid: 96bb2bd5-b274-43d4-a664-49cc1c526b3f
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: 4ec4c674-d7d3-4988-9d77-78d274970672
role: Developer
exl-id: e861d848-b0b7-4ae9-a56d-c0957ec95730
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '458'
ht-degree: 0%

---

# PDF公用程式服務Java API快速入門(SOAP) {#pdf-utilities-service-java-apiquick-start-soap}

下列「快速啟動」適用於「PDF公用程式」服務。

[快速入門（SOAP模式）：使用Java API將PDF檔案轉換為XDP檔案](pdf-utilities-service-java-api.md#quick-start-soap-mode-converting-a-pdf-document-to-an-xdp-document-using-the-java-api)

[快速入門（SOAP模式）：使用Java API將XDP檔案轉換為PDF檔案](pdf-utilities-service-java-api.md#quick-start-soap-mode-converting-an-xdp-document-to-a-pdf-document-using-the-java-api)

[快速入門（SOAP模式）：使用Java API擷取PDF檔案屬性](pdf-utilities-service-java-api.md#quick-start-soap-mode-retrieving-pdf-document-properties-using-the-java-api)

[快速入門（SOAP模式）：使用Java API設定PDF檔案的儲存樣式](pdf-utilities-service-java-api.md#quick-start-soap-mode-setting-the-save-style-for-a-pdf-document-using-the-java-api)

[快速入門（SOAP模式）：清除PDF檔案](pdf-utilities-service-java-api.md#quick-start-soap-mode-sanitizing-pdf-documents)

AEM Forms作業可使用AEM Forms強型別API執行，且連線模式應設定為SOAP。

>[!NOTE]
>
>「使用AEM表單進行程式設計」中的「快速入門」是以Forms Server作業系統為基礎。 不過，如果您使用其他作業系統（例如UNIX），請以適用的作業系統支援的路徑取代Windows特定路徑。 同樣地，如果您使用其他J2EE應用程式伺服器，請務必指定有效的連線屬性。 另請參閱 [設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).

## 快速入門（SOAP模式）：使用Java API將PDF檔案轉換為XDP檔案 {#quick-start-soap-mode-converting-a-pdf-document-to-an-xdp-document-using-the-java-api}

下列程式碼範例會將PDF檔案轉換為XDP檔案。 (請參閱 [將PDF檔案轉換為XDP檔案](/help/forms/developing/pdf-utilities.md#converting-pdf-documents-into-xdp-documents).

```java
 /*
     * This Java Quick Start uses the SOAP mode and contains the following JAR files
     * in the class path:
     * 1. adobe-pdfutility-client.jar
     * 2. adobe-livecycle-client.jar
     * 3. adobe-usermanager-client.jar
    * 4. activation.jar (required for SOAP mode)
    * 5. axis.jar (required for SOAP mode)
    * 6. commons-codec-1.3.jar (required for SOAP mode)
    * 7. commons-collections-3.2.jar  (required for SOAP mode)
    * 8. commons-discovery.jar (required for SOAP mode)
    * 9. commons-logging.jar (required for SOAP mode)
    * 10. dom3-xml-apis-2.5.0.jar (required for SOAP mode)
    * 11. jaxen-1.1-beta-9.jar (required for SOAP mode)
    * 12. jaxrpc.jar (required for SOAP mode)
    * 13. log4j.jar (required for SOAP mode)
    * 14. mail.jar (required for SOAP mode)
    * 15. saaj.jar (required for SOAP mode)
    * 16. wsdl4j.jar (required for SOAP mode)
    * 17. xalan.jar (required for SOAP mode)
    * 18. xbean.jar (required for SOAP mode)
    * 19. xercesImpl.jar (required for SOAP mode)
     *
     * The JBoss files must be kept in the jboss\client folder. You can copy the client folder to
     * your local development environment and then include the 3 JBoss JAR files in your class path
     *
     * These JAR files are located in the following path:
     * <install directory>/sdk/client-libs/common
     *
     *
     * <install directory>/jboss/bin/client
     *
     * If you want to invoke a remote forms server instance and there is a
     * firewall between the client application and the server, then it is
     * recommended that you use the SOAP mode. When using the SOAP mode,
     * you have to include additional JAR files located in the following
     * path
     * <install directory>/sdk/client-libs/thirdparty
     *
     * For information about the SOAP
     * mode and the additional JAR files that need to be included,
     * see "Setting connection properties" in Programming
     * with AEM Forms
     *
     * For complete details about the location of the AEM Forms JAR files,
     * see "Including AEM Forms Java library files" in Programming
     * with AEM Forms
     */
 
 import java.util.*;
 import com.adobe.livecycle.pdfutility.client.*;
 import java.io.*;
 import com.adobe.idp.Document;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 
 public class ConvertPDFToXDP
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
 
             // Specify a PDF document to convert to an XDP file
             FileInputStream fileInputStream = new FileInputStream("C:\\Adobe\Loan.pdf");
             Document inDoc = new Document(fileInputStream);
 
             // Convert the PDF document to an XDP file
             Document myXDP = pdfUt.convertPDFtoXDP(inDoc);
 
             //Save the returned Document object as an XDP file
             File xdpFile = new File("C:\\Adobe\Loan.xdp");
             myXDP.copyToFile(xdpFile);
         }
         catch (Exception e)
         {
             e.printStackTrace();
         }
     }
 }
 
```

## 快速入門（SOAP模式）：使用Java API將XDP檔案轉換為PDF檔案 {#quick-start-soap-mode-converting-an-xdp-document-to-a-pdf-document-using-the-java-api}

下列程式碼範例會將XDP檔案轉換為PDF檔案。 (請參閱 [將XDP檔案轉換為PDF檔案](/help/forms/developing/pdf-utilities.md#converting-xdp-documents-into-pdf-documents).)

```java
 /*
     * This Java Quick Start uses the SOAP mode and contains the following JAR files
     * in the class path:
     * 1. adobe-pdfutility-client.jar
     * 2. adobe-livecycle-client.jar
     * 3. adobe-usermanager-client.jar
    * 4. activation.jar (required for SOAP mode)
    * 5. axis.jar (required for SOAP mode)
    * 6. commons-codec-1.3.jar (required for SOAP mode)
    * 7. commons-collections-3.2.jar  (required for SOAP mode)
    * 8. commons-discovery.jar (required for SOAP mode)
    * 9. commons-logging.jar (required for SOAP mode)
    * 10. dom3-xml-apis-2.5.0.jar (required for SOAP mode)
    * 11. jaxen-1.1-beta-9.jar (required for SOAP mode)
    * 12. jaxrpc.jar (required for SOAP mode)
    * 13. log4j.jar (required for SOAP mode)
    * 14. mail.jar (required for SOAP mode)
    * 15. saaj.jar (required for SOAP mode)
    * 16. wsdl4j.jar (required for SOAP mode)
    * 17. xalan.jar (required for SOAP mode)
    * 18. xbean.jar (required for SOAP mode)
    * 19. xercesImpl.jar (required for SOAP mode)
     *
     * The JBoss files must be kept in the jboss\client folder. You can copy the client folder to
     * your local development environment and then include the 3 JBoss JAR files in your class path
     *
     * These JAR files are located in the following path:
     * <install directory>/sdk/client-libs/common
     *
     *
     * <install directory>/jboss/bin/client
     *
     * If you want to invoke a remote forms server instance and there is a
     * firewall between the client application and the server, then it is
     * recommended that you use the SOAP mode. When using the SOAP mode,
     * you have to include additional JAR files located in the following
     * path
     * <install directory>/sdk/client-libs/thirdparty
     *
     * For information about the SOAP
     * mode and the additional JAR files that need to be included,
     * see "Setting connection properties" in Programming
     * with AEM Forms
     *
     * For complete details about the location of the AEM Forms JAR files,
     * see "Including AEM Forms Java library files" in Programming
     * with AEM Forms
     */
 import com.adobe.livecycle.pdfutility.client.*;
 import java.util.*;
 import java.io.*;
 import com.adobe.idp.Document;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 
 public class ConvertXDPToPDF
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
 
             // Specify an XDP file to convert to a PDF document
             FileInputStream fileInputStream = new FileInputStream("C:\\Adobe\Loan.xdp");
             Document inDoc = new Document(fileInputStream);
 
             // Convert the XDP file to a PDF document
             Document myPDF = pdfUt.convertXDPtoPDF(inDoc);
 
             //Save the returned Document object as a PDF file
             File pdfFile = new File("C:\\Adobe\Loan.pdf");
             myPDF.copyToFile(pdfFile);
         }
         catch (Exception e)
         {
             e.printStackTrace();
         }
     }
 }
 
```

## 快速入門（SOAP模式）：使用Java API擷取PDF檔案屬性 {#quick-start-soap-mode-retrieving-pdf-document-properties-using-the-java-api}

下列程式碼範例會判斷檔案是否為PDF檔案，若是，則為能夠讀取該檔案的最早Acrobat版本。 (請參閱 [正在擷取PDF檔案屬性](/help/forms/developing/pdf-utilities.md#retrieving-pdf-document-properties).)

```java
 /*
     * This Java Quick Start uses the SOAP mode and contains the following JAR files
     * in the class path:
     * 1. adobe-pdfutility-client.jar
     * 2. adobe-livecycle-client.jar
     * 3. adobe-usermanager-client.jar
     * 4. activation.jar (required for SOAP mode)
     * 5. axis.jar (required for SOAP mode)
     * 6. commons-codec-1.3.jar (required for SOAP mode)
     * 7. commons-collections-3.2.jar  (required for SOAP mode)
     * 8. commons-discovery.jar (required for SOAP mode)
     * 9. commons-logging.jar (required for SOAP mode)
     * 10. dom3-xml-apis-2.5.0.jar (required for SOAP mode)
     * 11. jaxen-1.1-beta-9.jar (required for SOAP mode)
     * 12. jaxrpc.jar (required for SOAP mode)
     * 13. log4j.jar (required for SOAP mode)
     * 14. mail.jar (required for SOAP mode)
     * 15. saaj.jar (required for SOAP mode)
     * 16. wsdl4j.jar (required for SOAP mode)
     * 17. xalan.jar (required for SOAP mode)
     * 18. xbean.jar (required for SOAP mode)
     * 19. xercesImpl.jar (required for SOAP mode)
     *
     * The JBoss files must be kept in the jboss\client folder. You can copy the client folder to
     * your local development environment and then include the 3 JBoss JAR files in your class path
     *
     * These JAR files are located in the following path:
     * <install directory>/sdk/client-libs/common
     *
     *
     * <install directory>/jboss/bin/client
     *
     * If you want to invoke a remote forms server instance and there is a
     * firewall between the client application and the server, then it is
     * recommended that you use the SOAP mode. When using the SOAP mode,
     * you have to include additional JAR files located in the following
     * path
     * <install directory>/sdk/client-libs/thirdparty
     *
     * For information about the SOAP
     * mode and the additional JAR files that need to be included,
     * see "Setting connection properties" in Programming
     * with AEM Forms
     *
     * For complete details about the location of the AEM Forms JAR files,
     * see "Including AEM Forms Java library files" in Programming
     * with AEM Forms
     */
 import com.adobe.livecycle.pdfutility.client.*;
 import java.util.*;
 import java.io.*;
 import com.adobe.idp.Document;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 
 public class RetrievePDFProperties
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
 
             // Specify a document whose properties are retrieved
             FileInputStream fileInputStream = new FileInputStream("C:\\Adobe\Loan.pdf");
             Document inDoc = new Document(fileInputStream);
 
             // Create a properties options specification
             PDFPropertiesOptionSpec optionsSpec = new PDFPropertiesOptionSpec();
 
             // Set the properties to be evaluated in the options specification.
             // In this example, the options specification will be used to determine
             // if the document is a PDF document, and if so,
             // which Acrobat version is required to read it.
             optionsSpec.setIsPDFDocument(true);
             optionsSpec.setQueryRequiredAcrobatVersion(true);
 
             // Perform the query and retrieve the document properties
             PDFPropertiesResult propertiesResult = pdfUt.getPDFProperties(inDoc, optionsSpec);
 
             // Inspect the result and determine whether the file is a PDF document
             if (propertiesResult.getIsPDFDocument().booleanValue())
             {
                 System.out.println("Loan.pdf has been verified to be a PDF document.");
 
                 // Determine the required Acrobat version for reading the document
                 String acrobatVersion = propertiesResult.getRequiredAcrobatVersion();
                 System.out.println("The required Acrobat version is: " + acrobatVersion);
             }
         }
         catch (Exception e)
         {
             System.out.println("Error occurred: " + e.getMessage());
         }
     }
 }
 
 
```

## 快速入門（SOAP模式）：使用Java API設定PDF檔案的儲存樣式 {#quick-start-soap-mode-setting-the-save-style-for-a-pdf-document-using-the-java-api}

下列程式碼範例會設定快速檢視Web的儲存模式，然後將PDF檔案傳遞給加密服務，並在其中進行加密。 為了快速檢視網頁而儲存的加密PDF檔案會儲存為名為* FastWebViewLoan.pdf*的PDF檔案。 (請參閱 [設定PDF檔案儲存模式](/help/forms/developing/pdf-utilities.md#setting-pdf-document-save-modes).)

```java
 /*
     * This Java Quick Start uses the SOAP mode and contains the following JAR files
     * in the class path:
     * 1. adobe-pdfutility-client.jar
     * 2. adobe-livecycle-client.jar
     * 3. adobe-usermanager-client.jar
     * 4. activation.jar (required for SOAP mode)
     * 5. axis.jar (required for SOAP mode)
     * 6. commons-codec-1.3.jar (required for SOAP mode)
     * 7. commons-collections-3.2.jar  (required for SOAP mode)
     * 8. commons-discovery.jar (required for SOAP mode)
     * 9. commons-logging.jar (required for SOAP mode)
     * 10. dom3-xml-apis-2.5.0.jar (required for SOAP mode)
     * 11. jaxen-1.1-beta-9.jar (required for SOAP mode)
     * 12. jaxrpc.jar (required for SOAP mode)
     * 13. log4j.jar (required for SOAP mode)
     * 14. mail.jar (required for SOAP mode)
     * 15. saaj.jar (required for SOAP mode)
     * 16. wsdl4j.jar (required for SOAP mode)
     * 17. xalan.jar (required for SOAP mode)
     * 18. xbean.jar (required for SOAP mode)
     * 19. xercesImpl.jar (required for SOAP mode)
     *
     * The JBoss files must be kept in the jboss\client folder. You can copy the client folder to
     * your local development environment and then include the 3 JBoss JAR files in your class path
     *
     * These JAR files are located in the following path:
     * <install directory>/sdk/client-libs/common
     *
     *
     * <install directory>/jboss/bin/client
     *
     * If you want to invoke a remote forms server instance and there is a
     * firewall between the client application and the server, then it is
     * recommended that you use the SOAP mode. When using the SOAP mode,
     * you have to include additional JAR files located in the following
     * path
     * <install directory>/sdk/client-libs/thirdparty
     *
     * For information about the SOAP
     * mode and the additional JAR files that need to be included,
     * see "Setting connection properties" in Programming
     * with AEM Forms
     *
     * For complete details about the location of the AEM Forms JAR files,
     * see "Including AEM Forms Java library files" in Programming
     * with AEM Forms
     */
 import com.adobe.livecycle.encryption.client.EncryptionServiceClient;
 import com.adobe.livecycle.encryption.client.PasswordEncryptionCompatability;
 import com.adobe.livecycle.encryption.client.PasswordEncryptionOption;
 import com.adobe.livecycle.encryption.client.PasswordEncryptionOptionSpec;
 import com.adobe.livecycle.encryption.client.PasswordEncryptionPermission;
 import com.adobe.livecycle.pdfutility.client.*;
 import java.util.*;
 import java.io.*;
 import com.adobe.idp.Document;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 
 public class SaveDocument
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
 
             // Specify a document to be saved
             FileInputStream fileInputStream = new FileInputStream("C:\\Adobe\Loan.pdf");
             Document inDoc = new Document(fileInputStream);
 
             // Specify the save option
             PDFUtilitySaveMode saveMode = new PDFUtilitySaveMode();
             saveMode.setSaveStyle("FAST_WEB_VIEW");
             Document outFastWebView = pdfUt.setSaveMode(inDoc, saveMode, true);
 
             //Pass the document that is saved as 'Fast
             //Web View'  to the Encryption service
             EncryptionServiceClient encryptClient = new EncryptionServiceClient(myFactory);
 
             //Create a PasswordEncryptionOptionSpec object that
             //stores encryption run-time values
             PasswordEncryptionOptionSpec passSpec = new PasswordEncryptionOptionSpec();
 
             //Specify the PDF document resource to encrypt
             passSpec.setEncryptOption(PasswordEncryptionOption.ALL);
 
             //Specify the permission associated with the password
             List encrypPermissions = new ArrayList();
             encrypPermissions.add(PasswordEncryptionPermission.PASSWORD_EDIT_EXTRACT);
             encrypPermissions.add(PasswordEncryptionPermission.PASSWORD_EDIT_FORM_FILL);
             passSpec.setPermissionsRequested(encrypPermissions);
 
             //Specify the Acrobat version
             passSpec.setCompatability(PasswordEncryptionCompatability.ACRO_7);
 
             //Specify the password values
             passSpec.setDocumentOpenPassword("OpenPassword");
             passSpec.setPermissionPassword("PermissionPassword");
 
             //Encrypt the PDF document
             Document encryptDoc = encryptClient.encryptPDFUsingPassword(inDoc,passSpec);
 
             //Save the encrypted document that is saved as FAST_WEB_VIEW
             //as a PDF file named FastWebViewLoan.pdf
             File pdfFile = new File("C:\\Adobe\FastWebViewLoan.pdf");
             encryptDoc.copyToFile(pdfFile);
 
             // Inspect the document?s save option
             PDFUtilitySaveMode verifySaveMode = pdfUt.getSaveMode(outFastWebView);
             String verifySaveStyle = verifySaveMode.getSaveStyle();
             System.out.println("The save mode is " + verifySaveStyle);
         }
         catch (Exception e)
         {
             System.out.println("Error occurred: " + e.getMessage());
         }
     }
 }
 
```

## 快速入門（SOAP模式）：使用Java API將檔案轉換為PDF/A-2b檔案 {#quick-start-soap-mode-converting-a-document-to-a-pdf-a-2b-document-using-the-java-api}

以下Java程式碼範例會轉換名為的PDF檔案 *Loan.pdf* 至儲存為名為之PDF檔案的PDF/A-2b檔案 *LoanArchive.pdf*. (請參閱 [將檔案轉換為PDF/A檔案](/help/forms/developing/pdf-a-documents.md#converting-documents-to-pdf-a-documents).)

```java
/*
 * This Java Quick Start uses the SOAP mode and contains the following JAR files
 * in the class path:
 * 1. adobe-docconverter-client.jar
 * 2. adobe-livecycle-client.jar
 * 3. adobe-usermanager-client.jar
 *
 * These JAR files are located in the following path:
 * <install directory>/Adobe/Adobe_Experience_Manager_forms/sdk/client-libs/common
 *
 * <install directory>/Adobe/Adobe_Experience_Manager_forms/sdk/client-libs/jboss
 *
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
import java.io.File;
import java.io.FileInputStream;
import com.adobe.idp.Document;
import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
import com.adobe.livecycle.docconverter.client.DocConverterServiceClient;
import com.adobe.livecycle.docconverter.client.PDFAConversionOptionSpec;
import com.adobe.livecycle.docconverter.client.PDFAConversionResult;
import com.adobe.livecycle.docconverter.client.PDFAConversionOptionSpec.Compliance;

public class CreatePDFADocument {

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

        //Create a DocConverterServiceClient object
        DocConverterServiceClient docConverter = new DocConverterServiceClient(myFactory);

        //Reference a PDF document to convert to a PDF/A document
        FileInputStream myPDF = new FileInputStream("C:\\Adobe\\Loan.pdf");
        Document inDoc = new Document(myPDF);

        //Create a PDFAConversionOptionSpec object and set
        //tracking information
        PDFAConversionOptionSpec spec = new PDFAConversionOptionSpec();
        spec.setLogLevel("FINE");
        spec.setCompliance(Compliance.PDFA_2B);

        //Convert the PDF document to a PDF/A document
        PDFAConversionResult result =  docConverter.toPDFA(inDoc,spec);

        //Save the PDF/A file
        Document pdfADoc= result.getPDFADocument();
        File pdfAFile = new File("C:\\Adobe\\LoanArchive.pdf");
        pdfADoc.copyToFile(pdfAFile);
   }catch (Exception e) {
        e.printStackTrace();
    }
  }
}
```

## 快速入門（SOAP模式）：清除PDF檔案 {#quick-start-soap-mode-sanitizing-pdf-documents}

以下Java程式碼範例會清理名為的PDF檔案 *Loan.pdf*.

```java
/*
 * This Java Quick Start uses the SOAP mode and contains the following JAR files
 * in the class path:
 * 1. adobe-docconverter-client.jar
 * 2. adobe-livecycle-client.jar
 * 3. adobe-usermanager-client.jar
 *
 * These JAR files are located in the following path:
 * <install directory>/Adobe/Adobe_Experience_Manager_forms/sdk/client-libs/common
 *
 * <install directory>/Adobe/Adobe_Experience_Manager_forms/sdk/client-libs/jboss
 *
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
import java.io.File;
import java.io.FileInputStream;
import java.util.Properties;
import com.adobe.idp.Document;
import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
import com.adobe.livecycle.pdfutility.client.PDFUtilityServiceClient;
import com.adobe.livecycle.pdfutility.client.SanitizationResult;
public class Sanitization {
    public static void main (String[] args){

        try {
            //Set connection properties required to invoke AEM Forms
            Properties connectionProps = new Properties();
            connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
            connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
            connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
            connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
            connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");

          //Create a ServiceClientFactory instance
            ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);

          //Create a PDFUtilityServiceClient object
            PDFUtilityServiceClient pdfutility = new PDFUtilityServiceClient(myFactory);

          //Reference a PDF document to Sanitize
            FileInputStream myPDF;
            myPDF = new FileInputStream("C://loan.pdf");
            Document inDoc = new Document(myPDF);

            //Sanitize the document.
            SanitizationResult result = pdfutility.sanitize(inDoc);

            //Save the Sanitized document
            if(result.isSanitizationSuccessful()){
                Document pdfADoc= result.getDocument();
                File pdfAFile = new File("C://annotations_sanitized.pdf");
                pdfADoc.copyToFile(pdfAFile);
            }
        } catch (Exception e) {
            e.printStackTrace();
        }

    }
}
```
