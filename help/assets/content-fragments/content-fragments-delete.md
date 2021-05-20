---
title: 内容片段 - 删除注意事项
seo-title: 内容片段 - 删除注意事项
description: 内容片段 - 删除注意事项
seo-description: 内容片段 - 删除注意事项
uuid: e7ac1809-159f-4d02-ad30-dc6c246e8a04
contentOwner: aheimoz
topic-tags: content-fragments
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
content-type: reference
discoiquuid: ec21237f-9186-49b4-8039-99df4db7c14a
docset: aem65
feature: 内容片段
role: Business Practitioner, Administrator
exl-id: cc212f95-0be0-4705-8dfd-beda9bfb13e0
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '457'
ht-degree: 13%

---

# 内容片段 - 删除注意事项{#content-fragments-delete-considerations}

## 权限 — 删除或不删除{#permissions-delete-or-not-delete}

删除内容的功能非常强大，但可能很敏感，许多行业都需要限制和控制这些权限的分配方式。

关于删除权限，内容片段必须考虑在两个级别：

1. **内容片段作为单个实体。**

   * **用例**:需要编辑/更新内容片段 — 和删除 **整个片段的用户**。
   * **权限**:可以 [](/help/sites-administering/security.md#actions) 通过用户 [和/或群组管理来分配“删除”权限](/help/sites-administering/security.md#managing-permissions)。

1. **构成内容片段的多个子实体；例如，变体、子节点。**

   内容片段编辑器的基本操作要求可以删除此类临时子元素。 例如，在处理变量时；在编辑元数据或管理关联的内容时，也可以。

   * **用例**:需要编辑/更新内容片段的用户 —  **不允许删除整个片段**。
   * **权限**:请参 [阅仅编辑器功能所需的权限](/help/assets/content-fragments/content-fragments-delete.md#permissions-required-for-editor-functionality-only)。

>[!NOTE]
>
>当用户没有任何[Delete](/help/sites-administering/security.md#actions)权限时，内容片段编辑器将以&#x200B;*只读*&#x200B;模式运行。

>[!NOTE]
>
>另请参阅[如何在AEM](/help/sites-administering/audit-user-management-operations.md)中审核用户管理操作。

## 仅{#permissions-required-for-editor-functionality-only}编辑器功能所需的权限

对于需要编辑／更新内容片段的用户， **不允许他们删除整个片段**，必须分配特定权限，因为内容片段编辑器的基本操作要求可以删除临时子元素。

例如，在处理变量时；在编辑元数据或管理关联的内容时，也可以。

>[!NOTE]
>
>编辑/更新内容片段所需的删除权限包含在通过“用户”和/或“组管理”分配的“删除”权限[中。](/help/sites-administering/security.md#managing-permissions)

编辑/更新片段所需的权限需要应用于包含内容片段的节点或相应的父节点（在`/content/dam`下的任何级别）。 当分配给此类父节点时，权限将应用于该分支中的所有节点。

例如，将包含所有内容片段的文件夹，例如：

* `/content/dam/contentfragments`

>[!CAUTION]
>
>也可以对`/content/dam`设置权限，因为此处存储了所有内容片段。
>
>但是，此操作也会将相同的删除权限应用于&#x200B;*所有*&#x200B;其他资产类型。

允许特定用户和/或群组编辑/更新内容片段的先决条件是：

>[!NOTE]
>
>此列表显示所需的所有权限，而不只是删除权限。

* 对于内容片段节点或文件夹：

   * `jcr:addChildNodes`, `jcr:modifyProperties`

* 对于所有内容片段的`jcr:content`节点：

   * `jcr:addChildNodes`、 `jcr:modifyProperties` 和  `jcr:removeChildNodes`

* 对于所有内容片段的`jcr:content`以下的所有节点：

   * `jcr:addChildNodes`、 `jcr:modifyProperties` 和 `jcr:removeChildNodes`、  `jcr:removeNode`

这些`remove`权限必须使用CRXDE Lite](/help/sites-administering/user-group-ac-admin.md#access-right-management)中的访问控制列表进行[管理。

`add`和`modify`权限也可以在CRXDE Lite中管理，或使用用户管理控制台管理。

例如，对组`content-authors-no-delete`的`remove`权限的定义：

![cf-delete-03](assets/cf-delete-03.png)
