---
title: 使用HSM对文档进行数字签名或验证
seo-title: 使用HSM验证电子签名文档
description: 使用HSM或etoken设备验证电子签名文档
seo-description: 使用HSM或etoken设备验证电子签名文档
uuid: bbe057c1-6150-41f9-9c82-4979d31d305d
contentOwner: vishgupt
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: document_services
discoiquuid: 536bcba4-b754-4799-b0d2-88960cc4c44a
translation-type: tm+mt
source-git-commit: 35b2c9c8c79b3cc3d81e0b92ea17cd7d599fa7ee
workflow-type: tm+mt
source-wordcount: '1010'
ht-degree: 0%

---


# 使用HSM对文档进行数字签名或验证 {#use-hsm-to-digitally-sign-or-certify-documents}

硬件安全模块(HSM)和令牌是专用的、经过硬化的和抗篡改的计算设备，设计用于安全地管理、处理和存储数字密钥。 这些设备直接连接到计算机或网络服务器。

Adobe Experience Manager Forms可以使用存储在HSM或etoken上的凭据进行电子签名，或将服务器端数字签名应用于文档。 要将HSM或令牌设备与AEM Forms一起使用：

1. 启用DocAssurance服务。
1. 设置Reader扩展的证书。
1. 在AEM Web控制台中为HSM或令牌设备创建别名。
1. 使用DocAssurance Service API用存储在设备上的数字密钥对文档进行签名或验证。

## 在配置HSM或令牌设备之前，请使用AEM Forms {#configurehsmetoken}

* Install [AEM Forms add-on](https://helpx.adobe.com/cn/aem-forms/kb/aem-forms-releases.html) package.
* 在AEM服务器所在的计算机上安装和配置HSM或etoken客户端软件。 客户端软件需要与HSM和令牌设备进行通信。
* （仅限Microsoft Windows）将JAVA_HOME_32环境变量设置为指向安装32位版本Java 8 Development Kit(JDK 8)的目录。 目录的默认路径为C:\Program Files(x86)\Java\jdk&lt;version>
* (AEM Forms仅在OSGi上)在信任存储中安装根证书。 需要验证已签名的PDF

>[!NOTE]
>
>在Microsoft Windows上，仅支持32位LunaSA或EToken客户端。

## 启用DocAssurance服务 {#configuredocassurance}

默认情况下，DocAssurance服务未启用。 请执行以下步骤以启用服务：

1. 停止您的AEM Forms环境的作者实例。

1. 打开AEM_ [root]\crx-quickstart\conf\sling.properties文件进行编辑。

   >[!NOTE]
   >
   >如果已使用AEM_ [root]\crx-quickstart\bin\start.bat文件来开始AEM实例， [请打开AEM_root]\crx-quickstart\sling.properties文件进行编辑。

1. 在sling.properties文件中添加或替换以下属性：

   ```shell
   sling.bootdelegation.sun=sun.*,com.sun.*,sun.misc.*
   sling.bootdelegation.ibm=com.ibm.xml.*,com.ibm.*
   sling.bootdelegation.class.com.rsa.jsafe.provider.JsafeJCE=com.rsa.*  
   ```

1. 保存并关闭sling.properties文件。
1. 重新启动AEM实例。

## 为Reader扩展设置证书 {#set-up-certificates-for-reader-extensions}

请执行以下步骤来设置证书：

1. 以管理员身份登录到AEM作者实例。

1. 单&#x200B;**击全局导航** 栏上的AdobeExperience Manager。 转到“工 **具** ”>“ **安全** ” **>“**&#x200B;用户”。
1. 单击 **用户帐户** 的名称字段。 此时将 **打开“编辑用户** 设置”页。
1. 在AEM作者实例中，证书驻留在KeyStore中。 如果您之前尚未创建KeyStore，请单 **击“创建KeyStore** ”并为KeyStore设置新密码。 如果服务器已包含KeyStore，请跳过此步骤。

1. 在“编辑 **用户设置”页** ，单击“ **管理密钥商店”**。

1. 在“密钥存储管理”对话框中，展 **开“从密钥存储文件添加私钥** ”选项并提供别名。 别名用于执行Reader扩展操作。
1. 要上传证书文件，请单击“选 **择密钥存储文件** ”并上传 `.pfx` 文件。
1. 将与证 **书关联的**“密钥&#x200B;**存储密码**”、“私钥密 **码”和“私钥别名** ”添加到相应的字段。 单击 **提交**。

   >[!NOTE]
   >
   >要确定证&#x200B;**书的私钥** “别名”，可以使用Java keytool命令： `keytool -list -v -keystore [keystore-file] -storetype pkcs12`

   >[!NOTE]
   >
   >在“密 **钥存储密码** ”和 **“私钥密码”字段中** ，指定随证书文件提供的密码。

>[!NOTE]
>
>对于OSGi上的AEM Forms，要验证已签名的PDF（信任存储中安装的根证书）。

>[!NOTE]
>
>转到生产环境时，请用生产凭据替换评估凭据。 请确保在更新过期或评估凭据之前删除旧的Reader扩展凭据。

## 为设备创建别名 {#configuredeviceinaemconsole}

别名包含HSM或etoken需要的所有参数。 执行下面列出的说明，为电子签名或数字签名使用的每个HSM或电子令牌凭据创建别名：

1. 打开AEM控制台。 AEM控制台的默认URL为https://&lt;host>:&lt;port>/system/console/configMgr
1. 打开HSM **凭据配置服务** ，并指定以下字段的值：

   * **凭据别名**:指定用于标识别名的字符串。 此值用作某些数字签名操作（如签名字段操作）的属性。
   * **DLL路径**:在服务器上指定HSM或etoken客户端库的完全限定路径。 例如，C:\Program Files\LunaSA\cryptoki.dll。 在群集环境中，此路径必须对群集中的所有服务器都相同。
   * **HSM管脚**:指定访问设备密钥所需的口令。
   * **HSM插槽ID**:指定整数类型的插槽标识符。 插槽ID是按客户端逐个设置的。 如果您向另一个分区（例如，同一HSM设备上的HSMPART2）注册另一台计算机，则插槽1与客户端的HSMPART2分区相关联。

   >[!NOTE]
   >
   >配置Etoken时，为HSM插槽ID字段指定一个数值。 要使“签名”操作正常工作，需要一个数值。

   * **证书SHA1**:为您使用的凭据指定公钥(.cer)文件的SHA1值（指纹）。 确保SHA1值中没有使用空格。 如果您使用的是物理证书，则不需要它。
   * **HSM设备类型**:选择HSM（Luna或其他）或eToken设备的制造商。

   单击&#x200B;**保存**。硬件安全模块配置为AEM Forms。 现在，您可以将硬件安全模块与AEM Forms一起使用，对文档进行签名或认证。

## 使用DocAssurance Service API使用存储在设备上的数字密钥签署或验证文档  {#programatically}

以下示例代码使用HSM或etoken对文档进行签名或验证。

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

如果您已从AEM 6.0表单或AEM 6.1Forms升级，并且您在先前版本中使用DocAssurance服务，那么：

* 要使用没有HSM或令牌设备的DocAssurance服务，请继续使用现有代码。
* 要将DocAssurance服务与HSM或令牌设备一起使用，请将您现有的CredentialContext对象代码替换为下面列出的API。

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

有关API和DocAssurance服务示例代码的详细信息，请参 [阅以编程方式使用AEM文档服务](/help/forms/using/aem-document-services-programmatically.md)。
