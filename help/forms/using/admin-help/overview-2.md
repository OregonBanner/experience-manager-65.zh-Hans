---
title: 管理憑證和憑證的基本知識
seo-title: Basics of managing certificates and credentials
description: 瞭解管理憑證和憑證的基本知識。
seo-description: Learn about the basics of managing certificates and credentials.
uuid: f421e206-e7b5-416c-b9fb-974094f10a66
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_certificates_and_credentials
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 986d16fc-4c81-4785-b1f3-fe8bd7ff669e
exl-id: 74bf0e77-f47b-475a-b2a7-52cfb3baaa22
source-git-commit: 0c7dba43dad8608b4a5de271e1e44942c950fb16
workflow-type: tm+mt
source-wordcount: '339'
ht-degree: 0%

---

# 管理憑證和憑證的基本知識 {#basics-of-managing-certificates-and-credentials}

A *認證* 包含您簽署或識別檔案所需的私密金鑰資訊。 A *憑證* 是您為信任而設定的公開金鑰資訊。 AEM forms將憑證和認證用於多種用途：

* Acrobat Reader DC擴充功能會使用認證來啟用PDF檔案中的Adobe Reader使用許可權。 (請參閱 [設定用於Acrobat Reader DC擴充功能的認證](/help/forms/using/admin-help/configuring-credentials-acrobat-reader-dc.md#configuring-credentials-for-use-with-acrobat-reader-dc-extensions).)
* 您可以設定Rights Management，以顯示只有來自受信任發行者的憑證以用於Acrobat。 (請參閱 [設定Rights Management顯示設定](/help/forms/using/admin-help/configuring-client-server-options.md#configure-document-security-display-settings).) 通用名稱(CN)必須存在於憑證中。
* 簽章服務會存取憑證和認證。 如需Signature服務的詳細資訊，請參閱 [服務參考](https://www.adobe.com/go/learn_aemforms_services_65).

**產生配對金鑰**

AEM Forms使用其「信任存放區」來儲存和管理憑證、憑證和憑證撤銷清單(CRL)。 此外，您可以使用獨立的Hardware Security Module (HSM)裝置來儲存私密金鑰。

AEM forms不提供任何選項來產生金鑰組。 不過，您可以使用Java keytool等工具產生它，並將其匯入AEM Forms信任存放區。 如需Java keytool的詳細資訊，請參閱下列內容：

[https://docs.oracle.com/javase/tutorial/security/toolsign/step3.html](https://docs.oracle.com/javase/tutorial/security/toolsign/step3.html)

[https://docs.oracle.com/cd/E19798-01/821-1841/gjrgy/index.html](https://docs.oracle.com/cd/E19798-01/821-1841/gjrgy/index.html)

[https://helpcenter.gsx.com/hc/en-us/articles/115015960428-How-to-Generate-a-Self-Signed-Certificate-and-Private-Key-using-OpenSSL](https://helpcenter.gsx.com/hc/en-us/articles/115015960428-How-to-Generate-a-Self-Signed-Certificate-and-Private-Key-using-OpenSSL)

下列簽章型別受到支援，並可在AEM Forms中匯入：

* XML簽章
* XMLTimeStampToken
* RFC 3161 TimeStampToken
* PKCS#7
* PKCS#1
* DSA簽章

**處理遺失或損壞的金鑰**

如果您懷疑您的金鑰已遺失或已遭侵入，請採取下列動作：

1. 通知憑證授權單位，讓他們將損壞的金鑰新增到憑證撤銷清單中，以撤銷金鑰。
1. 從憑證授權單位取得新金鑰及其憑證。
1. 使用新金鑰再次簽署使用洩露金鑰簽署的檔案。
