---
title: 管理证书
seo-title: 管理证书
description: 了解如何导入和导出证书以及编辑其信任设置。
seo-description: 了解如何导入和导出证书以及编辑其信任设置。
uuid: 46b1dbe5-517c-4294-bb52-cc6700a768e8
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_certificates_and_credentials
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 9fd531c0-5206-4be0-a450-13e0dc806068
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '656'
ht-degree: 0%

---


# 管理证书{#managing-certificates}

使用信任存储管理，您可以导入、编辑和删除您信任的证书，以验证数字签名和证书身份验证。 您可以导入和导出任意数量的证书。 导入证书后，您可以编辑信任设置和信任存储类型。 组合信任存储类型时，请考虑以下选项：

* **使用CA信任证书身份验证：对于** CRL验证，请选择“信任身份”。
* **使用ICA信任证书身份验证：** 仅选择信任身份。不应信任ICA进行证书身份验证。 如果信任ICA进行证书身份验证，则ICA将成为路径构建的CA。 如果ICA在证书身份验证和标识方面都受信任，则忽略CA供应商证书，因为ICA将成为CA。
* **OCSP服务器与HTTP的信** 任：如果OSCP响应服务器位于HTTPs位置，则还必须选择“信任SSL连接”。如果OSCP答复者需要CRL验证，请确保您还选择“信任身份”。
* **Adobe根：** 不选择SSL连接或OCSP服务器信任存储类型。Adobe根对于SSL连接和OCSP服务器不受信任。 Adobe不颁发OCSP和SSL证书。 Adobe根被隐式信任，别名为=&quot;ADOBEROOT&quot;。

仅支持X509v3证书。 此证书类型可以以二进制DER编码文件（.cer文件）或包含同一DER编码证书(包括X509证书，以隐私增强邮件(PEM)格式)的Base64编码版本的文本文件提供。

完成签名验证所需的证书必须位于同一存储（HSM或数据库）中。

您还可以使用信任管理器API导入和删除证书。 有关详细信息，请参阅AEM forms](https://www.adobe.com/go/learn_aemforms_programming_63)编程[中的“使用信任管理器API导入证书”和“使用信任管理器API删除证书”。

## 导入证书{#import-a-certificate}

1. 在管理控制台中，单击&#x200B;**[!UICONTROL 设置>信任存储管理>证书]**。
1. 单击“导入”，在“信任存储类型”下，选择下列选项之一：

   * **信任SSL连接：指** 定AEM表单可以使用证书通过SSL连接到外部系统。
   * **信任认证签名：指** 定证书在验证作者数字签名的文档签名操作中受信任。
   * **信任签名：指** 定证书在非作者数字签名的文档签名操作中受信任。
   * **证书身份验证信任：指** 定AEM表单使用证书对使用证书或智能卡身份验证的用户进行身份验证。
   * **信任OCSP服务器：指** 定AEM表单可以使用证书连接到外部OCSP响应器
   * **身份信任：指** 定证书可用于信任除上述指定类型以外的信息。

   >[!NOTE]
   >
   >信任存储隐式信任Adobe根证书以进行证书身份验证、签名、验证签名和标识。

1. 在“别名”框中，键入证书的标识符。
1. 单击&#x200B;**[!UICONTROL 浏览]**&#x200B;以找到证书，然后单击&#x200B;**[!UICONTROL 确定]**。

## 导出证书{#export-a-certificate}

1. 在管理控制台中，单击&#x200B;**[!UICONTROL 设置>信任存储管理>证书]**。
1. 单击要导出的证书的别名。 将显示&#x200B;**[!UICONTROL 证书详细信息]**&#x200B;页。
1. 单击&#x200B;**[!UICONTROL 导出]**，按照指示导出证书，然后单击&#x200B;**[!UICONTROL 确定]**。

## 编辑证书的信任设置和信任存储类型{#edit-a-certificate-s-trust-settings-and-trust-store-type}

1. 在管理控制台中，单击&#x200B;**[!UICONTROL 设置>信任存储管理>证书]**。
1. 单击要编辑的证书的别名。
1. 单击&#x200B;**[!UICONTROL 更新证书]**。
1. 要更改证书的别名，请在“别名”框中键入新名称。
1. 要更新证书的信任存储类型，请选择相应的信任存储类型。
1. 要更新策略限制，请在“证书策略”框中键入策略信息，然后单击&#x200B;**[!UICONTROL 确定]**。

## 删除证书{#delete-a-certificate}

1. 在管理控制台中，单击&#x200B;**[!UICONTROL 设置>信任存储管理>证书]**。
1. 选中要删除的证书的复选框，单击&#x200B;**[!UICONTROL 删除]**，然后单击&#x200B;**[!UICONTROL 确定]**。

