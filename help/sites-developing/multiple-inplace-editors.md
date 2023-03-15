---
title: 为多个就地编辑器配置RTE。
description: 通过配置富文本编辑器，在Adobe Experience Manager中创建多个就地编辑器。
contentOwner: AG
exl-id: 03030317-8b7d-408a-bdfd-619824d7260c
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '445'
ht-degree: 2%

---

# 配置多个就地编辑器 {#configure-multiple-in-place-editors}

您可以在Adobe Experience Manager中配置富文本编辑器，以便具有多个就地编辑器。 配置后，您可以选择相应的内容并打开相应的编辑器。

![特定的就地编辑器](assets/rte-inplace-editor.png)

## 配置多个编辑器 {#configure-multiple-editors}

启用多个就地编辑器的结构 `cq:InplaceEditingConfig` 节点类型已通过的定义得到增强 `cq:ChildEditorConfig` 节点类型。

例如：

```js
   /**
       * Configures in-place editing of a component.
       *
       * @prop active true to activate in-place editing for the component.
       * @prop editorType ID of in-place editor to use.
       * @prop cq:childEditors collection of {@link cq:ChildEditorConfig} nodes.
       * @prop configPath path to editor's config (optional).
       * @node config editor's config (used if no configPath is specified; optional).
     */
    [cq:InplaceEditingConfig] > nt:unstructured
      - active (boolean)
      - editorType (string)
      + cq:childEditors (nt:base) = nt:unstructured
      - configPath (string)
      + config (nt:unstructured) = nt:unstructured

    /**
      * Configures one child editor for a sub-component. The name of the this node is
      * used as DD ID.
      *
      * @prop type type of the inline editor. For example, ["image"].
      * @prop title Title of the inline editor.
      * @prop icon Icon to represent the inline editor.
    */
    [cq:ChildEditorConfig] > nt:unstructured
      orderable
      - type (string)
      - title (string)
```

要配置多个编辑器，请执行以下步骤：

1. 在节点上 `cq:inplaceEditing` (类型 `cq:InplaceEditingConfig`)定义以下属性：

   * 名称:`editorType`
   * 类型: `String`
   * 值: `hybrid`

1. 在此节点下，创建一个节点：

   * 名称: `cq:ChildEditors`
   * 类型: `nt:unstructured`

1. 下 `cq:childEditors` 节点，为每个就地编辑器创建一个节点：

   * 名称：每个节点的名称是它所代表的属性的名称，删除目标的情况也是如此。 例如， `image` 和 `text`.
   * 类型: `cq:ChildEditorConfig`

   >[!NOTE]
   >
   >定义的放置目标和子编辑器之间存在相关性。 的名称 `cq:ChildEditorConfig` 节点被视为放置目标ID，用作所选子编辑器的参数。 如果可编辑子区域没有放置目标（例如，在文本组件中），则子编辑器的名称仍将被视为标识相应可编辑区域的ID。

1. 在每个节点上(`cq:ChildEditorConfig`)定义属性：

   * 名称: `type`.
   * 值：已注册的就地编辑器的名称；例如， `image` 和 `text`.

   * 名称: `title`.
   * 值：在可用编辑器的组件选择列表中显示的标题。 例如， `Image` 和 `Text`.

### 富文本编辑器的其他配置 {#additional-configuration-for-rich-text-editors}

多个富文本编辑器的配置略有不同，因为您可以单独配置每个RTE实例。 有关详细信息，请参阅 [配置富文本编辑器](/help/sites-administering/rich-text-editor.md). 要拥有多个RTE，请为每个就地RTE创建一个配置。 Adobe建议在下创建新配置节点 `cq:InplaceEditingConfig` 因为每个RTE可以有不同的配置。 在新节点下，创建每个RTE配置。

```xml
    texttext
        cq:dialog
        cq:editConfig
            cq:inplaceEditing
                cq:childEditors
                    someconfig
                        text1
                            rtePlugins
                        text2
                            rtePlugins
```

>[!NOTE]
>
>但是，对于RTE ，使用 `configPath` 当组件中只有一个文本编辑器实例（可编辑的子区域）时，支持属性。 此用法 `configPath` 支持与组件的旧版用户界面对话框向后兼容。

>[!CAUTION]
>
>不要将RTE配置节点命名为 `config`. 否则，RTE配置仅对管理员可用，对组中的用户不可用 `content-author`.

## 代码示例 {#code-samples}

您可以在此页面中找到代码 [GitHub上的aem-authoring-hybrideditors项目](https://github.com/Adobe-Marketing-Cloud/aem-authoring-hybrideditors). 您可以将完整项目下载为 [ZIP存档](https://github.com/Adobe-Marketing-Cloud/aem-authoring-hybrideditors/archive/master.zip).

## 添加就地编辑器 {#add-an-in-place-editor}

有关添加就地编辑器的常规信息，请参阅文档 [自定义页面创作](/help/sites-developing/customizing-page-authoring-touch.md#add-new-in-place-editor).

>[!MORELIKETHIS]
>
>* [在Experience Manager中配置富文本编辑器](/help/sites-administering/rich-text-editor.md).

