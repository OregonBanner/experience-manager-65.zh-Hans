---
title: 使用HSM以數位方式簽署或認證檔案
seo-title: Use HSM to certify eSigned documents
description: 使用HSM或eToken裝置來認證eSigned檔案
seo-description: Use HSM or etoken devices to certify eSigned documents
uuid: bbe057c1-6150-41f9-9c82-4979d31d305d
contentOwner: vishgupt
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: document_services
discoiquuid: 536bcba4-b754-4799-b0d2-88960cc4c44a
exl-id: 4d423881-18e0-430a-849d-e1762366a849
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '995'
ht-degree: 0%

---

# 使用HSM以數位方式簽署或認證檔案 {#use-hsm-to-digitally-sign-or-certify-documents}

硬體安全性模組(HSM)和權杖是專屬、強化和防篡改運算裝置，旨在安全地管理、處理和儲存數位金鑰。 這些裝置直接連線到電腦或網路伺服器。

Adobe Experience Manager Forms可以使用儲存在HSM上的憑證或eSign電子代號，或將伺服器端數位簽名套用至檔案。 若要搭配AEM Forms使用HSM或etoken裝置：

1. 啟用DocAssurance服務
1. 設定Reader擴充功能的憑證。
1. 在AEM Web Console中建立HSM或Etoken裝置的別名。
1. 使用DocAssurance Service API，以儲存在裝置上的數位金鑰簽署或認證檔案。

## 使用AEM Forms設定HSM或etoken裝置之前 {#configurehsmetoken}

* 安裝 [AEM Forms附加元件](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html) 封裝。
* 在與AEM伺服器相同的電腦上安裝及設定HSM或Etoken使用者端軟體。 使用者端軟體必須與HSM和Etoken裝置通訊。
* (僅限Microsoft Windows)將JAVA_HOME_32環境變數設定為指向安裝32位元版Java 8 Development Kit (JDK 8)的目錄。 目錄的預設路徑為C:\Program Files(x86)\Java\jdk&lt;version>
* (僅限OSGi上的AEM Forms)在信任存放區中安裝根憑證。 必須驗證已簽署的PDF

>[!NOTE]
>
>在Microsoft Windows上，僅支援32位元LunaSA或EToken使用者端。

## 啟用DocAssurance服務 {#configuredocassurance}

預設不會啟用DocAssurance服務。 執行以下步驟來啟用服務：

1. 停止AEM Forms環境的Author例項。

1. 開啟 [AEM_root]\crx-quickstart\conf\sling.properties檔案進行編輯。

   >[!NOTE]
   >
   >如果您已使用 [AEM_root]\crx-quickstart\bin\start.bat檔案啟動AEM執行個體，然後開啟 [AEM_root]\crx-quickstart\sling.properties檔案以進行編輯。

1. 在sling.properties檔案中新增或取代以下屬性：

   ```shell
   sling.bootdelegation.sun=sun.*,com.sun.*,sun.misc.*
   sling.bootdelegation.ibm=com.ibm.xml.*,com.ibm.*
   sling.bootdelegation.class.com.rsa.jsafe.provider.JsafeJCE=com.rsa.*  
   ```

1. 儲存並關閉sling.properties檔案。
1. 重新啟動AEM執行個體。

## 設定Reader擴充功能的憑證 {#set-up-certificates-for-reader-extensions}

執行以下步驟來設定憑證：

1. 以管理員身分登入AEM作者執行個體。

1. 按一下&#x200B;**Adobe Experience Manager** 全域導覽列上。 前往 **工具** >  **安全性** >  **使用者**.
1. 按一下 **名稱** 使用者帳戶的欄位。 此 **編輯使用者設定** 頁面隨即開啟。
1. 在AEM Author執行個體上，憑證位於KeyStore中。 如果您先前尚未建立KeyStore，請按一下 **建立KeyStore** 並設定KeyStore的新密碼。 如果伺服器已包含KeyStore，請略過此步驟。

1. 於 **編輯使用者設定** 頁面，按一下 **管理KeyStore**.

1. 在KeyStore管理對話方塊中，展開 **從金鑰庫檔案新增私密金鑰** 選項並提供別名。 別名可用來執行Reader擴充功能作業。
1. 若要上傳憑證檔案，請按一下 **選取金鑰庫檔案** 並上傳 `.pfx` 檔案。
1. 新增 **金鑰庫密碼**，**私密金鑰密碼**、和 **私密金鑰別名** 與對應欄位之憑證相關聯的內容區段。 按一下 **提交**.

   >[!NOTE]
   >
   >決定P **私密金鑰別名** 對於憑證，您可以使用Java keytool命令： `keytool -list -v -keystore [keystore-file] -storetype pkcs12`

   >[!NOTE]
   >
   >在 **金鑰庫密碼** 和 **私密金鑰密碼** 欄位中，指定憑證檔案所提供的密碼。

>[!NOTE]
>
>對於OSGi上的AEM Forms，若要驗證已簽署的PDF，根憑證會安裝在信任存放區中。

>[!NOTE]
>
>移至生產環境時，請以生產認證取代評估認證。 在更新過期的認證或評估認證之前，請務必刪除舊的Reader擴充功能認證。

## 建立裝置的別名 {#configuredeviceinaemconsole}

別名包含HSM或Etoken所需的所有引數。 執行以下指示，為eSign或Digital Signatures使用的每個HSM或Etoken認證建立別名：

1. 開啟AEM主控台。 AEM主控台的預設URL為https://&lt;host>：&lt;port>/system/console/configMgr
1. 開啟 **HSM認證組態服務** 並指定下列欄位的值：

   * **認證別名**：指定用來識別別名的字串。 此值會用作某些數位簽名作業（例如「簽名欄位」作業）的屬性。
   * **DLL路徑**：指定伺服器上HSM或Etoken使用者端程式庫的完整路徑。 例如，C:\Program Files\LunaSA\cryptoki.dll。 在叢集環境中，叢集內所有伺服器的此路徑必須相同。
   * **HSM Pin**：指定存取裝置金鑰所需的密碼。
   * **HSM插槽ID**：指定整數型別的位置識別碼。 插槽ID是依個別使用者端來設定。 如果您將第二部機器註冊到不同的磁碟分割（例如，同一HSM裝置上的HSMPART2），則插槽1會與使用者端的HSMPART2磁碟分割相關聯。

   >[!NOTE]
   >
   >設定Etoken時，請為「HSM插槽ID」欄位指定數值。 需要數值才能讓簽名作業正常運作。

   * **憑證SHA1**：為您使用的認證指定公開金鑰(.cer)檔案的SHA1值（指紋）。 請確定SHA1值中沒有使用空格。 如果您使用實體憑證，則不需要使用。
   * **HSM裝置型別**：選取HSM （Luna或其他）或eToken裝置的製造商。

   单击“**保存**”。已針對AEM Forms設定硬體安全性模組。 現在，您可以使用AEM Forms的硬體安全性模組來簽署或認證檔案。

## 使用DocAssurance Service API簽署或認證檔案，並使用儲存在裝置上的數位金鑰  {#programatically}

下列程式碼範例使用HSM或etoken來簽署或認證檔案。

```java
/*************************************************************************
 *
 * ADOBE CONFIDENTIAL
 * ___________________
 *
 * Copyright 2014 Adobe Systems Incorporated
 * All Rights Reserved.
 *
 * NOTICE:  All information contained herein is, and remains
 * the property of Adobe Systems Incorporated and its suppliers,
 * if any.  The intellectual and technical concepts contained
 * herein are proprietary to Adobe Systems Incorporated and its
 * suppliers and are protected by trade secret or copyright law.
 * Dissemination of this information or reproduction of this material
 * is strictly forbidden unless prior written permission is obtained
 * from Adobe Systems Incorporated.
 **************************************************************************/
package com.adobe.docassurance.samples;

import java.io.ByteArrayInputStream;
import java.io.IOException;
import java.io.InputStream;

import javax.jcr.Binary;
import javax.jcr.Node;
import javax.jcr.RepositoryException;
import javax.jcr.Session;

import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Reference;
import org.apache.felix.scr.annotations.Service;
import org.apache.sling.api.resource.ResourceResolver;
import org.apache.sling.jcr.api.SlingRepository;
import org.apache.sling.jcr.resource.JcrResourceResolverFactory;

import com.adobe.aemfd.docmanager.Document;
import com.adobe.fd.docassurance.client.api.DocAssuranceException;
import com.adobe.fd.docassurance.client.api.DocAssuranceService;
import com.adobe.fd.docassurance.client.api.DocAssuranceServiceOperationTypes;
import com.adobe.fd.docassurance.client.api.SignatureOptions;
import com.adobe.fd.signatures.client.types.exceptions.InvalidArgumentException;
import com.adobe.fd.signatures.pdf.inputs.CredentialContext;
import com.adobe.fd.signatures.pdf.inputs.DSSPreferences;
import com.adobe.fd.signatures.pdf.inputs.DSSPreferencesImpl;
import com.adobe.fd.signatures.pdf.inputs.PDFSignatureAppearenceOptions;
import com.adobe.fd.signatures.pdf.inputs.UnlockOptions;
import com.adobe.fd.signatures.pdf.inputs.PDFSignatureAppearenceOptions.PDFSignatureAppearanceType;
import com.adobe.fd.signatures.pdf.inputs.PDFSignatureAppearenceOptions.TextDirection;
import com.adobe.fd.signatures.pki.client.types.common.HashAlgorithm;
import com.adobe.fd.signatures.pki.client.types.common.RevocationCheckStyle;
import com.adobe.fd.signatures.pki.client.types.prefs.CRLPreferences;
import com.adobe.fd.signatures.pki.client.types.prefs.CRLPreferencesImpl;
import com.adobe.fd.signatures.pki.client.types.prefs.GeneralPreferencesImpl;
import com.adobe.fd.signatures.pki.client.types.prefs.PKIPreferences;
import com.adobe.fd.signatures.pki.client.types.prefs.PKIPreferencesImpl;
import com.adobe.fd.signatures.pki.client.types.prefs.PathValidationPreferences;
import com.adobe.fd.signatures.pki.client.types.prefs.PathValidationPreferencesImpl;

/**
 * Digital signatures can be applied to PDF documents to provide a level of security. Digital signatures, like handwritten signatures, provide a means by which signers
 * identify themselves and make statements about a document. The technology used to digitally sign documents helps to ensure that both the signer and recipients are clear
 * about what was signed and confident that the document was not altered since it was signed.
 *
 * PDF documents are signed by means of public-key technology. A signer has two keys: a public key and a private key. The private key is stored in a user's credential that
 * must be available at the time of signing. The public key is stored in the user's certificate that must be available to recipients to validate the signature. Information
 * about revoked certificates is found in certificate revocation lists (CRLs) and Online Certificate Status Protocol (OCSP) responses distributed by Certificate Authorities (CAs).
 * The time of signing can be obtained from a trusted source known as a Timestamping Authority.
 *
 * The following Java code example digitally signs a PDF document that is based on a PDF file.
 * The alias that is specified for the security credential is secure, and revocation checking is performed.
 * Because no CRL or OCSP server information is specified, the server information is obtained from the certificate used to
 * digitally sign the PDF document
 *
 * PreRequisites - Digital certificate for signing the document has to be uploaded on Granite Key Store
 */

@Component
@Service(value=Sign.class)
public class Sign{
 @Reference
 private DocAssuranceService docAssuranceService;

 @Reference
    private SlingRepository slingRepository;

 @Reference
    private JcrResourceResolverFactory jcrResourceResolverFactory ;

 /**
  *
  * @param inputFile - path to the pdf document stored at JCR node
  * @param outputFile - path to the pdf document where the output needs to be stored
  * @throws IOException
  * @throws RepositoryException
  * @throws InvalidArgumentException
  * @throws DocAssuranceException
  */
 public void signExtend(String inputFile, String outputFile, String alias) throws IOException, RepositoryException, InvalidArgumentException, DocAssuranceException{

  Document inDoc = new Document(inputFile);
  Document outDoc = null;

  Session adminSession = null;
        ResourceResolver resourceResolver = null;
        try {

          /** resourceResolver with admin privileges to be passed to SignatureServiceAPI and Reader Extensions
          the resource resolver for signature options has to be corresponding to the user who has the signing certificate in his granite key store
          the resource resolver for signature options has to be corresponding to the user who has the credential for reader extension in his granite key store
          here we are using the same resource resolver
          */
          adminSession = slingRepository.loginAdministrative(null);
             resourceResolver = jcrResourceResolverFactory.getResourceResolver(adminSession);

             //retrieve specifications for each of the services, you may pass null if you don't want to use that service
             //as we don't want encryption in this case, passing null for Encryption Options
             //for encrypted document pass Unlock Options - see the method getUnlockOptions() below
    outDoc = docAssuranceService.secureDocument(inDoc, null, getSignatureOptions(alias,resourceResolver),null,null);
        }
  catch(Exception e){
   e.printStackTrace();
  }
        finally{
            /**
             * always close the PDFDocument object after your processing is done.
             */
            if(inDoc != null){
                inDoc.close();
            }
            if(adminSession != null && adminSession.isLive()){
                if(resourceResolver != null){
                    resourceResolver.close();
                }
                adminSession.logout();
            }
        }

        //flush the output document contents to JCR Node
  flush(outDoc, outputFile);

 }

 /**
  *
  * @param rr resource resolver corresponding to the user with the access to signing credential for the
  * given alias "allcertificatesanypolicytest11ee_new" in this case
  * @return SignatureOptions
  */
 private SignatureOptions getSignatureOptions(String alias, ResourceResolver rr){

  //create an instance of SignatureOptions
  SignatureOptions signatureOptions = SignatureOptions.getInstance();

  //set the operation you want to perform - SIGN/CERTIFY
  signatureOptions.setOperationType(DocAssuranceServiceOperationTypes.SIGN);

  //field to sign
  String fieldName = "Signature1" ;

        //Hash Algo to be used to compute digest the PDF document
        HashAlgorithm algo = HashAlgorithm.SHA384;

        //Reason for signing/certifying
        String reason = "Test Reason";

        //location of the signer
        String location = "Test Location";

        //contact info of the signer
        String contactInfo = "Test Contact";

        //Create a PDFSignatureAppearanceOptions object
        //and show date information
        PDFSignatureAppearenceOptions appOptions = new PDFSignatureAppearenceOptions(
                PDFSignatureAppearanceType.NAME, null, 1.0d, null, true, true,
                true, true, true, true, true, TextDirection.AUTO);

        signatureOptions.setSignatureFieldName(fieldName);
        signatureOptions.setAlgo(algo);
        signatureOptions.setContactInfo(contactInfo);
        signatureOptions.setLocation(location);
        signatureOptions.setSigAppearence(appOptions);
        signatureOptions.setReason(reason);
        signatureOptions.setDssPref(getDSSPreferences(rr));
        signatureOptions.setCredential(new CredentialContext(alias, rr, true));
  return signatureOptions;
 }

 private DSSPreferences getDSSPreferences(ResourceResolver rr){
  //sets the DSS Preferences
        DSSPreferencesImpl prefs = DSSPreferencesImpl.getInstance();
        prefs.setPKIPreferences(getPKIPreferences());
        GeneralPreferencesImpl gp = (GeneralPreferencesImpl) prefs.getPKIPreferences().getGeneralPreferences();
        gp.setDisableCache(true);
        return prefs;
    }

    private PKIPreferences getPKIPreferences(){
     //sets the PKI Preferences
        PKIPreferences pkiPref = new PKIPreferencesImpl();
        pkiPref.setCRLPreferences(getCRLPreferences());
        pkiPref.setPathPreferences(getPathValidationPreferences());
        return pkiPref;
    }

    private CRLPreferences getCRLPreferences(){
        //specifies the CRL Preferences
        CRLPreferencesImpl crlPrefs = new CRLPreferencesImpl();
        crlPrefs.setRevocationCheck(RevocationCheckStyle.CheckIfAvailable);
        crlPrefs.setGoOnline(true);
        return crlPrefs;
    }

    private PathValidationPreferences getPathValidationPreferences(){
     //sets the path validation preferences
        PathValidationPreferencesImpl pathPref = new PathValidationPreferencesImpl();
        pathPref.setDoValidation(false);
        return pathPref;

    }

    /**
     * sets Unlock Options for encrypted PDF
     */
    private UnlockOptions getUnlockOptions(){
        UnlockOptions unlockOptions = new UnlockOptions();
        //sets the Open Password for password encrypted PDF
        unlockOptions.setPassword("OpenPassword");

        //for Certificate Encrypted Document, set the alias of the credential uploaded in the user's key store
        //and corresponding resource resolver

        return unlockOptions;

    }
    /**
     * This method copies the data from {@code Document}, to the specified file at the given resourcePath.
     * @param doc
     * @param resourcePath
     * @throws IOException
     */
    private void flush(Document doc, String resourcePath) throws IOException {
   //extracts the byte data from Document
   byte[] output = doc.getInlineData();
   Binary opBin;
   Session adminSession = null;
      try {
         adminSession = slingRepository.loginAdministrative(null);

         //get access to the specific node
         //here we are assuming that node exists
           Node node = adminSession.getNode(resourcePath);

           //convert byte[] to Binary
           opBin = adminSession.getValueFactory().createBinary((InputStream)new ByteArrayInputStream(output));

           //set the Binary data value to node's jcr:data
           node.getNode("jcr:content").getProperty("jcr:data").setValue(opBin);
      } catch (RepositoryException e) {

      }
      finally{

       if(adminSession != null && adminSession.isLive()){
        try {
      adminSession.save();
      adminSession.logout();
     } catch (RepositoryException e) {

     }

             }
      }

  }
}
```

如果您已經從AEM 6.0 Form或AEM 6.1 Forms升級，而且您在舊版中使用DocAssurance服務，則：

* 若要在沒有HSM或Edoken裝置的情況下使用DocAssurance服務，請繼續使用現有的程式碼。
* 若要搭配HSM或etoken裝置使用DocAssurance服務，請以下列的API取代現有的CredentialContext物件程式碼。

```java
/**
  *
  * @param credentialAlias alias of the PKI Credential stored in CQ Key Store or
  * the alias of the HSM Credential configured using HSM Credentials Configuration Service.
  * @param resourceResolver corresponding to the user with the access to the key store and trust store.
  * @param isHSMCredential if the alias is corresponding to HSM Credential.
  */
 public CredentialContext(String credentialAlias, ResourceResolver resourceResolver, boolean isHSMCredential);
```

如需API的詳細資訊和DocAssurance服務的範常式式碼，請參閱 [以程式設計方式使用AEM檔案服務](/help/forms/using/aem-document-services-programmatically.md).
