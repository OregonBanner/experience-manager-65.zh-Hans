---
title: 管理本機認證
seo-title: Managing local credentials
description: 瞭解如何管理本機認證。
seo-description: Learn how to manage local credentials.
uuid: 3c4358e0-aaff-4e94-a6b2-04b463fca260
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_certificates_and_credentials
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 598a9a03-3773-4620-8867-1f754d8ca031
exl-id: c5905272-7d09-47e4-8b35-4cc25a148477
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '501'
ht-degree: 0%

---

# 管理本機認證 {#managing-local-credentials}

本機認證是在信任存放區管理中託管的私密金鑰認證。 A *本機認證* 識別儲存使用者DES認證的位置。 使用「信任存放區管理」，您可以使用現有的PFX檔案來匯入和管理本機認證，以便可以匯入、編輯和刪除本機認證。

AEM forms支援標準PKCS12格式（.pfx和.p12檔案）中最多4096位元的RSA和DSA憑證。

您可以匯入和匯出任意數量的認證。 如果您想使用相同的別名來取代過期的認證，請刪除認證，然後使用相同的別名匯入新的認證。

如需Acrobat Reader DC擴充功能的相關資訊和指示，請參閱 [設定用於Acrobat Reader DC擴充功能的認證](/help/forms/using/admin-help/configuring-credentials-acrobat-reader-dc.md#configuring-credentials-for-use-with-acrobat-reader-dc-extensions).

## 匯入認證 {#import-a-credential}

1. 在管理控制檯中，按一下「設定」>「信任存放區管理」>「本機認證」。
1. 按一下「匯入」。 在「信任存放區型別」下，選取下列其中一個選項：

   * **檔案簽署認證：** 用於在檔案上簽發數位簽章的認證。
   * **Acrobat Reader DC擴充功能認證：** Acrobat Reader DC擴充功能專屬的數位憑證，可讓您在產生的PDF檔案中啟用Adobe Reader使用許可權。
   * **預設：** 指出這是搭配Acrobat Reader DC擴充功能使用的預設認證。

   如需取得認證的相關資訊，請參閱 [準備安裝AEM表單](https://www.adobe.com/go/learn_aemforms_prepareInstallsingle_63).

1. 在「別名」方塊中，輸入認證的識別碼。 此識別碼會用作Acrobat Reader DC擴充功能和Signature service中認證的顯示名稱。 此別名也可用來透過AEM Forms SDK以程式設計方式存取認證。

   >[!NOTE]
   >
   >別名會自動轉換為大寫，以便顯示。 您在程式中參考別名時，別名名稱不區分大小寫。

1. 按一下「瀏覽」以尋找證明資料，輸入證明資料的密碼，然後按一下「確定」。

   如果出現錯誤訊息「由於檔案格式不正確或密碼不正確而無法匯入認證」，請確認密碼有效。

## 匯出認證 {#export-a-credential}

認證會匯出為PKCS#12格式的P12檔案。

1. 在管理控制檯中，按一下「設定」>「信任存放區管理」>「本機認證」。
1. 按一下要匯出的認證的別名，然後按一下匯出。
1. 在「密碼」方塊中，輸入密碼。 此密碼是新密碼，用於加密匯出的認證。
1. 按一下「匯出」，依照指示匯出證明資料，然後按一下「確定」。

## 編輯認證的別名或信任存放區型別 {#edit-a-credential-s-alias-or-trust-store-type}

匯入認證後，您可以編輯其別名名稱和信任存放區型別。

1. 在管理控制檯中，按一下「設定」>「信任存放區管理」>「本機認證」。
1. 按一下您要編輯之認證的別名。
1. 按一下「更新認證」。
1. 視需要編輯別名名稱和信任存放區型別，然後按一下「確定」。

## 刪除認證 {#delete-a-credential}

1. 在管理控制檯中，按一下「設定」>「信任存放區管理」>「本機認證」。
1. 選取要刪除的認證核取方塊。
1. 按一下「刪除」，然後按一下「確定」。
