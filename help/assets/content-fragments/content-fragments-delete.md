---
title: 内容片段 – 删除注意事项
description: 在 AEM 中定义内容片段删除策略之前，请查看这些重要注意事项。 内容片段是用于投放 headless 内容的强大工具，必须仔细考虑删除这些片段的影响。
feature: Content Fragments
role: User
exl-id: 6212457e-a171-4c33-8d19-54c26516e981
source-git-commit: de38dbb9d0ce523543c11e665c02034f4b38f1e6
workflow-type: tm+mt
source-wordcount: '509'
ht-degree: 79%

---

# 内容片段 – 删除注意事项 {#content-fragments-delete-considerations}

在 AEM 中定义内容片段删除策略之前，请查看这些重要注意事项。 内容片段是用于投放 headless 内容的强大工具，必须仔细考虑删除这些片段的影响。

## 权限 – 删除或不删除 {#permissions-delete-or-not-delete}

删除内容的功能非常强大，但可能很敏感，许多行业都需要限制和控制这些权限的分配方式。

关于删除权限，内容片段必须考虑在两个级别：

1. **内容片段作为单个实体。**

   * **用例**：需要编辑/更新内容片段的用户 – **并删除整个片段**。
   * **許可權**：此 [刪除](/help/sites-administering/security.md#actions) 許可權可以是 [透過使用者和/或群組管理指派](/help/sites-administering/security.md#managing-permissions).

2. **构成内容片段的多个子实体；例如，变体、子节点。**

   内容片段编辑器的基本操作要求可以删除此类临时子元素。 例如，在处理变量时；在编辑元数据或管理关联的内容时，也可以。

   * **用例**：需要编辑/更新内容片段的用户 – **不允许删除整个片段**。
   * **权限**：请参阅 [仅编辑器功能所需的权限](#permissions-required-for-editor-functionality-only)。

>[!NOTE]
>
>當使用者沒有任何 [刪除](/help/sites-administering/security.md#actions) 許可權，內容片段編輯器便會在下列位置運作： *唯讀* 模式。

>[!NOTE]
>
>另請參閱 [如何在AEM中稽核使用者管理作業](/help/sites-administering/audit-user-management-operations.md).

## 仅编辑器功能所需的权限 {#permissions-required-for-editor-functionality-only}

对于需要编辑／更新内容片段的用户，**不允许他们删除整个片段**，必须分配特定权限，因为内容片段编辑器的基本操作要求可以删除临时子元素。

例如，在处理变量时；在编辑元数据或管理关联的内容时，也可以。

>[!NOTE]
>
>編輯/更新內容片段所需的刪除許可權包含在刪除許可權中 [透過使用者和/或群組管理指派](/help/sites-administering/security.md#managing-permissions).

编辑/更新片段所需的权限需要应用于包含内容片段的节点或适当的父节点（在 `/content/dam` 下的任何级别）。当分配给此类父节点时，权限将应用于该分支中的所有节点。

例如，将包含所有内容片段的文件夹，例如：

* `/content/dam/contentfragments`

>[!CAUTION]
>
>在 `/content/dam` 也是可能的，因为此处存储了所有内容片段。
>
>但是，此操作会将相同的删除权限应用到 *全部* 其他资产类型。

允许特定用户和/或群组编辑/更新内容片段的先决条件是：

>[!NOTE]
>
>此列表显示所需的所有权限，而不只是删除权限。

* 对于内容片段节点或文件夹：

   * `jcr:addChildNodes`、`jcr:modifyProperties`

* 对于 `jcr:content`所有内容片段的节点：

   * `jcr:addChildNodes`、`jcr:modifyProperties` 和 `jcr:removeChildNodes`

* 对于所有内容片段的`jcr:content`以下的所有节点：

   * `jcr:addChildNodes`, `jcr:modifyProperties` 和 `jcr:removeChildNodes`, `jcr:removeNode`

這些 `remove` 許可權必須為 [在CRXDE Lite中使用存取控制清單進行管理](/help/sites-administering/user-group-ac-admin.md#access-right-management).

此 `add` 和 `modify` 許可權也可以在CRXDE Lite中管理，或使用「使用者管理」主控台進行管理。

例如，定義 `remove` 群組的許可權 `content-authors-no-delete`：

![cf-delete-03](assets/cf-delete-03.png)
