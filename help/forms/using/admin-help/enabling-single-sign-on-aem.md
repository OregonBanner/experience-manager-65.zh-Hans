---
title: 在AEM表單中啟用單一登入
seo-title: Enabling single sign-on in AEM forms
description: 瞭解如何使用HTTP標頭和SPNEGO啟用單一登入(SSO)。
seo-description: Learn how to enable single sign-on (SSO) using HTTP headers and SPNEGO.
uuid: 2bc08b4f-dcbe-4a16-9025-32fc14605e13
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: ee54d9d4-190d-4665-925a-9740ac65fbd5
exl-id: 89561ed0-d094-4ef7-9bc1-bde11f3c5bc3
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1520'
ht-degree: 0%

---

# 在AEM表單中啟用單一登入{#enabling-single-sign-on-in-aem-forms}

AEM forms提供兩種啟用單一登入(SSO)的方式 — HTTP標頭和SPNEGO。

實作SSO時，AEM Forms使用者登入頁面不是必要頁面，且不會在使用者已透過其公司入口網站驗證時顯示。

如果AEM Forms無法使用其中一種方法驗證使用者，系統會將使用者重新導向至登入頁面。

## 使用HTTP標頭啟用SSO {#enable-sso-using-http-headers}

您可以使用「入口網站組態」頁面，在應用程式與任何支援透過HTTP標題傳送身分的應用程式之間啟用單一登入(SSO)。 實作SSO時，AEM Forms使用者登入頁面不是必要頁面，且不會在使用者已透過其公司入口網站驗證時顯示。

您也可以使用SPNEGO來啟用SSO。 (請參閱 [使用SPNEGO啟用SSO](enabling-single-sign-on-aem.md#enable-sso-using-spnego).)

1. 在管理控制檯中，按一下設定>使用者管理>設定>設定入口網站屬性。
1. 選取「是」以啟用SSO。 如果您選取「否」，頁面上的其餘設定將無法使用。
1. 視需要設定頁面上的其餘選項，然後按一下「確定」：

   * **SSO型別：** （必要）選取HTTP標頭以使用HTTP標頭啟用SSO。
   * **使用者識別碼的HTTP標頭：** （必要）其值包含登入使用者唯一識別碼的標頭名稱。 「使用者管理」會使用此值在「使用者管理」資料庫中尋找使用者。 從此標頭取得的值應與從LDAP目錄同步之使用者的唯一識別碼相符。 (請參閱 [使用者設定](/help/forms/using/admin-help/adding-configuring-users.md#user-settings).)
   * **識別碼值對應到使用者的使用者ID，而不是使用者的唯一識別碼：** 將使用者的唯一識別碼值對應至使用者ID。 如果使用者的唯一識別碼是無法透過HTTP標頭輕鬆傳播的二進位值（例如，如果您從Active Directory同步使用者，請選取objectGUID），請選取此選項。
   * **網域的HTTP標題：** （非必要）其值包含網域名稱的標頭名稱。 只有在沒有單一HTTP標頭可唯一識別使用者時，才使用此設定。 如有多個網域且唯一識別碼只在網域內唯一的情況，請使用此設定。 在這種情況下，請在此文字方塊中指定標頭名稱，並在「領域對應」方塊中指定多個領域的領域對應。 (請參閱 [編輯和轉換現有網域](/help/forms/using/admin-help/editing-converting-existing-domains.md#editing-and-converting-existing-domains).)
   * **網域對應：** （必要）指定格式中多個網域的對應 *標頭值=網域名稱*.

      例如，假設某個網域的HTTP標頭是domainName，而且它可能有domain1、domain2或domain3的值。 在這種情況下，請使用網域對應將domainName值對應到User Management網域名稱。 每個對應必須位於不同的行：

      domain1=UMdomain1

      domain2=UMdomain2

      domain3=UMdomain3

### 設定允許的查閱者 {#configure-allowed-referers}

如需設定允許的反向連結的步驟，請參閱 [設定允許的查閱者](/help/forms/using/admin-help/preventing-csrf-attacks.md#configure-allowed-referers).

## 使用SPNEGO啟用SSO {#enable-sso-using-spnego}

在Windows環境中使用Active Directory做為LDAP伺服器時，您可以使用簡單和受保護的GSSAPI交涉機制(SPNEGO)來啟用單一登入(SSO)。 啟用SSO時，AEM Forms使用者登入頁面不是必要專案，也不會出現。

您也可以使用HTTP標頭來啟用SSO。 (請參閱 [使用HTTP標頭啟用SSO](enabling-single-sign-on-aem.md#enable-sso-using-http-headers).)

>[!NOTE]
>
>JEE上的AEM Forms不支援在多個子網域環境中使用Kerberos/SPNEGO設定SSO。

1. 決定要使用哪個網域來啟用SSO。 AEM Forms伺服器和使用者必須屬於相同的Windows網域或受信任的網域。
1. 在Active Directory中，建立代表AEM表單伺服器的使用者。 (請參閱 [建立使用者帳戶](enabling-single-sign-on-aem.md#create-a-user-account).) 如果您要設定多個網域來使用SPNEGO，請確定每個使用者的密碼不同。 如果密碼不同，SPNEGO SSO將無法運作。
1. 對應服務主體名稱。 (請參閱 [對應服務主體名稱(SPN)](enabling-single-sign-on-aem.md#map-a-service-principal-name-spn).)
1. 設定網域控制站。 (請參閱 [防止Kerberos完整性檢查失敗](enabling-single-sign-on-aem.md#prevent-kerberos-integrity-check-failures).)
1. 新增或編輯企業網域，如所述 [新增網域](/help/forms/using/admin-help/adding-domains.md#adding-domains) 或 [編輯和轉換現有網域](/help/forms/using/admin-help/editing-converting-existing-domains.md#editing-and-converting-existing-domains). 當您建立或編輯企業網域時，請執行下列工作：

   * 新增或編輯包含Active Directory資訊的目錄。
   * 將LDAP新增為驗證提供者。
   * 將Kerberos新增為驗證提供者。 在Kerberos的「新增驗證」或「編輯驗證」頁面上提供下列資訊：

      * **驗證提供者：** Kerberos
      * **DNS IP：** 執行AEM表單的伺服器的DNS IP位址。 您可以執行以判斷此IP位址 `ipconfig/all` 在命令列上。
      * **KDC主機：** 用於驗證的Active Directory伺服器的完整主機名稱或IP位址
      * **服務使用者：** 傳遞到KtPass工具的服務主體名稱(SPN)。 在先前使用的範例中，服務使用者為 `HTTP/lcserver.um.lc.com`.
      * **服務範圍：** Active Directory網域名稱。 在先前使用的範例中，網域名稱為 `UM.LC.COM.`
      * **服務密碼：** 服務使用者的密碼。 在先前使用的範例中，服務密碼為 `password`.
      * **啟用SPNEGO：** 允許使用SPNEGO進行單一登入(SSO)。 選取此選項。

1. 設定SPNEGO使用者端瀏覽器設定。 (請參閱 [正在設定SPNEGO使用者端瀏覽器設定](enabling-single-sign-on-aem.md#configuring-spnego-client-browser-settings).)

### 建立使用者帳戶 {#create-a-user-account}

1. 在SPNEGO中，將服務註冊為網域控制站上Active Directory中的使用者，以代表AEM表單。 在網域控制站上，移至[開始]功能表>系統管理工具> Active Directory使用者和電腦。 如果[Administrative Tools]不在[Start]功能表中，請使用[Control Panel]。
1. 按一下「使用者」資料夾以顯示使用者清單。
1. 以滑鼠右鍵按一下使用者資料夾，然後選取「新增>使用者」。
1. 輸入「名字/姓氏」和「使用者登入名稱」，然後按「下一步」。 例如，設定下列值：

   * **名字**：umspnego
   * **使用者登入名稱**： spnegodemo

1. 輸入密碼。 例如，將其設為 *密碼*. 確保已選取「密碼永不過期」，且未選取其他選項。
1. 按一下「下一步」，然後按一下「完成」。

### 對應服務主體名稱(SPN) {#map-a-service-principal-name-spn}

1. 取得KtPass公用程式。 此公用程式可用來將SPN對應至REALM。 您可以取得KtPass公用程式作為Windows Server Tool Pack或Resource Kit的一部分。 (請參閱 [Windows Server 2003 Service Pack 1支援工具](https://support.microsoft.com/kb/892777).)
1. 在命令提示字元中，執行 `ktpass` 使用下列引數：

   `ktpass -princ HTTP/`*主機* `@`*領域* `-mapuser`*使用者*

   例如，輸入下列文字：

   `ktpass -princ HTTP/lcserver.um.lc.com@UM.LC.COM -mapuser spnegodemo`

   您必須提供的值說明如下：

   **主機：** 表單伺服器的完整名稱或任何唯一URL。 在此範例中，它被設定為lcserver.um.lc.com。

   **範圍：** 網域控制站的Active Directory範圍。 在此範例中，它被設定為UM.LC.COM。 請確定您以大寫字元輸入範圍。 若要判斷Windows 2003的領域，請完成下列步驟：

   * 用滑鼠右鍵按一下「我的電腦」並選取「內容」
   * 按一下「電腦名稱」標籤。 「網域名稱」值是範圍名稱。

   **使用者：** 您在上一個任務中建立的使用者帳戶的登入名稱。 在此範例中，它被設定為spnegedemo。

如果您遇到此錯誤：

```shell
DsCrackNames returned 0x2 in the name entry for spnegodemo.
ktpass:failed getting target domain for specified user.
```

請嘗試將使用者指定為spnegodemo@um.lc.com：

```shell
ktpass -princ HTTP/lcserver.um.lc.com@UM.LC.COM -mapuser spnegodemo
```

### 防止Kerberos完整性檢查失敗 {#prevent-kerberos-integrity-check-failures}

1. 在網域控制站上，移至[開始]功能表>系統管理工具> Active Directory使用者和電腦。 如果[Administrative Tools]不在[Start]功能表中，請使用[Control Panel]。
1. 按一下「使用者」資料夾以顯示使用者清單。
1. 以滑鼠右鍵按一下您在前一個任務中建立的使用者帳戶。 在此範例中，使用者帳戶為 `spnegodemo`.
1. 按一下「重設密碼」。
1. 輸入並確認您先前輸入的密碼。 在此範例中，設定為 `password`.
1. 取消選取「下次登入時變更密碼」，然後按一下「確定」。

### 正在設定SPNEGO使用者端瀏覽器設定 {#configuring-spnego-client-browser-settings}

若要讓SPNEGO型驗證能夠運作，使用者端電腦必須是建立使用者帳戶所在網域的一部分。 您也必須設定使用者端瀏覽器，以允許以SPNEGO為基礎的驗證。 此外，需要SPNEGO式驗證的網站必須是受信任的網站。

如果使用電腦名稱(例如https://lcserver:8080)存取伺服器，則Internet Explorer不需要任何設定。 如果您輸入的URL不包含任何點(「。」)，Internet Explorer會將網站視為本機內部網路網站。 如果您使用網站的完整名稱，則必須將網站新增為受信任的網站。

**設定Internet Explorer 6.x**

1. 前往「工具>網際網路選項」，然後按一下「安全性」標籤。
1. 按一下「本機內部網路」圖示，然後按一下「網站」。
1. 按一下「進階」，然後在「將此網站新增至區域」方塊中，輸入表單伺服器的URL。 例如，輸入 `https://lcserver.um.lc.com`
1. 按一下「確定」，直到關閉所有對話方塊。
1. 存取AEM表單伺服器的URL以測試設定。 例如，在瀏覽器URL方塊中，輸入 `https://lcserver.um.lc.com:8080/um/login?um_no_redirect=true`

**設定Mozilla Firefox**

1. 在瀏覽器URL方塊中，輸入 `about:config`

   about：config - Mozilla Firefox對話方塊隨即出現。

1. 在「篩選」方塊中，輸入 `negotiate`
1. 在顯示的清單中，按一下network.negotiate-auth.trusted-uri，然後輸入適合您環境的下列命令之一：

   `.um.lc.com` — 將Firefox設定為允許任何以um.lc.com結尾的URL使用SPNEGO。 請務必加入點(「。」) 在開頭。

   `lcserver.um.lc.com`  — 將Firefox設定為僅允許特定伺服器使用SPNEGO。 此值不能以點(「。」)開頭。

1. 存取應用程式以測試設定。 目標應用程式的歡迎頁面應該會出現。
