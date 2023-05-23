---
title: 匯入和匯出組態檔
seo-title: Importing and exporting the configuration file
description: 瞭解如何匯入和匯出設定檔案，以編輯伺服器偏好設定或設定其他AEM表單產品執行個體。
seo-description: Learn how to import and export the configuration file in order to edit server preferences or configure another AEM forms product instance.
uuid: 32e8a709-2d7c-4740-9533-d53aa751bc58
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: c1636537-f7dc-48d8-a3f0-9052bcd28b62
exl-id: 225dbeb5-a21c-4338-98c7-e10c32973721
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '254'
ht-degree: 0%

---

# 匯入和匯出組態檔 {#importing-and-exporting-the-configuration-file}

您可以在「手動組態」頁面下載XML格式的組態設定值復本。 此檔案中的設定可控制所有伺服器偏好設定。 然後，您可以編輯檔案並將其上傳回伺服器。 您也可以使用檔案來設定另一個AEM表單產品執行個體。

為了避免安全風險，匯出的組態檔中不包含目錄伺服器的繫結密碼值。 請先更新XML檔案中的密碼，然後再將檔案匯入新系統。

>[!NOTE]
>
>匯入組態檔案會根據檔案中的資訊重新設定AEM表單。 只有熟悉AEM表單產品和XML的系統管理員或專業服務顧問才應考慮修改設定檔。 例如，他們可能需要編輯設定檔案，以重新設定損毀的設定。

**匯出設定資訊**

1. 在Administration Console中，按一下「設定」>「使用者管理」>「組態」>「匯入和匯出組態檔」。
1. 按一下「匯出」。 如果您使用Microsoft Internet Explorer，系統會提示您指定儲存檔案的位置。 如果您使用Firefox，檔案會儲存在您的案頭上。

**匯入組態資訊**

1. 在Administration Console中，按一下「設定」>「使用者管理」>「組態」>「匯入和匯出組態檔」。
1. 按一下「瀏覽」以尋找組態檔，按一下「匯入」，然後按一下「確定」。
