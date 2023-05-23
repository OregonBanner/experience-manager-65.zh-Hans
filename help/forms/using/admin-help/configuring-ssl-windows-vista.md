---
title: 在Windows Vista上設定SSL
seo-title: Configuring SSL on Windows Vista
description: 瞭解如何在Windows Vista上設定SSL。
seo-description: Learn how to configure SSL on Windows Vista.
uuid: 20bfcefb-ec84-4c55-bceb-6af106d883d7
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_ssl
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 667645a0-53d0-4f9b-a0ba-cc7e366a23a1
exl-id: 36c4300d-7a44-41f4-b294-06f32bb01686
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '155'
ht-degree: 0%

---

# 在Windows Vista上設定SSL {#configuring-ssl-on-windows-vista}

若要在Windows Vista™上設定SSL，您需要具有RSA金鑰的SSL憑證以進行驗證。 您可以使用Java keytool來建立憑證。

>[!NOTE]
>
>Windows Vista無法搭配DSA金鑰使用。

您可以使用單一命令來執行keytool，該命令包含建立憑證和keystore所需的所有資訊。

**建立SSL憑證**

1. 在命令提示字元中，瀏覽至 *`[JAVA HOME]`*/bin ，然後輸入以下命令來建立憑證和金鑰存放區：

   `keytool -genkey -keyalg RSA -dname "CN=`*主機名稱* `, OU=`*群組名稱* `, O=`*公司名稱* `,L=`*城市名稱* `, S=`*州* `, C=`*國家/地區代碼* `" -alias`*&quot;LC Cert&quot;* `-keypass` `key`*_* *密碼* `-keystore`*keystorename* `.keystore`

   >[!NOTE]
   >
   >Replace *`[JAVA_HOME]`以安裝JDK的目錄，並將斜體文字取代為與您的環境相對應的值。*

1. 型別 `changeit` 作為密碼。 此密碼是Java安裝的預設密碼，系統管理員可能已將其變更。
