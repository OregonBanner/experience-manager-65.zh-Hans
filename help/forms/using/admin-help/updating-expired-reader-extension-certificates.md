---
title: Reader扩展证书过期及其影响
description: Reader扩展证书过期及其影响
exl-id: 4e14e0dc-f248-4f6e-a075-6012b6792d9d
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '1121'
ht-degree: 2%

---


# Reader扩展证书过期及其影响 {#expiration-of-reader-extensions-certificates-and-its-impact}

具有Adobe Managed Services或内部部署企业版基本许可证的Adobe Experience Manager Forms (AEM Forms)客户有权使用Acrobat Reader DC扩展服务。 该服务通过扩展具有其他使用权限的Acrobat Reader的功能，使企业能够轻松共享交互式PDF文档。 该服务向PDF文档添加使用权限，并激活在使用Adobe Acrobat Reader打开PDF文档时不可用的功能，例如向文档添加注释、填写表单和保存文档。 第三方用户无需其他软件或插件即可使用启用了权限的文档。 已添加使用权限的PDF文档称为启用权限的文档。 在Acrobat Reader中打开启用了权限的PDF文档的用户可以执行为该文档启用的操作。

Adobe使用公钥基础设施(PKI)颁发数字证书，用于许可和功能启用。 Adobe一直在证书颁发机构下颁发证书 **Adobe根CA**，将于2023年1月7日过期。 证书的过期不会影响使用由颁发的生产证书扩展的PDF文档。 **Adobe根CA** 基于的证书（旧证书）。 所有PDF文档(在2023年1月7日之前使用旧证书扩展的Reader，包括您的客户下载的文档)将继续使用应用于它们的所有使用权限，并且不需要任何更新。

新的证书颁发机构， **Adobe根CA G2**、和基于新证书颁发机构的证书现已可用。 在2023年1月7日或之前，开始使用新证书，这些证书基于 **Adobe根CA G2** —Reader扩展新的PDF文档。  您可以 [从Adobe授权网站获取新证书](https://licensing.adobe.com/) 或Adobe支持。

## 常见问题解答

**问：Adobe根证书与Acrobat Reader扩展证书有何区别？ Adobe根证书是否依赖于Acrobat Reader扩展证书？ 这两个证书是否都将于2023年1月到期？**

A.Adobe根CA是从中颁发Acrobat Reader扩展证书的证书颁发机构。 2023年1月7日，“Adobe根CA”及其颁发的所有证书将过期。

**问：Adobe以前曾就证书过期及其对使用/开启PDF文件的影响发出过信函。 应该忽略该通信吗？**

A.根据对情况的重新评估，所有使用旧“PDF根CA”2023年1月7日之前发放的生产证书延长的Adobe文件在2023年1月7日之后继续有效，没有发生任何变化。 如果您已更新PDF文档，则体验不会发生任何更改。

**如果还有其他问题，我应该联系谁？**

A.您可以联系 [Adobe支持](https://experienceleague.adobe.com/?support-solution=Experience+Manager#support) 或者提出支持票证。

**问：如果我在2023年1月7日之前不更新证书，会发生什么？**

A. 2023年1月7日之前使用旧“PDF根CA”颁发的生产证书延期的所有内部Adobe文件在2023年1月7日之后继续有效，没有发生任何变化。 使用评估证书扩展的PDF在过期日期后不起作用。

**问：新证书的描述是否与旧证书有所不同？**

A.对新的Acrobat Reader扩展证书的说明 **G3-P24** 作为项目名称。 在旧证书(基于“Adobe根CA”的证书)的描述中， **P24** 作为项目名称提及。

**问：如何获取最新的证书？**

A.所有授权的Forms客户（具有有效许可证）都可从以下网站下载新证书(基于“Adobe根CA G2”的证书)： [Adobe授权网站](https://licensing.adobe.com/). 如果您在Adobe授权网站上找不到证书，请联系 [Adobe支持](https://experienceleague.adobe.com/?support-solution=Experience+Manager&amp;lang=en#support) 或者提出支持票证。

**问：使用由“PDF根CA”（旧证书颁发机构）颁发的证书扩展的Adobe文档在2023年1月7日之后是否仍然有效？**

A.是，所有使用在2023年1月7日之前从“PDF根CA”（旧证书颁发机构）颁发的生产证书延期的Adobe文件，在2023年1月7日之后继续有效，无任何变更。 使用评估证书延长的PDF文档在过期日期后不再有效。

**问：要使用由“PDF根CA”（旧证书颁发机构）颁发的证书扩展的Adobe文档，需要哪个Adobe Acrobat Reader版本？**

A. Adobe Acrobat Reader 2020或更高版本需要使用扩展了“Adobe根CA”（旧证书颁发机构）的PDF文档。 它是发布本文档时支持的Acrobat Reader版本。 如果您使用 [不受支持的Adobe Acrobat版本](https://helpx.adobe.com/cn/support/programs/eol-matrix.html)，Adobe建议您 [下载并安装最新版本的Adobe Acrobat Reader](https://get.adobe.com/reader/).

**问：要使用由“PDF根CA 2”（新的证书颁发机构）颁发的证书扩展的Adobe文档，需要哪个Adobe Acrobat Reader版本？**

A. Adobe Acrobat Reader 2020或更高版本需要使用扩展了“Adobe根CA 2”（新证书颁发机构）的PDF文档。 如果您使用 [不受支持的Adobe Acrobat Reader版本](https://helpx.adobe.com/cn/support/programs/eol-matrix.html)，Adobe建议您 [下载并安装最新版本的Adobe Acrobat Reader](https://get.adobe.com/reader/).

**问：我能否在继续使用现有别名的同时，删除旧的Acrobat Reader Extensions证书，并在Adobe Experience Manager Forms Server上添加新证书？**

答：是的，您可以删除旧的Acrobat Reader扩展证书，然后使用现有别名向Adobe Experience Manager Forms服务器添加新证书。

**问：能否在Adobe Experience Manager Forms服务器上同时保留新证书和旧Acrobat Reader扩展证书？**

答：是的，您可以保留两个证书，但可以在Adobe Experience Manager Forms服务器上使用不同的别名。 自2023年1月7日起，您只能使用新证书Reader扩展PDF文档。

**问：我是否可以将相同的Acrobat Reader扩展证书导入所有Adobe Experience Manager Forms环境？**

答：是，可以在多个环境中使用相同的Acrobat Reader扩展证书。

**问：如何检查应用于PDF文档的使用权限？**

A.您可以使用 [getDocumentUsageRights](https://experienceleague.adobe.com/docs/experience-manager-65/forms/developer-reference/programming-aem-forms-jee/java-api-quick-start-code-examples/acrobat-reader-dc-extensions-service.html?lang=en#quick-start-soap-mode-retrieving-credential-information-using-the-java-api) 用于检索有关应用于PDF文档的使用权限的信息的API。

**问：如何更改Acrobat Reader扩展证书文件的密码？**

A.在Microsoft Windows上，要更改证书密码，请使用Microsoft管理控制台(MMC)安装证书并选择 **将密钥标记为可导出**. 安装后，使用私钥导出证书，然后为PFX文件使用其他密码。


<!-- 
## Applying the certificates {#obtaning-and-applying-the-certificates} 

You can choose one of the following paths to apply latest certificates:

* [Updating certificates for an AEM Forms on JEE environment](#Updating-and-Applying-certificates-for-an-AEM-Forms-on-JEE-environment) 
* [Updating certificates for an AEM Forms on OSGi environment](#Updating-and-applying-certificates-for-an-AEM-Forms-on-OSGi-environment)

>[!NOTE]
>
>The document uses the term certificates and credentials interchangeably.

### Pre-requisites {#Pre-requisites}

Updating the certificates requires using actions available on AEM Forms administrator console and Reader Extension APIs provided by AEM Forms. The document is intended for users and administrators with knowledge of using Adobe Experience Manger Forms APIs. Before you start, ensure that: 

* the user has administrator rights on underlying AEM Forms environment. 
* the user has setup the [development environment](https://experienceleague.adobe.com/docs/experience-manager-65/developing/devtools/howto-projects-eclipse.html) and has access to it.
* [obtain the certificates](#obtain-the-certificates).


### Obtain the certificates {#obtain-the-certificates}

The Rights credential is delivered as a digital certificate that contains the public key, the private key, and the password used to access the credential.

If your organization purchases a production version of Reader Extensions, the production Rights credential is delivered by Adobe Licensing Website (LWS). A production Rights credential is unique to your organization and can enable the specific usage rights that you require.

If you obtained Reader Extensions through a partner or software provider who integrated Reader Extensions into their software, the Rights credential is provided to you by that partner who, in turn, receives this credential from Adobe.

>[!NOTE]
>
>The Rights credential cannot be used for typical document signing or assertion of identity. For these applications, you can use a self-sign certificate or acquire an identity certificate from a Certificate Authority (CA).

The following types of Rights credentials are available:

**Customer Evaluation**: A credential with a short validity period that is provided to customers who want to evaluate Reader Extensions. Usage rights applied to documents using this credential expire when the credential expires. This type of credential is valid only for two to three months.

**Production**: A credential with a long validity period that is provided to customers who purchased the full product. Production credentials are unique to each customer but can be installed on multiple systems.

If you have already used certificates to reader extend PDF files, download a production certificate from [Adobe Licensing Website (LWS)](https://licensing.adobe.com/).

### Applying certificates for an AEM Forms on JEE environment {#Updating-and-Applying-certificates-for-an-AEM-Forms-on-JEE-environment} 

Applying new certificates on AEM Forms on JEE stack requires importing new credentials and applying usage rights. You can use admin console to import credentials and AEM Forms Reader Extension APIs to apply usage rights. 

#### Import and configure credentials 

You can use the Trust Store Management pages to import a new credential. The Trust Store may contain more than one Reader Extensions credential. You must designate one of those credentials as the default Reader Extensions credential. The default credential is used when a Workbench user is unable to determine which credential to use during process creation. These rules apply to default credentials:

* If you import a Reader Extensions credential and the Trust Store contains no other Reader Extensions credentials, it is set as the default.
* If you import a Reader Extensions credential with the Default option selected, the default type is removed from an existing default credential. The imported credential becomes the default.
* You cannot delete a default Reader Extensions credential. To delete the default credential, first set another credential as the default. An exception to this rule is that if there is only one credential, you can delete it even though it is the default.
* You cannot update a default Reader Extensions credential.

To import the credentials: 

1. In administration console, click Settings > Trust Store Management > Local Credentials.
1. Click Import and, under Trust Store Type, select Acrobat Reader DC extensions Credential.
1. (Optional) To indicate that this credential is the default credential to use with Acrobat Reader DC extensions, select Default.
1. In the Alias box, type an identifier for the credential. This identifier is used as the display name for the credential in Acrobat Reader DC extensions. This alias is also used to access the credential programmatically using the AEM forms SDK.
1. Click Choose File to locate the credential, type the password of the credential, and then click OK.

If the error message "Failed to import credential due to either incorrect file format, or incorrect password" appears, verify that the password is valid.

You can also import and delete credentials programmatically. (See [Programming with AEM forms](../../developing/credentials.md).)

<!-- ### Remove usage rights from existing rights-enabled PDF documents

Remove usage rights from existing rights-enabled PDF documents before applying usage rights with latest credentials. AEM Forms on JEE provides APIs to remove usage rights. For detailed instructions, see [Removing Usage Rights from PDF Documents](../../developing/assigning-usage-rights.md#removing-usage-rights-from-pdf-documents).

To remove usage rights for AEM Forms on JEE processes developed in Workbench, see [Workbench Help](https://helpx.adobe.com/content/dam/help/en/experience-manager/6-5/forms/pdf/WorkbenchHelp.pdf). 

#### Apply the usage rights to PDF documents 

After importing new credentials, you can apply usage rights to PDF documents using the Acrobat Reader DC extensions Java Client API and web service.  For details, see [Applying Usage Rights to PDF Documents](../../developing/assigning-usage-rights.md#applying-usage-rights-to-pdf-documents). 


### Applying certificates for an AEM Forms on OSGi environment {#Updating-and-applying-certificates-for-an-AEM-Forms-on-OSGi-environment}

Applying new certificates on AEM Forms on OSGi stack requires importing new credentials and applying usage rights. You can use admin console to import credentials and AEM Forms Reader Extension APIs to apply usage rights. 

#### Import credentials {#Import-credentials}

In an AEM Forms on OSGi environment, a Reader Extension credential is associated with fd-service user. Before adding credentials for fd-user key store, perform the following steps to create a key store: 

1. Log in to your AEM Author instance as an Administrator.
1. Go to **[!UICONTROL Tools]**> **[!UICONTROL Security]**>**[!UICONTROL Users]**.
1. Scroll down the list of users until you find fd-service user account.
1. Click **[!UICONTROL fd-service]** user.
1. Click keystore tab.
1. Click **[!UICONTROL Create KeyStore]**.
1. Set the KeyStore Access Password and save your settings to create the KeyStore password.

After creating the key-store, add credentials to fd-service user. The following video explains the steps: 

>[!VIDEO](https://images-tv.adobe.com/mpcv3/5577/8db8e554-f04b-4fae-8108-b9b5e0eb03ad_1627925794.854x480at800_h264.mp4)

The following command list the details of the pfx file. Before running the command, navigate to the directory that contains the .pfx file.

`keytool -v -list -storetype pkcs12 -keystore [name of your .pfx file]`

For example, keytool -v -list -storetype pkcs12 -keystore 1005566.pfx where 1005566.pfx is the name of my pfx file

<!-- ### Remove usage rights from existing rights-enabled PDF documents

Remove usage rights from existing rights-enabled PDF documents before applying usage rights with latest credentials. You can remove the usage rights for a document by invoking the removeUsageRights API from within the docAssuranceServiceAPI. For detailed information, see [Remove Usage Rights](/help/forms/using/aem-document-services-programmatically.md#removing-usage-rights) document.

#### Apply the usage rights to PDF documents 

To apply usage rights in an AEM Forms on OSGi environment, Create custom OSGi service to usage rights to the documents. You can also create a servlet with a POST method to return the reader extended PDF to the user. For detailed instructions, see [Applying Reader Extensions](https://experienceleague.adobe.com/docs/experience-manager-learn/forms/document-services/apply-reader-extension-rights-to-pdf.html).  -->
