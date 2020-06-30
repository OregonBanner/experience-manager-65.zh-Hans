---
title: 为多个就地编辑器配置RTE。
description: 通过配置富文本编辑器，在Adobe Experience Manager中创建多个就地编辑器。
contentOwner: AG
translation-type: tm+mt
source-git-commit: e49411a99a80e91c983afc103a8ea826e75569b8
workflow-type: tm+mt
source-wordcount: '445'
ht-degree: 2%

---


# 配置多个就地编辑器 {#configure-multiple-in-place-editors}

您可以在Adobe Experience Manager中配置富文本编辑器，使其具有多个就地编辑器。 配置后，您可以选择适当的内容并打开相应的编辑器。

![特定就地编辑器](assets/rte-inplace-editor.png)

## 配置多个编辑器 {#configure-multiple-editors}

要启用多个就地编辑器，已使用节 `cq:InplaceEditingConfig` 点类型的定义增强了节点类 `cq:ChildEditorConfig` 型的结构。

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

1. 在节点( `cq:inplaceEditing` 类型)上 `cq:InplaceEditingConfig`定义以下属性：

   * 名称:`editorType`
   * 类型: `String`
   * 值: `hybrid`

1. 在此节点下，创建一个节点：

   * 名称: `cq:ChildEditors`
   * 类型: `nt:unstructured`

1. 在节 `cq:childEditors` 点下，为每个就地编辑器创建一个节点：

   * 名称： 每个节点的名称是它所表示属性的名称，与放置目标一样。 例如， `image` 和 `text`。
   * 类型: `cq:ChildEditorConfig`

   >[!NOTE]
   >
   >定义的删除目标与子编辑器之间存在关联。 节点的名 `cq:ChildEditorConfig` 称被视为放置目标ID，用作选定子编辑器的参数。 如果可编辑的子区域没有放置目标（例如，在文本组件中），则子编辑器的名称仍被视为标识相应可编辑区域的ID。

1. 在这些节点()`cq:ChildEditorConfig`中定义属性：

   * 名称: `type`.
   * 值： 注册就地编辑的名称； 例如， `image` 和 `text`。

   * 名称: `title`.
   * 值： 在可用编辑器的组件选择列表中显示的标题。 例如， `Image` 和 `Text`。

### 富文本编辑器的其他配置 {#additional-configuration-for-rich-text-editors}

多个富文本编辑器的配置略有不同，因为您可以单独配置每个RTE实例。 有关详细信息， [请参阅配置富文本编辑器](/help/sites-administering/rich-text-editor.md)。 要使多个RTE为每个就地RTE创建配置。 Adobe建议在下创建新的配置节 `cq:InplaceEditingConfig` 点，因为每个RTE都可以有不同的配置。 在新节点下，创建每个单独的RTE配置。

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
>但是，对于RTE，当 `configPath` 组件中只有一个文本编辑器实例（可编辑的子区域）时，支持该属性。 提供此用 `configPath` 法是为了支持与组件的较旧用户界面对话框向后兼容。

>[!CAUTION]
>
>请勿将RTE配置节点命名为 `config`。 否则，RTE配置只适用于管理员，而不适用于组中的用户 `content-author`。

## Code samples {#code-samples}

您可以在GitHub上的aem-authoring- [hybridetors项目中找到此页面的代码](https://github.com/Adobe-Marketing-Cloud/aem-authoring-hybrideditors)。 您可以将整个项目作为ZIP [存档下载](https://github.com/Adobe-Marketing-Cloud/aem-authoring-hybrideditors/archive/master.zip)。

## 添加就地编辑器 {#add-an-in-place-editor}

有关添加就地编辑器的一般信息，请参阅文档自 [定义页面创作](/help/sites-developing/customizing-page-authoring-touch.md#add-new-in-place-editor)。

>[!MORELIKETHIS]
>
>* [以Experience Manager配置富文本编辑器](/help/sites-administering/rich-text-editor.md)。

