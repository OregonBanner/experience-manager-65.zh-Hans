---
title: 設定屬性的加密支援
seo-title: Encryption Support for Configuration Properties
description: 設定屬性的加密支援
seo-description: null
uuid: 26dc5e46-9332-4d9b-8874-895b90391e8c
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: security
discoiquuid: 4e08c297-aa4b-44cf-84c8-1e11582d9ebb
exl-id: 3c3db1c8-5b22-45dd-aeaf-5cf830a9486b
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '277'
ht-degree: 0%

---

# 設定屬性的加密支援{#encryption-support-for-configuration-properties}

## 概述 {#overview}

此功能可讓所有OSGi設定屬性以受保護的加密格式儲存，而非純文字。 Web主控台UI中的表單可用來使用系統範圍加密主金鑰，從純文字建立加密文字。

已新增OSGi設定外掛程式支援，以便在服務使用屬性之前將其解密。

>[!NOTE]
>
>預期加密值的服務需要使用IsProtected檢查，在嘗試解密值之前檢視值是否已加密，因為它可能已解密。

## 啟用加密支援 {#enabling-encryption-support}

這些步驟顯示如何加密Mail服務的SMTP密碼。 您可以針對要加密的OSGI屬性完成這些步驟。

1. 前往AEM Web Console，網址為 *https://&lt;serveraddress>：&lt;serverport>/system/console/configMgr*
1. 在左上角，前往 **主要 — 加密支援**

   ![chlimage_1-325](assets/chlimage_1-325.png)

1. 此 **Adobe Experience Manager Web主控台Crypto支援** 頁面隨即顯示。

   ![screen_shot_2018-08-01at113417am](assets/screen_shot_2018-08-01at113417am.png)

1. 在 **純文字** 欄位中，輸入要保護的敏感資料文字。
1. 選取 **Protect**. 受保護文字會顯示為加密文字。

   ![screen_shot_2018-08-01at113844am](assets/screen_shot_2018-08-01at113844am.png)

1. 從Step#5複製受保護的文字，並將其貼到OSGI表單值中。 在此範例中，已解密 **SMTP密碼** 新增至 *Day CQ郵件服務*.

   ![screen_shot_2016-12-18at105809pm](assets/screen_shot_2016-12-18at105809pm.png)

1. 儲存Day CQ Mail Service屬性。 SMTP密碼現在會以加密值傳送。

## 解密支援 {#decryption-support}

AEM現在提供設定外掛程式，以解密設定屬性。 此AEM外掛程式會自動解密及擷取純文字屬性。
