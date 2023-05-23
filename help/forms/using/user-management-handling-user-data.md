---
title: Forms使用者管理 |處理使用者資料
seo-title: Forms user management | Handling user data
description: Forms使用者管理 |處理使用者資料
uuid: 2b76b69f-6f3a-4f1a-a2a4-d39f5e529f75
topic-tags: grdp
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: a88fc933-f1af-4798-b72f-10e7b0d2fd11
role: Admin
exl-id: eeeab5d1-073a-4e13-a781-391dfe70bb37
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '884'
ht-degree: 0%

---

# Forms使用者管理 |處理使用者資料 {#forms-user-management-handling-user-data}

使用者管理是AEM Forms JEE元件，可建立、管理和授權AEM Forms使用者存取AEM Forms。 使用者管理使用網域作為取得使用者資訊的目錄。 支援的網域型別如下：

**本機網域**：此型別的網域未連線至協力廠商儲存系統。 而是由本機建立使用者與群組，並存放於「使用者管理」資料庫中。 密碼會儲存在本機，而驗證會使用本機資料庫完成。

**混合網域**：此型別的網域未連線至協力廠商儲存系統。 而是由本機建立使用者與群組，並存放於「使用者管理」資料庫中。 與本機網域不同，混合網域使用外部驗證提供者，可以是LDAP、Kerberos、SAML或自訂驗證提供者。

**企業網域**：由位於協力廠商儲存系統（例如LDAP目錄）中的使用者和群組所組成。 「使用者管理」不會寫入協力廠商儲存系統。 相反地，「使用者管理」會將使用者和群組資訊與「使用者管理」資料庫同步。 企業網域也使用外部驗證提供者，可以是LDAP、Kerberos、SAML或自訂驗證提供者。

<!-- Fix broken links For more information about how user management works and configured, see AEM Forms JEE administration help. -->

## 使用者資料和資料存放區 {#user-data-and-data-stores}

使用者管理會將使用者資料儲存在資料庫中，例如My Sql、Oracle、MS SQL Server和IBM DB2。 此外，任何至少在AEM作者的Forms應用程式中登入一次的使用者 `https://'[server]:[port]'lc`，即會在AEM存放庫中建立使用者。 因此，使用者管理會儲存在下列資料存放區中：

* 数据库
* AEM存放庫
* LDAP目錄之類的協力廠商儲存裝置

>[!NOTE]
>
>儲存在協力廠商儲存區中的資料不屬於本檔案的範圍。 請直接聯絡協力廠商以管理這類儲存庫中的使用者資料。

### 数据库 {#database}

使用者管理會將使用者資料儲存在下列資料庫表格中：

<table>
 <tbody>
  <tr>
   <td>資料庫表格</td>
   <td>描述</td>
  </tr>
  <tr>
   <td><code>EdcPrincipalEntity</code></td>
   <td><p>儲存有關主要實體的資訊。 主體可以是使用者、群組或角色。</p> <p> </p> </td>
  </tr>
  <tr>
   <td><code>EdcPrincipalUserEntity</code></td>
   <td>儲存使用者的個人識別資訊(PII)。 它包含本機、企業和混合網域中每個使用者的專案。</td>
  </tr>
  <tr>
   <td><p><code>EdcPrincipalLocalAccountEntity</code></p> <p><code class="code">EdcPrincipalLocalAccount
       </code>(Oracle和MS SQL資料庫)</p> </td>
   <td>僅儲存本機使用者的資料。</td>
  </tr>
  <tr>
   <td><p><code>EdcPrincipalEmailAliasEntity</code></p> <p><code class="code">EdcPrincipalEmailAliasEn
       </code>(Oracle和MS SQL資料庫)</p> </td>
   <td>包含本機、企業及混合網域中所有使用者的專案。 它包含使用者電子郵件ID。</td>
  </tr>
  <tr>
   <td><p><code>EdcPrincipalGrpCtmntEntity</code></p> <p><code>EdcPrincipalGrpCtmntEnti</code> (Oracle和MS SQL資料庫)</p> </td>
   <td>儲存使用者和群組之間的對應。</td>
  </tr>
  <tr>
   <td><code>EdcPrincipalRoleEntity</code></td>
   <td>儲存使用者和群組的角色和主體之間的對應。</td>
  </tr>
  <tr>
   <td><code>EdcPriResPrmEntity</code></td>
   <td>儲存使用者和群組的主體與許可權之間的對應。</td>
  </tr>
  <tr>
   <td><p><code>EdcPrincipalMappingEntity</code></p> <p><code>EdcPrincipalMappingEntit</code> (Oracle和MS SQL資料庫)</p> </td>
   <td>儲存與主體對應的舊屬性和新屬性值。<br /> </td>
  </tr>
 </tbody>
</table>

### AEM存放庫 {#aem-repository}

至少存取過下方Forms應用程式一次的使用者的使用者管理資料 `https://'[server]:[port]'lc` 也會儲存在AEM存放庫中。

## 存取和刪除使用者資料 {#access-and-delete-user-data}

您可以存取和匯出使用者管理資料庫和AEM儲存庫中使用者的使用者管理資料，並視需要永久刪除資料。

### 数据库 {#database-1}

若要從使用者管理資料庫匯出或刪除使用者資料，您必須使用資料庫使用者端連線資料庫，並根據使用者的某些PII找出主參與者ID。 例如，若要使用登入ID擷取使用者的主體ID，請執行下列動作 `select` 資料庫上的命令。

在 `select` 命令，取代 `<user_login_id>` 其主體ID您要擷取之使用者的登入ID。

```sql
select refprincipalid from EdcPrincipalUserEntity where uidstring = <user_login_id>
```

一旦您知道主體ID，就可以匯出或刪除使用者資料。

#### 匯出使用者資料 {#export-user-data}

執行以下資料庫命令，從資料庫表格匯出主體ID的使用者管理資料。 在 `select` 命令，取代 `<principal_id>` ，其中包含您要匯出其資料之使用者的主體ID。

>[!NOTE]
>
>下列命令使用My SQL和IBM DB2資料庫中的資料庫表格名稱。 在Oracle和MS SQL資料庫上執行這些命令時，請取代命令中的下清單格名稱：
>
>* Replace `EdcPrincipalLocalAccountEntity` 替換為 `EdcPrincipalLocalAccount`
>
>* Replace `EdcPrincipalEmailAliasEntity` 替換為 `EdcPrincipalEmailAliasEn`
>
>* Replace `EdcPrincipalMappingEntity` 替換為 `EdcPrincipalMappingEntit`
>
>* Replace `EdcPrincipalGrpCtmntEntity` 替換為 `EdcPrincipalGrpCtmntEnti`
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

#### 刪除使用者資料 {#delete-user-data}

執行下列動作，從資料庫表格中刪除主體ID的使用者管理資料。

1. 從AEM存放庫刪除使用者資料（如適用），如所述 [刪除使用者資料](/help/forms/using/user-management-handling-user-data.md#delete-aem).
1. 關閉AEM Forms伺服器。
1. 執行以下資料庫命令，從資料庫表格中刪除主體ID的使用者管理資料。 在 `Delete` 命令，取代 `<principal_id>` 包含您要刪除其資料之使用者的主體ID。

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

1. 啟動AEM Forms伺服器。

### AEM存放庫 {#aem-repository-1}

如果使用者已存取Forms編寫執行個體至少一個，則AEM Forms JEE使用者會有其資料在AEM存放庫中。 您可以存取和刪除AEM存放庫中的使用者資料。

#### 存取使用者資料 {#access-user-data}

若要檢視在AEM儲存庫中建立的使用者，請登入 `https://'[server]:[port]'/lc/useradmin` 具有AEM管理員認證。 請注意 `server` 和 `port` 在URL中是AEM編寫執行個體的URL。 在這裡，您可以使用使用者的使用者名稱來搜尋使用者。 連按兩下使用者以檢視使用者的屬性、許可權和群組等資訊。 此 `Path` 使用者的屬性會指定在AEM存放庫中建立之使用者節點的路徑。

#### 刪除使用者資料 {#delete-aem}

若要刪除使用者：

1. 前往 `https://'[server]:[port]'/lc/useradmin` 具有AEM管理員認證。
1. 搜尋使用者並連按兩下使用者名稱以開啟使用者屬性。 複製 `Path` 屬性。
1. 前往AEM CRX DELite，網址為 `https://'[server]:[port]'/lc/crx/de/index.jsp` 和導覽或搜尋使用者路徑。
1. 刪除路徑並按一下 **[!UICONTROL 全部儲存]** 以從AEM存放庫中永久刪除使用者。
