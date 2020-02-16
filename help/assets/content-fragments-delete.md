---
title: 内容片段——删除注意事项
seo-title: 内容片段——删除注意事项
description: 内容片段——删除注意事项
seo-description: 内容片段——删除注意事项
uuid: e7ac1809-159f-4d02-ad30-dc6c246e8a04
contentOwner: aheimoz
topic-tags: content-fragments
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
content-type: reference
discoiquuid: ec21237f-9186-49b4-8039-99df4db7c14a
docset: aem65
translation-type: tm+mt
source-git-commit: 6edecebec6d64a30fd05887a56d81f80863c5213

---


# 内容片段——删除注意事项{#content-fragments-delete-considerations}

## 权限——删除或不删除 {#permissions-delete-or-not-delete}

删除内容的功能强大，但可能非常敏感，许多行业需要限制和控制这些权限的分配方式。

关于删除权限，内容片段必须考虑在两个级别：

1. **内容片段作为单个实体。**

   * **用例**:需要编辑／更新内容片段——并删除整 **个片段的用户**。
   * **权限**:可以 [通过“用户](/help/sites-administering/security.md#actions) ”和／或“组 [管理”来分配“删除”权限](/help/sites-administering/security.md#managing-permissions)。

1. **构成内容片段的多个子实体；例如，变量，子节点。**

   内容片段编辑器的基本操作要求可以删除这种临时子元素。 例如，在操作变量时；编辑元数据或管理关联内容时。

   * **用例**:需要编辑／更新内容片段的用户- **不允许删除整个片段**。
   * **权限**:请参阅 [仅编辑器功能所需的权限](/help/assets/content-fragments-delete.md#permissions-required-for-editor-functionality-only)。

>[!NOTE]
>
>当用户没有任何删除权 [限](/help/sites-administering/security.md#actions) ，内容片段编辑器将以只 *读模式运行* 。

>[!NOTE]
>
>另请参阅 [如何在AEM中审核用户管理操作](/help/sites-administering/audit-user-management-operations.md)。

## 仅编辑器功能所需的权限 {#permissions-required-for-editor-functionality-only}

对于需要编辑／更新内容片段的用户， **不允许他们删除整个片段**，必须分配特定权限，因为内容片段编辑器的基本操作要求可以删除临时子元素。

例如，在操作变量时；编辑元数据或管理关联内容时。

>[!NOTE]
>
>编辑／更新内容片段所需的删除权限包含在通过用户和／或组管理 [分配的“删除”权限中](/help/sites-administering/security.md#managing-permissions)。

编辑／更新片段所需的权限需要应用于包含内容片段的节点或相应的父节点(在下的任何级别 `/content/dam`)。 当分配给此类父节点时，权限将应用于该分支中的所有节点。

例如，将包含所有内容片段的文件夹，如：

* `/content/dam/contentfragments`

>[!CAUTION]
>
>也可以对设置权 `/content/dam` 限，因为所有内容片段都存储在此处。
>
>但是，此操作也会将相同的删除权 *限应用* 到所有其他资产类型。

允许特定用户和／或用户组编辑／更新内容片段的前提条件是：

>[!NOTE]
>
>此列表显示所需的所有权限，而不仅仅是删除权限。

* 对于“内容片段”节点或文件夹：

   * `jcr:addChildNodes`, `jcr:modifyProperties`

* 对于所有 `jcr:content`内容片段的节点：

   * `jcr:addChildNodes`, `jcr:modifyProperties` and `jcr:removeChildNodes`

* 对于所有内容片段 `jcr:content` 下的所有节点：

   * `jcr:addChildNodes`, `jcr:modifyProperties` 和 `jcr:removeChildNodes`, `jcr:removeNode`

必须 `remove` 使用CRXDE lite中 [的访问控制列表来管理这些权限](/help/sites-administering/user-group-ac-admin.md#access-right-management)。

也 `add` 可以 `modify` 在CRXDE Lite中或使用用户管理控制台管理权限。

例如，组权限 `remove` 的定义 `content-authors-no-delete`:

![cf-delete-03](assets/cf-delete-03.png)

