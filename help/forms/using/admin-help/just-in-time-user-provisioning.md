---
title: 及时的用户配置
seo-title: 及时的用户配置
description: 使用即时配置将用户添加到用户管理中，并将相关角色和组动态分配给新用户。
seo-description: 使用即时配置将用户添加到用户管理中，并将相关角色和组动态分配给新用户。
uuid: a5ad4698-70bb-487b-a069-7133e2f420c2
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/setting_up_and_organizing_users
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: e80c3f98-baa1-45bc-b713-51a2eb5ec165
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '599'
ht-degree: 0%

---


# 及时的用户配置 {#just-in-time-user-provisioning}

AEM表单支持对用户管理中尚不存在的用户进行即时设置。 借助即时设置，用户凭据成功通过身份验证后，将自动添加到用户管理中。 此外，相关角色和组会动态分配给新用户。

## 需要及时的用户配置 {#need-for-just-in-time-user-provisioning}

传统身份验证的工作方式如下：

1. 当用户尝试登录AEM表单时，用户管理会按顺序将用户凭据传递给所有可用的身份验证提供者。 （登录凭据包括用户名／密码组合、Kerberos票证、PKCS7签名等。）
1. 身份验证提供程序验证凭据。
1. 然后，身份验证提供程序检查用户是否存在于用户管理数据库中。 可能有以下结果：

   **存在：** 如果用户当前处于解锁状态，则用户管理会返回身份验证成功。 但是，如果用户不是当前用户或已锁定，则用户管理会返回身份验证失败。

   **不存在：** 用户管理返回身份验证失败。

   **无效：** 用户管理返回身份验证失败。

1. 将评估身份验证提供程序返回的结果。 如果身份验证提供程序返回身份验证成功，则允许用户登录。 否则，用户管理会与下一个身份验证提供程序进行检查（步骤2-3）。
1. 如果没有可用的身份验证提供程序验证用户凭据，则会返回身份验证失败。

当实现及时配置时，如果其中一个身份验证提供者验证用户的凭据，则在用户管理中动态创建新用户。 （在传统的验证过程中，步骤3之后，如上。）

## 实施及时的用户配置 {#implement-just-in-time-user-provisioning}

### 适用于即时配置的API {#apis-for-just-in-time-provisioning}

AEM表单为即时设置提供以下API:

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

### 创建刚启用时间的域时的注意事项 {#considerations-while-creating-a-just-in-time-enabled-domain}

* 为混合域创 `IdentityCreator` 建自定义时，请确保为本地用户指定虚拟口令。 请勿将此密码字段留空。
* 建议： 使用 `DomainSpecificAuthentication` 验证特定域的用户凭据。

### 创建刚启用时间的域 {#create-a-just-in-time-enabled-domain}

1. 在“API for just-in-provisioning”部分编写实现API的DSC。
1. 将DSC部署到表单服务器。
1. 创建刚启用时间的域：

   * 在管理控制台中，单击设置>用户管理>域管理>新建企业域。
   * 配置域并选择“仅启用时间设置”。 <!--Fix broken link (See Setting up and managing domains).-->
   * 添加身份验证提供程序。 添加身份验证提供者时，在“新建身份验证”屏幕上，选择已注册的身份创建者和分配提供者。

1. 保存新域。

## 幕后工作 {#behind-the-scenes}

假定用户正尝试登录AEM表单，且身份验证提供程序接受其用户凭据。 如果用户管理数据库中尚不存在该用户，则用户的身份检查将失败。 AEM表单现在可执行以下操作：

1. 使用身 `UserProvisioningBO` 份验证数据创建一个对象，并将其放在凭据映射中。
1. 根据由返回的域 `UserProvisioningBO`信息，获取并调用已注 `IdentityCreator` 册的 `AssignmentProvider` 域和域。
1. 调用 `IdentityCreator`。 如果返回成功， `AuthResponse`请从 `UserInfo` 凭据映射中提取。 在创建用户 `AssignmentProvider` 后，将其传递给组／角色分配以及任何其他后处理。
1. 如果用户创建成功，则用户登录尝试将返回为成功。
1. 对于混合域，从提供给身份验证提供程序的身份验证数据中提取用户信息。 如果成功获取此信息，则立即创建用户。

>[!NOTE]
>
>即时供应功能附带有默认实现，您可 `IdentityCreator` 以使用它动态创建用户。 用户是使用与域中的目录关联的信息创建的。

