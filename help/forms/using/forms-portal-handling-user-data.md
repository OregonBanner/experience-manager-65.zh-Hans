---
title: Forms Portal|处理用户数据
seo-title: Forms Portal|处理用户数据
description: 'null'
seo-description: 'null'
uuid: 2ac2b2a9-b603-489a-86b8-a78b697f130d
contentOwner: vishgupt
topic-tags: grdp
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 48f841b7-0e7f-4216-9ee8-fb6e843acaf0
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Forms Portal|处理用户数据 {#forms-portal-handling-user-data}

AEM Forms Portal提供了可用于在AEM Sites页面上列出自适应表单、HTML5表单和其他表单资产的组件。 此外，您还可以将其配置为显示已登录用户的草稿和已提交的自适应表单以及HTML5表单。 有关表单门户的详细信息，请参 [阅在门户上发布表单的介绍](/help/forms/using/introduction-publishing-forms.md)。

当登录用户将自适应表单保存为草稿或提交它时，这些表单会显示在表单门户的“草稿和提交”选项卡中。 草稿或已提交表单的数据存储在为AEM部署配置的数据存储中。 匿名用户的草稿和提交内容不显示在表单门户页面上；但是，数据存储在配置的数据存储中。 有关详细信息，请参 [阅为草稿和提交配置存储服务](/help/forms/using/configuring-draft-submission-storage.md)。

## 用户数据和数据存储 {#user-data-and-data-stores}

在以下情况下，表单门户会存储草稿和提交表单的数据：

* 在自适应表单中配置的提交操作是 **Forms Portal提交操作**。
* 对于除表单门户提交 **操作之外的提交操作********** ，在自适应表单容器的“提交”属性中启用“在表单门户中存储数据”选项。

对于每个针对登录用户和匿名用户的草稿和提交的表单，表单门户会存储以下数据：

* 表单元数据，如表单名称、表单路径、草稿或提交ID、附件路径和用户数据ID
* 作为数据字节的表单附件
* 表单数据作为数据字节

根据配置的数据存储持久性，草稿和提交的表单数据存储在以下位置。

<table>
 <tbody>
  <tr>
   <td><p><strong>持久性类型</strong></p> </td>
   <td><p><strong>数据存储</strong></p> </td>
   <td><p><strong>位置</strong></p> </td>
  </tr>
  <tr>
   <td><p>默认</p> </td>
   <td><p>创作和发布实例的AEM存储库</p> </td>
   <td><p><code>/content/forms/fp/</code></p> </td>
  </tr>
  <tr>
   <td><p>远程</p> </td>
   <td><p>作者和远程AEM实例的AEM存储库</p> </td>
   <td><p><code>/content/forms/fp/</code></p> </td>
  </tr>
  <tr>
   <td><p>数据库</p> </td>
   <td><p>作者实例和数据库表的AEM存储库</p> </td>
   <td>数据库 <code>data</code>表 <code>metadata</code>、和 <code>additionalmetadata</code></td>
  </tr>
 </tbody>
</table>

## 访问和删除用户数据 {#access-and-delete-user-data}

您可以访问已配置数据存储中已登录和匿名用户的草稿和已提交的表单数据，并根据需要删除它。

### AEM实例 {#aem-instances}

在AEM实例（作者、发布或远程）中，登录用户和匿名用户的所有草稿和提交的表单数据都存储在适用的AEM `/content/forms/fp/` 存储库的节点中。 每次登录用户或匿名用户保存草稿或提交表单时，都会为每个附件（如果适用）生成一个或 `draft ID` 、一个随机表 `submission ID``user data ID``ID` 单，该表单与相应的草稿或提交相关联。

#### 访问用户数据 {#access-user-data}

当登录用户保存草稿或提交表单时，将使用其用户ID创建子节点。 例如，其用户ID存储在AEM存储库的节点中的Sarah rose的草 `srose` 稿和提交 `/content/forms/fp/srose/` 数据。 在用户ID节点内，数据以分层结构组织。

下表说明了AEM存储库中如何存储所有草 `srose` 稿的数据。

>[!NOTE]
>
>为节点下的已提 `drafts` 交表单复制了类似 `srose` 的精确 `/content/forms/fp/srose/submit/` 结构。
>
>用户提交的所有草稿 `anonymous` 和提交都存储在节点下， `/content/forms/fp/anonymous/` 该节点为该节点下的所有匿名用户组织草稿和提 `draft` 交 `submit` 内容。

| 节点 | 描述 |
|---|---|
| `/content/forms/fp/srose/drafts` | 用户所有草稿的容器节点数据 |
| `/content/forms/fp/srose/drafts/attachments/` | 根据草稿ID组织用户的所有附件 |
| `/content/forms/fp/srose/drafts/attachments/<ID>` | 包含所选ID的二进制格式的附件 |
| `/content/forms/fp/srose/drafts/metadata/` | 根据草稿ID组织用户的表单元数据 |
| `/content/forms/fp/srose/drafts/metadata/<draft ID>` | 包含选定草稿ID的表单元数据 |
| `/content/forms/fp/srose/drafts/data/` | 根据用户数据ID组织用户的表单数据 |
| `/content/forms/fp/srose/drafts/data/<user data ID>` | 包含所选用户数据ID的二进制格式表单数据 |

#### 删除用户数据 {#delete-user-data}

要从AEM系统中完全删除已登录用户的草稿和提交中的用户数据，必须从创作节点中删除特 `user ID` 定用户的节点。 您必须从所有适用的AEM实例中手动删除数据。

所有匿名用户的草稿和提交数据都存储在下面的公 `drafts` 用节 `submit` 点中 `/content/forms/fp/anonymous`。 除非某些可识别信息已知，否则无法查找特定匿名用户的数据。在此例中，您可以搜索在AEM存储库中标识匿名用户的信息，并从所有适用的AEM实例中手动删除包含该匿名用户的节点，以从AEM系统中删除数据。 但是，要删除所有匿名用户的数据，您可以删除该节 `anonymous` 点以删除所有匿名用户的草稿和提交数据。

### 数据库 {#database}

将AEM配置为在数据库中存储数据时，表单门户草稿和提交数据将存储在登录用户和匿名用户的以下数据库表中：

* 数据
* 元数据
* 附加元数据

#### 访问用户数据 {#access-user-data-1}

要访问数据库表中已登录和匿名用户的草稿和提交数据，请运行以下数据库命令。 在查询中，替 `logged-in user` 换为要访问其数据的用户ID或匿名用户 `anonymous` 的用户ID。

```sql
select * from metadata, data, additionalmetadatatable where metadata.owner = 'logged-in user' and metadata.id = additionalmetadatatable.id and metadata.userdataID = data.id
```

#### 删除用户数据 {#delete-user-data-1}

要从数据库表中删除已登录用户的草稿和提交数据，请运行以下数据库命令。 在查询中，替 `logged-in user` 换为要删除其数据的用户ID或匿名用户 `anonymous` 的用户ID。 请注意，要从数据库中删除特定匿名用户的数据，您需要使用一些可识别信息找到该数据，并从包含该信息的数据库表中删除该数据。

```sql
DELETE FROM metadata, data, additionalmetadatatable USING metadata INNER JOIN data ON metadata.userdataID = data.id INNER JOIN additionalmetadatatable ON metadata.id = additionalmetadatatable.id WHERE metadata.owner = 'logged-in user'
```

