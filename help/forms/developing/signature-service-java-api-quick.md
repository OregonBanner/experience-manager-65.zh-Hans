---
title: 簽名服務Java API快速入門(SOAP)
seo-title: Signature Service Java API QuickStart(SOAP)
description: 使用簽名服務將簽名欄位新增到PDF檔案、擷取簽名欄位名稱、修改簽名欄位、數位簽署PDF檔案、數位簽署XFA型表單、認證PDF檔案、驗證數位簽名、驗證多個數位簽名，以及移除數位簽名。
seo-description: Use the Signature service to add a signature field to a PDF document, retrieve signature field names, modify a signature field, digitally sign a PDF document, digitally sign an XFA-based form, certify a PDF document, verify a digital signature, verify multiple digital signatures, and remove a digital signature.
uuid: ae6adf23-b119-45f6-bd57-73d8d9ca8ecb
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: 07fffbd5-5430-4abc-b532-0840ecc7b1b0
role: Developer
exl-id: 34069505-a6cf-4540-932b-604f81823178
source-git-commit: 37d2c70bff770d13b8094c5959e488f5531aef55
workflow-type: tm+mt
source-wordcount: '872'
ht-degree: 0%

---

# 簽名服務Java API快速入門(SOAP) {#signature-service-java-api-quickstart-soap}

下列Java API快速入門(SOAP)適用於AEM Forms JEE簽名服務：

[快速入門（SOAP模式）：使用Java API將簽名欄位新增到PDF檔案](signature-service-java-api-quick.md#quick-start-soap-mode-adding-a-signature-field-to-a-pdf-document-using-the-java-api)

[快速入門（SOAP模式）：使用Java API擷取簽名欄位名稱](signature-service-java-api-quick.md#quick-start-soap-mode-retrieving-signature-field-names-using-the-java-api)

[快速入門（SOAP模式）：使用Java API修改簽名欄位](signature-service-java-api-quick.md#quick-start-soap-mode-modifying-a-signature-field-using-the-java-api)

[快速入門（SOAP模式）：使用Java API數位簽署PDF檔案](signature-service-java-api-quick.md#quick-start-soap-mode-digitally-signing-a-pdf-document-using-the-java-api)

[快速入門（SOAP模式）：使用Java API數位簽署XFA型表單](signature-service-java-api-quick.md#quick-start-soap-mode-digitally-signing-a-xfa-based-form-using-the-java-api)

[快速入門（SOAP模式）：使用Java API認證PDF檔案](signature-service-java-api-quick.md#quick-start-soap-mode-certifying-a-pdf-document-using-the-java-api)

[快速入門（SOAP模式）：使用Java API驗證數位簽名](signature-service-java-api-quick.md#quick-start-soap-mode-verifying-a-digital-signature-using-the-java-api)

[快速入門（SOAP模式）：使用Java API驗證多個數位簽名](signature-service-java-api-quick.md#quick-start-soap-mode-verifying-multiple-digital-signatures-using-the-java-api)

[快速入門（SOAP模式）：使用Java API移除數位簽名](signature-service-java-api-quick.md#quick-start-soap-mode-removing-a-digital-signature-using-the-java-api)

[快速入門（SOAP模式）：使用Java API套用檔案時間戳記](#quick-start-soap-mode-apply-document-timestamp-using-the-java-api)

AEM Forms JEE作業可使用AEM Forms強型別API執行，且連線模式應設定為SOAP。

>[!NOTE]
>
>「使用AEM Forms進行程式設計」中的「快速入門」是以部署在JBoss Application Server和Microsoft Windows作業系統上的Forms伺服器為基礎。 不過，如果您使用其他作業系統（例如UNIX），請以適用的作業系統支援的路徑取代Windows特定路徑。 同樣地，如果您使用其他J2EE應用程式伺服器，請務必指定有效的連線屬性。 另請參閱 [設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).

## 快速入門（SOAP模式）：使用Java API將簽名欄位新增到PDF檔案 {#quick-start-soap-mode-adding-a-signature-field-to-a-pdf-document-using-the-java-api}

以下Java程式碼範例新增名為的簽名欄位 *SignatureField1* 至以名為的PDF檔案為基礎的PDF檔案&#x200B;*Loan.pdf*. 包含新簽名欄位的PDF檔案會儲存為名為的PDF檔案 *LoanSig.pdf*. (請參閱 [新增簽名欄位](/help/forms/developing/digitally-signing-certifying-documents.md#adding-signature-fields).)

```java
 /*
     * This Java Quick Start uses the SOAP mode and contains the following JAR files
     * in the class path:
     * 1. adobe-signatures-client.jar
     * 2. adobe-livecycle-client.jar
     * 3. adobe-usermanager-client.jar
    * 4. activation.jar (required for SOAP mode)
     * 5. axis.jar (required for SOAP mode)
     * 6. commons-codec-1.3.jar (required for SOAP mode)
     * 7.  commons-collections-3.1.jar  (required for SOAP mode)
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
     */
 import java.util.*;
 import java.io.File;
 import java.io.FileInputStream;
 import com.adobe.livecycle.signatures.client.*;
 import com.adobe.livecycle.signatures.client.types.*;
 import com.adobe.idp.Document;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 
 public class AddSignatureFieldSOAP {
 
     public static void main(String[] args) {
 
         try
         {
          //Set connection properties required to invoke AEM Forms using SOAP mode
          Properties connectionProps = new Properties();
          connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
          connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
          connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
          connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
          connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 
           //Create a ServiceClientFactory instance
           ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
 
           //Create a SignatureServiceClient object
           SignatureServiceClient signClient = new SignatureServiceClient(myFactory);
 
           //Specify a PDF document to which a signature field is added
           FileInputStream fileInputStream = new FileInputStream("C:\\Adobe\Loan.pdf");
           Document inDoc = new Document (fileInputStream);
 
           //Specify the name of the signature field
           String fieldName = "SignatureField1";
 
           //Create a  PositionRectangle object that specifies
           //the signature fields location
           PositionRectangle post = new  PositionRectangle(193,47,133,12);
 
           //Specify the page number that will contain the signature field
           java.lang.Integer pageNum = new java.lang.Integer(1);
 
           //Add a signature field to the PDF document
           Document sigFieldPDF = signClient.addSignatureField(
              inDoc,
              fieldName,
              pageNum,
              post,
              null,
              null);
 
           //Save the PDF document that contains the signature field
           File outFile = new File("C:\\Adobe\LoanSig.pdf");
           sigFieldPDF.copyToFile(outFile);
             }
 
         catch (Exception ee)
             {
                 ee.printStackTrace();
             }
     }
 }
 
 
```

## 快速入門（SOAP模式）：使用Java API擷取簽名欄位名稱 {#quick-start-soap-mode-retrieving-signature-field-names-using-the-java-api}

以下Java程式碼範例會擷取位於名為的PDF檔案中的簽名欄位名稱 *LoanSig.pdf*. (請參閱 [正在擷取簽章欄位名稱](/help/forms/developing/digitally-signing-certifying-documents.md#retrieving-signature-field-names).)

```java
 /*
     * This Java Quick Start uses the SOAP mode and contains the following JAR files
     * in the class path:
     * 1. adobe-signatures-client.jar
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
     */
 import java.util.*;
 import java.io.FileInputStream;
 import com.adobe.livecycle.signatures.client.*;
 import com.adobe.livecycle.signatures.client.types.*;
 import com.adobe.idp.Document;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 
 public class GetSignatureFieldsSOAP {
 
 public static void main(String[] args) {
     try
     {
         //Set connection properties required to invoke AEM Forms using SOAP mode
         Properties connectionProps = new Properties();
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 
         //Create a ServiceClientFactory instance
         ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
 
         //Create a SignatureServiceClient object
         SignatureServiceClient signClient = new SignatureServiceClient(myFactory);
 
         //Specify a PDF document that contains signature fields
         FileInputStream fileInputStream = new FileInputStream("C:\\Adobe\LoanSig.pdf");
         Document inDoc = new Document (fileInputStream);
 
         //Retrieve the name of the document’s signature fields
         List fieldNames = signClient.getSignatureFieldList(inDoc);
 
         //Obtain the name of each signature field by iterating through the
         //List object
         Iterator iter = fieldNames.iterator();
         int i = 0 ;
         String fieldName="";
         while (iter.hasNext()) {
             PDFSignatureField signatureField = (PDFSignatureField)iter.next();
             fieldName = signatureField.getName();
             System.out.println("The name of the signature field is " +fieldName);
             i++;
              }
         }
         catch (Exception ee)
         {
             ee.printStackTrace();
         }
     }
 }
```

## 快速入門（SOAP模式）：使用Java API修改簽名欄位 {#quick-start-soap-mode-modifying-a-signature-field-using-the-java-api}

以下Java程式碼範例修改名為SignatureField1的簽章欄位，方法是在簽章套用至簽章欄位時，鎖定表單中的所有欄位，並確保不允許變更。 簽名服務傳回包含修改過簽名欄位的PDF檔案後，PDF檔案會儲存為名為LoanSig.pdf的PDF檔案。 (此範例會覆寫傳遞至Signature服務的PDF檔案。) (請參閱 [修改簽章欄位](/help/forms/developing/digitally-signing-certifying-documents.md#modifying-signature-fields).)

```java
 /*
     * This Java Quick Start uses the SOAP mode and contains the following JAR files
     * in the class path:
     * 1. adobe-signatures-client.jar
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
     */
 
 import java.util.*;
 import java.io.File;
 import java.io.FileInputStream;
 import com.adobe.livecycle.signatures.client.*;
 import com.adobe.livecycle.signatures.client.types.*;
 import com.adobe.idp.Document;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 
 public class ModifySignatureFieldSOAP {
 
     public static void main(String[] args) {
 
     try
     {
         //Set connection properties required to invoke AEM Forms using SOAP mode
         Properties connectionProps = new Properties();
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 
         //Create a ServiceClientFactory instance
         ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
 
         //Create a SignatureServiceClient object
         SignatureServiceClient signClient = new SignatureServiceClient(myFactory);
 
         //Specify a PDF document that contains a signature field to modify
         FileInputStream fileInputStream = new FileInputStream("C:\\Adobe\LoanSig.pdf");
         Document inDoc = new Document (fileInputStream);
 
         //Specify the name of the signature field
         String fieldName = "SignatureField1";
 
         //Create a PDFSignatureFieldProperties
         PDFSignatureFieldProperties fieldProperties = new PDFSignatureFieldProperties();
 
          //Create a PDFSeedValueOptionSpec object that stores
          //seed value dictionary information.
          PDFSeedValueOptionSpec seedOptionsSpec = new PDFSeedValueOptionSpec();
 
          //Disallow changes to the PDF document. Any change to the document invalidates
          //the signature
          seedOptionsSpec.setMdpValue(MDPPermissions.NoChanges);
 
          //Create a FieldMDPOptionSpec object that stores
          //signature field lock dictionary information.
          FieldMDPOptionSpec fieldMDPOptionsSpec = new FieldMDPOptionSpec();
 
          //Lock all fields in the PDF document
          fieldMDPOptionsSpec.setAction(FieldMDPAction.ALL);
 
          //Set dictionary information
          fieldProperties.setSeedValue(seedOptionsSpec);
          fieldProperties.setFieldMDP(fieldMDPOptionsSpec);
 
          //Modify the signature field
          Document modSignatureField =  signClient.modifySignatureField(inDoc,fieldName,fieldProperties);
 
          //Save the PDF document that contains modified signature field
          File file = new File("C:\\Adobe\LoanSig.pdf");
          modSignatureField.copyToFile(file);
 
     }
     catch (Exception ee)
       {
         ee.printStackTrace();
       }
     }
 }
 
```

## 快速入門（SOAP模式）：使用Java API數位簽署PDF檔案 {#quick-start-soap-mode-digitally-signing-a-pdf-document-using-the-java-api}

以下Java程式碼範例會以數位方式簽署以名為的PDF檔案為基礎的PDF檔案 *LoanSig.pdf*. 為安全性認證指定的別名是安全的，並且會執行撤銷檢查。 因為未指定CRL或OCSP伺服器資訊，所以伺服器資訊會從用來數位簽署PDF檔案的憑證取得。 已簽署的檔案會儲存為名為的PDF檔案 *LoanSigned.pdf*. (請參閱 [數位簽署PDF檔案](/help/forms/developing/digitally-signing-certifying-documents.md#digitally-signing-pdf-documents).)

```java
 /*
     * This Java Quick Start uses the SOAP mode and contains the following JAR files
     * in the class path:
     * 1. adobe-signatures-client.jar
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
     */
 import java.util.*;
 import java.io.File;
 import java.io.FileInputStream;
 import com.adobe.livecycle.signatures.client.*;
 import com.adobe.livecycle.signatures.client.types.*;
 import com.adobe.livecycle.signatures.pki.client.types.common.HashAlgorithm;
 import com.adobe.idp.Document;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 
 public class SignDocumentSOAP {
 
 public static void main(String[] args) {
 
     try
     {
       //Set connection properties required to invoke AEM Forms using SOAP mode
         Properties connectionProps = new Properties();
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 
       //Create a ServiceClientFactory instance
       ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
 
       //Create a SignatureServiceClient object
       SignatureServiceClient signClient = new SignatureServiceClient(myFactory);
 
       //Specify a PDF document to sign
       FileInputStream fileInputStream = new FileInputStream("C:\\Adobe\LoanSig.pdf");
       Document credDoc = new Document (fileInputStream);
 
       //Specify the name of the signature field
       String fieldName = "SignatureField1";
 
       //Create a Credential object
       Credential myCred = Credential.getInstance("secure");
 
       //Specify the reason to sign the document
       String reason = "The document was reviewed";
 
       //Specify the location of the signer
       String location  = "New York HQ";
 
       //Specify contact information
       String contactInfo = "Tony Blue";
 
       //Create a PDFSignatureAppearanceOptions object
       //and show date information
       PDFSignatureAppearanceOptionSpec appear = new  PDFSignatureAppearanceOptionSpec();
       appear.setShowDate(true);
       appear.setShowReason(true);
 
       //Set revocation checking to false
       java.lang.Boolean revCheck = new Boolean(true);
 
       //Create an OCSPOptionSpec object to pass to the sign method
            OCSPOptionSpec ocspSpec = new OCSPOptionSpec();
 
            //Create a CRLOptionSpec object to pass to the sign method
            CRLOptionSpec crlSpec = new CRLOptionSpec();
 
            //Create a TSPOptionSpec object to pass to the sign method
            TSPOptionSpec tspSpec = new TSPOptionSpec();
 
       //Sign the PDF document
       Document signedDoc = signClient.sign(
          credDoc,
          fieldName,
          myCred,
          HashAlgorithm.SHA1,
          reason,
          location,
          contactInfo,
          appear,
          revCheck,
         ocspSpec,
              crlSpec,
              tspSpec);
 
       //Save the signed PDF document
       File outFile = new File("C:\\Adobe\LoanSigned.pdf");
       signedDoc.copyToFile (outFile);
       }
 
     catch (Exception ee)
       {
         ee.printStackTrace();
       }
       }
 }
 
 
```

## 快速入門（SOAP模式）：使用Java API數位簽署XFA型表單 {#quick-start-soap-mode-digitally-signing-a-xfa-based-form-using-the-java-api}

以下Java程式碼範例會對Forms服務轉譯的互動式表單加上簽名。 此 `com.adobe.idp.Document` Forms服務傳回的執行個體會傳遞至簽名服務。 已簽署的互動式表單會儲存為名為的PDF檔案 *LoanXFASigned.pdf*.

```java
 /*
     * This Java Quick Start uses the SOAP mode and contains the following JAR files
     * in the class path:
     * 1. adobe-signatures-client.jar
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
     */
 import java.util.*;
 import java.io.File;
 import java.io.FileInputStream;
 
 import com.adobe.livecycle.formsservice.client.FormsResult;
 import com.adobe.livecycle.formsservice.client.FormsServiceClient;
 import com.adobe.livecycle.formsservice.client.PDFFormRenderSpec;
 import com.adobe.livecycle.signatures.client.*;
 import com.adobe.livecycle.signatures.client.types.*;
 import com.adobe.livecycle.signatures.pki.client.types.common.HashAlgorithm;
 import com.adobe.idp.Document;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 
 public class SignXFAFormsSOAP {
 
 public static void main(String[] args) {
 
     try
     {
 
      //Set connection properties required to invoke AEM Forms using SOAP mode
      Properties connectionProps = new Properties();
      connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
      connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
      connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
      connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
      connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 
      //Create a ServiceClientFactory instance
      ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
 
      //Get the XFA form to sign
      Document myForm = GetForm(myFactory);
 
     //Sign the XFA form
     SignXFA(myForm,myFactory);
     }
 
     catch (Exception ee)
       {
         ee.printStackTrace();
       }
       }
 
 
 //Creates an interactive PDF form based on a XFA form
 private static Document GetForm(ServiceClientFactory myFactory)
 {
 
     try
     {
     //Create a FormsServiceClient object
     FormsServiceClient formsClient = new FormsServiceClient(myFactory);
 
     //Specify a PDF document to sign
     FileInputStream fileInputStream = new FileInputStream("C:\\Adobe\LoanSigXFA.pdf");
     Document xfaForm = new Document (fileInputStream);
 
     //Retrieve form data
     FileInputStream cData = new FileInputStream("C:\\Adobe\Loan.xml");
     Document oInputData = new Document(cData);
 
     //Cache the PDF form
     PDFFormRenderSpec pdfFormRenderSpec = new PDFFormRenderSpec();
     pdfFormRenderSpec.setGenerateServerAppearance(true);
 
     //Invoke the renderPDFForm2 method
     FormsResult formOut = formsClient.renderPDFForm2(
             xfaForm,               //formQuery
             oInputData,             //inDataDoc
             pdfFormRenderSpec,      //PDFFormRenderSpec
             null,                //urlSpec
             null            //attachments
             );
 
     //Create a Document object that stores form data
     Document myForm = formOut.getOutputContent();
     return myForm;
 }
 
     catch (Exception ee)
       {
         ee.printStackTrace();
       }
     return null;
 
 }
 
 //Sign the PDF document
 private static void SignXFA(Document doc, ServiceClientFactory myFactory)
 {
     try
     {
 
     //Create a SignatureServiceClient object
      SignatureServiceClient signClient = new SignatureServiceClient(myFactory);
 
      //Specify the name of the signature field
      String fieldName = "SignatureField1";
 
      //Create a Credential object
      Credential myCred = Credential.getInstance("secure");
 
      //Specify the reason to sign the document
      String reason = "The document was reviewed";
 
      //Specify the location of the signer
      String location  = "New York HQ";
 
      //Specify contact information
      String contactInfo = "Tony Blue";
 
      //Create a PDFSignatureAppearanceOptions object
      //and show date information
      PDFSignatureAppearanceOptionSpec appear = new  PDFSignatureAppearanceOptionSpec();
      appear.setShowDate(true);
      appear.setShowReason(true);
 
      //Set revocation checking to false
      java.lang.Boolean revCheck = new Boolean(true);
 
      //Create an OCSPOptionSpec object to pass to the sign method
      OCSPOptionSpec ocspSpec = new OCSPOptionSpec();
 
      //Create a CRLOptionSpec object to pass to the sign method
      CRLOptionSpec crlSpec = new CRLOptionSpec();
 
      //Create a TSPOptionSpec object to pass to the sign method
      TSPOptionSpec tspSpec = new TSPOptionSpec();
 
      //Sign the PDF document
       Document signedDoc = signClient.sign(
          doc,
          fieldName,
          myCred,
          HashAlgorithm.SHA1,
          reason,
          location,
          contactInfo,
          appear,
          revCheck,
         ocspSpec,
         crlSpec,
         tspSpec);
 
       //Save the signed PDF document
       File outFile = new File("C:\\Adobe\LoanXFASigned.pdf");
       signedDoc.copyToFile (outFile);
 }
 
     catch (Exception ee)
       {
         ee.printStackTrace();
       }
      }
 }
 
```

## 快速入門（SOAP模式）：使用Java API認證PDF檔案 {#quick-start-soap-mode-certifying-a-pdf-document-using-the-java-api}

以下Java程式碼範例會根據名為的PDF檔案來認證PDF檔案 *LoanSig.pdf*. 為安全性認證指定的別名是安全的，不會執行撤銷檢查。 已驗證的檔案會儲存為名為的PDF檔案 *LoanCertified.pdf*. (請參閱 [認證PDF檔案](/help/forms/developing/digitally-signing-certifying-documents.md#certifying-pdf-documents).)

```java
 /*
     * This Java Quick Start uses the SOAP mode and contains the following JAR files
     * in the class path:
     * 1. adobe-signatures-client.jar
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
     */
 import java.util.*;
 import java.io.File;
 import java.io.FileInputStream;
 import com.adobe.livecycle.signatures.client.*;
 import com.adobe.livecycle.signatures.client.types.*;
 import com.adobe.livecycle.signatures.pki.client.types.common.HashAlgorithm;
 import com.adobe.idp.Document;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 
 public class CertifyDocumentSOAP {
 
     public static void main(String[] args) {
     try
     {
         //Set connection properties required to invoke AEM Forms using SOAP mode
         Properties connectionProps = new Properties();
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 
       //Create a ServiceClientFactory instance
       ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
 
       //Create a SignatureServiceClient object
       SignatureServiceClient signClient = new SignatureServiceClient(myFactory);
 
       //Specify a PDF document to certify
       FileInputStream fileInputStream = new FileInputStream("C:\\Adobe\LoanSig.pdf");
       Document credDoc = new Document (fileInputStream);
 
       //Specify the name of the signature field
       String fieldName = "SignatureField1";
 
       //Create a Credential object
       Credential myCred = Credential.getInstance("secure");
 
       //Specify the reason to sign the document
       String reason = "The document was reviewed";
 
       //Specify the location of the signer
       String location  = "My company";
 
       //Specify contact information
           String contactInfo = "New York, New York";
 
       //Create a PDFSignatureAppearanceOptions object and show date information
       PDFSignatureAppearanceOptionSpec appear = new  PDFSignatureAppearanceOptionSpec();
       appear.setShowDate(true);
 
       //Set revocation checking to false
            java.lang.Boolean revCheck = new Boolean(false);
 
            //Set locking to false
            java.lang.Boolean lockField = new Boolean(false);
 
            //Specify a legalAttestation value
            String msg = "Any change to this document will invalidate the certificate";
 
            //Create objects to pass to the certify method
            OCSPOptionSpec ocspSpec = new OCSPOptionSpec();
            CRLOptionSpec crlSpec = new CRLOptionSpec();
            TSPOptionSpec tspSpec = new TSPOptionSpec();
 
            //Certify the PDF document
            Document signedDoc = signClient.certify(
               credDoc,
               fieldName,
               myCred,
               HashAlgorithm.SHA1,
               reason,
               location,
               contactInfo,
               MDPPermissions.NoChanges,
               msg,
               appear,
               revCheck,
               lockField,
              ocspSpec,
              crlSpec,
              tspSpec);
 
         //Save the signed PDF document
              File outFile = new File("C:\\Adobe\LoanCertified.pdf");
              signedDoc.copyToFile (outFile);
         }
 
     catch (Exception ee)
         {
         ee.printStackTrace();
         }
     }
 }
```

## 快速入門（SOAP模式）：使用Java API驗證數位簽名 {#quick-start-soap-mode-verifying-a-digital-signature-using-the-java-api}

以下Java程式碼範例會驗證位於已簽署PDF檔案中的數位簽名，該檔案是根據名為LoanSigned.pdf的PDF檔案。 驗證時間設定為目前時間，撤銷檢查選項設定為「盡最大努力」。 (請參閱 [驗證數位簽名](#verifying-digital-signatures).)

```java
 /*
     * This Java Quick Start uses the following JAR files
     * 1. adobe-signatures-client.jar
     * 2. adobe-livecycle-client.jar
     * 3. adobe-usermanager-client.jar
    * 4. activation.jar (required for SOAP mode)
     * 5. axis.jar (required for SOAP mode)
     * 6. commons-codec-1.3.jar (required for SOAP mode)
     * 7.  commons-collections-3.1.jar  (required for SOAP mode)
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
     */
 import java.util.*;
 import java.io.FileInputStream;
 import com.adobe.livecycle.signatures.client.*;
 import com.adobe.livecycle.signatures.client.types.*;
 import com.adobe.livecycle.signatures.pki.client.types.common.RevocationCheckStyle;
 import com.adobe.idp.Document;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 
 public class VerifySignatureSOAP{
 
     public static void main(String[] args) {
 
     try
     {
       //Set connection properties required to invoke AEM Forms using SOAP mode
       Properties connectionProps = new Properties();
       connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
      connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
       connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
       connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
       connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 
       //Create a ServiceClientFactory instance
       ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
 
       //Create a SignatureServiceClient object
       SignatureServiceClient signClient = new SignatureServiceClient(myFactory);
 
       //Specify a PDF document that contains a digital signature
       FileInputStream fileInputStream = new FileInputStream("C:\\Adobe\LoanSigned.pdf");
       Document inDoc = new Document (fileInputStream);
 
       //Specify the name of the signature field
       String fieldName = "SignatureField1";
 
       //Create a PKIOptions object that contains PKI run-time options
       PKIOptions pkiOptions = new PKIOptions();
       pkiOptions.setVerificationTime(VerificationTime.CURRENT_TIME);
       pkiOptions.setRevocationCheckStyle(RevocationCheckStyle.BestEffort);
 
       //Verify the digital signature
       PDFSignatureVerificationInfo  signInfo = signClient.verify2(
          inDoc,
          fieldName,
          pkiOptions,
          null);
 
       //Get the Signature Status
       SignatureStatus sigStatus = signInfo.getStatus();
       String myStatus="";
 
       //Determine the status of the signature
       if (sigStatus == SignatureStatus.DynamicFormSignatureUnknown)
              myStatus = "The signatures located in the dynamic PDF form are unknown";
          else if (sigStatus == SignatureStatus.DocumentSignatureUnknown)
              myStatus = "The signatures located in the PDF document are unknown";
          else if (sigStatus == SignatureStatus.CertifiedDynamicFormSignatureTamper)
              myStatus = "The signatures located in a certified PDF form are valid";
          else if (sigStatus == SignatureStatus.SignedDynamicFormSignatureTamper)
              myStatus = "The signatures located in a signed dynamic PDF form are valid";
          else if (sigStatus == SignatureStatus.CertifiedDocumentSignatureTamper)
              myStatus = "The signatures located in a certified PDF document are valid";
          else if (sigStatus == SignatureStatus.SignedDocumentSignatureTamper)
              myStatus = "The signatures located in a signed PDF document are valid";
          else if (sigStatus == SignatureStatus.SignatureFormatError)
              myStatus = "The format of a signature in a signed document is invalid";
          else if (sigStatus == SignatureStatus.DynamicFormSigNoChanges)
              myStatus = "No changes were made to the signed dynamic PDF form";
          else if (sigStatus == SignatureStatus.DocumentSigNoChanges)
              myStatus = "No changes were made to the signed PDF document";
          else if (sigStatus == SignatureStatus.DynamicFormCertificationSigNoChanges)
              myStatus = "No changes were made to the certified dynamic PDF form";
          else if (sigStatus == SignatureStatus.DocumentCertificationSigNoChanges)
              myStatus = "No changes were made to the certified PDF document";
          else if (sigStatus == SignatureStatus.DocSigWithChanges)
              myStatus = "There were changes to a signed PDF document";
         else if (sigStatus == SignatureStatus.CertificationSigWithChanges)
              myStatus = "There were changes made to the PDF document.";
 
       //Get the signature type
       SignatureType sigType = signInfo.getSignatureType();
       String myType = "";
 
       if (sigType.getType() == PDFSignatureType.AUTHORSIG)
              myType="Certification";
       else if(sigType.getType() == PDFSignatureType.RECIPIENTSIG)
              myType="Recipient";
 
       //Get the identity of the signer
       IdentityInformation signerId = signInfo.getSigner();
       String signerMsg = "";
 
      if (signerId.getStatus() == IdentityStatus.UNKNOWN)
          signerMsg = "Identity Unknown";
      else if (signerId.getStatus() == IdentityStatus.TRUSTED)
          signerMsg = "Identity Trusted";
      else if (signerId.getStatus() == IdentityStatus.NOTTRUSTED)
          signerMsg = "Identity Not Trusted";
 
      //Get the Signature properties returned by the Signature service
      SignatureProperties sigProps = signInfo.getSignatureProps();
      String signerName =  sigProps.getSignerName();
 
     System.out.println("The status of the signature is: "+myStatus +". The signer identity is "+signerMsg +". The signature type is "+myType +". The name of the signer is "+signerName+".");
     }
     catch (Exception ee)
     {
         ee.printStackTrace();
     }
      }
 }
 
 
```

## 快速入門（SOAP模式）：使用Java API驗證多個數位簽名 {#quick-start-soap-mode-verifying-multiple-digital-signatures-using-the-java-api}

以下Java程式碼範例會根據名為LoanAllSigs.pdf的PDF檔案，驗證位於已簽署PDF檔案中的多個數位簽名。 驗證時間設定為目前時間，撤銷檢查選項設定為「盡最大努力」。 (請參閱 [驗證多個數位簽名](signature-service-java-api-quick.md#quick-start-soap-mode-verifying-multiple-digital-signatures-using-the-java-api).)

```java
 /*
     * This Java Quick Start uses the SOAP mode and contains the following JAR files
     * in the class path:
     * 1. adobe-signatures-client.jar
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
     */
 import java.util.*;
 import java.io.FileInputStream;
 import com.adobe.livecycle.signatures.client.*;
 import com.adobe.livecycle.signatures.client.types.*;
 import com.adobe.livecycle.signatures.pki.client.types.common.RevocationCheckStyle;
 import com.adobe.idp.Document;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 
 public class VerifyAllSignaturesSOAP{
 
     public static void main(String[] args) {
 
     try
     {
       //Set connection properties required to invoke AEM Forms using SOAP mode
       Properties connectionProps = new Properties();
       connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
      connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
       connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
       connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
       connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 
       //Create a ServiceClientFactory instance
       ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
 
       //Create a SignatureServiceClient object
       SignatureServiceClient signClient = new SignatureServiceClient(myFactory);
 
       //Specify a PDF document that contains multiple digital signatures
       FileInputStream fileInputStream = new FileInputStream("C:\\Adobe\LoanAllSigs.pdf");
       Document inDoc = new Document (fileInputStream);
 
       //Create a PKIOptions object that contains PKI run-time options
       PKIOptions pkiOptions = new PKIOptions();
       pkiOptions.setVerificationTime(VerificationTime.CURRENT_TIME);
       pkiOptions.setRevocationCheckStyle(RevocationCheckStyle.BestEffort);
 
       //Verify all digital signatures that are located in a PDF document
       PDFDocumentVerificationInfo  allSig = signClient.verifyPDFDocument(
          inDoc,
          pkiOptions,
          null);
 
       //Get a list of all signatures that are located in the PDF document
       List allSignatures = allSig.getVerificationInfos();
 
     //Create an Iterator object and iterate through
     //the List object
     Iterator<PDFSignatureVerificationInfo> iter = allSignatures.iterator();
 
     while (iter.hasNext()) {
            PDFSignatureVerificationInfo signInfo = (PDFSignatureVerificationInfo)iter.next();
 
            //Get the Signature Status
               SignatureStatus sigStatus = signInfo.getStatus();
               String myStatus="";
 
             //Determine the status of the signature
               if (sigStatus == SignatureStatus.DynamicFormSignatureUnknown)
                   myStatus = "The signatures located in the dynamic PDF form are unknown";
               else if (sigStatus == SignatureStatus.DocumentSignatureUnknown)
                   myStatus = "The signatures located in the PDF document are unknown";
               else if (sigStatus == SignatureStatus.CertifiedDynamicFormSignatureTamper)
                   myStatus = "The signatures located in a certified PDF form are valid";
               else if (sigStatus == SignatureStatus.SignedDynamicFormSignatureTamper)
                   myStatus = "The signatures located in a signed dynamic PDF form are valid";
               else if (sigStatus == SignatureStatus.CertifiedDocumentSignatureTamper)
                   myStatus = "The signatures located in a certified PDF document are valid";
               else if (sigStatus == SignatureStatus.SignedDocumentSignatureTamper)
                   myStatus = "The signatures located in a signed PDF document are valid";
               else if (sigStatus == SignatureStatus.SignatureFormatError)
                   myStatus = "The format of a signature in a signed document is invalid";
               else if (sigStatus == SignatureStatus.DynamicFormSigNoChanges)
                   myStatus = "No changes were made to the signed dynamic PDF form";
               else if (sigStatus == SignatureStatus.DocumentSigNoChanges)
                   myStatus = "No changes were made to the signed PDF document";
               else if (sigStatus == SignatureStatus.DynamicFormCertificationSigNoChanges)
                   myStatus = "No changes were made to the certified dynamic PDF form";
               else if (sigStatus == SignatureStatus.DocumentCertificationSigNoChanges)
                   myStatus = "No changes were made to the certified PDF document";
               else if (sigStatus == SignatureStatus.DocSigWithChanges)
                   myStatus = "There were changes to a signed PDF document";
              else if (sigStatus == SignatureStatus.CertificationSigWithChanges)
                   myStatus = "There were changes made to the PDF document.";
 
               //Get the signature type
              SignatureType sigType = signInfo.getSignatureType();
              String myType = "";
 
              if (sigType.getType() == PDFSignatureType.AUTHORSIG)
                  myType="Certification";
              else if(sigType.getType() == PDFSignatureType.RECIPIENTSIG)
                  myType="Recipient";
 
              //Get the Signature properties returned by the Signature service
              SignatureProperties sigProps = signInfo.getSignatureProps();
              String signerName =  sigProps.getSignerName();
 
             System.out.println("The status of the signature is: "+myStatus +". The signature type is "+myType +". The name of the signer is "+signerName+".");
         }
     }
     catch (Exception ee)
     {
         ee.printStackTrace();
     }
      }
 }
```

## 快速入門（SOAP模式）：使用Java API移除數位簽名 {#quick-start-soap-mode-removing-a-digital-signature-using-the-java-api}

以下Java程式碼範例會從名為的簽名欄位中移除數位簽名 *SignatureField1*. 包含簽名欄位的PDF檔案的名稱為 *LoanSigned.pdf*. (請參閱 [移除數位簽名](/help/forms/developing/digitally-signing-certifying-documents.md#removing-digital-signatures).)

```java
 /*
     * This Java Quick Start uses the SOAP mode and contains the following JAR files
     * in the class path:
     * 1. adobe-signatures-client.jar
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
     */
 
 import java.util.*;
 import java.io.File;
 import java.io.FileInputStream;
 import com.adobe.livecycle.signatures.client.*;
 import com.adobe.idp.Document;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 
 public class ClearSignatureFieldSOAP {
 
     public static void main(String[] args) {
 
     try
     {
         //Set connection properties required to invoke AEM Forms using SOAP mode
         Properties connectionProps = new Properties();
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 
         //Create a ServiceClientFactory instance
         ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
 
         //Create a SignatureServiceClient object
         SignatureServiceClient signClient = new SignatureServiceClient(myFactory);
 
         //Specify a PDF document that contains the signature to remove
         FileInputStream fileInputStream = new FileInputStream("C:\\Adobe\LoanSigned.pdf");
         Document inDoc = new Document (fileInputStream);
 
         //Specify the name of the signature field
         String fieldName = "SignatureField1";
 
         //Clear the signature field
         Document outPDF = signClient.clearSignatureField(inDoc,fieldName);
 
         //Save the PDF document
         File outFile = new File("C:\\Adobe\Loan.pdf");
         outPDF.copyToFile(outFile);
         }
 
     catch (Exception ee)
         {
         ee.printStackTrace();
         }
     }
 }


 
 
 
```

## 快速入門（SOAP模式）：使用Java API套用檔案時間戳記 {#quick-start-soap-mode-apply-document-timestamp-using-the-java-api}

以下Java程式碼範例會將時間戳記套用至PDF檔案：

```java
 /*
 * This Java Quick Start uses the SOAP mode and contains the following JAR files
 * in the class path:
 * 1. adobe-signatures-client.jar
 * 2. adobe-livecycle-client.jar
 * 3. adobe-usermanager-client.jar
 * 4. adobe-utilities.jar
 * 5. commons-httpclient-<version>.jar
 * 6. axis.jar (required for SOAP mode)
 * 7. jaxrpc-api.jar (required for SOAP mode)
 * 8. commons-logging.jar (required for SOAP mode)
 * 9. commons-discovery.jar (required for SOAP mode)
 * 10. wsdl4j.jar (required for SOAP mode)
 * 11. adobe-utilities.jar (required for SOAP mode)
 *
 *
 * These JAR files are located in the following path:
 * <install directory>/sdk/client-libs/common
 *
 * The adobe-utilities.jar file is located in the following path:
 * <install directory>/sdk/client-libs/jboss
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
 */
import java.io.File;
import java.io.FileInputStream;
import java.util.Properties;

import com.adobe.idp.Document;
import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
import com.adobe.livecycle.signatures.client.SignatureServiceClient;
import com.adobe.livecycle.signatures.client.types.AddSignatureValidationOptionSpec;
import com.adobe.livecycle.signatures.client.types.TSPOptionSpec;

public class ApplyDocumentTimeStamp {

    public static void main(String args[]){
        {

            try
            {
                //Set connection properties required to invoke AEM Forms using SOAP mode
                Properties connectionProps = new Properties();
                connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
                connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
                connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
                connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
                connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");

                //Create a ServiceClientFactory instance
                ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);

                //Create a SignatureServiceClient object
                SignatureServiceClient signClient = new SignatureServiceClient(myFactory);

                //Specify a PDF document to sign
                FileInputStream fileInputStream = new FileInputStream("test.pdf");

                //Sign the PDF document
                Document inPDFDoc = new Document (fileInputStream);

                // create AddSignatureValidationOptionSpec Object. later we will set the required OptionSpecs
                AddSignatureValidationOptionSpec addSigValidiationSpec =  new AddSignatureValidationOptionSpec();

                //Create a TSPOptionSpec object to pass to in AddSignatureValidationOptionSpec
                TSPOptionSpec tspSpec = new TSPOptionSpec();
                tspSpec.setTspServerURL("https://tsp-server-url.com");
                tspSpec.setTspServerPassword("provide Timestamp server password");
                tspSpec.setTspServerUsername("provide Timestamp server username");
                addSigValidiationSpec.setTSPOptionSpec(tspSpec);

                Document signedDoc = signClient.applyDocumentTimeStamp(inPDFDoc,addSigValidiationSpec);

                //Save the signed PDF document
                File outFile = new File("testout.pdf");
                signedDoc.copyToFile (outFile);

            }

            catch (Exception ee)
            {
                ee.printStackTrace();
            }
        }
    }
}
```
