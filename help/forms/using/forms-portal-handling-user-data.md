---
title: Forms门户 |处理用户数据
seo-title: Forms门户 |处理用户数据
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
source-wordcount: '862'
ht-degree: 0%

---

# Forms门户 |处理用户数据 {#forms-portal-handling-user-data}

[!DNL AEM Forms] Portal提供了一些组件，您可以使用这些组件在页面上列出自适应表单、HTML5表单和其他Forms [!DNL AEM Sites] 资产。此外，您还可以将其配置为为登录用户显示草稿和提交的自适应表单以及HTML5表单。 有关表单门户的更多信息，请参阅[在门户上发布表单简介](/help/forms/using/introduction-publishing-forms.md)。

当登录用户将自适应表单保存为草稿或提交它时，它们会显示在表单门户的“草稿和提交”选项卡中。 草稿或已提交表单的数据将存储在为AEM部署配置的数据存储中。 匿名用户的草稿和提交内容不显示在表单门户页面上；但是，数据存储在配置的数据存储中。 有关更多信息，请参阅[为草稿和提交配置存储服务](/help/forms/using/configuring-draft-submission-storage.md)。

## 用户数据和数据存储 {#user-data-and-data-stores}

Forms门户会在以下情况下存储草稿和提交表单的数据：

* 在自适应表单中配置的提交操作为&#x200B;**Forms Portal Submit Action**。
* 对于除&#x200B;**Forms Portal提交操作**&#x200B;之外的提交操作，在自适应表单容器的&#x200B;**[!UICONTROL 提交]**&#x200B;属性中启用了&#x200B;**[!UICONTROL 在表单门户中存储数据]**&#x200B;选项。

对于登录用户和匿名用户提交的每个草稿表单，Forms Portal会存储以下数据：

* 表单元数据，如表单名称、表单路径、草稿或提交ID、附件路径和用户数据ID
* 作为数据字节的表单附件
* 表单数据作为数据字节

根据配置的数据存储持久性，草稿和提交的表单数据将存储在以下位置。

<table>
 <tbody>
  <tr>
   <td><p><strong>持久性类型</strong></p> </td>
   <td><p><strong>数据存储</strong></p> </td>
   <td><p><strong>位置</strong></p> </td>
  </tr>
  <tr>
   <td><p>默认</p> </td>
   <td><p>AEM创作和发布实例存储库</p> </td>
   <td><p><code>/content/forms/fp/</code></p> </td>
  </tr>
  <tr>
   <td><p>远程</p> </td>
   <td><p>AEM创作存储库和远程AEM实例</p> </td>
   <td><p><code>/content/forms/fp/</code></p> </td>
  </tr>
  <tr>
   <td><p>数据库</p> </td>
   <td><p>AEM创作实例存储库和数据库表</p> </td>
   <td>数据库表<code>data</code>、<code>metadata</code>和 <code>additionalmetadata</code></td>
  </tr>
 </tbody>
</table>

## 访问和删除用户数据 {#access-and-delete-user-data}

您可以在配置的数据存储中访问已登录用户和匿名用户的草稿和已提交的表单数据，并根据需要删除该数据。

### AEM实例 {#aem-instances}

登录用户和匿名用户在AEM实例（创作、发布或远程）中提交的所有草稿和表单数据都存储在适用的AEM存储库的`/content/forms/fp/`节点中。 每次登录用户或匿名用户保存草稿或提交表单时，都会为每个附件（如果适用）生成`draft ID`或`submission ID`、`user data ID`和随机`ID`，并与相应的草稿或提交相关联。

#### 访问用户数据 {#access-user-data}

登录用户保存草稿或提交表单时，将使用其用户ID创建子节点。 例如，用户ID为`srose`的Sarah Rose的草稿和提交数据存储在AEM存储库的`/content/forms/fp/srose/`节点中。 在用户ID节点内，数据以分层结构组织。

下表说明了`srose`所有草稿的数据如何存储在AEM存储库中。

>[!NOTE]
>
>在`/content/forms/fp/srose/submit/`节点下，会为`srose`提交的表单复制诸如`drafts`之类的确切结构。
>
>`anonymous`用户提交的所有草稿和提交都存储在`/content/forms/fp/anonymous/`节点下，该节点将`draft`和`submit`节点下所有匿名用户的草稿和提交都组织起来。

| 节点 | 描述 |
|---|---|
| `/content/forms/fp/srose/drafts` | 用户所有草稿的容器节点数据 |
| `/content/forms/fp/srose/drafts/attachments/` | 根据草稿ID组织用户的所有附件 |
| `/content/forms/fp/srose/drafts/attachments/<ID>` | 以二进制格式包含所选ID的附件 |
| `/content/forms/fp/srose/drafts/metadata/` | 根据草稿ID为用户组织表单元数据 |
| `/content/forms/fp/srose/drafts/metadata/<draft ID>` | 包含所选草稿ID的表单元数据 |
| `/content/forms/fp/srose/drafts/data/` | 根据用户数据ID组织用户的表单数据 |
| `/content/forms/fp/srose/drafts/data/<user data ID>` | 包含二进制格式的选定用户数据ID的表单数据 |

#### 删除用户数据 {#delete-user-data}

要从AEM系统中完全删除已登录用户的草稿和提交中的用户数据，必须从创作节点中删除特定用户的`user ID`节点。 您必须从所有适用的AEM实例中手动删除数据。

所有匿名用户的草稿和提交数据都存储在`/content/forms/fp/anonymous`下的公共`drafts`和`submit`节点中。 除非已知某些可识别信息，否则无法查找特定匿名用户的数据。 在这种情况下，您可以在AEM存储库中搜索标识匿名用户的信息，并从所有适用的AEM实例中手动删除包含该用户的节点，以从AEM系统中删除数据。 但是，要删除所有匿名用户的数据，您可以删除`anonymous`节点，以删除所有匿名用户的草稿和提交数据。

### 数据库 {#database}

将AEM配置为将数据存储在数据库中时，Forms Portal草稿和提交数据会存储在以下数据库表中，供登录用户和匿名用户使用：

* 数据
* 元数据
* 其他元数据

#### 访问用户数据 {#access-user-data-1}

要访问数据库表中登录用户和匿名用户的草稿和提交数据，请运行以下数据库命令。 在查询中，将`logged-in user`替换为要访问其数据的用户ID，或将`anonymous`替换为匿名用户。

```sql
select * from metadata, data, additionalmetadatatable where metadata.owner = 'logged-in user' and metadata.id = additionalmetadatatable.id and metadata.userdataID = data.id
```

#### 删除用户数据 {#delete-user-data-1}

要从数据库表中删除已登录用户的草稿和提交数据，请运行以下数据库命令。 在查询中，将`logged-in user`替换为要删除其数据的用户ID，或将`anonymous`替换为匿名用户。 请注意，要从数据库中删除特定匿名用户的数据，您需要使用一些可识别信息找到该数据，并从包含该信息的数据库表中将其删除。

```sql
DELETE FROM metadata, data, additionalmetadatatable USING metadata INNER JOIN data ON metadata.userdataID = data.id INNER JOIN additionalmetadatatable ON metadata.id = additionalmetadatatable.id WHERE metadata.owner = 'logged-in user'
```
