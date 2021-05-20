---
title: 及时用户配置
seo-title: 及时用户配置
description: 使用即时配置可在成功进行身份验证后将用户添加到用户管理，并将相关角色和组动态分配给新用户。
seo-description: 使用即时配置可在成功进行身份验证后将用户添加到用户管理，并将相关角色和组动态分配给新用户。
uuid: a5ad4698-70bb-487b-a069-7133e2f420c2
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/setting_up_and_organizing_users
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: e80c3f98-baa1-45bc-b713-51a2eb5ec165
exl-id: 7bde0a09-192a-44a8-83d0-c18e335e9afa
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '599'
ht-degree: 0%

---

# 及时用户配置{#just-in-time-user-provisioning}

AEM Forms支持及时配置用户管理中尚不存在的用户。 通过即时配置，用户的凭据成功验证后，会自动将其添加到用户管理中。 此外，相关角色和组被动态地分配给新用户。

## 需要及时设置用户{#need-for-just-in-time-user-provisioning}

传统身份验证的工作方式如下：

1. 当用户尝试登录AEM表单时，用户管理会按顺序将用户的凭据传递到所有可用的身份验证提供程序。 （登录凭据包括用户名/密码组合、Kerberos票证、PKCS7签名等。）
1. 身份验证提供程序将验证凭据。
1. 然后，身份验证提供程序检查用户是否存在于用户管理数据库中。 可能会得到以下结果：

   **存在：** 如果用户当前已解锁，则用户管理会返回身份验证成功。但是，如果用户不是当前用户或该用户被锁定，则用户管理会返回身份验证失败。

   **不存在：** 用户管理返回身份验证失败。

   **无效：** 用户管理返回身份验证失败。

1. 将评估验证提供程序返回的结果。 如果身份验证提供程序返回身份验证成功，则允许用户登录。 否则，用户管理会与下一个身份验证提供程序进行检查（步骤2-3）。
1. 如果没有可用的身份验证提供程序验证用户凭据，则返回身份验证失败。

当实施即时预配时，如果其中一个身份验证提供程序验证用户的凭据，则会在用户管理中动态创建新用户。 （在上述传统身份验证过程中的步骤3之后。）

## 实施即时用户配置{#implement-just-in-time-user-provisioning}

### 用于即时配置的API {#apis-for-just-in-time-provisioning}

AEM forms提供了以下API以供即时配置：

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

### 创建刚刚启用时间的域{#considerations-while-creating-a-just-in-time-enabled-domain}时的注意事项

* 在为混合域创建自定义`IdentityCreator`时，请确保为本地用户指定了虚拟密码。 请勿将此密码字段留空。
* 建议：使用`DomainSpecificAuthentication`验证特定域的用户凭据。

### 创建刚启用时间的域{#create-a-just-in-time-enabled-domain}

1. 在“用于即时配置的API”部分中编写一个实施API的DSC。
1. 将DSC部署到表单服务器。
1. 创建刚启用时间的域：

   * 在管理控制台中，单击设置>用户管理>域管理>新建企业域。
   * 配置域，然后选择仅在时间配置中启用。<!--Fix broken link (See Setting up and managing domains).-->
   * 添加身份验证提供程序。 添加身份验证提供程序时，在“新建身份验证”屏幕上，选择已注册的身份创建者和分配提供程序。

1. 保存新域。

## 幕后{#behind-the-scenes}

假设用户尝试登录AEM表单，并且身份验证提供程序接受其用户凭据。 如果用户管理数据库中尚不存在该用户，则用户的身份检查将失败。 AEM Forms现在会执行以下操作：

1. 使用身份验证数据创建`UserProvisioningBO`对象，并将其置于凭据映射中。
1. 根据`UserProvisioningBO`返回的域信息，获取并调用该域的注册`IdentityCreator`和`AssignmentProvider`。
1. 调用`IdentityCreator`。 如果返回成功的`AuthResponse`，则从凭据映射中提取`UserInfo`。 将其传递到`AssignmentProvider`，以便在创建用户后进行组/角色分配和任何其他后处理。
1. 如果用户创建成功，则用户登录尝试会成功返回。
1. 对于混合域，从提供给身份验证提供商的身份验证数据中提取用户信息。 如果成功获取了此信息，请即时创建用户。

>[!NOTE]
>
>即时配置功能随`IdentityCreator`的默认实施一起提供，您可以使用该实施动态创建用户。 用户是使用与域中目录关联的信息创建的。
