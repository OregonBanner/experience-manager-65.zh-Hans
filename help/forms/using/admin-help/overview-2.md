---
title: 证书和凭据管理基础知识
seo-title: 证书和凭据管理基础知识
description: 了解管理证书和凭据的基础知识。
seo-description: 了解管理证书和凭据的基础知识。
uuid: f421e206-e7b5-416c-b9fb-974094f10a66
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_certificates_and_credentials
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 986d16fc-4c81-4785-b1f3-fe8bd7ff669e
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 证书和凭据管理基础知识 {#basics-of-managing-certificates-and-credentials}

凭 *据包含签署* 或识别文档所需的私钥信息。 证 *书* ，是您为信任配置的公钥信息。 AEM表单使用证书和凭据用于多种用途：

* Acrobat Reader DC扩展使用凭据在PDF文档中启用Adobe Reader使用权限。 (请参 [阅配置凭据以与Acrobat Reader DC扩展一起使用](/help/forms/using/admin-help/configuring-credentials-acrobat-reader-dc.md#configuring-credentials-for-use-with-acrobat-reader-dc-extensions)。)
* 您可以将Rights Management配置为显示凭据，以便仅从受信任的发行商在Acrobat中使用。 (请参阅 [配置Rights Management显示设置](/help/forms/using/admin-help/configuring-client-server-options.md#configure-document-security-display-settings)。)证书中必须有通用名称(CN)。
* 签名服务访问证书和凭据。 有关签名服务的详细信息，请参阅服 [务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

**生成对密钥**

AEM表单使用其信任存储来存储和管理证书、凭据和证书撤销列表(CRL)。 此外，您还可以使用独立的硬件安全模块(HSM)设备存储私钥。

AEM表单不提供任何用于生成密钥对的选项。 但是，您可以使用工具（如Java keytool）生成它，并将它导入AEM表单信任存储中。 有关Java Keytool的详细信息，请参阅以下内容：

[https://docs.oracle.com/javase/tutorial/security/toolsign/step3.html](https://docs.oracle.com/javase/tutorial/security/toolsign/step3.html)

[https://docs.oracle.com/cd/E19798-01/821-1841/gjrgy/index.html](https://docs.oracle.com/cd/E19798-01/821-1841/gjrgy/index.html)

[https://blogs.adobe.com/livecycle/2010/01/creating_ssl_keys_and_certific.html](https://blogs.adobe.com/livecycle/2010/01/creating_ssl_keys_and_certific.html)

支持以下签名类型，并可以在AEM表单中导入这些类型：

* XML签名
* XMLTimeStampToken
* RFC 3161 timeStampToken
* PKCS#7
* PKCS#1
* DSA签名

**处理丢失或损坏的密钥**

如果您怀疑您的密钥丢失或已泄露，请采取以下措施：

1. 通知认证机构，以便他们在证书撤销列表中添加已泄露的密钥以撤销该密钥。
1. 从认证机构处获得新密钥及其证书。
1. 使用新密钥再次对使用已破坏的密钥签名的文档进行签名。

