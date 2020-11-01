---
title: 文档安全 |处理用户数据
seo-title: 文档安全 |处理用户数据
description: 文档安全 |处理用户数据
uuid: 1624a465-8b0c-4347-a53f-1118bfa6e18f
topic-tags: grdp
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 898268cb-4426-421f-8f63-d75bd85cb57f
translation-type: tm+mt
source-git-commit: a873cf3e7efd3bc9cd4744bf09078d9040efcdda
workflow-type: tm+mt
source-wordcount: '953'
ht-degree: 0%

---


# 文档安全 |处理用户数据 {#document-security-handling-user-data}

AEM Forms文档安全允许您创建、存储和应用预定义的安全设置到文档。 它确保只有授权用户才能使用文档。 您可以使用策略保护文档。 策略是包含安全性设置和授权用户列表的信息集合。 您可以将策略应用于一个或多个文档，并授权在AEM FormsJEE用户管理中添加的用户。

<!-- Fix broken link For more information about how document security works, see AEM Forms JEE administration help. -->

## 用户数据和数据存储 {#user-data-and-data-stores}

文档安全性存储与受保护文档相关的策略和数据，包括My Sql、Oracle、MS SQL Server和IBM DB2等数据库中的用户数据。 此外，在用户管理中存储的策略中授权用户的数据。 有关用户管理中存储的数据的信息，请参 [阅Forms用户管理：处理用户数据](/help/forms/using/user-management-handling-user-data.md)。

下表映射了文档安全如何在数据库表中组织数据。

<table>
 <tbody>
  <tr>
   <td>数据库表</td>
   <td>描述</td>
  </tr>
  <tr>
   <td><code>EdcPrincipalKeyEntity</code></td>
   <td>存储有关用户的主键的信息。 这些键用于脱机文档安全工作流。</td>
  </tr>
  <tr>
   <td><code>EdcAuditEntity</code></td>
   <td>存储有关审计事件的信息，如用户事件、文档事件和策略事件。</td>
  </tr>
  <tr>
   <td><p><code>EdcLicenseEntity</code></p> </td>
   <td>存储受保护文档的记录。 它存储每个受保护文档的许可证详细信息。</td>
  </tr>
  <tr>
   <td><p><code>EdcDocumentEntity</code></p> </td>
   <td>存储系统中创建的每个许可证的文档名称。</td>
  </tr>
  <tr>
   <td><p><code>EdcRevokationEntity</code></p> </td>
   <td>存储有关被保护文档撤销和恢复的信息。</td>
  </tr>
  <tr>
   <td><code>EdcMyPolicyListEntity</code></td>
   <td>存储有关用户的信息，这些用户可以创建出现在“策略”页的“我的策略”选项卡下的个人策略。 </td>
  </tr>
  <tr>
   <td><code>EdcPolicyEntity</code></td>
   <td>存储有关策略的信息。 每个策略都与此表中的一行相对应。</td>
  </tr>
  <tr>
   <td><code>EdcPolicyXmlEntity</code></td>
   <td>存储活动策略的XML文件。 策略XML包<sup></sup>含对与策略关联的用户的主体ID的引用。 策略XML存储为Blob对象。</td>
  </tr>
  <tr>
   <td><code>EdcPolicyArchiveEntity</code></td>
   <td>存储有关存档策略的信息。 存档的策略包含其作为Blob对象存储的策略XML。</td>
  </tr>
  <tr>
   <td><p><code>EdcPolicySetPrincipalEntity</code></p> <p><code>EdcPolicySetPrincipalEnt</code> （Oracle和MS SQL数据库）</p> </td>
   <td>存储策略集和用户之间的映射。</td>
  </tr>
  <tr>
   <td><code>EdcInvitedUserEntity</code></td>
   <td>存储有关已邀请用户的信息。</td>
  </tr>
 </tbody>
</table>

## 访问和删除用户数据 {#access-and-delete-user-data}

您可以访问和导出文档库中用户的数据安全数据，如果需要，还可以永久删除它。

要从数据库导出或删除用户数据，您需要使用数据库客户端连接到数据库，并根据用户的某些个人身份信息查找主体ID。 例如，要使用登录ID检索用户的主体ID，请在数据库上运 `select` 行以下命令。

在命 `select` 令中，将 `<user_login_id>` 其替换为要从数据库表检索其主体ID的用户的登录 `EdcPrincipalUserEntity` ID。

```sql
select refprincipalid from EdcPrincipalUserEntity where uidstring = <user_login_id>
```

知道主体ID后，即可导出或删除用户数据。

### 导出用户数据 {#export-user-data}

运行以下数据库命令，从数据库表中导出主体ID的用户数据。 在命 `select` 令中， `<principal_id>` 替换为要导出其数据的用户的主体ID。

>[!NOTE]
>
>以下命令在My SQL和IBM DB2数据库中使用数据库表名。 在Oracle和MS SQL数据库上运行这些命令时，请 `EdcPolicySetPrincipalEntity` 替换为 `EdcPolicySetPrincipalEnt` 命令中的命令。

```sql
Select * from EdcPrincipalKeyEntity where principalid = '<principal_id>';

Select * from EdcLicenseEntity where publisherId = '<principal_id>';

Select * from EdcDocumentEntity where id in (Select documentid from EdcLicenseEntity where publisherId = '<principal_id>');

Select * from EdcRevokationEntity where licenseid in (Select id from EdcLicenseEntity where publisherId = '<principal_id>');

Select * from EdcMyPolicyListEntity where principalId = '<principal_id>';

Select * from edcpolicyentity where policyownerId = '<principal_id>';

Select * from edcpolicyxmlentity where policyidref in (Select id from edcpolicyentity where policyownerId = '<principal_id>');

Select * from edcpolicyarchiveentity where policyownerId = '<principal_id>';

Select * from edcpolicysetprincipalentity where principalId = '<principal_id>';

Select * from edcinviteduserentity where principalId = '<principal_id>';
```

>[!NOTE]
>
>要从表中导出 `EdcAuditEntity` 数据，请使用 [EventManager.exportEvents API，它将EventSearchFilter](https://helpx.adobe.com/experience-manager/6-5/forms/programlc/javadoc/index.html?com/adobe/livecycle/rightsmanagement/client/EventManager.html) 作为参数来导出基于、 [、](https://helpx.adobe.com/experience-manager/6-5/forms/programlc/javadoc/com/adobe/livecycle/rightsmanagement/client/infomodel/EventSearchFilter.html)`principalId``policyId``licenseId`或的审核数据。

要获取系统中某个用户的完整数据，您必须访问并从用户管理数据库导出数据。 有关详细信息，请参阅 [Forms用户管理：处理用户数据](/help/forms/using/user-management-handling-user-data.md)。

### 删除用户数据 {#delete-user-data}

请执行以下操作，从文档库表中删除主体ID的安全数据。

1. 关闭AEM Forms服务器。
1. 运行以下数据库命令，从数据库表中删除主体ID的文档，以确保数据安全。 在命 `Delete` 令中， `<principal_id>` 替换为要删除其数据的用户的主体ID。

   ```sql
   Delete from EdcPrincipalKeyEntity where principalid = '<principal_id>';
   
   Delete from EdcMyPolicyListEntity where principalId = '<principal_id>';
   
   Delete from edcpolicyarchiveentity where policyownerId = '<principal_id>';
   
   Delete from edcpolicysetprincipalentity where principalId = '<principal_id>';
   
   Delete from edcinviteduserentity where principalId = '<principal_id>';
   ```

   >[!NOTE]
   >
   >要从表中删除数 `EdcAuditEntity` 据，请使用 [EventManager.deleteEvents](https://helpx.adobe.com/experience-manager/6-5/forms/programlc/javadoc/index.html?com/adobe/livecycle/rightsmanagement/client/EventManager.html) API，它将 [EventSearchFilter](https://helpx.adobe.com/experience-manager/6-5/forms/programlc/javadoc/com/adobe/livecycle/rightsmanagement/client/infomodel/EventSearchFilter.html) 作为参数来删除基于、、 `principalId``policyId``licenseId`或的审核数据。

1. 活动策略XML文件和归档策略XML文件分别 `EdcPolicyXmlEntity` 存储在 `EdcPolicyArchiveEntity` 数据库表中。 要从这些表中删除用户的数据，请执行以下操作：

   1. 打开或表中每行的XML blob `EdcPolicyXMLEntity` 并 `EdcPolicyArchiveEntity` 提取XML文件。 XML文件与下面所示的文件类似。
   1. 编辑XML文件以删除主体ID的blob。
   1. 对另一个文件重复步骤1和2。

   >[!NOTE]
   >
   >必须删除主体ID标记中 `Principal` 的完整blob，否则策略XML可能已损坏或无法使用。

   ```xml
   <ns2:Principal PrincipalNameType="USER">
       <ns2:PrincipalDomain>OID</ns2:PrincipalDomain>
       <ns2:PrincipalName>56F33FEB-098A-1036-A651-00000A2A2656</ns2:PrincipalName>
   </ns2:Principal>
   </ns2:PolicyEntry>
       <ns2:Property PropertyName="isCertified">
           <ns2:PropertyValue xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance" xmlns:xs="https://www.w3.org/2001/XMLSchema" xsi:type="xs:string">false</ns2:PropertyValue>
       </ns2:Property>
       <ns2:Property PropertyName="encryptionAlgorithm">
           <ns2:PropertyValue xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance" xmlns:xs="https://www.w3.org/2001/XMLSchema" xsi:type="xs:string">AES128</ns2:PropertyValue>
       </ns2:Property>
       <ns2:Property PropertyName="AccessDeniedErrorMessage">
           <ns2:PropertyValue xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance" xmlns:xs="https://www.w3.org/2001/XMLSchema" xsi:type="xs:string"></ns2:PropertyValue>
       </ns2:Property>
   <ns2:PolicyEntry>
   <ns2:Permission PermissionName="ns3:com.adobe.aps.onlineOpen" Access="ALLOW"/>
   <ns2:Permission PermissionName="ns3:com.adobe.aps.pdf.copy" Access="ALLOW"/>
   <ns2:Permission PermissionName="ns3:com.adobe.aps.offlineOpen" Access="ALLOW"/>
   <ns2:Permission PermissionName="ns3:com.adobe.aps.pdf.accessible" Access="ALLOW"/>
   <ns2:Permission PermissionName="ns3:com.adobe.aps.pdf.editNotes" Access="ALLOW"/>
   <ns2:Permission PermissionName="ns3:com.adobe.aps.pdf.edit" Access="ALLOW"/>
   <ns2:Permission PermissionName="ns3:com.adobe.aps.pdf.fillAndSign" Access="ALLOW"/>
   <ns2:Permission PermissionName="ns3:com.adobe.aps.pdf.printHigh" Access="ALLOW"/>
   <ns2:Permission PermissionName="ns3:com.adobe.aps.pdf.printLow" Access="ALLOW"/>
   ```

   除了直接从表中删除数 `EdcPolicyXmlEntity` 据外，还有两种方法可以实现：

   **使用管理控制台**

   1. 以管理员身份登录FormsJEE管理控制台，网址为&#x200B;[*https://*] server [*:port*]/adminui。
   1. 导航到 **[!UICONTROL 服务>文档安全>策略集]**。
   1. 打开策略集，并从策略中删除用户。

   **使用文档安全网页**

   文档安全用户有权创建个人策略，可以从策略中删除用户数据。 为此，请执行以下操作：

   1. 拥有个人策略的用户登录其文档安全网页&#x200B;[*https://*] server [*:port*]/edc。
   1. 导航到 **[!UICONTROL 服务>文档安全>我的策略]**。
   1. 打开策略并从策略中删除用户。

   >[!NOTE]
   >
   >管理员可以使用管理控制台在“服务”>“文档安全”>“我的策略” **[!UICONTROL 中搜索、访问和删除其他用户的个人]** 策略中的用户数据。

1. 从用户管理数据库中删除主体ID的数据。 有关详细步骤，请参阅 [Forms用户管理 |处理用户数据](/help/forms/using/user-management-handling-user-data.md)。
1. 开始AEM Forms服务器。

