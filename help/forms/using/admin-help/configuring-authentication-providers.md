---
title: 配置身份验证提供者
seo-title: 配置身份验证提供者
description: 添加、编辑或删除身份验证提供者，更改身份验证设置，并及时阅读用户配置。
seo-description: 添加、编辑或删除身份验证提供者，更改身份验证设置，并及时阅读用户配置。
uuid: 90e7690b-1ce0-4604-b58f-6dca4f2372cf
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/setting_up_and_managing_domains
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 31dd8db3-ddac-429e-82f8-8c5dc4ffc186
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '1595'
ht-degree: 0%

---


# 配置身份验证提供程序{#configuring-authentication-providers}

混合域需要至少一个身份验证提供程序，而企业域需要至少一个身份验证提供程序或目录提供程序。

如果使用SPNEGO启用SSO，请添加启用SPNEGO的Kerberos身份验证提供程序和LDAP提供程序作为备份。 如果SPNEGO不工作，此配置将启用用户ID和密码的用户身份验证。 （请参阅[使用SPNEGO](/help/forms/using/admin-help/enabling-single-sign-on-aem.md#enable-sso-using-spnego)启用SSO。）

## 添加身份验证提供程序{#add-an-authentication-provider}

1. 在管理控制台中，单击设置>用户管理>域管理。
1. 单击列表中的现有域。 如果要为新域添加身份验证，请参阅[添加企业域](/help/forms/using/admin-help/adding-domains.md#add-an-enterprise-domain)或[添加混合域](/help/forms/using/admin-help/adding-domains.md#add-a-hybrid-domain)。
1. 单击“添加身份验证”，然后在“身份验证提供程序”列表中，根据您的单位使用的身份验证机制选择一个提供程序。
1. 在页面上提供所需的任何其他信息。 （请参阅[身份验证设置](configuring-authentication-providers.md#authentication-settings)。）
1. （可选）单击测试以测试配置。
1. 单击“确定”，然后再次单击“确定”。

## 编辑现有的身份验证提供程序{#edit-an-existing-authentication-provider}

1. 在管理控制台中，单击设置>用户管理>域管理。
1. 在列表中单击相应的域。
1. 在显示的页面上，从列表中选择适当的身份验证提供程序，并根据需要进行更改。 （请参阅[身份验证设置](configuring-authentication-providers.md#authentication-settings)。）
1. 单击确定。

## 删除身份验证提供程序{#delete-an-authentication-provider}

1. 在管理控制台中，单击设置>用户管理>域管理。
1. 在列表中单击相应的域。
1. 选中要删除的身份验证提供者的复选框，然后单击“删除”。
1. 在显示的确认页面上单击“确定”，然后再次单击“确定”。

## 身份验证设置{#authentication-settings}

根据您选择的域类型和身份验证类型，可以使用以下设置。

### LDAP设置{#ldap-settings}

如果要为企业或混合域配置身份验证并选择LDAP身份验证，则可以选择使用在目录配置中指定的LDAP服务器，也可以选择其他LDAP服务器进行身份验证。 如果选择其他服务器，则用户必须同时存在于两个LDAP服务器上。

要使用在目录配置中指定的LDAP服务器，请选择LDAP作为身份验证提供程序，然后单击“确定”。

要使用其他LDAP服务器执行身份验证，请选择LDAP作为身份验证提供程序，然后选中“自定义LDAP身份验证”复选框。 将显示以下配置设置。

**服务器** :（必填）目录服务器的完全限定域名(FQDN)。例如，对于corp.example.com网络上名为x的计算机，FQDN为x.corp.example.com。 可以使用IP地址代替FQDN服务器名称。

**端口：** （必需）目录服务器使用的端口。如果使用安全套接字层(SSL)协议通过网络发送身份验证信息，则通常为389或636。

**SSL:** （必需）指定在通过网络发送数据时目录服务器是否使用SSL。默认值为“否”。 如果设置为“是”，则相应的LDAP服务器证书必须由应用程序服务器的Java™运行时环境(JRE)信任。

**绑定** （强制）指定如何访问目录。

**匿名：** 无需用户名或密码。

**用户：需** 要身份验证。在“名称”框中，指定可访问目录的用户记录的名称。 最好输入用户帐户的完整辨别名(DN)，如cn=Jane Doe、ou=user、dc=can、dc=com。 在“口令”框中，指定关联的口令。 当您选择“用户”作为“绑定”选项时，需要这些设置。

**检索基本DN** :（非必需）检索基本DN并在下拉列表中显示它们。当您有多个基本DN并且需要选择值时，此设置很有用。

**基本DN:** （必需）用作从LDAP层次结构同步用户和用户组的起点。最好在层次结构的最低级别指定基本DN，该DN包含需要同步服务的所有用户和组。 不要在此设置中包含用户的DN。 要同步特定用户，请使用“搜索筛选器”设置。

**用以下内容填充页** 面：（非必填）选中后，使用相应的默认LDAP值填充“用户”和“用户组”设置页面的属性。

**搜索筛选器** :（必填）用于查找与用户关联的记录的搜索筛选器。请参阅搜索筛选器语法。

### Kerberos设置{#kerberos-settings}

如果要为企业或混合域配置身份验证并选择Kerberos身份验证，则可以使用以下设置。

**DNS IP:** 运行AEM表单的服务器的DNS IP地址。在Windows上，可以通过在命令行运行ipconfig /all来确定此IP地址。

**KDC主机：** 用于身份验证的Active Directory服务器的完全限定的主机名或IP地址。

**服务用** 户：如果您使用Active Directory 2003，此值是为表单中的服务主体创建的映射 `HTTP/<server name>`。如果您使用Active Directory 2008，此值是服务主体的登录ID。 例如，假定服务主体名为um spnego，用户ID为spnegodemo，映射为HTTP/example.corp.yourcompany.com。 在Active Directory 2003中，将服务用户设置为HTTP/example.corp.yourcompany.com。 在Active Directory 2008中，您将服务用户设置为spnegodemo。 （请参阅使用SPNEGO启用SSO。）

**服务领域：** Active Directory的域名

**服务密码：** 服务用户的密码

**启用SPNEGO:** 启用SPNEGO进行单点登录(SSO)。（请参阅使用SPNEGO启用SSO。）

### SAML设置{#saml-settings}

如果要为企业或混合域配置身份验证并选择SAML身份验证，则可使用以下设置。 有关其他SAML设置的信息，请参阅[配置SAML服务提供商设置](/help/forms/using/admin-help/configure-saml-service-provider-settings.md#configure-saml-service-provider-settings)。

**请选择要导入的SAML标识提供者元数据文件：** 单击“浏览”以选择从您的IDP生成的SAML标识提供者元数据文件，然后单击“导入”。将显示来自IDP的详细信息。

**标题：** 由EntityID表示的URL的别名。对于企业和本地用户，标题也会显示在登录页面上。

**标识提供者支持客户端基本身** 份验证：当IDP使用SAML对象解析用户档案时，将使用客户端基本身份验证。在此用户档案中，用户管理将连接回在IDP处运行的Web服务，以检索实际的SAML断言。 IDP可能需要身份验证。 如果IDP确实需要身份验证，请选择此选项并在提供的框中指定用户名和密码。

**自定义属** 性：允许您指定其他属性。附加属性为name=值对，用新行分隔。

如果使用对象绑定，则需要以下自定义属性。

* 添加以下自定义属性以指定表示AEM表单服务提供商的用户名，该用户名将用于对IDP对象解析服务进行身份验证。
   `saml.idp.resolve.username=<username>`

* 添加以下自定义属性以指定在`saml.idp.resolve.username`中指定的用户的口令。
   `saml.idp.resolve.password=<password>`

* 添加以下自定义属性，以允许服务提供商在通过SSL建立与对象解析服务的连接时忽略证书验证。
   `saml.idp.resolve.ignorecert=true`

### 自定义设置{#custom-settings}

如果要为企业或混合域配置身份验证并选择“自定义身份验证”，请选择自定义身份验证提供程序的名称。

## 用户{#just-in-time-provisioning-of-users}的及时配置

在用户通过身份验证提供程序成功通过身份验证后，即时设置会在用户管理数据库中自动创建用户。 相关角色和组也会动态分配给新用户。 您可以为企业和混合域启用即时配置。

此过程描述了传统身份验证在AEM表单中的工作方式：

1. 当用户尝试登录AEM表单时，用户管理会按顺序将其凭据传递给所有可用的身份验证提供者。 （登录凭据包括用户名／密码组合、Kerberos票证、PKCS7签名等。）
1. 身份验证提供程序验证凭据。
1. 然后，身份验证提供程序检查用户是否存在于用户管理数据库中。 可能具有以下状态：

   **存** 在如果用户当前并已解锁，则用户管理将返回身份验证成功。但是，如果用户不是当前用户或已锁定，则用户管理会返回身份验证失败。

   **不存在** 用户管理返回身份验证失败。

   **InvalidUser** Management返回身份验证失败。

1. 将评估身份验证提供程序返回的结果。 如果身份验证提供程序返回身份验证成功，则允许用户登录。 否则，用户管理会与下一个身份验证提供程序进行检查（步骤2-3）。
1. 如果没有可用的身份验证提供程序验证用户凭据，则会返回身份验证失败。

启用即时设置后，如果其中一个身份验证提供者验证其凭据，则会在用户管理中动态创建新用户。 （上述步骤中的步骤3之后。）

如果不及时进行设置，则当用户成功通过身份验证但在用户管理数据库中找不到时，身份验证将失败。 即时设置在身份验证过程中添加了一个步骤，用于创建用户并为用户分配角色和组。

### 为域{#enable-just-in-time-provisioning-for-a-domain}启用即时配置

1. 编写实现IdentityCreator和AssignmentProvider接口的服务容器。 (请参阅[使用AEM表单进行编程](https://www.adobe.com/go/learn_aemforms_programming_63)。)
1. 将服务容器部署到表单服务器。
1. 在管理控制台中，单击设置>用户管理>域管理。

   选择现有域或单击“新建企业域”。

1. 要创建域，请单击“新建企业域”或“新建混合域”。 要编辑现有域，请单击域的名称。
1. 选择“仅启用时间设置”。

   ***注&#x200B;**:如果缺少“启用即时配置”复选框，请单击“主页”>“设置”>“用户管理”>“配置”>“高级系统属性”，然后单击“重新加载”。*

1. 添加身份验证提供程序。 添加身份验证提供者时，在“新建身份验证”屏幕上，选择已注册的身份创建者和分配提供者。 （请参阅[配置身份验证提供程序](configuring-authentication-providers.md#configuring-authentication-providers)。）
1. 保存域。

