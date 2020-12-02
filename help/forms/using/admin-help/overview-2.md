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
workflow-type: tm+mt
source-wordcount: '358'
ht-degree: 0%

---


# 管理证书和凭据{#basics-of-managing-certificates-and-credentials}的基础知识

*凭据*&#x200B;包含签名或识别文档所需的私钥信息。 *证书*&#x200B;是您为信任配置的公钥信息。 AEM表单使用证书和凭据用于以下几种用途：

* Acrobat Reader DC扩展使用凭据启用PDF文档中的Adobe Reader使用权。 (请参阅[配置用于Acrobat Reader DC扩展的凭据](/help/forms/using/admin-help/configuring-credentials-acrobat-reader-dc.md#configuring-credentials-for-use-with-acrobat-reader-dc-extensions)。)
* 您可以将Rights Management配置为仅显示来自受信任发行商的凭据，以便在Acrobat使用。 (请参阅[配置Rights Management显示设置](/help/forms/using/admin-help/configuring-client-server-options.md#configure-document-security-display-settings)。) 证书中必须存在公用名称(CN)。
* 签名服务访问证书和凭据。 有关签名服务的详细信息，请参阅[服务引用](https://www.adobe.com/go/learn_aemforms_services_63)。

**生成对密钥**

AEM表单使用其信任存储来存储和管理证书、凭据和证书吊销列表(CRL)。 此外，您可以使用独立的硬件安全模块(HSM)设备存储私钥。

AEM表单不提供任何用于生成密钥对的选项。 但是，您可以使用工具（如Java keytool）生成它，并将它导入AEM表单信任存储。 有关Java密钥工具的详细信息，请参阅：

[https://docs.oracle.com/javase/tutorial/security/toolsign/step3.html](https://docs.oracle.com/javase/tutorial/security/toolsign/step3.html)

[https://docs.oracle.com/cd/E19798-01/821-1841/gjrgy/index.html](https://docs.oracle.com/cd/E19798-01/821-1841/gjrgy/index.html)

[https://blogs.adobe.com/livecycle/2010/01/creating_ssl_keys_and_certific.html](https://blogs.adobe.com/livecycle/2010/01/creating_ssl_keys_and_certific.html)

支持以下签名类型，并可以在AEM表单中导入它们：

* XML签名
* XMLTimeStampToken
* RFC 3161 TimeStampToken
* PKCS#7
* PKCS#1
* DSA签名

**处理丢失或被盗的密钥**

如果您怀疑密钥丢失或已泄露，请采取以下操作：

1. 通知认证机构，以便他们在证书吊销列表中添加被泄露的密钥来撤销该密钥。
1. 从认证机构处获取新密钥及其证书。
1. 使用新密钥再次对使用已泄露的密钥签名的文档进行签名。

