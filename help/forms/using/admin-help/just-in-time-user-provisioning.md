---
title: 即時使用者布建
seo-title: Just-in-time user provisioning
description: 在成功驗證後，使用即時布建來將使用者新增至「使用者管理」，並動態地將相關角色和群組指派給新使用者。
seo-description: Use just-in-time provisioning to add users to User Management after successfull authentication and dynamically assign relevant roles and groups to the new user.
uuid: a5ad4698-70bb-487b-a069-7133e2f420c2
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/setting_up_and_organizing_users
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: e80c3f98-baa1-45bc-b713-51a2eb5ec165
exl-id: 7bde0a09-192a-44a8-83d0-c18e335e9afa
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '573'
ht-degree: 0%

---

# 即時使用者布建 {#just-in-time-user-provisioning}

AEM Forms支援「使用者管理」中尚未存在的使用者即時布建。 透過即時布建，使用者在成功驗證其認證後，就會自動新增到「使用者管理」。 此外，相關的角色和群組會動態指派給新使用者。

## 需要即時使用者布建 {#need-for-just-in-time-user-provisioning}

這就是傳統驗證的工作方式：

1. 當使用者嘗試登入AEM表單時，「使用者管理」會依序將使用者的認證傳遞給所有可用的驗證服務提供者。 （登入憑證包括使用者名稱/密碼組合、Kerberos票證、PKCS7簽名等。）
1. 驗證提供者會驗證認證。
1. 驗證提供者接著會檢查使用者是否存在於使用者管理資料庫中。 可能會出現以下結果：

   **存在：** 如果使用者為最新狀態且已解除鎖定，「使用者管理」會傳回驗證成功。 但是，如果使用者不是最新使用者或已鎖定，「使用者管理」會傳回驗證失敗。

   **不存在：** User Management傳回驗證失敗。

   **無效：** User Management傳回驗證失敗。

1. 會評估驗證提供者傳回的結果。 如果驗證提供者傳回驗證成功，則允許使用者登入。 否則，「使用者管理」會檢查下一個驗證提供者（步驟2-3）。
1. 如果沒有可用的驗證提供者驗證使用者認證，則會傳回驗證失敗。

實作即時布建時，如果其中一個驗證提供者驗證使用者的認證，則會在「使用者管理」中動態建立新使用者。 （上述傳統驗證程式中的步驟3之後。）

## 實作即時使用者布建 {#implement-just-in-time-user-provisioning}

### 適用於即時布建的API {#apis-for-just-in-time-provisioning}

AEM forms提供下列API用於即時布建：

```java
package com.adobe.idp.um.spi.authentication  ;
publ ic interface IdentityCreator {
/**
* Tries  to create a user with the  in formation  provided in the <code>UserProvisioningBO</code> object.
* If the user is successfully created, a valid AuthResponse is returned along with the information using which the user was created.
* It is the responsibility of the IdentityCreator to set the User obje ct  in the cre dential map with th e  ke y  <code>UMA u thenticationUtil.authenticatedUserKey</code>
* The credentials are available in the <code>UserProvisioningBO</code> object in the 'credentials' property.
* If the IdentityCreator is unable to create a user due to any reason, it returns <code>null</code>
* @param userBO An object of <code>com.adobe. i dp.um . spi.authenti c ationUserProvisioningBO</code>
* @return */public AuthResponse create(UserProvisioningBO userBO);
/**
* Returns the name of the IdentityCreator which will be registered in preferences.
* This name is used to associate the IdentityProvider with the Auth Provider Configuration in the domain.
* @return The name of the Identity Creator which is recognized in Configuration.
*/
public String getName();
}
package com.adobe.idp.um.spi.authentication;
import com.adobe.idp.um.api.infomodel.User;
public interface AssignmentProvider {
/**
* Tries to assign roles or permissions or group memberships to users created via Just-in-time provisioning.
* @param user The User created via the Just-in-time provisioning process.
* @return a Boolean flag indicating whether the assignment was successful or not.
*/
public Boolean assign(User user);
/**
* Returns the name of the AssignmentProvider through which it is registered under preferences.
* This name is used to associate the AssignmentProvider with the Auth Provider Configuration in the domain.
* @return The name of the AssignmentProvider which is recognized in Configuration.
*/public String getName();
}
```

### 建立即時啟用網域時的考量事項 {#considerations-while-creating-a-just-in-time-enabled-domain}

* 建立自訂時 `IdentityCreator` 對於混合網域，請確保為本機使用者指定了虛擬密碼。 請勿將此密碼欄位留空。
* 建議：使用 `DomainSpecificAuthentication` 驗證特定網域的使用者認證。

### 建立即時啟用的網域 {#create-a-just-in-time-enabled-domain}

1. 在「即時布建的API」一節中撰寫實作API的DSC。
1. 將DSC部署至表單伺服器。
1. 建立即時啟用的網域：

   * 在Administration Console中，按一下「設定>使用者管理>網域管理>新增企業網域」。
   * 設定網域，然後選取「啟用即時(Just In Time)布建」。 <!--Fix broken link (See Setting up and managing domains).-->
   * 新增驗證服務提供者。 新增驗證提供者時，請在[新增驗證]畫面上，選取已註冊的[身分建立者]和[指派提供者]。

1. 儲存新網域。

## 幕後 {#behind-the-scenes}

假設使用者正在嘗試登入AEM表單，而驗證提供者接受其使用者認證。 如果使用者尚未存在於「使用者管理」資料庫中，則使用者的身分檢查會失敗。 AEM forms現在會執行下列動作：

1. 建立 `UserProvisioningBO` 物件，並將它放置在認證對應中。
1. 根據傳回的網域資訊 `UserProvisioningBO`，擷取並叫用註冊的 `IdentityCreator` 和 `AssignmentProvider` 用於網域。
1. 叫用 `IdentityCreator`. 如果它傳回成功 `AuthResponse`，擷取 `UserInfo` 從認證對應。 將其傳遞給 `AssignmentProvider` 用於群組/角色指派，以及建立使用者後的任何其他後處理。
1. 如果已成功建立使用者，請將使用者的登入嘗試傳回為成功。
1. 對於混合網域，從提供給驗證提供者的驗證資料提取使用者資訊。 如果成功擷取此資訊，請立即建立使用者。

>[!NOTE]
>
>即時布建功能隨附預設實作 `IdentityCreator` 可用來以動態方式建立使用者的資訊。 使用者是以與網域中目錄相關聯的資訊建立的。
