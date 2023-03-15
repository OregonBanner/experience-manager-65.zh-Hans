---
title: 配置富文本编辑器以在Adobe Experience Manager中创作内容。
description: 了解如何配置Adobe Experience Manager富文本编辑器以在Adobe Experience Manager中创作内容。
contentOwner: AG
exl-id: 2e7ec22f-0856-44c4-bb15-1086dae0b85a
source-git-commit: 63f066013c34a5994e2c6a534d88db0c464cc905
workflow-type: tm+mt
source-wordcount: '3020'
ht-degree: 1%

---

# 配置富文本编辑器 {#configure-the-rich-text-editor}

富文本编辑器(RTE)为作者提供了一系列广泛的功能来编辑其文本内容。 为所见即所得文本编辑体验提供了图标、选择框、工具栏和菜单。

要了解如何使用RTE功能进行创作，请参阅 [使用富文本编辑器进行创作](/help/sites-authoring/rich-text-editor.md). 可以将RTE配置为启用、禁用和扩展创作组件中可用的功能。 以下工作流说明了在Experience Manager中完成RTE配置任务的建议顺序。

![了解如何配置RTE的一系列步骤](assets/rte_workflow_v1.png)

*图：了解如何配置RTE的步骤顺序*

## 了解触屏优化UI和经典UI {#understand-touch-enabled-ui-and-classic-ui}

触屏优化UI是Experience Manager的标准用户界面。 Adobe引入了触屏优化UI [响应式设计](/help/sites-authoring/responsive-layout.md) （创作环境）。 触屏优化UI专为触控设备和桌面设备而设计。 该界面与原始经典UI有很大区别。

![触屏用户界面中的富文本编辑器工具栏](assets/chlimage_1-35.png)

*图：触屏UI中的富文本编辑器工具栏*

![经典UI中的富文本编辑器工具栏](assets/rtedefault.png)

*图：经典UI中的富文本编辑器工具栏*

>[!MORELIKETHIS]
>
>* [UI推荐](/help/sites-deploying/ui-recommendations.md)
>* 有关弃用经典UI的信息，请参阅 [Experience Manager6.5发行说明](/help/release-notes/deprecated-removed-features.md)
>* 有关UI之间的差异，请参阅 [触控UI和经典UI](https://aemcq5pedia.wordpress.com/2018/01/05/touch-enabled-ui-aem6-3/)
>* 要详细了解触屏优化UI，请参阅 [Experience Manager触控UI的概念](/help/sites-developing/touch-ui-concepts.md)


## 各种编辑模式 {#editingmodes}

作者可以使用各种组件模式在Experience Manager中创建和编辑文本内容。 在不同编辑模式下，用于创作内容和设置内容格式的工具栏选项以及启用RTE的组件的用户体验因RTE配置而异。

| 编辑模式 | 编辑区域 | 建议启用的功能 | 触屏 UI | 经典 UI |
|--- |--- |--- |--- |--- |
| 内嵌 | 就地编辑以进行快速、次要的编辑；格式化而不打开对话框 | 最小的RTE功能 | Y | Y |
| RTE全屏 | 涵盖整个页面 | 所有必需的RTE功能 | Y | N |
| 对话框 | 对话框但不覆盖整个页面 | 经典UI中所有必需的RTE功能；在触屏UI中谨慎启用功能 | Y | Y |
| 全屏对话框 | 与全屏模式相同；包含对话框的字段以及RTE | 所有必需的RTE功能 | Y | N |

>[!NOTE]
>
>在触屏UI中，源编辑功能在内联编辑模式下不可用。 您无法在全屏模式下拖动图像。 所有其他功能在所有模式中都有效。

### 内联编辑 {#inline-editing}

打开时（缓慢双击/单击），可以在页面中编辑内容。 此时会显示一个包含非常基本选项的紧凑工具栏。

![在触屏UI中使用基本工具栏进行内联编辑](assets/chlimage_1-36.png)

*图：在触屏UI中使用基本工具栏的内联编辑*

在经典UI中，通过缓慢双击组件，可以内联编辑，并且橙色轮廓会突出显示内容。 如果“内容查找器”处于打开状态，则窗口顶部会显示一个包含可用RTE格式选项的工具栏。 如果“内容查找器”未打开，则格式选项不会显示，并且您只能进行基本的文本编辑。

### 全屏编辑 {#full-screen-editing}

Experience Manager组件能够以全屏视图打开，该视图会隐藏页面内容并占据可用屏幕。 请考虑全屏编辑内联编辑的详细版本，因为它提供了最多的编辑选项。 可以通过单击将其打开 ![rte_fullscreen](assets/rte_fullscreen.png)，使用内联编辑模式时，从压缩工具栏删除。

在对话框的全屏模式以及详细的RTE工具栏中，对话框中可用的选项和组件也可用。 它仅适用于包含RTE以及其他组件的对话框。

![在触屏UI中以全屏模式编辑时的详细RTE工具栏](assets/chlimage_1-37.png)

*图：在触屏UI中以全屏模式编辑时的详细RTE工具栏*

### 对话框编辑 {#dialog-editing}

双击组件时，将打开一个对话框以编辑内容。 对话框将在现有页面的顶部打开。 在某些特定情况下，对话框会作为弹出窗口打开。 例如，当文本组件属于多列页面布局中的列的一部分并且可用于对话框的区域较少时。

![触屏UI中的对话框编辑模式](assets/dialog_editing_modetouchui.png)

*图：触控式UI中的对话框编辑模式*

![经典UI中的对话框，其中包含用于编辑的详细工具栏](assets/chlimage_1-38.png)

*图：经典UI中包含用于编辑的详细工具栏的对话框*

## 关于RTE插件和相关功能 {#aboutplugins}

该功能可通过一系列插件提供，每个插件均具有：

* A `features` 属性：

   * 用于激活或取消激活该插件的基本功能
   * 可使用标准化的过程配置该属性

* 适当时，需要专门配置的其他属性和选项。

RTE的基本功能由的值激活或停用 `features` 属性的特定于相应插件的节点。

下表列出了当前的插件，其中显示：

* 包含指向API文档链接的插件ID。 在以下情况下，ID用作节点名称 [激活插件](/help/sites-administering/configure-rich-text-editor-plug-ins.md#activateplugin).
* 允许的值 `features` 属性。
* 插件提供的功能描述。

| 插件Id | 功能 | 描述 |
|--- |--- |--- |
| 编辑 | 剪切copy paste-default paste-plaintext paste-wordhtml | [剪切、复制和三种粘贴模式](/help/sites-administering/configure-rich-text-editor-plug-ins.md#textstyles). |
| [findreplace](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.rte.plugins.FindReplacePlugin) | 查找替换 | 查找并替换. |
| [format](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.rte.plugins.FormatPlugin) | 加粗斜体下划线 | [基本文本格式](/help/sites-administering/configure-rich-text-editor-plug-ins.md#textstyles). |
| [图像](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.rte.plugins.ImagePlugin) | 图像 | 基本图像支持（从内容或内容查找器拖动）。 根据浏览器的不同，对作者的支持有不同的行为 |
| [键](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.rte.plugins.KeyPlugin) |  | 要定义此值，请参阅 [制表符大小](/help/sites-administering/configure-rich-text-editor-plug-ins.md#tabsize). |
| [两端对齐](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.rte.plugins.JustifyPlugin) | Justifyleft justifycenter justifyright | 段落对齐方式。 |
| [链接](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.rte.plugins.LinkPlugin) | modifylink取消链接锚点 | [超链接和锚点](/help/sites-administering/configure-rich-text-editor-plug-ins.md#linkstyles). |
| [列表](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.rte.plugins.ListPlugin) | 有序无序缩进缩进 | 此插件会同时控制两者 [缩进和列表](/help/sites-administering/configure-rich-text-editor-plug-ins.md#indentmargin)；包括嵌套列表。 |
| [misctools](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.rte.plugins.MiscToolsPlugin) | specialchars sourceedit | 其他工具允许作者输入 [特殊字符](/help/sites-administering/configure-rich-text-editor-plug-ins.md#spchar) 或编辑HTML源。 此外，您还可以添加整个 [特殊字符的范围](/help/sites-administering/configure-rich-text-editor-plug-ins.md#definerangechar) 如果您想要定义自己的列表。 |
| 参数格式 | 参数格式 | 默认段落格式为段落、标题1、标题2和标题3 (`<p>`， `<h1>`， `<h2>`、和 `<h3>`)。 您可以 [添加更多段落格式](/help/sites-administering/configure-rich-text-editor-plug-ins.md#paraformats) 或者扩展列表。 |
| 拼写检查 | 复选文本 | [语言感知拼写检查器](/help/sites-administering/configure-rich-text-editor-plug-ins.md#adddict). |
| 样式 | 样式 | 支持使用CSS类进行样式。 [添加新文本样式](/help/sites-administering/configure-rich-text-editor-plug-ins.md#textstyles) 如果要添加（或扩展）自己的样式范围以用于文本。 |
| 下标 | 下标上标 | 基本格式的扩展，可添加子脚本和超级脚本。 |
| 表 | 表删除表插入行删除插入列删除列cellprops mergecells拆分单元选择列选择列 | 参见 [配置表样式](/help/sites-administering/configure-rich-text-editor-plug-ins.md#tablestyles)，如果要为整个表或单个单元格添加自己的样式。 |
| 撤消 | 撤消重做 | 历史记录大小 [撤消和重做](/help/sites-administering/configure-rich-text-editor-plug-ins.md#undohistory) 操作。 |

>[!NOTE]
>
>对话框模式不支持全屏插件。 使用 `dialogFullScreen` 设置以将工具栏配置为全屏模式。

## 了解配置路径和位置 {#understand-the-configuration-paths-and-locations}

此 [RTE编辑模式（和UI）](#editingmodes) 由您为作者提供的位置来确定配置详细信息的位置， [激活RTE插件](/help/sites-administering/configure-rich-text-editor-plug-ins.md#activateplugin)：

| 编辑模式 | 触控UI的位置 | 经典UI的位置 |
|---|---|---|
| 内嵌 | `cq:editConfig/cq:inplaceEditing` | `cq:editConfig/cq:inplaceEditing` |
| 全屏 | `cq:editConfig/cq:inplaceEditing` | 不适用 |
| 对话框 | `cq:dialog` | `dialog` |
| 全屏对话框 | `cq:dialog` | 不适用 |

>[!NOTE]
>
>不要将节点命名为 `cq:inplaceEditing` 作为 `config`. 日期 `cq:inplaceEditing` 节点，定义以下属性：
>* **名称**: `configPath`
>* **类型**: `String`
>* **值**：包含实际配置的节点的路径
>
>不要将RTE配置节点命名为 `config`. 否则，RTE配置将仅对管理员生效，而不对组中的用户生效 `content-author`.

配置以下属性，这些属性仅适用于Touch UI中的对话框编辑模式：

* `useFixedInlineToolbar`：设置在RTE节点（具有sling：resourceType=的节点）上定义的此Boolean属性 `cq/gui/components/authoring/dialog/richtext`)至 `True`，以固定RTE工具栏而不是浮动工具栏。

   当此属性为true时，默认情况下，RTF编辑在“foundation-contentloaded”事件中启动。

   要防止出现这种情况，请设置属性 `customStart` 到 `True`和触发“rte-start”事件以开始RTE编辑。 当此属性为“true”时，默认行为（单击时启动rte）不起作用。

* `customStart`：将此RTE节点上定义的布尔属性设置为 `True`，以通过触发事件来控制何时启动RTE `rte-start`.

* `rte-start`：在上触发此事件 `contenteditable-div` ，则表示何时开始编辑RTE。 仅当满足以下条件时，此项才有效 `customStart` 已设置为true。

在启用了触屏的对话框中使用RTE时，设置属性 `useFixedInlineToolbar` 设置为true是避免出现问题的必选项。

## 自定义就地编辑 {#customizing-in-place-editing}

通过配置以下HTML，您可以定义文本编辑器从哪个属性选择器开始：

* **`editElementQuery`**  — 定义于 `cq:InplaceEditingConfig`，此属性用于指定启动文本组件的内联编辑的HTML元素选择器。 如果未指定，则会在文本组件HTML上直接开始内联编辑。
* **`textPropertyName`**  — 定义于 `cq:InplaceEditingConfig`，此属性用于指定将保存在内容节点上的属性的名称，其中文本组件的HTML值将在内联编辑后保留。

对话框模式的相应属性为 `name`.

## 通过激活插件启用RTE功能 {#enable-rte-functionalities-by-activating-plug-ins}

RTE功能通过一系列插件提供，每个插件都具有功能属性。 您可以配置features属性以启用或禁用每个插件的各种功能。

有关RTE插件的详细配置，请参阅 [如何激活和配置RTE插件](/help/sites-administering/configure-rich-text-editor-plug-ins.md).

**示例**：下载 [此示例配置](/help/sites-administering/assets/rte-sample-all-features-enabled-10.zip) 说明了如何配置RTE。 在此程序包中，所有功能均已启用。

>[!NOTE]
>
>此 [核心组件文本组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/text.html?lang=en#the-text-component-and-the-rich-text-editor) 允许模板编辑器在GUI中配置许多RTE插件作为内容策略，而无需技术配置。 内容策略可以与RTE UI配置配合使用，如本文档中所述。
>
>欲了解更多信息，请参见 [RTE UI设置和内容策略](/help/sites-administering/rich-text-editor.md) 以及本文档的章节 [创建页面模板](/help/sites-authoring/templates.md) 和 [核心组件开发人员文档](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/developing.html).

>[!NOTE]
>
>出于参考目的，可以在以下位置找到默认的文本组件（作为标准安装的一部分提供）：
>
>* `/libs/wcm/foundation/components/text`
>* `/libs/foundation/components/text`
>
>要创建您自己的文本组件，请复制上述组件而不是编辑这些组件。

## 配置RTE工具栏 {#dialogfullscreen}

AEM允许您针对不同的编辑模式以不同的方式配置富文本编辑器的界面。 默认设置如下所示。 您可以根据自己的要求覆盖这些默认值。 您只需自定义要提供给作者的工具栏功能。 您无需指定所有工具栏配置。

要配置工具栏，请执行以下操作 `dialogFullScreen`，请使用以下示例配置。

```java
<uiSettings jcr:primaryType="nt:unstructured">
  <cui jcr:primaryType="nt:unstructured">
    <inline
      jcr:primaryType="nt:unstructured"
      toolbar="[format#bold,format#italic,format#underline,#justify,#lists,links#modifylink,links#unlink,#paraformat]">
      <popovers jcr:primaryType="nt:unstructured">
        <justify
          jcr:primaryType="nt:unstructured"
          items="[justify#justifyleft,justify#justifycenter,justify#justifyright,justify#justifyjustify]"
          ref="justify"/>
        <lists
          jcr:primaryType="nt:unstructured"
          items="[lists#unordered,lists#ordered,lists#outdent,lists#indent]"
          ref="lists"/>
        <paraformat
          jcr:primaryType="nt:unstructured"
          items="paraformat:getFormats:paraformat-pulldown"
          ref="paraformat"/>
      </popovers>
    </inline>
    <dialogFullScreen
      jcr:primaryType="nt:unstructured"
      toolbar="[format#bold,format#italic,format#underline,justify#justifyleft,justify#justifycenter,justify#justifyright,justify#justifyjustify,lists#unordered,lists#ordered,lists#outdent,lists#indent,links#modifylink,links#unlink,table#createoredit,#paraformat,image#imageProps]">
      <popovers jcr:primaryType="nt:unstructured">
        <paraformat
          jcr:primaryType="nt:unstructured"
          items="paraformat:getFormats:paraformat-pulldown"
          ref="paraformat"/>
      </popovers>
    </dialogFullScreen>
    <tableEditOptions
      jcr:primaryType="nt:unstructured"
      toolbar="[table#insertcolumn-before,table#insertcolumn-after,table#removecolumn,-,table#insertrow-before,table#insertrow-after,table#removerow,-,table#mergecells-right,table#mergecells-down,table#mergecells,table#splitcell-horizontal,table#splitcell-vertical,-,table#selectrow,table#selectcolumn,-,table#ensureparagraph,-,table#modifytableandcell,table#removetable,-,undo#undo,undo#redo,-,table#exitTableEditing,-]">
    </tableEditOptions>
  </cui>
</uiSettings>
```

内联模式和全屏模式使用不同的UI设置。 toolbar属性用于指定工具栏的按钮。

例如，如果按钮本身是功能(例如， `Bold`)，则指定为 `PluginName#FeatureName` (例如， `links#modifylink`)。

如果按钮是弹出框（包含插件的某些功能），则将其指定为 `#PluginName` (例如， `#format`)。

分隔符(`|`)之间，可以使用以下方式指定多个按钮： `-`.

内联或全屏模式下的弹出节点包含正在使用的弹出框列表。 “弹出框”节点下的每个子节点均以插件的名称（例如，格式）命名。 它具有包含插件功能列表（例如，format#bold）的“items”属性。

## RTE用户界面设置和内容策略 {#rtecontentpolicies}

管理员可以使用内容策略来控制RTE选项，而不是执行上述配置。 内容策略在用作组件的一部分时定义组件的设计属性 [可编辑模板](/help/sites-authoring/templates.md). 例如，如果将使用RTE的文本组件与可编辑模板一起使用，则内容策略可以定义粗体选项可用，并且一些段落格式选项可用。 内容策略可重用，并且可以跨多个模板应用。

RTE中的可用选项会从用户界面配置下游流向内容策略。

* 用户界面配置设置定义哪些选项可用于内容策略。
* 如果RTE的用户界面配置已删除或未启用某个项目，则内容策略无法对其进行配置。
* 作者只能访问由用户界面配置和内容策略提供的功能。

例如，您可以看到 [文本核心组件文档](https://docs.adobe.com/help/en/experience-manager-core-components/using/components/text.html#the-text-component-and-the-rich-text-editor).

## 自定义工具栏图标和命令之间的映射 {#iconstoolbar}

您可以自定义RTE工具栏上显示的Coral图标与可用命令之间的映射。 除了Coral图标之外，您无法使用任何其他图标。

1. 创建名为的节点 `icons` 下 `uiSettings/cui`.

1. 为下面的各个图标创建节点。
1. 在每个图标节点上，指定一个Coral图标和一个要映射到图标的命令。

以下是将命令Bold映射到名为的Coral图标的示例代码片段 `textItalic`.

```java
<text jcr:primaryType="nt:unstructured" sling:resourceType="cq/gui/components/authoring/dialog/richtext" name="./text" useFixedInlineToolbar="{Boolean}true">
    <rtePlugins jcr:primaryType="nt:unstructured">
        <format jcr:primaryType="nt:unstructured" features="bold,italic"/>
    </rtePlugins>
    <uiSettings jcr:primaryType="nt:unstructured">
        <cui jcr:primaryType="nt:unstructured">
            <inline jcr:primaryType="nt:unstructured"
                toolbar="[format#bold,format#italic,format#underline,links#modifylink,links#unlink]">
            </inline>
            <icons jcr:primaryType="nt:unstructured">
                <bold jcr:primaryType="nt:unstructured"
                    command="format#bold"
                    icon="textItalic"/>
            </icons>
        </cui>
    </uiSettings>
</text>
```

## 切换到CoralUI 2富文本编辑器 {#switch-to-coralui-rich-text-editor}

在页面上，您可以包含CoralUI 2 RTE clientlib或CoralUI 3 RTE clientlib。 默认情况下，富文本编辑器包含CoralUI 3 RTE clientlib。 要切换到CoralUI 2 RTE，请执行以下步骤。

>[!NOTE]
>
>Adobe不建议将其作为最佳实践。 最后才切换到CoralUI 2 RTE。 如果自定义插件不依赖于RTE内部（如类），则CoralUI 2 RTE的插件可与CoralUI 3 RTE配合使用。
>
>如果要使用CoralUI3 RTE的自定义插件，请使用 `rte.coralui3` 库。


1. 覆盖节点 `/libs/cq/gui/components/authoring/editors/clientlibs/core` 下 `/apps`，并执行以下操作：

   * Replace `rte.coralui3` 替换为 `rte.coralui2` 依赖关系属性。
   * Replace `cq.authoring.editor.core.inlineediting.rte.coralui3` 替换为 `cq.authoring.editor.core.inlineediting.rte.coralui2` （对于嵌入属性）。
   * Replace `cq.authoring.rte.coralui3` 替换为 `cq.authoring.rte.coralui2` （对于嵌入属性）。

1. 覆盖节点 `/libs/cq/gui/components/authoring/dialog/richtext/clientlibs/rte/coralui3` 和 `/libs/cq/gui/components/authoring/dialog/richtext/clientlibs/rte/coralui2` 下 `/apps`.

   删除类别 `cq.authoring.dialog` 起始日期 `/apps/cq/gui/components/authoring/dialog/richtext/clientlibs/rte/coralui3` 并将其添加到 `/apps/cq/gui/components/authoring/dialog/richtext/clientlibs/rte/coralui2`.

1. 将页面上包含的任何其他依赖项从 `rte.coralui3` 到 `rte.coralui2`. 例如，覆盖节点后 `/libs/mcm/campaign/components/touch-ui/clientlibs/rte` 下 `/apps`，更改对它的任何依赖关系从 `rte.coralui3` 到 `rte.coralui2`.

1. 覆盖节点 `cq/ui/widgets` 下 `/apps`. 替换依赖项 `cq.rte` 在节点上 `/apps/cq/ui/widgets` 替换为 `cq.coralui2.rte`.

>[!NOTE]
>
>CoralUI 2 RTE使用Handlebars模板作为插件对话框。 因此，CoralUI 2 RTE clientlib依赖于handlebars clientlib。 CoralUI 3 RTE不使用handlebars模板，因此没有任何关联的依赖项。 如果您的自定义插件使用handlebars模板，请在网页中包含handlebars clientlib。

## 更多信息 {#further-information}

有关配置RTE的更多信息，请参阅 [AEM小组件API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.RichText) 引用。

具体来说，要查看可用的插件和相关选项，请执行以下操作：

* 此 [CQ.form.RichText](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.rte.plugins.Plugin) 组件提供了一个表单字段，用于编辑样式化文本信息（富文本）。 要了解富文本表单的所有可用参数，请参阅配置选项。
* 富文本组件使用下面列出的插件提供多种功能 [CQ.form.rte.plugins.Plugin](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.rte.plugins.Plugin). 对于每个插件：

   * 有关可以启用（或禁用）的功能的详细信息，请参阅功能
   * 有关相应插件的详细配置，请参阅所有可用参数的配置选项

* 此外，还提供了有关链接的HTML规则的更多信息。

这些资源可用于扩展和自定义您自己的RTE。 例如，要在创建链接时列出页面中可用的锚点，您可以提供自己的实施 `LinkPlugin`.

## 已知限制 {#known-limitations}

AEM RTE功能具有以下限制：

* 仅在AEM组件对话框中支持RTE功能。 向导或类似的基础表单不支持RTE [页面属性](/help/sites-developing/page-properties-views.md) 和 [基架](/help/sites-authoring/scaffolding.md) 触屏UI上。

* AEM不适用于 [混合设备](/help/release-notes/release-notes.md).

* 不要命名RTE配置节点 `config`. 否则，RTE配置仅对管理员生效，对组中的用户无效 `content-author`.

* RTE不支持将内联框架或iframe嵌入内容。

## 最佳实践和提示 {#best-practices-and-tips}

* 仅启用插件，而不显示浮动对话框的弹出窗口。 没有弹出窗口的插件尺寸较小，最适合用于浮动对话框。
* 通过较大的弹出窗口启用插件，例如 `Paste` 插件，但仅限于全屏对话框模式或全屏模式。 具有大型弹出窗口的插件需要更多的屏幕空间才能提供良好的创作体验。
* 如果要使用CoralUI3 RTE的自定义插件，请使用 `rte.coralui3` 库。

## 解决RTE的常见问题 {#troubleshoot-issues-with-aem-rich-text-editor}

**如何选择多个表单元格？**

要选择表格中的多个单元格，请按 `Ctrl` 或 `Cmd` 键，然后逐一单击表单元格。

现在，对选定内容执行操作，例如设置选定单元格的属性。

**使用“配置”按钮编辑组件时，超链接丢失**

通过使用“配置”按钮编辑文本组件，在文本组件中添加超链接。 再次编辑超链接并再次验证超链接时，可能会丢失该超链接。

解决方法是第二次显示“编辑”对话框时单击文本组件，然后运行链接验证。

此问题可在AEM 6.3及更高版本中解决。

**在源编辑模式下添加的HTML内容将丢失**

不要添加易受XSS影响的HTML。 AEM而非RTE，可能会删除一些HTML内容以遵守XSS反精神病规则。

要验证粘贴的HTML是否已保存，请检查CRXDE中保存的内容（在“内容”节点中）。

如果未保存，则必须由RTE删除HTML，因为它不符合RTE规则。

如果保存在CRXDE中但未在页面上渲染(要检查渲染，请参阅页面的 [预览](/help/sites-authoring/editing-content.md#preview-mode)，则会被AEM XSS规则删除。

**多字段组件未按预期工作**

要创建多字段组件，请专门使用CoralUI 3。 请勿使用CoralUI 2组件对话框。

此外，请验证多字段实施代码和节点结构是否正确。

**管理员可用的配置不可用于作者**

如果界面配置更新反映在管理员而非作者帐户中，请确保配置节点未命名 `config`. 使用 [`configPath` 属性](/help/sites-developing/components-basics.md#cq-inplaceediting).

>[!MORELIKETHIS]
>
>* [配置RTE插件](configure-rich-text-editor-plug-ins.md)
>* [使用富文本编辑器进行创作](../sites-authoring/rich-text-editor.md)
>* [为可访问的站点配置RTE](rte-accessible-content.md)
>* [Touch UI和Classic UI对等功能](../release-notes/touch-ui-features-status.md)
>* [创建复合多字段组件的教程示例](https://experience-aem.blogspot.com/2019/05/aem-65-touchui-composite-multifield-with-coral3-rte-rich-text.html)

