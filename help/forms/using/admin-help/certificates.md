---
title: 管理证书
seo-title: Managing certificates
description: 了解如何导入和导出证书并编辑其信任设置。
seo-description: Learn how to import and export a certificate and edit its trust settings.
uuid: 46b1dbe5-517c-4294-bb52-cc6700a768e8
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_certificates_and_credentials
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 9fd531c0-5206-4be0-a450-13e0dc806068
exl-id: 1fe0e7b4-6109-4f7a-8858-8237a1c5c93b
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '641'
ht-degree: 0%

---

# 管理证书 {#managing-certificates}

使用信任存储区管理，您可以导入、编辑和删除信任在服务器上的证书，以验证数字签名和证书身份验证。 您可以导入和导出任意数量的证书。 导入证书后，可以编辑信任设置和信任存储类型。 组合信任存储类型时，请考虑以下选项：

* **信任使用CA的证书身份验证：** 对于CRL验证，也请选择“信任身份”。
* **信任使用ICA进行证书身份验证：** 仅选择“信任身份”。 不应信任ICA进行证书身份验证。 如果您信任ICA进行证书身份验证，则ICA将成为用于路径构建的CA。 如果ICA在证书身份验证和身份方面都受信任，则CA供应商证书将被忽略，因为ICA将成为CA。
* **信任具有HTTP的OCSP服务器：** 如果OSCP响应服务器驻留在HTTPs位置，则还必须选择“信任SSL连接”。 如果OSCP响应者需要CRL验证，请确保您还选择“信任身份”。
* **Adobe根目录：** 请勿选择SSL连接或OCSP服务器信任存储类型。 对于SSL连接和OCSP服务器，Adobe根不受信任。 Adobe不颁发OCSP和SSL证书。 Adobe根被隐式信任，别名为“ADOBEROOT”。

仅支持X509v3证书。 此证书类型可以在二进制DER编码文件（.cer文件）或包含同一DER编码证书的Base64编码版本的文本文件(包括Privacy Enhanced Mail (PEM)格式的X509证书)中提供。

完成签名验证所需的证书必须位于同一存储区（HSM或数据库）中。

您还可以使用信任管理器API导入和删除证书。 有关详细信息，请参阅中的“使用信任管理器API导入证书”和“使用信任管理器API删除证书” [使用AEM表单编程](https://www.adobe.com/go/learn_aemforms_programming_63).

## 导入证书 {#import-a-certificate}

1. 在管理控制台中，单击 **[!UICONTROL 设置>信任存储区管理>证书]**.
1. 单击“导入”，然后在“信任存储类型”下，选择以下选项之一：

   * **SSL连接信任：** 指定AEM表单可使用证书通过SSL连接到外部系统。
   * **信任证书签名：** 指定在文档签名操作中信任证书以验证作者数字签名。
   * **信任签名：** 指定证书在非作者数字签名的文档签名操作中受信任。
   * **信任证书身份验证：** 指定AEM Forms使用证书来通过证书或智能卡身份验证对用户进行身份验证。
   * **OCSP服务器的信任：** 指定AEM表单可以使用证书连接到外部OCSP响应程序
   * **信任身份：** 指定证书可用于信任上述类型以外的信息。

   >[!NOTE]
   >
   >信任存储区隐式信任Adobe根证书以进行证书身份验证、签名、证书签名和身份。

1. 在“别名”框中，键入证书的标识符。
1. 单击 **[!UICONTROL 浏览]** 找到证书，然后单击 **[!UICONTROL 确定]**.

## 导出证书 {#export-a-certificate}

1. 在管理控制台中，单击 **[!UICONTROL 设置>信任存储区管理>证书]**.
1. 单击要导出的证书的别名。 此 **[!UICONTROL 证书详细信息]** 页面。
1. 单击 **[!UICONTROL 导出]**，按照说明导出证书，然后单击 **[!UICONTROL 确定]**.

## 编辑证书的信任设置和信任存储类型 {#edit-a-certificate-s-trust-settings-and-trust-store-type}

1. 在管理控制台中，单击 **[!UICONTROL 设置>信任存储区管理>证书]**.
1. 单击要编辑的证书的别名。
1. 单击 **[!UICONTROL 更新证书]**.
1. 要更改证书的别名，请在“别名”框中键入新名称。
1. 要更新证书的信任存储类型，请选择适当的信任存储类型。
1. 要更新策略限制，请在证书策略框中键入策略信息，然后单击 **[!UICONTROL 确定]**.

## 删除证书 {#delete-a-certificate}

1. 在管理控制台中，单击 **[!UICONTROL 设置>信任存储区管理>证书]**.
1. 选中要删除的证书对应的复选框，然后单击 **[!UICONTROL 删除]**，然后单击 **[!UICONTROL 确定]**.
