---
title: 配置身份验证提供程序
seo-title: Configuring authentication providers
description: 添加、编辑或删除身份验证提供程序，更改身份验证设置，并阅读有关及时配置用户的内容。
seo-description: Add, edit, or delete authentication providers, change authentication settings, and read about just-in-time provisioning of users.
uuid: 90e7690b-1ce0-4604-b58f-6dca4f2372cf
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/setting_up_and_managing_domains
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 31dd8db3-ddac-429e-82f8-8c5dc4ffc186
exl-id: d72a3977-1423-49e0-899b-234bb76be378
source-git-commit: c4cd9a61a226ace2a72d60b5b7b7432de12cb873
workflow-type: tm+mt
source-wordcount: '1575'
ht-degree: 0%

---

# 配置身份验证提供程序 {#configuring-authentication-providers}

混合域至少需要一个身份验证提供程序，企业域至少需要一个身份验证提供程序或目录提供程序。

如果使用SPNEGO启用SSO，请添加启用了SPNEGO的Kerberos身份验证提供程序和LDAP提供程序作为备份。 如果SPNEGO无法正常工作，此配置将启用使用用户ID和密码进行用户身份验证。 (请参阅 [使用SPNEGO启用SSO](/help/forms/using/admin-help/enabling-single-sign-on-aem.md#enable-sso-using-spnego).)

## 添加身份验证提供程序 {#add-an-authentication-provider}

1. 在管理控制台中，单击设置>用户管理>域管理。
1. 单击列表中的现有域。 如果要为新域添加身份验证，请参阅 [添加企业域](/help/forms/using/admin-help/adding-domains.md#add-an-enterprise-domain) 或 [添加混合域](/help/forms/using/admin-help/adding-domains.md#add-a-hybrid-domain).
1. 单击添加验证，然后在“验证提供方”列表中选择提供方，具体取决于您的组织使用的验证机制。
1. 在页面上提供所需的任何其他信息。 (请参阅 [身份验证设置](configuring-authentication-providers.md#authentication-settings).)
1. （可选）单击测试以测试配置。
1. 单击“确定”，然后再次单击“确定”。

## 编辑现有的身份验证提供程序 {#edit-an-existing-authentication-provider}

1. 在管理控制台中，单击设置>用户管理>域管理。
1. 单击列表中的相应域。
1. 在出现的页面上，从列表中选择相应的身份验证提供程序，并根据需要进行更改。 (请参阅 [身份验证设置](configuring-authentication-providers.md#authentication-settings).)
1. 单击确定。

## 删除身份验证提供程序 {#delete-an-authentication-provider}

1. 在管理控制台中，单击设置>用户管理>域管理。
1. 单击列表中的相应域。
1. 选中要删除的身份验证提供程序的复选框，然后单击删除。
1. 在显示的确认页上单击确定，然后再次单击确定。

## 身份验证设置 {#authentication-settings}

以下设置可用，具体取决于域类型和您选择的身份验证类型。

### LDAP设置 {#ldap-settings}

如果要配置企业域或混合域的验证并选择LDAP验证，可以选择使用在目录配置中指定的LDAP服务器，也可以选择其他LDAP服务器用于验证。 如果选择其他服务器，则您的用户必须存在于两个LDAP服务器上。

要使用在目录配置中指定的LDAP服务器，请选择LDAP作为验证提供程序，然后单击“确定”。

要使用其他LDAP服务器执行身份验证，请选择LDAP作为身份验证提供程序，然后选中“自定义LDAP身份验证”复选框。 将显示以下配置设置。

**服务器：** （必需）目录服务器的完全限定域名(FQDN)。 例如，对于example.com网络上名为x的计算机，FQDN为x.example.com。 可以使用IP地址代替FQDN服务器名称。

**端口：** （必需）目录服务器使用的端口。 通常为389，如果安全套接字层(SSL)协议用于通过网络发送身份验证信息，则为636。

**SSL：** （必需）指定目录服务器通过网络发送数据时是否使用SSL。 默认值为“否”。 当设置为“是”时，相应的LDAP服务器证书必须受到应用程序服务器的Java™运行时环境(JRE)的信任。

**绑定** （必需）指定访问目录的方式。

**匿名：** 不需要用户名或密码。

**用户：** 需要身份验证。 在“名称”框中，指定可以访问目录的用户记录的名称。 最好输入用户帐户的完整可分辨名称(DN)，如cn=Jane Doe、ou=user、dc=can、dc=com。 在“密码”框中，指定关联的密码。 选择“用户”作为“绑定”选项时，需要这些设置。

**检索基本DN：** （非必需）检索基本DN并在下拉列表中显示它们。 当您有多个基本DN并且需要选择一个值时，此设置非常有用。

**基本DN：** （必需）用作从LDAP层次结构同步用户和组的起点。 最好在层次结构的最低级别指定一个基本DN，该层级包含所有需要为服务同步的用户和组。 请勿在此设置中包含用户的DN。 要同步特定用户，请使用“搜索过滤器”设置。

**使用以下内容填充页面：** （非必需）在选中时，会使用相应的默认LDAP值填充“用户”和“组”设置页面上的属性。

**搜索筛选器：** （必需）用于查找与用户关联的记录的搜索过滤器。 请参阅搜索筛选器语法。

### Kerberos设置 {#kerberos-settings}

如果要配置企业域或混合域的身份验证，并选择Kerberos身份验证，则以下设置可用。

**DNS IP：** 运行AEM表单的服务器的DNS IP地址。 在Windows上，可通过在命令行运行ipconfig /all来确定此IP地址。

**KDC主机：** 用于身份验证的Active Directory服务器的完全限定的主机名或IP地址。

**服务用户：** 如果您使用的是Active Directory 2003，此值是在表单中为服务主体创建的映射 `HTTP/<server name>`. 如果您使用的是Active Directory 2008，此值是服务主体的登录ID。 例如，假定服务主体名为um spnego，用户ID为spnegedemo，映射为HTTP/example.yourcompany.com。 使用Active Directory 2003时，可以将Service User设置为HTTP/example.yourcompany.com。 使用Active Directory 2008时，可以将Service User设置为spnegodemo。 （请参阅使用SPNEGO启用SSO。）

**服务领域：** Active Directory的域名

**服务密码：** 服务用户的密码

**启用SPNEGO：** 支持使用SPNEGO进行单点登录(SSO)。 （请参阅使用SPNEGO启用SSO。）

### SAML设置 {#saml-settings}

如果您正在配置企业域或混合域的身份验证，并选择SAML身份验证，则以下设置可用。 有关其他SAML设置的信息，请参见 [配置SAML服务提供程序设置](/help/forms/using/admin-help/configure-saml-service-provider-settings.md#configure-saml-service-provider-settings).

**请选择要导入的SAML身份提供程序元数据文件：** 单击浏览选择从IDP生成的SAML身份提供方元数据文件，然后单击导入。 显示来自IDP的详细信息。

**标题：** EntityID表示的URL的别名。 企业用户和本地用户的登录页面上也会显示标题。

**身份提供程序支持客户端基本身份验证：** 当IDP使用SAML工件解析配置文件时，将使用客户端基本身份验证。 在此配置文件中，用户管理连接回在IDP上运行的Web服务，以检索实际的SAML断言。 IDP可能需要身份验证。 如果IDP确实需要验证，请选择此选项，并在提供的框中指定用户名和密码。

**自定义属性：** 允许您指定其他属性。 其他属性为名称=值对，用新行分隔。

如果使用工件绑定，则需要以下自定义属性。

* 添加以下自定义属性以指定表示AEM表单服务提供程序的用户名，该用户名用于对IDP工件解析服务进行身份验证。
  `saml.idp.resolve.username=<username>`

* 添加以下自定义属性，以指定中指定用户的密码 `saml.idp.resolve.username`.
  `saml.idp.resolve.password=<password>`

* 添加以下自定义属性，以允许服务提供商在通过SSL与工件解析服务建立连接时忽略证书验证。
  `saml.idp.resolve.ignorecert=true`

### 自定义设置 {#custom-settings}

如果要配置企业域或混合域的身份验证，并选择自定义身份验证，请选择自定义身份验证提供程序的名称。

## 及时配置用户 {#just-in-time-provisioning-of-users}

即时设置会在用户通过身份验证提供程序成功进行身份验证后，在User Management数据库中自动创建用户。 相关的角色和组也会动态分配给新用户。 您可以为企业域和混合域启用及时资源调配。

此过程描述了传统身份验证在AEM Forms中的工作方式：

1. 当用户尝试登录AEM表单时，用户管理会按顺序将其凭据传递到所有可用的身份验证提供程序。 （登录凭据包括用户名/密码组合、Kerberos票证、PKCS7签名等。）
1. 身份验证提供程序验证凭据。
1. 然后，验证提供程序会检查用户是否存在于用户管理数据库中。 可能存在以下状态：

   **存在** 如果用户是当前用户且已解锁，则“用户管理”返回身份验证成功。 但是，如果用户不是最新用户或被锁定，则“用户管理”返回验证失败。

   **不存在** 用户管理返回身份验证失败。

   **无效** 用户管理返回身份验证失败。

1. 将评估身份验证提供程序返回的结果。 如果身份验证提供程序返回身份验证成功，则允许用户登录。 否则，User Management会检查下一个身份验证提供程序（步骤2-3）。
1. 如果没有可用的身份验证提供程序验证用户凭据，则返回身份验证失败。

启用实时设置后，如果其中一个身份验证提供程序验证其凭据，则将在“用户管理”中动态创建新用户。 （在上述过程中的步骤3之后。）

如果没有及时预配，当成功对用户进行身份验证但在用户管理数据库中未找到用户时，身份验证将失败。 即时预配在验证过程中添加了一个步骤，用于创建用户并为用户分配角色和组。

### 为域启用及时资源调配 {#enable-just-in-time-provisioning-for-a-domain}

1. 编写实现IdentityCreator和AssignmentProvider接口的服务容器。 (请参阅 [使用AEM表单编程](https://www.adobe.com/go/learn_aemforms_programming_63).)
1. 将服务容器部署到Forms服务器。
1. 在管理控制台中，单击设置>用户管理>域管理。

   选择现有域或单击“新建企业域”。

1. 要创建域，请单击“新建企业域”或“新建混合域”。 要编辑现有域，请单击该域的名称。
1. 选择启用实时预配。

   ***注意&#x200B;**：如果缺少“启用及时预配”复选框，请单击“主页”>“设置”>“用户管理”>“配置”>“高级系统属性”，然后单击“重新加载”。*

1. 添加身份验证提供程序。 添加身份验证提供程序时，请在“新建身份验证”屏幕上，选择已注册的身份创建者和分配提供程序。 (请参阅 [配置身份验证提供程序](configuring-authentication-providers.md#configuring-authentication-providers).)
1. 保存域。
