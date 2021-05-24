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

# 配置多个就地编辑器{#configure-multiple-in-place-editors}

您可以在Adobe Experience Manager中配置富文本编辑器，以使其具有多个就地编辑器。 配置完毕后，您可以选择相应的内容并打开相应的编辑器。

![特定就地编辑器](assets/rte-inplace-editor.png)

## 配置多个编辑器{#configure-multiple-editors}

为了启用多个就地编辑器，`cq:InplaceEditingConfig`节点类型的结构已通过`cq:ChildEditorConfig`节点类型的定义得到增强。

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

1. 在节点`cq:inplaceEditing`（类型为`cq:InplaceEditingConfig`）上定义以下属性：

   * 名称:`editorType`
   * 类型: `String`
   * 值: `hybrid`

1. 在此节点下，创建一个节点：

   * 名称: `cq:ChildEditors`
   * 类型: `nt:unstructured`

1. 在`cq:childEditors`节点下，为每个就地编辑器创建一个节点：

   * 名称：每个节点的名称是它所表示属性的名称，与放置目标的名称一样。 例如，`image`和`text`。
   * 类型: `cq:ChildEditorConfig`

   >[!NOTE]
   >
   >定义的放置目标与子编辑器之间存在关联。 `cq:ChildEditorConfig`节点的名称会被视为放置目标ID，以用作所选子编辑器的参数。 如果可编辑的子区域没有放置目标（例如，在文本组件中），则子编辑器的名称仍会被视为标识相应可编辑区域的ID。

1. 在每个节点(`cq:ChildEditorConfig`)上定义属性：

   * 名称: `type`.
   * 值：注册的就地编辑器名称；例如，`image`和`text`。

   * 名称: `title`.
   * 值：可用编辑器的组件选择列表中显示的标题。 例如，`Image`和`Text`。

### 富文本编辑器的其他配置{#additional-configuration-for-rich-text-editors}

多个富文本编辑器的配置略有不同，因为您可以单独配置每个RTE实例。 有关详细信息，请参阅[配置富文本编辑器](/help/sites-administering/rich-text-editor.md)。 要让多个RTE为每个就地RTE创建配置，请执行以下操作： Adobe建议在`cq:InplaceEditingConfig`下创建新配置节点，因为每个RTE都可以有不同的配置。 在新节点下，创建每个RTE配置。

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
>但是，对于RTE，当组件中只有一个文本编辑器实例（可编辑的子区域）时，支持`configPath`属性。 提供`configPath`的这种用法是为了支持向后兼容组件较旧的用户界面对话框。

>[!CAUTION]
>
>请勿将RTE配置节点命名为`config`。 否则，RTE配置仅适用于管理员，而不适用于组`content-author`中的用户。

## 代码示例{#code-samples}

您可以在GitHub](https://github.com/Adobe-Marketing-Cloud/aem-authoring-hybrideditors)上的[aem-authoring-hybrideditors项目上找到此页面的代码。 您可以将完整项目下载为[a ZIP存档](https://github.com/Adobe-Marketing-Cloud/aem-authoring-hybrideditors/archive/master.zip)。

## 添加就地编辑器{#add-an-in-place-editor}

有关添加就地编辑器的一般信息，请参阅文档[自定义页面创作](/help/sites-developing/customizing-page-authoring-touch.md#add-new-in-place-editor)。

>[!MORELIKETHIS]
>
>* [在Experience Manager中配置富文本编辑器](/help/sites-administering/rich-text-editor.md)。

