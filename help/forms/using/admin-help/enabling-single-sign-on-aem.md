---
title: 在AEM表单中启用单点登录
seo-title: 在AEM表单中启用单点登录
description: 了解如何使用HTTP头和SPNEGO启用单点登录(SSO)。
seo-description: 了解如何使用HTTP头和SPNEGO启用单点登录(SSO)。
uuid: 2bc08b4f-dcbe-4a16-9025-32fc14605e13
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: ee54d9d4-190d-4665-925a-9740ac65fbd5
translation-type: tm+mt
source-git-commit: 998a127ce00c6cbb3db3a81d8a89d97ab9ef7469
workflow-type: tm+mt
source-wordcount: '1538'
ht-degree: 0%

---


# 在AEM forms{#enabling-single-sign-on-in-aem-forms}中启用单一登录

AEM表单提供两种启用单一登录(SSO)的方法- HTTP头和SPNEGO。

实施SSO时，AEM表单用户登录页面不是必需的，如果用户已通过其公司门户进行身份验证，则不显示。

如果AEM表单无法使用以下任一方法验证用户身份，则会将用户重定向到登录页。

## 使用HTTP头{#enable-sso-using-http-headers}启用SSO

您可以使用“门户配置”页在应用程序和支持通过HTTP头传递标识的任何应用程序之间启用单一登录(SSO)。 实施SSO时，AEM表单用户登录页面不是必需的，如果用户已通过其公司门户进行身份验证，则不显示。

您还可以使用SPNEGO启用SSO。 （请参阅[使用SPNEGO](enabling-single-sign-on-aem.md#enable-sso-using-spnego)启用SSO。）

1. 在管理控制台中，单击“设置”>“用户管理”>“配置”>“配置门户属性”。
1. 选择是以启用SSO。 如果选择“否”，则页面上的其余设置不可用。
1. 根据需要在页面上设置其余选项，然后单击确定：

   * **SSO类型：** （必选）选择HTTP头以使用HTTP头启用SSO。
   * **用户标识符的HTTP头** :（必填）其值包含登录用户的唯一标识符的头的名称。用户管理使用此值在用户管理数据库中查找用户。 从此头获取的值应与从LDAP目录同步的用户的唯一标识符匹配。 （请参阅[用户设置](/help/forms/using/admin-help/adding-configuring-users.md#user-settings)。）
   * **标识符值映射到用户的用户ID而不是用户的唯一标识符：将** 用户的唯一标识符值映射到用户ID。如果用户的唯一标识符是无法通过HTTP头轻松传播的二进制值（例如，如果正在从Active Directory同步用户，则选择此选项）。
   * **域的HTTP头：** （非强制）其值包含域名的头的名称。仅当没有单个HTTP头可唯一标识用户时，才使用此设置。 当存在多个域且唯一标识符仅在域内唯一时，请使用此设置。 在这种情况下，请在此文本框中指定标题名称，并在“域映射”框中指定多个域的域映射。 （请参阅[编辑和转换现有域](/help/forms/using/admin-help/editing-converting-existing-domains.md#editing-and-converting-existing-domains)。）
   * **域映射：** （必需）指定以头值=域名 *格式映射多个域*。

      例如，考虑域的HTTP头为domainName且其值可以为domain1、domain2或domain3的情况。 在这种情况下，请使用域映射将domainName值映射到用户管理域名。 每个映射必须位于不同的行上：

      domain1=UMdomain1

      domain2=UMdomain2

      domain3=UMdomain3

### 配置允许的引用者{#configure-allowed-referers}

有关配置允许的引用器的步骤，请参阅[配置允许的引用器](/help/forms/using/admin-help/preventing-csrf-attacks.md#configure-allowed-referers)。

## 使用SPNEGO {#enable-sso-using-spnego}启用SSO

在Windows环境中将Active Directory用作LDAP服务器时，可以使用简单和受保护的GSSAPI协商机制(SPNEGO)启用单一登录(SSO)。 启用SSO后，AEM表单用户登录页面不是必需的，也不显示。

您还可以使用HTTP头启用SSO。 （请参阅[使用HTTP头](enabling-single-sign-on-aem.md#enable-sso-using-http-headers)启用SSO。）

>[!NOTE]
>
>AEM Forms在JEE上不支持在多子域环境中使用Kerberos/SPNEGO配置SSO。

1. 确定启用SSO的域。 AEM表单服务器和用户必须属于同一Windows域或受信任域。
1. 在Active Directory中，创建一个表示AEM表单服务器的用户。 （请参阅[创建用户帐户](enabling-single-sign-on-aem.md#create-a-user-account)。） 如果要配置多个域以使用SPNEGO，请确保每个用户的口令不同。 如果密码不同，则SPNEGO SSO不起作用。
1. 映射服务主体名称。 (请参阅[映射服务主体名称(SPN)](enabling-single-sign-on-aem.md#map-a-service-principal-name-spn)。)
1. 配置域控制器。 （请参阅[防止Kerberos完整性检查失败](enabling-single-sign-on-aem.md#prevent-kerberos-integrity-check-failures)。）
1. 添加或编辑企业域，如[添加域](/help/forms/using/admin-help/adding-domains.md#adding-domains)或[编辑和转换现有域](/help/forms/using/admin-help/editing-converting-existing-domains.md#editing-and-converting-existing-domains)中所述。 创建或编辑企业域时，请执行以下任务:

   * 添加或编辑包含Active Directory信息的目录。
   * 将LDAP添加为身份验证提供程序。
   * 将Kerberos添加为身份验证提供程序。 在Kerberos的“新建”或“编辑身份验证”页上提供以下信息：

      * **身份验证提供程序：** Kerberos
      * **DNS IP:** 运行AEM表单的服务器的DNS IP地址。您可以通过在命令行上运行`ipconfig/all`来确定此IP地址。
      * **KDC主机：用** 于身份验证的Active Directory服务器的完全限定的主机名或IP地址
      * **服务用** 户：传递到KtPass工具的服务主体名称(SPN)。在以前使用的示例中，服务用户为`HTTP/lcserver.um.lc.com`。
      * **服务领域：** Active Directory的域名。在以前使用的示例中，域名为`UM.LC.COM.`
      * **服务密码：** 服务用户的密码。在以前使用的示例中，服务密码为`password`。
      * **启用SPNEGO:** 启用SPNEGO进行单点登录(SSO)。选择此选项。

1. 配置SPNEGO客户端浏览器设置。 （请参阅[配置SPNEGO客户端浏览器设置](enabling-single-sign-on-aem.md#configuring-spnego-client-browser-settings)。）

### 创建用户帐户{#create-a-user-account}

1. 在SPNEGO中，将服务注册为域控制器上Active Directory中的用户，以表示AEM表单。 在域控制器上，转到“开始菜单”>“管理工具”>“Active Directory用户和计算机”。 如果“管理工具”不在“开始”菜单中，请使用控制面板。
1. 单击“用户”文件夹以显示用户列表。
1. 右键单击用户文件夹，然后选择“新建”>“用户”。
1. 键入名／姓和用户登录名，然后单击下一步。 例如，设置以下值：

   * **名字**:乌姆斯佩戈
   * **用户登录名**:spnegodemo

1. 键入密码。 例如，将其设置为&#x200B;*password*。 确保已选择“密码永不过期”，且未选择其他选项。
1. 单击“Next（下一步）” ，然后单击“Finish（完成）”。

### 映射服务主体名称(SPN){#map-a-service-principal-name-spn}

1. 获取KtPass实用程序。 此实用程序用于将SPN映射到REALM。 您可以作为Windows服务器工具包或资源工具包的一部分获得KtPass实用程序。 （请参阅[Windows Server 2003 Service Pack 1支持工具](https://support.microsoft.com/kb/892777)。）
1. 在命令提示符下，使用以下参数运行`ktpass`:

   `ktpass -princ HTTP/`** `@`** `-mapuser`*hostREALMuser*

   例如，键入以下文本：

   `ktpass -princ HTTP/lcserver.um.lc.com@UM.LC.COM -mapuser spnegodemo`

   您必须提供的值如下所述：

   **主机：** 表单服务器或任何唯一URL的完全限定名称。在此示例中，它设置为lcserver.um.lc.com。

   **REALM:** 域控制器的Active Directory领域。在此示例中，它设置为UM.LC.COM。 确保输入大写字符的领域。 要确定Windows 2003的领域，请完成以下步骤：

   * 右键单击“我的计算机”并选择“属性”
   * 单击“计算机名称”选项卡。 域名值是领域名称。

   **user:** 您在上一任务创建的用户帐户的登录名。在此示例中，它设置为spnegodemo。

如果遇到此错误：

```shell
DsCrackNames returned 0x2 in the name entry for spnegodemo.
ktpass:failed getting target domain for specified user.
```

尝试将用户指定为spnegodemo@um.lc.com:

```shell
ktpass -princ HTTP/lcserver.um.lc.com@UM.LC.COM -mapuser spnegodemo
```

### 防止Kerberos完整性检查失败{#prevent-kerberos-integrity-check-failures}

1. 在域控制器上，转到“开始菜单”>“管理工具”>“Active Directory用户和计算机”。 如果“管理工具”不在“开始”菜单中，请使用控制面板。
1. 单击“用户”文件夹以显示用户列表。
1. 右键单击您在上一个任务中创建的用户帐户。 在此示例中，用户帐户为`spnegodemo`。
1. 单击“重置密码”。
1. 键入并确认之前键入的口令。 在本例中，它设置为`password`。
1. 取消选择“下次登录时更改口令”，然后单击“确定”。

### 配置SPNEGO客户端浏览器设置{#configuring-spnego-client-browser-settings}

要使基于SPNEGO的身份验证正常工作，客户端计算机必须是创建用户帐户的域的一部分。 您还必须配置客户端浏览器以允许基于SPNEGO的身份验证。 此外，需要基于SPNEGO的身份验证的站点必须是可信站点。

如果使用计算机名称(如https://lcserver:8080)访问服务器，则Internet Explorer无需设置。 如果输入的URL不包含任何点(“.”),Internet Explorer会将该站点视为本地Intranet站点。 如果您为站点使用完全限定的名称，则必须将该站点添加为受信任的站点。

**配置Internet Explorer 6.x**

1. 转到“工具”>“Internet选项”，然后单击“安全”选项卡。
1. 单击“本地内部网”图标，然后单击“站点”。
1. 单击“高级”，在“将此网站添加到区域”框中，键入表单服务器的URL。 例如，键入`https://lcserver.um.lc.com`
1. 单击“确定”，直到关闭所有对话框。
1. 通过访问AEM forms服务器的URL测试配置。 例如，在浏览器URL框中，键入`https://lcserver.um.lc.com:8080/um/login?um_no_redirect=true`

**配置Mozilla Firefox**

1. 在浏览器URL框中，键入`about:config`

   出现about:config - Mozilla Firefox对话框。

1. 在“过滤器”框中，键入`negotiate`
1. 在显示的列表中，单击network.negotiate-auth.trusted-uri，并根据您的环境键入以下命令之一：

   `.um.lc.com`-将Firefox配置为允许SPNEGO访问以um.lc.com结尾的任何URL。确保包含点(“”)。 开始时。

   `lcserver.um.lc.com` -将Firefox配置为仅允许特定服务器使用SPNEGO。请勿将此值与点(&quot;。&quot;)开始。

1. 通过访问应用程序测试配置。 应显示目标应用程序的欢迎页面。

