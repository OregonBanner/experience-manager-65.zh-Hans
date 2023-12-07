---
title: 管理证书和凭据的基础知识
description: 了解管理证书和凭据的基础知识。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_certificates_and_credentials
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 74bf0e77-f47b-475a-b2a7-52cfb3baaa22
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '301'
ht-degree: 0%

---

# 管理证书和凭据的基础知识 {#basics-of-managing-certificates-and-credentials}

A *凭据* 包含签名或识别文档所需的私钥信息。 A *证书* 是您为信任配置的公钥信息。 AEM forms将证书和凭据用于多种用途：

* Acrobat Reader DC扩展使用凭据在PDF文档中启用Adobe Reader使用权限。 (请参阅 [配置凭据以用于Acrobat Reader DC扩展](/help/forms/using/admin-help/configuring-credentials-acrobat-reader-dc.md#configuring-credentials-for-use-with-acrobat-reader-dc-extensions).)
* 您可以将Rights Management配置为仅显示凭据以便在Acrobat中使用，这些凭据来自受信任的颁发者。 (请参阅 [配置Rights Management显示设置](/help/forms/using/admin-help/configuring-client-server-options.md#configure-document-security-display-settings).) 通用名称(CN)必须存在于证书中。
* 签名服务访问证书和凭据。 有关Signature服务的详细信息，请参阅 [服务参考](https://www.adobe.com/go/learn_aemforms_services_65).

**生成配对密钥**

AEM Forms使用信任存储区来存储和管理证书、凭据和证书吊销列表(CRL)。 此外，您可以使用独立的Hardware Security Module (HSM)设备存储私钥。

AEM forms不提供任何用于生成密钥对的选项。 但是，您可以使用Java keytool等工具生成它，并将其导入AEM Forms信任存储区。 有关Java keytool的详细信息，请参阅以下内容：

[https://docs.oracle.com/javase/tutorial/security/toolsign/step3.html](https://docs.oracle.com/javase/tutorial/security/toolsign/step3.html)

[https://docs.oracle.com/cd/E19798-01/821-1841/gjrgy/index.html](https://docs.oracle.com/cd/E19798-01/821-1841/gjrgy/index.html)

[https://helpcenter.gsx.com/hc/en-us/articles/115015960428-How-to-Generate-a-Self-Signed-Certificate-and-Private-Key-using-OpenSSL](https://helpcenter.gsx.com/hc/en-us/articles/115015960428-How-to-Generate-a-Self-Signed-Certificate-and-Private-Key-using-OpenSSL)

以下签名类型受支持，可以在AEM表单中导入：

* XML签名
* XMLTimeStampToken
* RFC 3161时间戳令牌
* PKCS#7
* PKCS#1
* DSA签名

**处理丢失或损坏的密钥**

如果您怀疑您的密钥已丢失或已被泄漏，请采取以下措施：

1. 通知证书颁发机构，以便他们将损坏的密钥添加到证书撤销列表以撤销该密钥。
1. 从证书颁发机构获取新密钥及其证书。
1. 使用新密钥再次签署使用泄露密钥签署的文档。
