---
title: 新增網域
seo-title: Adding domains
description: 瞭解如何使用網域管理設定和網域名稱和ID的一般考量來新增企業、本機或混合網域。
seo-description: Learn how to add an enterprise, local, or hybrid domain using Domain Management settings and general considerations for domain names and IDs.
uuid: 3ae1e5d4-ea5b-4e0b-be97-3957c3702d5f
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/setting_up_and_managing_domains
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: d4004ffe-c981-487d-b803-dc4492ae5998
exl-id: c708936d-7aa7-4b92-be2d-d97008f187d2
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '922'
ht-degree: 0%

---

# 新增網域 {#adding-domains}

## 新增企業網域 {#add-an-enterprise-domain}

1. 在管理控制檯中，按一下「設定>使用者管理>網域管理」。
1. 按一下新增企業網域。
1. 在ID方塊中，輸入網域的唯一識別碼，然後在「名稱」方塊中，輸入網域的描述性名稱。 (請參閱 [網域名稱和ID的重要考量](adding-domains.md#important-considerations-for-domain-names-and-ids).)
1. 指定是否啟用帳戶鎖定。 (請參閱 [設定帳戶鎖定設定](/help/forms/using/admin-help/configure-account-locking-settings.md#configure-account-locking-settings).) 依預設，會選取[啟用帳戶鎖定]。
1. 按一下「新增驗證」，然後在「驗證提供者」清單中，根據您的組織所使用的驗證機制選取提供者。 可能的值包括LDAP、Kerberos、SAML或自訂驗證提供者。

   如果您選取LDAP，則可以使用目錄組態中指定的LDAP伺服器，也可以選擇不同的LDAP伺服器來用於驗證。 如果您選擇不同的伺服器，您的使用者必須存在於兩個LDAP伺服器上。

1. 在頁面上提供所需的任何其他資訊。 (請參閱 [驗證設定](/help/forms/using/admin-help/configuring-authentication-providers.md#authentication-settings).)
1. 新增目錄或自訂服務提供者介面(SPI)。 (請參閱 [新增目錄或自訂SPI](/help/forms/using/admin-help/configuring-directories.md#adding-directories-or-custom-spis).)
1. 按一下「完成」，然後按一下「確定」。

建立企業網域後，手動同步目錄或建立觸發程式以執行同步，然後「使用者管理」才能使用它。 然後，您可以設定目錄同步處理排程，並視需要執行手動同步處理。 (請參閱 [同步目錄](/help/forms/using/admin-help/synchronizing-directories.md#synchronizing-directories).)

## 新增本機網域 {#add-a-local-domain}

1. 在管理控制檯中，按一下「設定>使用者管理>網域管理」。
1. 按一下「新增本機網域」。
1. 在ID方塊中，輸入網域的唯一識別碼，並在Name方塊中，輸入網域的描述性名稱。 (請參閱 [網域名稱和ID的重要考量](adding-domains.md#important-considerations-for-domain-names-and-ids).)
1. 指定是否啟用帳戶鎖定，然後按一下[確定]。 (請參閱 [設定帳戶鎖定設定](/help/forms/using/admin-help/configure-account-locking-settings.md#configure-account-locking-settings).) 依預設，會選取[啟用帳戶鎖定]。

## 新增混合網域 {#add-a-hybrid-domain}

1. 在管理控制檯中，按一下「設定>使用者管理>網域管理」。
1. 按一下「新增混合式網域」。
1. 在ID方塊中，輸入網域的唯一識別碼，並在Name方塊中，輸入網域的描述性名稱。 (請參閱 [網域名稱和ID的重要考量](adding-domains.md#important-considerations-for-domain-names-and-ids).)
1. 按一下「新增驗證」，然後在「驗證提供者」清單中，根據您的組織所使用的驗證機制選取提供者。 可能的值包括LDAP、Kerberos、SAML或自訂驗證提供者。
1. 在頁面上提供所需的任何其他資訊。 (請參閱 [驗證設定](/help/forms/using/admin-help/configuring-authentication-providers.md#authentication-settings).)
1. 按一下「確定」，然後再次按一下「確定」。

## 網域名稱和ID的重要考量 {#important-considerations-for-domain-names-and-ids}

選擇網域名稱和ID時，請記住以下注意事項：

### 一般考量 {#general-considerations}

* 當您使用DB2以外的資料庫提供者時，網域ID最多可包含50個位元組。 如果您使用單位元組ASCII字元，上限為50個字元。 如果網域識別碼包含多位元組字元，則此限制會降低。 例如，如果您建立的網域識別碼包含3個位元組字元，則限製為16個字元。 此外，您無法建立包含4位元組字元的網域。 如果您建立的網域ID超過此限制，AEM表單將處於不穩定狀態。 若要從此不穩定狀態復原，請參閱&quot; [移除包含延伸或多位元組字元的網域](adding-domains.md#remove-a-domain-that-contains-extended-or-multi-byte-characters)」在本頁上。
* 可在AEM表單中建立的企業網域和本機網域數目，取決於每個網域ID的長度。 當您新增企業或混合式網域時，「使用者管理」會更新AEM表單組態檔(config.xml)之AuthProviders節點中的configInstance字串。 configInstance字串包含與授權提供者相關聯之所有網域的絕對路徑清單（以冒號分隔）。 此字串的大小限製為8192個字元。 當達到該限制時，您無法建立其他網域。

### 使用DB2時的注意事項 {#considerations-when-using-db2}

在AEM表單資料庫中使用DB2時，網域ID的允許長度上限取決於使用的字元型別：

* 100單位元組(ASCII) （例如使用英文、法文或德文的字元）
* 50個雙位元組（例如中文、日文或韓文使用的字元）
* 25個四位元組（例如，繁體中文中使用的字元）

### 使用MySQL時的注意事項 {#considerations-when-using-mysql}

使用MySQL做為AEM表單資料庫時，會套用下列限制：

* 網域ID和網域名稱僅使用單位元組(ASCII)字元。 如果您使用擴充ASCII字元，AEM表單將會處於不穩定狀態，而且如果您嘗試刪除網域，可能會擲回例外狀況。 若要從此不穩定狀態復原，請參閱&quot; [移除包含延伸或多位元組字元的網域](adding-domains.md#remove-a-domain-that-contains-extended-or-multi-byte-characters)」主題。
* 您無法建立兩個同名但大小寫不同的網域。 例如，嘗試建立名為 *Adobe* 當網域名為 *adobe* 已經存在導致錯誤。
* 「使用者管理」無法區分僅在使用擴充字元時不同的兩個網域名稱。 例如，如果您建立名為 *abcde* 和名為的網域 *abcde*，則視為相同。

### 移除包含延伸或多位元組字元的網域 {#remove-a-domain-that-contains-extended-or-multi-byte-characters}

1. 匯出組態檔，如所述 [匯入和匯出組態檔](/help/forms/using/admin-help/importing-exporting-configuration-file.md#importing-and-exporting-the-configuration-file).
1. 開啟組態檔，並在「網域」節點下，找出名稱屬性與使用延伸或多位元組字元建立的網域名稱相符的節點。 刪除與該網域相關的整個節點。
1. 在您的資料庫中，搜尋edprincipaldomainentity表格中的網域：

   * 選取 `*` 來自edcparcipaldomainentity。
   * 尋找包含延伸或多位元組字元的網域名稱，並將其狀態設定為OBSOLETE。

1. 匯入更新的組態檔，如所述 [匯入和匯出組態檔](/help/forms/using/admin-help/importing-exporting-configuration-file.md#importing-and-exporting-the-configuration-file).
