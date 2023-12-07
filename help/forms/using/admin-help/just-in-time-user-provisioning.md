---
title: 即时用户配置
description: 在成功进行身份验证后，使用及时设置将用户添加到“用户管理”，并动态地将相关角色和组分配给新用户。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/setting_up_and_organizing_users
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 7bde0a09-192a-44a8-83d0-c18e335e9afa
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '575'
ht-degree: 0%

---

# 即时用户配置 {#just-in-time-user-provisioning}

AEM Forms支持对User Management中尚不存在的用户进行实时配置。 利用及时配置，用户在其凭据成功进行身份验证后会自动添加到“用户管理”中。 此外，相关的角色和组会动态分配给新用户。

## 需要及时配置用户 {#need-for-just-in-time-user-provisioning}

传统身份验证的工作原理如下：

1. 当用户尝试登录AEM表单时，用户管理会按顺序将用户的凭据传递到所有可用的身份验证提供程序。 （登录凭据包括用户名/密码组合、Kerberos票证、PKCS7签名等。）
1. 身份验证提供程序验证凭据。
1. 然后，验证提供程序会检查用户是否存在于用户管理数据库中。 可能会产生以下结果：

   **存在：** 如果用户是当前用户且已解锁，则“用户管理”返回身份验证成功。 但是，如果用户不是最新用户或被锁定，则“用户管理”返回验证失败。

   **不存在：** 用户管理返回身份验证失败。

   **无效：** 用户管理返回身份验证失败。

1. 将评估身份验证提供程序返回的结果。 如果身份验证提供程序返回身份验证成功，则允许用户登录。 否则，User Management会检查下一个身份验证提供程序（步骤2-3）。
1. 如果没有可用的身份验证提供程序验证用户凭据，则返回身份验证失败。

实施及时预配时，如果其中一个身份验证提供程序验证用户的凭据，则将在“用户管理”中动态创建新用户。 （在传统的身份验证过程中执行了上述步骤3。）

## 实施及时用户配置 {#implement-just-in-time-user-provisioning}

### 用于及时资源调配的API {#apis-for-just-in-time-provisioning}

AEM forms为及时配置提供了以下API：

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

### 创建启用实时功能的域时的注意事项 {#considerations-while-creating-a-just-in-time-enabled-domain}

* 创建自定义时 `IdentityCreator` 对于混合域，请确保为本地用户指定了虚拟密码。 请勿将此密码字段留空。
* 建议：使用 `DomainSpecificAuthentication` 验证特定域的用户凭据。

### 创建及时启用的域 {#create-a-just-in-time-enabled-domain}

1. 在“用于及时资源调配的API”部分中，编写一个实施API的DSC。
1. 将DSC部署到Forms服务器。
1. 创建即时启用的域：

   * 在Administration Console中，单击设置>用户管理>域管理>新建企业域。
   * 配置域，然后选择启用及时预配。 <!--Fix broken link (See Setting up and managing domains).-->
   * 添加身份验证提供程序。 添加身份验证提供程序时，请在“新建身份验证”屏幕上，选择已注册的身份创建者和分配提供程序。

1. 保存新域。

## 幕后 {#behind-the-scenes}

假设用户正在尝试登录AEM表单，并且身份验证提供程序接受其用户凭据。 如果用户在User Management数据库中尚不存在，则用户的身份检查将失败。 AEM forms现在执行以下操作：

1. 创建 `UserProvisioningBO` 对象中的身份验证数据，并将其放入凭据映射中。
1. 基于返回的域信息 `UserProvisioningBO`，获取并调用已注册的 `IdentityCreator` 和 `AssignmentProvider` 对于域。
1. 调用 `IdentityCreator`. 如果返回成功 `AuthResponse`，提取 `UserInfo` 凭证映射中。 将其传递给 `AssignmentProvider` 用于组/角色分配，以及创建用户之后的任何其他后处理。
1. 如果已成功创建用户，则将该用户的登录尝试作为成功返回。
1. 对于混合域，从提供给身份验证提供程序的身份验证数据中提取用户信息。 如果成功获取此信息，请动态创建用户。

>[!NOTE]
>
>即时配置功能附带默认实施 `IdentityCreator` 可用来动态创建用户的插件。 创建用户时将与域中的目录相关联的信息。
