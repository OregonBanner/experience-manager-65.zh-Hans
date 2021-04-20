---
title: Forms门户 |处理用户数据
seo-title: Forms门户 |处理用户数据
description: Forms门户 |处理用户数据
uuid: 2ac2b2a9-b603-489a-86b8-a78b697f130d
contentOwner: vishgupt
topic-tags: grdp
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 48f841b7-0e7f-4216-9ee8-fb6e843acaf0
role: Administrator
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '863'
ht-degree: 0%

---


# Forms门户 |处理用户数据{#forms-portal-handling-user-data}

[!DNL AEM Forms] portal提供了可用于列表页面上的自适应表单、HTML5表单和其他Forms资源的 [!DNL AEM Sites] 组件。此外，您还可以对其进行配置，以显示已登录用户的草稿和提交的自适应表单以及HTML5表单。 有关表单门户的详细信息，请参阅[在门户上发布表单的简介](/help/forms/using/introduction-publishing-forms.md)。

当登录用户将自适应表单保存为草稿或提交它时，它们将显示在表单门户的“草稿和提交”选项卡中。 草稿或已提交表单的数据存储在为AEM部署配置的数据存储中。 匿名用户的草稿和提交内容不显示在表单门户页面上；但是，数据存储在配置的数据存储中。 有关详细信息，请参阅[配置草稿和提交的存储服务](/help/forms/using/configuring-draft-submission-storage.md)。

## 用户数据和数据存储{#user-data-and-data-stores}

Forms门户在以下情况下存储草稿和提交表单的数据：

* 在自适应表单中配置的提交操作为&#x200B;**Forms Portal提交操作**。
* 对于除&#x200B;**Forms Portal提交操作**&#x200B;之外的提交操作，在自适应表单容器的&#x200B;**[!UICONTROL Submission]**&#x200B;属性中启用&#x200B;**[!UICONTROL 在表单门户中存储数据]**&#x200B;选项。

对于登录用户和匿名用户的每个草稿和提交的表单，表单门户会存储以下数据：

* 表单元数据，如表单名称、表单路径、草稿或提交ID、附件路径和用户数据ID
* 表单附件作为数据字节
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
   <td><p>AEM创作和发布实例存储库</p> </td>
   <td><p><code>/content/forms/fp/</code></p> </td>
  </tr>
  <tr>
   <td><p>远程</p> </td>
   <td><p>AEM作者存储库和远程AEM实例</p> </td>
   <td><p><code>/content/forms/fp/</code></p> </td>
  </tr>
  <tr>
   <td><p>数据库</p> </td>
   <td><p>AEM创作实例库和数据库表</p> </td>
   <td>数据库表<code>data</code>、<code>metadata</code>和 <code>additionalmetadata</code></td>
  </tr>
 </tbody>
</table>

## 访问和删除用户数据{#access-and-delete-user-data}

您可以访问已配置数据存储中已登录和匿名用户的草稿和已提交的表单数据，并根据需要删除它。

### AEM实例{#aem-instances}

已登录和匿名用户的AEM实例（作者、发布或远程）中的所有草稿和提交的表单数据都存储在适用AEM存储库的`/content/forms/fp/`节点中。 每次登录或匿名用户保存草稿或提交表单时，都会生成每个附件的`draft ID`或`submission ID`、`user data ID`和随机`ID`（如果适用），这些附件与相应的草稿或提交相关联。

#### 访问用户数据{#access-user-data}

当登录用户保存草稿或提交表单时，将使用其用户ID创建子节点。 例如，用户ID为`srose`的Sarah Rose的草稿和提交数据存储在AEM存储库的`/content/forms/fp/srose/`节点中。 在用户ID节点内，数据以分层结构组织。

下表说明了`srose`的所有草稿的数据如何存储在AEM存储库中。

>[!NOTE]
>
>对于`/content/forms/fp/srose/submit/`节点下的`srose`提交的表单，将复制`drafts`等精确结构。
>
>`anonymous`用户提交的所有草稿和提交都存储在`/content/forms/fp/anonymous/`节点下，该节点为`draft`和`submit`节点下的所有匿名用户组织草稿和提交。

| 节点 | 描述 |
|---|---|
| `/content/forms/fp/srose/drafts` | 容器用户所有草稿的节点数据 |
| `/content/forms/fp/srose/drafts/attachments/` | 根据草稿ID组织用户的所有附件 |
| `/content/forms/fp/srose/drafts/attachments/<ID>` | 包含所选ID的二进制格式附件 |
| `/content/forms/fp/srose/drafts/metadata/` | 根据草稿ID组织用户的表单元数据 |
| `/content/forms/fp/srose/drafts/metadata/<draft ID>` | 包含选定草稿ID的表单元数据 |
| `/content/forms/fp/srose/drafts/data/` | 根据用户数据ID组织用户的表单数据 |
| `/content/forms/fp/srose/drafts/data/<user data ID>` | 包含所选用户数据ID的二进制格式表单数据 |

#### 删除用户数据{#delete-user-data}

要从AEM系统中完整删除已登录用户的草稿和提交的用户数据，必须从作者节点中删除特定用户的`user ID`节点。 您必须从所有适用的AEM实例中手动删除数据。

所有匿名用户的草稿和提交数据存储在`/content/forms/fp/anonymous`下的公用`drafts`和`submit`节点中。 除非某些可识别信息已知，否则无法查找特定匿名用户的数据。 在这种情况下，您可以搜索在AEM存储库中标识匿名用户的信息，并从所有适用的AEM实例中手动删除包含该用户的节点，以从AEM系统中删除数据。 但是，要删除所有匿名用户的数据，您可以删除`anonymous`节点以删除所有匿名用户的草稿和提交数据。

### 数据库 {#database}

将AEM配置为在数据库中存储数据时，登录用户和匿名用户的表单门户草稿和提交数据都存储在以下数据库表中：

* 数据
* 元数据
* 其他元数据

#### 访问用户数据{#access-user-data-1}

要访问数据库表中已登录和匿名用户的草稿和提交数据，请运行以下database命令。 在该查询中，将`logged-in user`替换为要访问其数据的用户ID，或将`anonymous`替换为匿名用户。

```sql
select * from metadata, data, additionalmetadatatable where metadata.owner = 'logged-in user' and metadata.id = additionalmetadatatable.id and metadata.userdataID = data.id
```

#### 删除用户数据{#delete-user-data-1}

要从数据库表中删除已登录用户的草稿和提交数据，请运行以下database命令。 在该查询中，将`logged-in user`替换为您要删除其数据的用户ID，或将`anonymous`替换为匿名用户。 请注意，要从数据库中删除特定匿名用户的数据，您需要使用一些可识别信息找到该数据，并从包含该信息的数据库表中删除该数据。

```sql
DELETE FROM metadata, data, additionalmetadatatable USING metadata INNER JOIN data ON metadata.userdataID = data.id INNER JOIN additionalmetadatatable ON metadata.id = additionalmetadatatable.id WHERE metadata.owner = 'logged-in user'
```

