---
title: 設定驗證服務提供者
seo-title: Configuring authentication providers
description: 新增、編輯或刪除驗證提供者、變更驗證設定，以及閱讀有關即時布建使用者的資訊。
seo-description: Add, edit, or delete authentication providers, change authentication settings, and read about just-in-time provisioning of users.
uuid: 90e7690b-1ce0-4604-b58f-6dca4f2372cf
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/setting_up_and_managing_domains
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 31dd8db3-ddac-429e-82f8-8c5dc4ffc186
exl-id: d72a3977-1423-49e0-899b-234bb76be378
source-git-commit: 1cdd15800548362ccdd9e70847d9df8ce93ee06e
workflow-type: tm+mt
source-wordcount: '1576'
ht-degree: 0%

---

# 設定驗證服務提供者 {#configuring-authentication-providers}

混合式網域至少需要一個驗證提供者，而企業網域至少需要一個驗證提供者或目錄提供者。

如果您使用SPNEGO啟用SSO，請新增已啟用SPNEGO的Kerberos驗證提供者和LDAP提供者作為備份。 如果SPNEGO無法運作，此設定會啟用具有使用者ID和密碼的使用者驗證。 (請參閱 [使用SPNEGO啟用SSO](/help/forms/using/admin-help/enabling-single-sign-on-aem.md#enable-sso-using-spnego).)

## 新增驗證提供者 {#add-an-authentication-provider}

1. 在管理控制檯中，按一下「設定>使用者管理>網域管理」。
1. 按一下清單中的現有網域。 如果您要新增新網域的驗證，請參閱 [新增企業網域](/help/forms/using/admin-help/adding-domains.md#add-an-enterprise-domain) 或 [新增混合網域](/help/forms/using/admin-help/adding-domains.md#add-a-hybrid-domain).
1. 按一下「新增驗證」，然後在「驗證提供者」清單中，根據您的組織所使用的驗證機制選取提供者。
1. 在頁面上提供所需的任何其他資訊。 (請參閱 [驗證設定](configuring-authentication-providers.md#authentication-settings).)
1. （選用）按一下「測試」以測試設定。
1. 按一下「確定」，然後再次按一下「確定」。

## 編輯現有的驗證提供者 {#edit-an-existing-authentication-provider}

1. 在管理控制檯中，按一下「設定>使用者管理>網域管理」。
1. 按一下清單中適當的網域。
1. 在出現的頁面上，從清單中選取適當的驗證提供者，並視需要進行變更。 (請參閱 [驗證設定](configuring-authentication-providers.md#authentication-settings).)
1. 单击确定。

## 刪除驗證提供者 {#delete-an-authentication-provider}

1. 在管理控制檯中，按一下「設定>使用者管理>網域管理」。
1. 按一下清單中適當的網域。
1. 選取要刪除的驗證提供者核取方塊，然後按一下刪除。
1. 在出現的確認頁面上按一下「確定」，然後再次按一下「確定」。

## 驗證設定 {#authentication-settings}

根據您選擇的網域型別和驗證型別，可使用下列設定。

### LDAP設定 {#ldap-settings}

如果您要設定企業或混合式網域的驗證，並選取LDAP驗證，您可以選擇使用目錄組態中指定的LDAP伺服器，或者選擇不同的LDAP伺服器來用於驗證。 如果您選擇不同的伺服器，您的使用者必須存在於兩個LDAP伺服器上。

若要使用目錄組態中指定的LDAP伺服器，請選取LDAP作為驗證提供者，然後按一下確定。

若要使用不同的LDAP伺服器來執行驗證，請選取LDAP作為驗證提供者，然後選取「自訂LDAP驗證」核取方塊。 下列組態設定會顯示。

**伺服器：** （必要）目錄伺服器的完整網域名稱(FQDN)。 例如，在example.com網路上名為x的電腦，FQDN是x.example.com。 可以使用IP位址取代FQDN伺服器名稱。

**連線埠：** （必要）目錄伺服器使用的連線埠。 通常為389，如果安全通訊端層(SSL)通訊協定用於透過網路傳送驗證資訊，則為636。

**SSL：** （必要）指定在透過網路傳送資料時，目錄伺服器是否使用SSL。 預設值為「否」。 設定為Yes時，應用程式伺服器的Java™執行階段環境(JRE)必須信任對應的LDAP伺服器憑證。

**繫結** （必要）指定存取目錄的方式。

**匿名：** 不需要使用者名稱或密碼。

**使用者：** 需要驗證。 在「名稱」方塊中，指定可存取目錄的使用者記錄名稱。 最好輸入使用者帳戶的完整辨別名稱(DN)，例如cn=Jane Doe、ou=user、dc=can、dc=com。 在「密碼」方塊中，指定相關的密碼。 當您選取「使用者」作為「繫結」選項時，需要這些設定。

**擷取基本DN：** （非必要）擷取基本DN並在下拉式清單中顯示它們。 當您有多個基本DN且需要選取值時，此設定很有用。

**基本DN：** （必要）用來作為從LDAP階層同步化使用者和群組的起點。 最好在階層的最低層級指定基本DN，該階層包含需要同步處理服務的所有使用者和群組。 請勿在此設定中包含使用者的DN。 若要同步特定使用者，請使用「搜尋篩選器」設定。

**將以下專案填入頁面：** （非必要）選取時，會使用對應的預設LDAP值填入「使用者」和「群組」設定頁面上的屬性。

**搜尋篩選器：** （必要）用來尋找與使用者相關聯之記錄的搜尋篩選器。 請參閱搜尋篩選語法。

### Kerberos設定 {#kerberos-settings}

如果您要設定企業或混合式網域的驗證，並選取Kerberos驗證，則可使用下列設定。

**DNS IP：** 執行AEM表單的伺服器的DNS IP位址。 在Windows上，您可以在命令列執行ipconfig /all來判斷此IP位址。

**KDC主機：** 用於驗證的Active Directory伺服器的完整主機名稱或IP位址。

**服務使用者：** 如果您使用的是Active Directory 2003，此值是在表單中為服務主體建立的對應 `HTTP/<server name>`. 如果您使用Active Directory 2008，這個值就是服務主體的登入ID。 例如，假設服務主體名為um spnego，使用者ID為spnegedemo，對應為HTTP/example.yourcompany.com。 使用Active Directory 2003時，您可以將「服務使用者」設定為HTTP/example.yourcompany.com。 使用Active Directory 2008時，您可以將「服務使用者」設定為spnegodemo。 （請參閱使用SPNEGO啟用SSO。）

**服務範圍：** 主動式目錄的網域名稱

**服務密碼：** 服務使用者的密碼

**啟用SPNEGO：** 允許使用SPNEGO進行單一登入(SSO)。 （請參閱使用SPNEGO啟用SSO。）

### SAML設定 {#saml-settings}

如果您要設定企業或混合網域的驗證，並選取SAML驗證，則可使用下列設定。 如需其他SAML設定的相關資訊，請參閱 [設定SAML服務提供者設定](/help/forms/using/admin-help/configure-saml-service-provider-settings.md#configure-saml-service-provider-settings).

**請選取要匯入的SAML身分提供者中繼資料檔案：** 按一下「瀏覽」選取從IDP產生的SAML身分提供者中繼資料檔案，然後按一下「匯入」。 顯示來自IDP的詳細資訊。

**標題：** EntityID所表示之URL的別名。 企業及本機使用者的登入頁面上也會顯示標題。

**身分提供者支援使用者端基本驗證：** 當IDP使用SAML成品解析設定檔時，會使用使用者端基本驗證。 在此設定檔中，「使用者管理」會連回在IDP上執行的Web服務，以擷取實際的SAML判斷提示。 IDP可能需要驗證。 如果IDP確實需要驗證，請選取此選項，並在提供的方塊中指定使用者名稱和密碼。

**自訂屬性：** 可讓您指定其他屬性。 其他屬性是以新行分隔的名稱=值組。

如果使用成品繫結，則需要下列自訂屬性。

* 新增下列自訂屬性，以指定代表AEM Forms服務提供者的使用者名稱，該使用者名稱將用於驗證IDP成品解析服務。
   `saml.idp.resolve.username=<username>`

* 新增以下自訂屬性，為中指定的使用者指定密碼 `saml.idp.resolve.username`.
   `saml.idp.resolve.password=<password>`

* 新增下列自訂屬性，以允許服務提供者在透過SSL建立與成品解析服務的連線時忽略憑證驗證。
   `saml.idp.resolve.ignorecert=true`

### 自訂設定 {#custom-settings}

如果您要設定企業或混合網域的驗證，並選取自訂驗證，請選取自訂驗證提供者的名稱。

## 使用者即時布建 {#just-in-time-provisioning-of-users}

即時布建會在使用者透過驗證提供者成功驗證後，自動在「使用者管理」資料庫中建立使用者。 相關角色和群組也會動態指派給新使用者。 您可以啟用企業網域和混合網域的即時布建。

此程式說明傳統驗證在AEM Forms中的運作方式：

1. 當使用者嘗試登入AEM表單時，「使用者管理」會依序將其憑證傳遞給所有可用的驗證服務提供者。 （登入憑證包括使用者名稱/密碼組合、Kerberos票證、PKCS7簽名等。）
1. 驗證提供者會驗證認證。
1. 驗證提供者接著會檢查使用者是否存在於使用者管理資料庫中。 可能的狀態如下：

   **存在** 如果使用者為最新狀態且已解除鎖定，「使用者管理」會傳回驗證成功。 但是，如果使用者不是最新使用者或已鎖定，「使用者管理」會傳回驗證失敗。

   **不存在** User Management傳回驗證失敗。

   **無效** User Management傳回驗證失敗。

1. 會評估驗證提供者傳回的結果。 如果驗證提供者傳回驗證成功，則允許使用者登入。 否則，「使用者管理」會檢查下一個驗證提供者（步驟2-3）。
1. 如果沒有可用的驗證提供者驗證使用者認證，則會傳回驗證失敗。

啟用即時布建時，如果其中一個驗證提供者驗證其認證，則會在「使用者管理」中動態建立新使用者。 （上述程式中的步驟3之後。）

如果沒有即時布建，當使用者成功通過驗證，但在「使用者管理」資料庫中找不到時，驗證會失敗。 即時布建會在驗證程式中新增一個步驟，以建立使用者並為使用者指派角色和群組。

### 為網域啟用即時布建 {#enable-just-in-time-provisioning-for-a-domain}

1. 編寫實作IdentityCreator和AssignmentProvider介面的服務容器。 (請參閱 [使用AEM表單程式設計](https://www.adobe.com/go/learn_aemforms_programming_63).)
1. 將服務容器部署至表單伺服器。
1. 在管理控制檯中，按一下「設定>使用者管理>網域管理」。

   選取現有網域，或按一下「新增企業網域」。

1. 若要建立網域，請按一下[新增企業網域]或[新增混合網域]。 若要編輯現有網域，請按一下網域名稱。
1. 選取「啟用及時布建」。

   ***注意&#x200B;**：如果缺少「啟用及時布建」核取方塊，請按一下「首頁>設定>使用者管理>設定>進階系統屬性」 ，然後按一下「重新載入」。*

1. 新增驗證服務提供者。 新增驗證提供者時，請在[新增驗證]畫面上，選取已註冊的[身分建立者]和[指派提供者]。 (請參閱 [設定驗證服務提供者](configuring-authentication-providers.md#configuring-authentication-providers).)
1. 儲存網域。
