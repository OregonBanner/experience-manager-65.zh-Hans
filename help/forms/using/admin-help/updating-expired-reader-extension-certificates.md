---
title: 更新过期的Reader扩展服务证书
description: Reader扩展文档无法工作，请更新证书
exl-id: 4e14e0dc-f248-4f6e-a075-6012b6792d9d
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '1581'
ht-degree: 0%

---

# 更新过期的Reader扩展服务证书 {#Updating-expired-Reader-Extension-service-certificates}

Adobe Experience Manager Forms(AEM Forms)拥有Adobe Managed Services或内部部署企业基础许可证的客户有权使用Reader扩展服务。 该服务通过扩展Adobe Reader的功能（具有其他使用权限），使组织能够轻松共享交互式PDF文档。 该服务可向PDF文档添加使用权限，并激活在使用Adobe Acrobat Reader DC打开PDF文档时通常不可用的功能，例如向文档添加注释、填写表单和保存文档。 第三方用户无需使用其他软件或插件即可处理启用了权限的文档。 添加了使用权限的PDF文档称为启用权限的文档。 在Adobe Reader中打开启用了权限的PDF文档的用户可以执行为该文档启用的操作。

Adobe利用PKI（公钥基础结构）颁发数字证书，以用于许可和功能启用。 Adobe一直在根据证书颁发机构“Adobe根CA”颁发证书，该证书计划于2023年1月7日到期。 它将导致根据此证书颁发机构颁发的所有证书过期。 证书过期后，所有依赖于证书的功能都将不再有效。 例如，一个读者扩展的PDF文档，允许在2023年1月7日之后使用Adobe Acrobat Reader添加注释，该文档将停止为客户使用。 要解决此问题，Reader扩展服务的管理员应使用旧证书获取新Adobe根CA G2颁发的新证书并重新将其应用到其PDF文档(阅读器使用新证书扩展PDF文档)。

证书的过期会对JEE上的AEM Forms和OSGi堆栈上的AEM Forms造成影响。 两个堆栈具有不同的一组指令。 在 [先决条件](#Pre-requisites) 和 [获取新证书](#obtain-the-certificates)，根据您的堆栈，选择以下路径之一：

* [在JEE环境中更新AEM Forms的证书](#Updating-and-Applying-certificates-for-an-AEM-Forms-on-JEE-environment)
* [在OSGi环境中更新AEM Forms的证书](#Updating-and-applying-certificates-for-an-AEM-Forms-on-OSGi-environment)

>[!NOTE]
>
>该文件可交替使用术语证书和凭据。

## 先决条件 {#Pre-requisites}

更新证书时，需要使用AEM Forms管理员控制台上可用的操作以及AEM Forms提供的Reader扩展API。 本文档面向了解使用Adobe Experience Manager Forms API的用户和管理员。 在开始之前，请确保：

* 用户具有基础AEM Forms环境的管理员权限。
* 用户已设置 [开发环境](https://experienceleague.adobe.com/docs/experience-manager-65/developing/devtools/howto-projects-eclipse.html) 并有权访问。
* 获取证书。

### 获取证书 {#obtain-the-certificates}

权限凭据将作为数字证书提交，其中包含用于访问凭据的公钥、私钥和密码。

如果贵组织购买Reader扩展的生产版本，则生产权限凭据将由Adobe授权网站(LWS)提供。 生产权限凭据是您的组织特有的，可以启用您需要的特定使用权限。

如果您通过将Reader扩展集成到其软件中的合作伙伴或软件提供商获取了Reader扩展，则该合作伙伴会向您提供权限凭据，而该合作伙伴又会从Adobe中接收此凭据。

>[!NOTE]
>
>权限凭据不能用于典型的文档签名或身份声明。 对于这些应用程序，您可以使用自签名证书或从证书颁发机构(CA)获取身份证书。

提供了以下类型的权限凭据：

**客户评估**:向要评估Reader扩展的客户提供的具有较短有效期的凭据。 当凭据过期时，对使用此凭据的文档应用的使用权限会过期。 此类凭据的有效期仅为两到三个月。

**生产**:为购买完整产品的客户提供的具有较长有效期的凭据。 生产凭据对每个客户都是唯一的，但可以安装在多个系统上。

如果您已使用证书来读取器扩展PDF文件，请从下载生产证书 [Adobe许可网站(LWS)](https://licensing.adobe.com/).

## 在JEE环境中更新和应用AEM Forms的证书 {#Updating-and-Applying-certificates-for-an-AEM-Forms-on-JEE-environment}

在JEE堆栈上的AEM Forms上更新和应用新证书时，需要导入新凭据、从现有PDF文档中删除使用权限，以及应用使用权限。 您可以使用Admin Console导入凭据，使用AEM FormsReader扩展API删除和应用使用权限。

### 导入和配置凭据

您可以使用“信任存储管理”页导入新的或替换的凭据。 信任存储可以包含多个Reader扩展凭据。 必须将其中一个凭据指定为默认的Reader扩展凭据。 当Workbench用户无法确定在流程创建过程中要使用的凭据时，将使用默认凭据。 这些规则适用于默认凭据：

* 如果导入Reader扩展凭据，而信任存储不包含其他Reader扩展凭据，则会将其设置为默认凭据。
* 如果导入选中了默认选项的Reader扩展凭据，则会从现有默认凭据中删除默认类型。 导入的凭据将成为默认凭据。
* 您无法删除默认的Reader扩展凭据。 要删除默认凭据，请首先将另一个凭据设置为默认凭据。 此规则的一个例外是，如果只有一个凭据，则可以删除它，即使它是默认凭据。
* 无法更新默认的Reader扩展凭据。

要导入凭据，请执行以下操作：

1. 在管理控制台中，单击设置>信任存储管理>本地凭据。
1. 单击导入，然后在信任存储类型下，选择Acrobat Reader DC扩展凭据。
1. （可选）要指示此凭据是与Acrobat Reader DC扩展一起使用的默认凭据，请选择“默认”。
1. 在“别名”框中，键入凭据的标识符。 此标识符用作Acrobat Reader DC扩展中凭据的显示名称。 此别名还用于使用AEM Forms SDK以编程方式访问凭据。
1. 单击选择文件以找到凭据，键入凭据的密码，然后单击确定。

如果出现错误消息“由于文件格式不正确或密码不正确而导入凭据失败”，请验证密码是否有效。

您还可以采用编程方式导入和删除凭据。 (请参阅 [使用AEM表单进行编程](../../developing/credentials.md).)

### 从已启用权限的现有PDF文档中删除使用权限

在应用具有最新凭据的使用权限之前，请从已启用权限的现有PDF文档中删除使用权限。 AEM Forms on JEE提供了用于删除使用权限的API。 有关详细说明，请参阅 [从PDF文档中删除使用权限](../../developing/assigning-usage-rights.md#removing-usage-rights-from-pdf-documents).

要删除在Workbench中开发的JEE进程上AEM Forms的使用权限，请参阅 [Workbench帮助](https://helpx.adobe.com/content/dam/help/en/experience-manager/6-5/forms/pdf/WorkbenchHelp.pdf).

### 将使用权限应用于PDF文档

在导入新凭据并从已启用权限的现有PDF文档中删除使用权限后，使用新凭据对PDF文档应用使用权限。 您可以使用Acrobat Reader DC扩展Java客户端API和Web服务将使用权限应用于PDF文档。  有关详细信息，请参阅 [将使用权限应用于PDF文档](../../developing/assigning-usage-rights.md#applying-usage-rights-to-pdf-documents).


## 在OSGi环境中更新和申请AEM Forms的证书 {#Updating-and-applying-certificates-for-an-AEM-Forms-on-OSGi-environment}

在OSGi堆栈上的AEM Forms上更新和应用新证书时，需要导入新凭据、从现有PDF文档中删除使用权限，以及应用使用权限。 您可以使用Admin Console导入凭据，使用AEM FormsReader扩展API删除和应用使用权限。

### 导入凭据 {#Import-credentials}

在OSGi环境的AEM Forms中，Reader扩展凭据与fd-service用户关联。 在添加fd用户密钥存储的凭据之前，请执行以下步骤以创建密钥存储：

1. 以管理员身份登录AEM创作实例。
1. 转到 **[!UICONTROL 工具]**> **[!UICONTROL 安全性]**>**[!UICONTROL 用户]**.
1. 向下滚动用户列表，直到找到fd-service用户帐户。
1. 单击 **[!UICONTROL fd-service]** 用户。
1. 单击密钥库选项卡。
1. 单击 **[!UICONTROL 创建KeyStore]**.
1. 设置KeyStore访问密码并保存您的设置以创建KeyStore密码。

创建密钥存储后，向fd-service用户添加凭据。 以下视频介绍了相关步骤：

>[!VIDEO](https://images-tv.adobe.com/mpcv3/5577/8db8e554-f04b-4fae-8108-b9b5e0eb03ad_1627925794.854x480at800_h264.mp4)

以下命令列出了pfx文件的详细信息。 运行命令之前，导航到包含.pfx文件的目录。

`keytool -v -list -storetype pkcs12 -keystore <name of your .pfx file>`

例如keytool -v -list -storetype pkcs12 -keystore 1005566.pfx，其中1005566.pfx是我的pfx文件的名称

### 从已启用权限的现有PDF文档中删除使用权限

在应用具有最新凭据的使用权限之前，请从已启用权限的现有PDF文档中删除使用权限。 您可以通过从docAssuranceServiceAPI中调用removeUsageRights API来删除文档的使用权限。 有关详细信息，请参阅 [删除使用权限](/help/forms/using/aem-document-services-programmatically.md#removing-usage-rights) 文档。

### 将使用权限应用于PDF文档

要在OSGi环境的AEM Forms中应用使用权限，请创建自定义OSGi服务以获取文档的使用权限。 您还可以使用POST方法创建Servlet，以将读取器扩展PDF返回给用户。 有关详细说明，请参阅 [应用Reader扩展](https://experienceleague.adobe.com/docs/experience-manager-learn/forms/document-services/apply-reader-extension-rights-to-pdf.html).

## 常见问题解答

**如果我有其他问题，应该联系谁？**

您可以联系 [Adobe支持](https://experienceleague.adobe.com/?support-solution=Experience+Manager#support) 或者提供支持票。

**如果我在2023年1月7日之前未更新证书，会发生什么情况？**

在尝试打开PDF文档Reader已扩展且使用旧证书时，用户会遇到错误消息，并且无法再访问阅读器扩展功能。 示例错误为。

`The document has been changed since it was created and use of extended features in no longer available. Please contact the author for the orignal version of this document.`

**新描述的名称有任何变化吗？**

新的Reader扩展证书在描述中将G3-P24作为程序名称。 在较旧的证书中，说明中提到了方案名称P24。
