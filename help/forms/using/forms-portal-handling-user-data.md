---
title: Forms门户 |处理用户数据
seo-title: Forms Portal | Handling user data
description: Forms门户 |处理用户数据
uuid: 2ac2b2a9-b603-489a-86b8-a78b697f130d
contentOwner: vishgupt
topic-tags: grdp
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 48f841b7-0e7f-4216-9ee8-fb6e843acaf0
role: Admin
exl-id: 791524a4-a8bb-4632-a68d-e96864e139a9
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '857'
ht-degree: 0%

---

# Forms门户 |处理用户数据 {#forms-portal-handling-user-data}

[!DNL AEM Forms] portal提供用于列出自适应表单、HTML5表单和其他Forms资源的组件 [!DNL AEM Sites] 页面。 此外，您还可以将其配置为显示草稿以及为登录用户提交的自适应表单和HTML5表单。 有关表单门户的更多信息，请参阅 [在门户上发布表单的简介](/help/forms/using/introduction-publishing-forms.md).

当登录用户将自适应表单另存为草稿或提交时，它们显示在Forms Portal的“草稿”和“提交”选项卡中。 草稿或已提交表单的数据存储在为AEM部署配置的数据存储中。 匿名用户的草稿和提交不会显示在Forms Portal页面上；但是，数据存储到配置的数据存储中。 有关更多信息，请参阅 [为草稿和提交配置存储服务](/help/forms/using/configuring-draft-submission-storage.md).

## 用户数据和数据存储 {#user-data-and-data-stores}

Forms portal在以下场景中存储草稿和已提交表单的数据：

* 在自适应表单中配置的提交操作为 **Forms Portal提交操作**.
* 对于提交操作，而不是 **Forms Portal提交操作**，则 **[!UICONTROL 在表单门户中存储数据]** 选项在中启用 **[!UICONTROL 提交]** 自适应表单容器的属性。

对于登录用户和匿名用户的每个草稿和提交的表单，表单门户都会存储以下数据：

* 表单元数据，例如表单名称、表单路径、草稿或提交ID、附件路径和用户数据ID
* 数据字节形式的表单附件
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
   <td><p>创作实例和远程AEM实例的AEM存储库</p> </td>
   <td><p><code>/content/forms/fp/</code></p> </td>
  </tr>
  <tr>
   <td><p>数据库</p> </td>
   <td><p>创作实例和数据库表的AEM存储库</p> </td>
   <td>数据库表 <code>data</code>， <code>metadata</code>、和 <code>additionalmetadata</code></td>
  </tr>
 </tbody>
</table>

## 访问和删除用户数据 {#access-and-delete-user-data}

您可以在配置的数据存储中访问已登录和匿名用户的草稿和已提交的表单数据，并根据需要将其删除。

### AEM实例 {#aem-instances}

AEM实例（创作、发布或远程）中登录用户和匿名用户的所有草稿和提交的表单数据都存储在 `/content/forms/fp/` AEM存储库的节点。 每次登录的用户或匿名用户保存草稿或提交表单时， `draft ID` 或 `submission ID`， a `user data ID`和随机 `ID` 每个附件（如果适用）生成，与相应的草稿或提交内容相关联。

#### 访问用户数据 {#access-user-data}

当登录用户保存草稿或提交表单时，将使用其用户ID创建一个子节点。 例如，用户ID为 `srose` 存储在 `/content/forms/fp/srose/` AEM节点。 在用户ID节点中，数据按层次结构组织。

下表说明了以下条件的所有草稿的数据 `srose` 存储在AEM存储库中。

>[!NOTE]
>
>完全相同的结构，如 `drafts` 为已提交的表单复制 `srose` 在 `/content/forms/fp/srose/submit/` 节点。
>
>所有草稿和提交方式 `anonymous` 用户存储在 `/content/forms/fp/anonymous/` 节点，用于组织草稿和提交的所有匿名用户。 `draft` 和 `submit` 节点。

| 节点 | 描述 |
|---|---|
| `/content/forms/fp/srose/drafts` | 用户所有草稿的容器节点数据 |
| `/content/forms/fp/srose/drafts/attachments/` | 根据草稿ID组织用户的所有附件 |
| `/content/forms/fp/srose/drafts/attachments/<ID>` | 包含所选ID的附件（以二进制格式） |
| `/content/forms/fp/srose/drafts/metadata/` | 根据草稿ID组织用户的表单元数据 |
| `/content/forms/fp/srose/drafts/metadata/<draft ID>` | 包含选定草稿ID的表单元数据 |
| `/content/forms/fp/srose/drafts/data/` | 根据用户数据ID组织用户的表单数据 |
| `/content/forms/fp/srose/drafts/data/<user data ID>` | 以二进制格式包含选定用户数据ID的表单数据 |

#### 删除用户数据 {#delete-user-data}

要从AEM系统的已登录用户的草稿和提交中完全删除用户数据，您必须删除 `user ID` 节点。 您必须从所有适用的AEM实例中手动删除数据。

所有匿名用户的草稿和提交数据都存储在公共内 `drafts` 和 `submit` 下的节点 `/content/forms/fp/anonymous`. 除非某些可识别的信息是已知的，否则没有方法可查找特定匿名用户的数据。 在这种情况下，您可以搜索在AEM存储库中标识匿名用户的信息，并从所有适用的AEM实例中手动删除包含该信息的节点，以从AEM系统中删除数据。 但是，要删除所有匿名用户的数据，您可以删除 `anonymous` 节点，用于为所有匿名用户删除草稿和提交数据。

### 数据库 {#database}

将AEM配置为将数据存储在数据库中时，Forms Portal草稿和提交数据会存储在以下数据库表中，以供登录用户和匿名用户使用：

* 数据
* 元数据
* 其他元数据

#### 访问用户数据 {#access-user-data-1}

要访问数据库表中已登录和匿名用户的草稿和提交数据，请运行以下数据库命令。 在查询中，替换 `logged-in user` 包含要访问其数据的用户ID，或者使用 `anonymous` 匿名用户。

```sql
select * from metadata, data, additionalmetadatatable where metadata.owner = 'logged-in user' and metadata.id = additionalmetadatatable.id and metadata.userdataID = data.id
```

#### 删除用户数据 {#delete-user-data-1}

要从数据库表中删除登录用户的草稿和提交数据，请运行以下数据库命令。 在查询中，替换 `logged-in user` ，并使用要删除其数据的用户ID或 `anonymous` 匿名用户。 请注意，要从数据库中删除特定匿名用户的数据，您需要使用一些可识别的信息找到该数据，并从包含该信息的数据库表中删除它。

```sql
DELETE FROM metadata, data, additionalmetadatatable USING metadata INNER JOIN data ON metadata.userdataID = data.id INNER JOIN additionalmetadatatable ON metadata.id = additionalmetadatatable.id WHERE metadata.owner = 'logged-in user'
```
