---
title: 設定SAML服務提供者設定
seo-title: Configure SAML service provider settings
description: 您可以設定SAML服務提供者設定，讓使用者透過指定的第三方身分提供者(IDP)登入並驗證AEM表單。
seo-description: You can configure SAML service provider settings to allow users to login and authenticate to AEM forms via a specified third-party identity provider (IDP).
uuid: 14c706ad-8b1c-4c03-9cd4-97424f2162bc
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 1169d0d1-cbfb-486b-acca-9b9de3d410dc
exl-id: dd302cfb-eae1-4189-aa7b-9f2533ebd164
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '599'
ht-degree: 0%

---

# 設定SAML服務提供者設定{#configure-saml-service-provider-settings}

安全性宣告標籤語言(SAML)是您設定企業或混合網域授權時可以選取的選項之一。 SAML主要用於支援跨多個網域的SSO。 當SAML設定為您的驗證提供者時，使用者會透過指定的協力身分識別提供者(IDP)登入並驗證AEM Forms。

如需SAML的說明，請參閱 [安全性判斷提示標籤語言(SAML) V2.0技術概覽](https://www.oasis-open.org/committees/download.php/20645/sstc-saml-tech-overview-2%200-draft-10.pdf).

1. 在管理控制檯中，按一下「設定>使用者管理>組態> SAML服務提供者設定」。
1. 在「服務提供者實體ID」方塊中，輸入唯一ID以用作AEM Forms服務提供者實作的識別碼。 您也可以在設定IDP時指定此唯一ID (例如， `um.lc.com`.) 您也可以使用用來存取AEM表單的URL (例如， `https://AEMformsserver`)。
1. 在「服務提供者基本URL」方塊中，輸入表單伺服器的基本URL (例如， `https://AEMformsserver:8080`)。
1. （可選）若要讓AEM表單傳送已簽署的驗證要求給IDP，請執行下列工作：

   * 使用信任管理員匯入PKCS #12格式的認證，並選取[檔案簽署認證]作為[信任存放區型別]。 (請參閱 [管理本機認證](/help/forms/using/admin-help/local-credentials.md#managing-local-credentials).)
   * 在「服務提供者認證金鑰別名」清單中，選取您在「信任存放區」中指派給認證的別名。
   * 按一下「匯出」將URL內容儲存至檔案，然後將該檔案匯入您的IDP。

1. （選擇性）在「服務提供者名稱ID原則」清單中，選取IDP在SAML判斷提示中用來識別使用者的名稱格式。 選項包括「未指定」、「電子郵件」和「Windows網域限定名稱」。

   >[!NOTE]
   >
   >名稱格式不區分大小寫。

1. （選擇性）選取「啟用本機使用者的驗證提示」。 選取此選項時，使用者會看到兩個連結：

   * 第三方SAML識別提供者登入頁面的連結，屬於企業網域的使用者可在此進行驗證。
   * AEM表單登入頁面的連結，屬於本機網域的使用者可在此進行驗證。

   未選取此選項時，系統會將使用者直接帶至第三方SAML身分提供者的登入頁面，屬於企業網域的使用者可在此進行驗證。

1. （選用）選取「啟用成品繫結」以啟用成品繫結支援。 根據預設，POST繫結會與SAML搭配使用。 但如果您已設定成品繫結，請選取此選項。 選取此選項時，實際的使用者判斷提示不會透過瀏覽器請求傳遞。 相反地，會傳遞一個指向宣告的指標，並使用後端Web服務呼叫來擷取宣告。
1. （選擇性）選取「啟用重新導向繫結」以支援使用重新導向的SAML繫結。
1. （選用）在自訂屬性中，指定其他屬性。 其他屬性是以新行分隔的名稱=值組。

   * 您可以設定AEM表單，針對符合協力廠商判斷提示的有效期間的有效期間發出SAML判斷提示。 若要遵守第三方SAML宣告逾時，請在自訂屬性中新增下列行：

      `saml.sp.honour.idp.assertion.expiry=true`

   * 新增下列自訂屬性，以使用RelayState來判斷在成功驗證後要將使用者重新導向的URL。

      `saml.sp.use.relaystate=true`

   * 新增下列自訂屬性，以設定自訂Java Server Pages (JSP)的URL，其將用於呈現已註冊的身分識別提供者清單。 如果您尚未部署自訂Web應用程式，它將使用預設的「使用者管理」頁面來呈現清單。

   `saml.sp.discovery.url=/custom/custom.jsp`

1. 单击“保存”。
