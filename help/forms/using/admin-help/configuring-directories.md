---
title: 配置目录
seo-title: Configuring directories
description: 了解如何添加、编辑和删除目录以及配置用户管理以使用虚拟列表视图。
seo-description: Learn how to add, edit and delete directories and configure user management to use virtual list view.
uuid: 0bf1a8a7-c917-4248-9937-d24e31c5ba17
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/setting_up_and_managing_domains
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 1f15f028-aa81-478e-97eb-f83a4dc0418c
exl-id: 30edcef2-e8fa-403a-9850-b8dfeeb9ac65
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '3226'
ht-degree: 0%

---

# 配置目录 {#configuring-directories}

对于您配置的每个企业域，指定验证提供程序查询用户信息的目录。 您可以为一个域配置多个目录。

## 添加目录或自定义SPI {#adding-directories-or-custom-spis}

对于您配置的每个企业域，指定验证提供程序查询用户信息的目录。 可以将目录添加到现有企业域或要添加的新企业域。 您可以为一个域配置多个目录。 您还可以配置域以使用自定义服务提供者接口(SPI)进行同步。

### 添加目录 {#add-a-directory}

1. 在管理控制台中，单击设置>用户管理>域管理。
1. 单击新建企业域或选择现有企业域。
1. 单击添加目录。
1. 在“配置文件名称”框中，键入一个名称以区分此目录，然后单击“下一步”。
1. 配置目录服务器设置。 (请参阅 [目录设置](configuring-directories.md#directory-settings).)
1. 要验证是否可以与LDAP服务器建立连接，请单击“测试”。 如果测试失败，请查看应用程序服务器日志文件中的异常以确定失败的根本原因。 单击“关闭” ，然后单击“下一步”。
1. 选择“用户设置”并根据需要配置设置。 (请参阅 [目录设置](configuring-directories.md#directory-settings).)
1. 要验证基本DN和其他配置的属性是否收集了正确的用户批次，请单击“测试”。 LDAP会尝试使用提供的设置（例如基本DN、搜索过滤器和所有属性）检索前200条记录。

   如果返回用户，则结果将显示根据属性集分配给每个字段的值。 如果由于服务器名称不存在、授权信息不正确或属性不正确而导致测试失败，则会显示以下错误消息：“指定的搜索条件未返回任何结果”。 要确定失败的根本原因，请查看应用程序服务器日志文件中的异常。 单击“关闭” ，然后单击“下一步”。

1. 选择“组设置”并根据需要配置设置。 (请参阅 [目录设置](configuring-directories.md#directory-settings).)
1. 要验证基本DN和其他配置的属性是否收集正确的组批次，请单击“测试”。 如果返回组，结果将显示根据属性集分配给每个字段的值。 单击关闭。

### 添加自定义SPI {#add-a-custom-spi}

有关创建自定义SPI的信息，请参阅中的“为AEM表单开发SPI” [使用AEM表单编程](https://www.adobe.com/go/learn_aemforms_programming_63). 要使新部署的自定义SPI可与域关联，请重新启动服务器。

1. 在管理控制台中，单击设置>用户管理>域管理。
1. 单击新建企业域或选择现有企业域。
1. 单击添加目录。
1. 在“配置文件名称”框中键入名称，选择“自定义SPI提供程序”，然后单击“下一步”。
1. 从列表中选择自定义用户提供程序，然后单击“下一步”。
1. 从列表中选择自定义组提供程序，然后单击“完成”。

## 编辑目录 {#edit-a-directory}

您可以编辑以前配置的目录的详细信息。

1. 在管理控制台中，单击设置>用户管理>域管理。
1. 单击列表中的相应域，然后在出现的页面上，从列表中选择相应的目录。
1. 根据需要配置目录、用户和组设置。 (请参阅 [目录设置](configuring-directories.md#directory-settings).)
1. 单击确定。

## 删除目录 {#delete-a-directory}

在删除目录后同步域时，该目录中的所有用户和组在数据库中都标记为过时。 它们将不会在管理控制台的任何搜索中返回。

>[!NOTE]
>
>企业域至少需要一个身份验证提供程序和目录提供程序。

1. 在管理控制台中，单击设置>用户管理>域管理。
1. 单击列表中的相应域。
1. 选中相应目录的复选框，然后单击“删除”。
1. 在显示的确认页上单击确定，然后再次单击确定。

## 目录设置 {#directory-settings}

将目录添加到域时，请指定以下目录设置。

**服务器：** （必需）目录服务器的完全限定域名(FQDN)。 例如，对于adobe.com网络上名为x的计算机，FQDN为x.adobe.com。 可以使用IP地址代替FQDN服务器名称。

**端口：** （必需）目录服务器使用的端口。 通常为389，如果安全套接字层(SSL)协议用于通过网络发送身份验证信息，则为636。

**SSL：** （必需）指定目录服务器通过网络发送数据时是否使用SSL。 默认值为“否”。 当设置为“是”时，相应的LDAP服务器证书必须受到应用程序服务器的Java™运行时环境(JRE)的信任。

**绑定** （必需）指定访问目录的方式。

**匿名：** 不需要用户名或密码。 匿名用户可能只能获取有限数量的数据。 此选项对初始测试可能很有用。

**用户：** 需要身份验证。 在“名称”框中，指定可以访问目录的用户记录的名称。 最好输入用户帐户的完整可分辨名称(DN)，如cn=Jane Doe、ou=user、dc=can、dc=com。 在“密码”框中，指定关联的密码。 选择“用户”作为“绑定”选项时，需要这些设置。

**名称：** 在未启用匿名访问时可用于连接到LDAP数据库的名称。 对于Active Directory 2003，请指定 `[domain name]\[userid]`. 对于Sun™ One、eDirectory或IBM Tivoli Directory Server，请指定用户的完全限定名称，如uid=lcuser，ou=it，o=company.com。

**密码：** 在未启用匿名访问的情况下，与指定用于连接到LDAP数据库的名称对应的口令。

**在页面中填充以下内容：** 选中后，会使用相应的默认LDAP值填充“用户”和“组”设置页面上的属性。

**检索基本DN：** 检索基本DN并在下拉列表中显示它们。 当您有多个基本DN并且需要选择一个值时，此设置非常有用。

**启用反向链接：** 当您的组织使用以层次结构组织的多个Active Directory域，并且您仅为父域指定了目录设置时，此设置适用。 在此情况下，当您选择此选项时，“用户管理”可以从子域访问用户和组的详细信息。

>[!NOTE]
>
>单击测试以验证是否可以与LDAP服务器建立连接。 要确定任何失败的根本原因，请查看应用程序服务器日志文件中的异常。

### 用户设置 {#user-settings}

**唯一标识符：** （必需）用于标识用户的唯一且常量的属性。 将非DN属性用作唯一标识符，因为如果用户移至组织的其他部分，其DN可能会发生更改。 此设置取决于目录服务器。 该值是Active Directory 2003的objectGUID、Sun™ One的nsuniqueID和eDirectory的guid。

>[!NOTE]
>
>确保输入的属性在您的组织中必须是唯一的。 输入不正确的值可能会导致严重的系统问题。

**基本DN：** 设置为从LDAP层次结构同步用户和组的起点。 最好在层次结构的最低级别指定一个基本DN，该层级包含所有需要为服务同步的用户和组。

如果在“目录”设置中选择了“启用引用”选项，则将“基本DN”选项设置为 *dc* DN的一部分。 要使反向链接生效，搜索范围必须包括父域和子域。

>[!NOTE]
>
>请勿在此设置中包含用户的DN。 要同步特定用户，请使用“搜索过滤器”设置。

虽然Base DN是Administration Console中的强制设置，但某些目录服务器(如IBM Domino Enterprise Server)可能需要空的BaseDN。 要指定空的基本DN，请导出config.xml文件，编辑config.xml文件中的设置，然后重新导入它。 (请参阅 [导入和导出配置文件](/help/forms/using/admin-help/importing-exporting-configuration-file.md#importing-and-exporting-the-configuration-file).)

**搜索筛选器：** （必需）用于查找与用户关联的记录的搜索过滤器。 您可以执行一级搜索或子级搜索。 （请参阅搜索筛选器语法或RFC 2254。） 有关Microsoft AD架构的其他信息，请参阅Active Directory架构。

**描述：** 用户说明的架构属性

**全名：** （必需）用户全名的架构属性

**登录ID：** （必需）用户登录ID的架构属性

**姓氏：** （必需）用户姓氏的架构属性

**名字：** （必需）用户名字的架构属性

**首字母：** 用户首字母的架构属性

**业务日历：** 使您能够根据此设置的值（业务日历键）将业务日历映射到用户。 业务日历定义业务日和非业务日。 在计算事件（如提醒、截止日期和呈报）的未来日期和时间时，AEM表单可以使用业务日历。 为用户分配业务日历键的方式取决于您使用的是企业域、本地域还是混合域。 （请参阅配置业务日历。）

如果您使用的是企业域，则可以将“业务日历”设置映射到LDAP目录中的字段。 例如，如果目录中的每个用户记录包含 *国家/地区* 字段，并且要根据用户所在的国家/地区分配业务日历，请指定 *国家/地区* 字段名称作为业务日历设置的值。 然后，您可以映射业务日历键（为定义的值） *国家/地区* 字段)，用于表单工作流中的业务日历。

表单工作流页面中用于显示业务日历键名称的空间量有限。 将业务日历键的名称限制为少于53个字符，以避免其在这些页面上被截断。

**修改时间戳：** 要启用增量目录同步，请设置此值以修改时间戳。 （请参阅启用增量目录同步。）

**组织：** 用户所属组织名称的架构属性。

**主电子邮件：** 用户的主要电子邮件地址的架构属性。

**辅助电子邮件：** 用户辅助电子邮件地址的架构属性。

**电话：** 用户电话号码的模式属性。

**邮政地址：** 用户邮寄地址的架构属性。

**区域设置：** 包含ISO区域设置信息的架构属性。 该值是一个由两个字母组成的语言代码或语言和国家/地区代码。

**时区：** 包含用户所在时区的架构属性。 该值是一个字符串，例如城市/国家/地区。

**启用虚拟列表视图(VLV)控制：** 一种LDAP控件，它使AEM表单能够从目录服务器中批量检索数据。 如果将Sun One用作LDAP目录并且该目录包含许多用户，则启用VLV将创建一个索引，“用户管理”可在搜索用户时使用该索引。 当使用只能同步有限数量数据的普通用户帐户时，此功能非常有用。 也可以为组启用VLV。 如果选择“启用虚拟列表视图(VLV)控件”，请在“排序字段”框中指定一个名称。

>[!NOTE]
>
>要启用VLV，请配置Sun One。 请参阅 [配置用户管理以使用虚拟列表视图(VLV)](configuring-directories.md#configure-user-management-to-use-virtual-list-view-vlv).

**排序字段：** 如果选择了“启用虚拟列表视图(VLV)控件”，请指定用于对索引进行排序的属性名称。 此属性名称（如uid）是在目录服务器上创建VLV索引时指定的名称。

### 组设置 {#group-settings}

**唯一标识符：** （必需）用于标识组的唯一且常量的属性。 使用非DN属性作为唯一标识符。 此设置取决于目录服务器。 该值是Active Directory 2003的objectGUID、Sun One的nsuniqueID和eDirectory的guid。

>[!NOTE]
>
>确保输入的属性在您的组织中必须是唯一的。 输入不正确的值可能会导致严重的系统问题。

**基本DN：** （必需）目录的基本可分辨名称。

虽然Base DN是Administration Console中的强制设置，但某些目录服务器(如IBM Domino Enterprise Server)需要空的BaseDN。 要指定空的基本DN，请导出config.xml文件，编辑config.xml文件中的设置，然后重新导入它。 (请参阅 [导入和导出配置文件](/help/forms/using/admin-help/importing-exporting-configuration-file.md#importing-and-exporting-the-configuration-file).)

**搜索筛选器：** （必需）用于查找与组关联的记录的搜索筛选器。 您可以执行一级搜索或子级搜索。

**描述：** 组的说明的架构属性

**全名：** （必需）组全名的架构属性

**成员DN：** （必需）组中成员的唯一判别名的模式属性

**成员唯一标识符：** 作为选定组成员的用户或组的唯一标识符。 此值取决于目录服务器。 该值是AD2003的objectSID、Sun One的nsuniqueID和eDirectory的guid。

如果使用非DN属性指定成员DN，则“用户管理”使用成员唯一标识符查询LDAP以收集与唯一标识符值对应的用户DN。

如果DN被指定为唯一标识符，则无需配置成员唯一标识符。

**组织：** 组所属组织名称的架构属性

**主电子邮件：** 组的主要电子邮件地址的架构属性

**辅助电子邮件：** 组的辅助电子邮件地址的架构属性

**修改时间戳：** 要启用增量目录同步，请设置此值以修改时间戳。 （请参阅启用增量目录同步。）

**启用虚拟列表视图(VLV)控制：** 一种LDAP控件，它使AEM表单能够从目录服务器中批量检索数据。 如果将Sun One用作LDAP目录并且该目录包含许多组，则启用VLV将创建一个索引，“用户管理”可在搜索组时使用该索引。 当使用只能同步有限数量数据的普通用户帐户时，此功能非常有用。 您也可以为用户启用VLV。 如果选择启用虚拟列表视图(VLV)控件，请指定排序字段名称。

>[!NOTE]
>
>要启用VLV，请配置Sun One。 请参阅 [配置用户管理以使用虚拟列表视图(VLV)](configuring-directories.md#configure-user-management-to-use-virtual-list-view-vlv).

**排序字段名称：** 如果选择了“启用虚拟列表视图(VLV)控件”，请指定用于对索引进行排序的属性名称。 此属性名称是在目录服务器上创建VLV索引时指定的名称。

>[!NOTE]
>
>单击测试以验证是否根据基本DN和搜索条件收集用户和组设置。

如果返回用户和组，则结果将显示根据属性集分配给每个字段的值。

>[!NOTE]
>
>“用户管理”不支持在域中使用重复的用户ID；只同步一个具有用户ID的用户。

## 配置用户管理以使用虚拟列表视图(VLV) {#configure-user-management-to-use-virtual-list-view-vlv}

目录同步是User Management的重要要求。 用户和组从企业目录同步到AEM表单数据库，以分配角色和权限。 用户数量从100到100000+不等，这取决于需求，对数据的有效同步提出了工程上的挑战。

LDAP协议提供了一种机制，通过使用请求控件以分页方式查询大型数据集。 使用Microsoft Active Directory时，LDAP到AEM表单的数据库同步使用PagedResultsControl检索特定大小的批次数据。 Sun ONE Directory Server不支持此控制。 要完成针对Sun ONE Directory Server的分页查询，请使用Virtual List View (VLV)控件。 此控件包括目录服务器端配置和客户端实施。

>[!NOTE]
>
>本节介绍如何将VLV控件用于Sun ONE Directory Server。 但是，您可以将此控件用于支持VLV控制的任何目录服务器。

1. 配置目录时，在“用户设置”页面和“组设置”页面上选择“启用虚拟列表视图(VLV)控制”。 选中该复选框时，还必须在“排序字段”框中指定排序名称。 默认值为uid。 (请参阅 [添加目录或自定义SPI](configuring-directories.md#adding-directories-or-custom-spis) 或 [编辑目录](configuring-directories.md#edit-a-directory).)
1. 使用Sun ONE管理控制台或命令行脚本为用户和组创建LDAP VLV条目。 如果使用命令行脚本，则可以使用示例用户和组LDIF文件。 (请参阅 [为VLV配置Sun ONE Directory Server](configuring-directories.md#configuring-the-sun-one-directory-server-for-vlv).)
1. 停止服务器并创建所需的索引。 (请参阅 [创建VLV的目录服务器索引](configuring-directories.md#create-the-directory-server-index-for-vlv).)

### 为VLV配置Sun ONE Directory Server {#configuring-the-sun-one-directory-server-for-vlv}

创建VLV需要一对条目，其中包括 `vlvSearch` 和 `vlvIndex` 对象类。 vlvSearch条目包括搜索基和 `vlvFilter` 属性，指定包含要排序的属性的对象类。 此 `vlvIndex` 对象类包括 `vlvSort` 属性，指定要排序的一个或多个属性以及它们的排序顺序。 (减号(-)表示反字母顺序)。 在AEM表单中使用VLV时，需要为用户和组设置单独的条目。

>[!NOTE]
>
>可以使用Sun ONE图形用户界面(GUI)或通过命令行脚本创建Object条目。 有关使用GUI创建Object条目的说明，请参见Sun ONE文档。

以下是用户VLV条目的脚本LDIF示例：

```text
 dn: cn=lcuser,cn=userRoot,cn=ldbm database,cn=plugins,cn=config
 objectclass: top
 objectclass: vlvSearch
 cn: lcuser
 vlvBase: dc=corp,dc=adobe,dc=com
 vlvScope: 2
 vlvFilter: (&(objectclass=inetOrgPerson))
 aci: (target="ldap:///cn=lcuser,cn=userRoot,cn=ldbm database,cn=plugins,cn=config")(targetattr="*")(version 3.0; acl "Config"
 ;allow(read,search,compare) userdn="ldap:///all"; )
 dn: cn=lcuser,cn=lcuser,cn=userRoot,cn=ldbm database,cn=plugins,cn=config
 cn: lcuser
 vlvSort: cn
 objectclass: top
 objectclass: vlvIndex
```

**使用脚本创建对象条目**

1. 示例脚本中有一个名为的LDAP条目 `lcuser`. 此条目用于在AEM表单中进行用户同步的VLV相关配置。 相应地修改以下属性：

   **条目名称：** 此示例中的条目名称为 `lcuser`. 如果 `lcuser` 更改，必须在示例脚本的所有区域对其进行更改。

   **vlvBase：** 在“用户设置”页面上指定的基本DN。

   **vlvFilter：** “用户设置”页面上指定的“搜索筛选器”。

   **vlvSort：** 在“用户设置”页面的VLV设置部分中指定的“排序字段”。 VLV控件要求指定排序控件。 此字段用作创建的vlv索引的排序参数。

   **aci：** 示例脚本中指定的访问控制授予任何经过身份验证的用户访问VLV索引以进行读取、搜索和比较操作的权限。 管理员可以限制对绑定用户的访问，该绑定用户在“用户管理”用户界面指定的“目录服务器设置”页中配置。 如果未指定权限，则用户搜索无法使用VLV，并且LDAP服务器会引发权限异常。

   >[!NOTE]
   >
   >作为约定，vlvIndex条目名称也设置为 `lcuser`，但您可以为其指定其他名称。 在vlvindex工具中使用相同的名称。 (请参阅 [创建VLV的目录服务器索引&#x200B;](configuring-directories.md#create-the-directory-server-index-for-vlv)*.)*

1. 使用 `ldapmodify` Sun ONE Server提供的工具，请分别使用组的基本DN、搜索过滤器和排序字段为组创建类似的条目：

   `server directory\shared\bin>ldapmodify -v -a -h host -p port -D "admin user" -w "password" -f "LDIF file location"`

   例如，键入以下文本：

   `D:\tools\ldap\sun\shared\bin> -v -a -h localhost -p 55850 -D "uid=admin,ou=administrators,ou=topologymanagement,o=netscaperoot" -w "admin" -f "D:\tools\ldap\data\vlv feature\users.ldif"`

### 创建VLV的目录服务器索引 {#create-the-directory-server-index-for-vlv}

配置目录设置并为用户和组创建LDAP VLV条目后，停止服务器并创建所需的索引。

1. 创建对象条目后，停止Sun ONE Server。
1. 使用vlvindex工具，通过键入以下文本生成索引：

   *目录服务器实例* `\vlvindex.bat -n userRoot -T lcuser`

   将生成以下输出：

   ```shell
    D:\tools\ldap\sun\shared\bin>..\..\slapd-chetanmeh-xp3\vlvindex.bat -n userRoot -T livecycle
    [21/Nov/2007:16:47:26 +051800] - userRoot: Indexing VLV: livecycle
    [21/Nov/2007:16:47:27 +051800] - userRoot: Indexed 1000 entries (5%).
    [21/Nov/2007:16:47:27 +051800] - userRoot: Indexed 2000 entries (9%).
    ...
    [21/Nov/2007:16:47:29 +051800] - userRoot: Indexed 20000 entries (94%).
    [21/Nov/2007:16:47:29 +051800] - userRoot: Indexed 21000 entries (99%).
    [21/Nov/2007:16:47:29 +051800] - userRoot: Finished indexing.
   ```

   vlvindex工具位于目录服务器实例目录中。 如果Sun ONE Server有两个运行server1和server2的实例，则vlvindex工具位于 *Sun ONE服务器目录*\server1目录。 参数的值 `-T` 的值为 `cn` 之前在示例LDIF中创建的vlvindex条目的属性。 在这种情况下，它是 `lcuser`.

1. 如果还为组启用了VLV，请为组创建相应的索引。 通过运行以下命令验证是否创建了索引：

   *sun one server目录* `\shared\bin>ldapsearch -h`*主机名* `-p`*端口号* `-s base -b "" objectclass=*`

   生成诸如以下示例数据的输出：

   ```shell
    D:\tools\ldap\sun\shared\bin>ldapsearch.exe -h localhost -p 55850 -s base -b "" objectclass=*
    ldapsearch.exe: started Tue Nov 27 16:34:20 2007
    version: 1
    dn:
    objectClass: top
    namingContexts: dc=corp,dc=adobe,dc=com
    supportedExtension: 2.16.840.1.113730.3.5.7
    ...
    vlvsearch: cn=MCC ou=testdata dc=corp dc=adobe dc=com, cn=userRoot,cn=ldbm dat
        abase,cn=plugins,cn=config
    vlvsearch: cn=lcuser,cn=userRoot,cn=ldbm database,cn=plugins,cn=config
    vlvsearch: cn=Browsing ou=testdata,cn=userRoot,cn=ldbm database,cn=plugins,cn=
        config
    1 matches
   ```
