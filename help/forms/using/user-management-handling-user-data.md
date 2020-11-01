---
title: Forms用户管理 |处理用户数据
seo-title: Forms用户管理 |处理用户数据
description: Forms用户管理 |处理用户数据
uuid: 2b76b69f-6f3a-4f1a-a2a4-d39f5e529f75
topic-tags: grdp
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: a88fc933-f1af-4798-b72f-10e7b0d2fd11
translation-type: tm+mt
source-git-commit: a873cf3e7efd3bc9cd4744bf09078d9040efcdda
workflow-type: tm+mt
source-wordcount: '890'
ht-degree: 0%

---


# Forms用户管理 |处理用户数据 {#forms-user-management-handling-user-data}

用户管理是一个AEM FormsJEE组件，它允许创建、管理和授权AEM Forms用户访问AEM Forms。 用户管理使用域作为获取用户信息的目录。 支持以下域类型：

**本地域**:此类域未连接到第三方存储系统。 而是在本地创建用户和组并驻留在用户管理数据库中。 口令存储在本地，身份验证使用本地数据库完成。

**混合域**:此类域未连接到第三方存储系统。 而是在本地创建用户和组并驻留在用户管理数据库中。 与本地域不同，混合域使用外部身份验证提供程序，该提供程序可以是LDAP、Kerberos、SAML或自定义身份验证提供程序。

**企业域**:由驻留在第三方存储系统（如LDAP目录）中的用户和用户组组成。 用户管理不写入第三方存储系统。 相反，用户管理会将用户和组信息与用户管理数据库同步。 企业域还使用外部身份验证提供程序，该提供程序可以是LDAP、Kerberos、SAML或自定义身份验证提供程序。

<!-- Fix broken links For more information about how user management works and configured, see AEM Forms JEE administration help. -->

## 用户数据和数据存储 {#user-data-and-data-stores}

用户管理将用户数据存储在数据库中，如My Sql、Oracle、MS SQL Server和IBM DB2。 此外，在AEM作者的Forms应用程序中至少登录一次的任何用户，都 `https://'[server]:[port]'lc`会在AEM存储库中创建该用户。 因此，用户管理存储在以下数据存储中：

* 数据库
* AEM存储库
* 第三方存储，如LDAP目录

>[!NOTE]
>
>存储在第三方存储中的数据超出此文档的范围。 直接与第三方供应商联系以管理此类存储中的用户数据。

### 数据库 {#database}

用户管理将用户数据存储在以下数据库表中：

<table>
 <tbody>
  <tr>
   <td>数据库表</td>
   <td>描述</td>
  </tr>
  <tr>
   <td><code>EdcPrincipalEntity</code></td>
   <td><p>存储有关主体实体的信息。 主体可以是用户、组或角色。</p> <p> </p> </td>
  </tr>
  <tr>
   <td><code>EdcPrincipalUserEntity</code></td>
   <td>存储用户的个人身份信息(PII)。 它包含本地、企业和混合域中每个用户的条目。</td>
  </tr>
  <tr>
   <td><p><code>EdcPrincipalLocalAccountEntity</code></p> <p><code class="code">EdcPrincipalLocalAccount
       </code>（Oracle和MS SQL数据库）</p> </td>
   <td>仅存储本地用户的数据。</td>
  </tr>
  <tr>
   <td><p><code>EdcPrincipalEmailAliasEntity</code></p> <p><code class="code">EdcPrincipalEmailAliasEn
       </code>（Oracle和MS SQL数据库）</p> </td>
   <td>包含本地、企业和混合域中所有用户的条目。 它包含用户电子邮件ID。</td>
  </tr>
  <tr>
   <td><p><code>EdcPrincipalGrpCtmntEntity</code></p> <p><code>EdcPrincipalGrpCtmntEnti</code> （Oracle和MS SQL数据库）</p> </td>
   <td>存储用户和用户组之间的映射。</td>
  </tr>
  <tr>
   <td><code>EdcPrincipalRoleEntity</code></td>
   <td>存储用户和用户组的角色和主体之间的映射。</td>
  </tr>
  <tr>
   <td><code>EdcPriResPrmEntity</code></td>
   <td>存储用户和用户组的主体和权限之间的映射。</td>
  </tr>
  <tr>
   <td><p><code>EdcPrincipalMappingEntity</code></p> <p><code>EdcPrincipalMappingEntit</code> （Oracle和MS SQL数据库）</p> </td>
   <td>存储与主体对应的新旧属性值。<br /> </td>
  </tr>
 </tbody>
</table>

### AEM存储库 {#aem-repository}

至少访问过Forms应用程序的用户管理数据也 `https://'[server]:[port]'lc` 存储在AEM存储库中。

## 访问和删除用户数据 {#access-and-delete-user-data}

您可以访问和导出用户管理数据库和AEM存储库中用户的用户管理数据，如果需要，还可以永久删除它。

### 数据库 {#database-1}

要从用户管理数据库导出或删除用户数据，您需要使用数据库客户端连接到数据库，并根据用户的某些PII查找主体ID。 例如，要使用登录ID检索用户的主体ID，请在数据库上运 `select` 行以下命令。

在命 `select` 令中，将 `<user_login_id>` 其替换为要检索其主体ID的用户的登录ID。

```sql
select refprincipalid from EdcPrincipalUserEntity where uidstring = <user_login_id>
```

知道主体ID后，即可导出或删除用户数据。

#### 导出用户数据 {#export-user-data}

运行以下数据库命令，从数据库表中导出主体ID的用户管理数据。 在命 `select` 令中， `<principal_id>` 替换为要导出其数据的用户的主体ID。

>[!NOTE]
>
>以下命令在My SQL和IBM DB2数据库中使用数据库表名。 在Oracle和MS SQL数据库上运行这些命令时，请替换命令中的以下表名：
>
>* Replace `EdcPrincipalLocalAccountEntity` with `EdcPrincipalLocalAccount`
   >
   >
* Replace `EdcPrincipalEmailAliasEntity` with `EdcPrincipalEmailAliasEn`
   >
   >
* Replace `EdcPrincipalMappingEntity` with `EdcPrincipalMappingEntit`
   >
   >
* Replace `EdcPrincipalGrpCtmntEntity` with `EdcPrincipalGrpCtmntEnti`

>



```sql
Select * from EdcPrincipalLocalAccountEntity where refuserprincipalid in (Select id from EdcPrincipalUserEntity where refprincipalid in (Select id from EDCPRINCIPALENTITY where id='<principal_id>'));

Select * from EdcPrincipalEmailAliasEntity where refprincipalid in (Select id from EdcPrincipalEntity where id='<principal_id>');

Select * from EdcPrincipalRoleEntity where refprincipalid in (Select id from EdcPrincipalEntity where id='<principal_id>');

Select * from EdcPriResPrmEntity where refprinid in (Select id from EdcPrincipalEntity where id='<principal_id>');

Select * from EdcPrincipalUserEntity where refprincipalid in (Select id from EdcPrincipalEntity where id='<principal_id>');

Select * from EdcPrincipalMappingEntity where refprincipalid in (Select id from EdcPrincipalEntity where id='<principal_id>');

Select * from EdcPrincipalGrpCtmntEntity where refchildprincipalid in (Select id from EdcPrincipalEntity where id='<principal_id>');

Select * from EdcPrincipalEntity where id='<principal_id>';
```

#### 删除用户数据 {#delete-user-data}

请执行以下操作，从数据库表中删除主体ID的用户管理数据。

1. 如删除用户数据中所述，从AEM存储库中删除用户数据(如果 [适用)](/help/forms/using/user-management-handling-user-data.md#delete-aem)。
1. 关闭AEM Forms服务器。
1. 运行以下数据库命令，从数据库表中删除主体ID的用户管理数据。 在命 `Delete` 令中， `<principal_id>` 替换为要删除其数据的用户的主体ID。

   ```sql
   Delete from EdcPrincipalLocalAccountEntity where refuserprincipalid in (Select id from EdcPrincipalUserEntity where refprincipalid in (select id from EdcPrincipalEntity where id='<principal_id>'));
   
   Delete from EdcPrincipalEmailAliasEntity where refprincipalid in (Select id from EdcPrincipalEntity where id='<principal_id>');
   
   Delete from EdcPrincipalRoleEntity where refprincipalid in (Select id from EdcPrincipalEntity where id='<principal_id>');
   
   Delete from EdcPriResPrmEntity where refprinid in (Select id from EdcPrincipalEntity where id='<principal_id>');
   
   Delete from EdcPrincipalUserEntity where refprincipalid in (Select id from EdcPrincipalEntity where id='<principal_id>');
   
   Delete from EdcPrincipalMappingEntity where refprincipalid in (Select id from EdcPrincipalEntity where id='<principal_id>');
   
   Delete from EdcPrincipalGrpCtmntEntity where refchildprincipalid in (Select id from EdcPrincipalEntity where id='<principal_id>');
   
   Delete from EdcPrincipalEntity where id='<principal_id>';
   ```

1. 开始AEM Forms服务器。

### AEM存储库 {#aem-repository-1}

FormsJEE用户在AEM存储库中拥有其数据(如果他们至少访问了AEM Forms创作实例一个)。 您可以从AEM存储库访问和删除其用户数据。

#### 访问用户数据 {#access-user-data}

要视图在AEM存储库中创建的用户，请使用AEM管 `https://'[server]:[port]'/lc/useradmin` 理员凭据登录。 请注 `server` 意， `port` URL中和是AEM作者实例的实例。 在此，您可以使用用户名搜索用户。 多次-单击用户可视图用户的属性、权限和用户组等信息。 用户 `Path` 的属性指定在AEM存储库中创建的用户节点的路径。

#### 删除用户数据 {#delete-aem}

删除用户：

1. 使用AEM管 `https://'[server]:[port]'/lc/useradmin` 理员凭据转到。
1. 搜索用户，然后多次单击用户名以打开用户属性。 复制属 `Path` 性。
1. 转到AEM CRX DELite, `https://'[server]:[port]'/lc/crx/de/index.jsp` 然后导航或搜索用户路径。
1. 删除路径，然后单 **[!UICONTROL 击全部保存]** ，从AEM存储库中永久删除用户。

