---
title: 配置多个就地编辑器
seo-title: 配置多个就地编辑器
description: 可以配置组件，使其具有多个就地编辑器
seo-description: 可以配置组件，使其具有多个就地编辑器
uuid: 4abbfcd5-fe1b-4c02-b115-97db20e60e1e
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: components
content-type: reference
discoiquuid: 0fac1e4a-f08f-4c46-b070-cb1d5a05b6e0
translation-type: tm+mt
source-git-commit: b3e1493811176271ead54bae55b1cd0cf759fe71

---


# 配置多个就地编辑器{#configuring-multiple-in-place-editors}

您可以配置组件，使其在触屏优化UI中具有多个就地编辑器。

配置后，您可以选择适当的内容并打开相应的编辑器。 例如：

![chlimage_1-8](assets/chlimage_1-8a.png)

## 配置多个编辑器 {#configuring-multiple-editors}

为了启用多个就地编辑器，节点类型的 `cq:InplaceEditingConfig` 结构已通过节点类型的定义得到 `cq:ChildEditorConfig` 了增强。

例如：

```
   /**
       * Configures inplace editing of a component.
       *
       * @prop active true to activate inplace editing for the component
       * @prop editorType ID of inplace editor to use
       * @prop cq:childEditors collection of {@link cq:ChildEditorConfig} nodes.
       * @prop configPath path to editor's config (optional)
       * @node config editor's config (used if no configPath is specified; optional)
     */
    [cq:InplaceEditingConfig] > nt:unstructured
      - active (boolean)
      - editorType (string)
      + cq:childEditors (nt:base) = nt:unstructured
      - configPath (string)
      + config (nt:unstructured) = nt:unstructured

    /**
      * Configures one child editor for a subcomponent. The name of the this node will
      * be used as DD id.
      *
      * @prop type type of the inline editor. eg: ["image"]
      * @prop title totle od the inline editor
      * @prop icon icon to represent the inline editor
    */
    [cq:ChildEditorConfig] > nt:unstructured
      orderable
      - type (string)
      - title (string)
```

要配置多个编辑器，请执行以下操作：

1. 在节点( `cq:inplaceEditing` 类型)上 `cq:InplaceEditingConfig`定义属性：

   * 名称:`editorType`
   * 类型: `String`
   * 值: `hybrid`

1. 在此节点下，创建新节点：

   * 名称: `cq:ChildEditors`
   * 类型: `nt:unstructured`

1. 在该节 `cq:childEditors` 点下，为每个就地编辑器创建一个新节点：

   * 名称：每个节点的名称应该是它所表示属性的名称（与drop targets一样）。 For example, `image`, `text`.
   * 类型：cq: `ChildEditorConfig`
   >[!NOTE]
   >
   >定义的放置目标与子编辑器之间存在关联。 节点的名 `cq:ChildEditorConfig` 称将被视为放置目标ID，以用作所选子编辑器的参数。 如果可编辑子区域没有放置目标（例如，与文本组件一样），则子编辑器的名称仍被视为标识相应可编辑区域的ID。

1. 在以下每个节点上( `cq:ChildEditorConfig`)定义属性：

   * 名称: `type`
   * 值：注册就地编辑器的名称；例如， `image``text`

   * 名称: `title`
   * 值：要在组件选择列表中显示的标题（可用编辑器的标题）;例如， `Image``Text`

### 富文本编辑器的其他配置 {#additional-configuration-for-rich-text-editors}

多个富文本编辑器的配置略有不同，因为您可以分别配置每个RTE实例。

>[!NOTE]
>
>有关更多详细信息， [请参阅配置富文本编辑器](/help/sites-administering/rich-text-editor.md)。

要拥有多个RTE，您需要为每个就地RTE配置：

* 在 `cq:InplaceEditingConfig` 定义节 `config` 点下。

   * 在节点 `config` 下定义每个单独的RTE配置。

```xml
    texttext
        cq:dialog
        cq:editConfig
            cq:inplaceEditing
                cq:childEditors
                    config
                        text1
                            rtePlugins
                        text2
                            rtePlugins
```

>[!NOTE]
>
>建议的最佳实践是定义下 `config` 的节点， `cq:InplaceEditingConfig` 因为每个RTE都可以有不同的配置。
>
>但是，对于RTE，当组 `configPath` 件中只有一个文本编辑器实例（可编辑的子区域）时，支持该属性。 提供此功能 `configPath` 是为了支持与组件较早的UI对话框的向后兼容性。

## 代码样本 {#code-samples}

**GITHUB上的代码**

您可以在GitHub上找到此页面的代码

* [在GitHub上打开aem-authoring-hybrideditors项目](https://github.com/Adobe-Marketing-Cloud/aem-authoring-hybrideditors)
* 将项目下载为 [ZIP文件](https://github.com/Adobe-Marketing-Cloud/aem-authoring-hybrideditors/archive/master.zip)

## 添加就地编辑器 {#adding-an-in-place-editor}

有关添加就地编辑器的常规信息，请参阅文档自 [定义页面创作](/help/sites-developing/customizing-page-authoring-touch.md#add-new-in-place-editor)。
