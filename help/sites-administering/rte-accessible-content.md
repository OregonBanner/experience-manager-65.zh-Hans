---
title: 配置RTE以生成可访问站点
description: 了解如何配置AEM富文本编辑器以生成可访问站点。
uuid: 87539fee-3ecc-49f4-af3d-8dde72399c28
contentOwner: AG
products: SG_EXPERIENCEMANAGER/6.5/SITES
discoiquuid: ff0f006d-461c-4cc4-b6eb-d665f3f3b498
translation-type: tm+mt
source-git-commit: 07c1a4102539ba4678c55dee3a4882101e39864f

---


# 配置RTE以生成可访问站点 {#configuring-rte-for-producing-accessible-sites}

AEM支持以下两种方式：

* 标准辅助功能，包括图像的替代文本
* 以及使用使用富文本编辑器(RTE)的组件创建内容时可访问的其他功能

内容作者可以使用RTE的功能在向页面添加内容时提供辅助功能信息。 这可以包括通过标题和段落元素添加结构性信息。

您可以 [通过为组件配置RTE插件来配置和自定义这些功能](#configuring-the-plugin-features) 。 例如，该插 `paraformat` 件允许您添加其他块级语义元素，包括将支持的标题级别数量扩展到基本级别以外 `H1`, `H2` 并默 `H3` 认提供。

RTE在触屏优化UI和经典UI的各种组件中都可用。 但是，使用RTE的主要组件是文 **本组件** 。

AEM **中的** “文本”组件可用于触屏优化UI和经典UI。 以下图像显示了启用了一系列插件的富文本编辑器，包括 `paraformat`:

* 触屏 **优化** UI中的文本组件：

   ![触屏优化UI中全屏模式的文本组件(RTE)。](assets/chlimage_1-206.png)

* 经典 **UI中的** “文本”组件：

   ![经典UI中文本组件的编辑对话框(RTE)。](assets/chlimage_1-207.png)

>[!NOTE]
>
>经典UI和触屏优化UI中的可用RTE功能之间存在差异。 有关详细信息，请参阅
>
>* [插件及其功能](/help/sites-administering/rich-text-editor.md#aboutplugins)
>* [插件及其功能——触屏优化UI](/help/sites-administering/rich-text-editor.md#aboutplugins)
>



## 配置插件功能 {#configuring-the-plugin-features}

有关配置RTE的完整说明，请参阅配 [置富文本编辑器页](/help/sites-administering/rich-text-editor.md) 。 这涵盖所有问题，包括关键步骤：

* [插件及其功能](/help/sites-administering/rich-text-editor.md#aboutplugins)
* [配置位置](/help/sites-administering/rich-text-editor.md#understand-the-configuration-paths-and-locations)
* [激活插件并配置功能属性](/help/sites-administering/rich-text-editor.md#enable-rte-functionalities-by-activating-plug-ins)
* [配置RTE的其他功能](/help/sites-administering/rich-text-editor.md#enable-rte-functionalities-by-activating-plug-ins)

通过在CRXDE Lite中相应的子 `rtePlugins` 分支中配置插件（请参阅下图），您可以激活该插件的全部或特定功能。

![CRXDE Lite，显示示例rtePlugin。](assets/chlimage_1-208.png)

### 示例——指定RTE选择字段中可用的段落格式 {#example-specifying-paragraph-formats-available-in-rte-selection-field}

新的语义块格式可通过以下方式可供选择：

1. 根据您的RTE，确定并导航到配 [置位置](/help/sites-administering/rich-text-editor.md#understand-the-configuration-paths-and-locations)。
1. [启用段落选择字段](/help/sites-administering/rich-text-editor.md);通过 [激活插件](/help/sites-administering/rich-text-editor.md#enable-rte-functionalities-by-activating-plug-ins)。
1. [在“段落”选择字段中指定要使用的格式](/help/sites-administering/rich-text-editor.md)。
1. 然后，RTE中的选择字段中的内容作者可以使用段落格式。 可以访问它们：

   * 使用触屏优化UI中的段落标记图标。
   * 在经典 **UI中使用** “格式”字段（弹出选择器）。

AEM通过段落格式选项在RTE中提供结构元素，为可访问内容的开发提供了良好的基础。 内容作者不能使用RTE设置字体大小或颜色格式或其他相关属性，从而阻止创建内联格式。 相反，它们必须选择相应的结构元素，如标题，并使用从“样式”选项中选择的全局样式。 这为使用自己的样式表和正确结构化内容浏览的用户确保了清晰的标记和更好的选项。

## 使用源编辑功能 {#use-of-the-source-edit-feature}

在某些情况下，内容作者会发现有必要检查和调整使用RTE创建的HTML源代码。 例如，在RTE中创建的一段内容可能需要额外的标记，以确保符合WCAG 2.0。这可以通过RTE的源 [编辑](/help/sites-administering/rich-text-editor.md#aboutplugins) 选项来完成。 您可以在插件 [ 上 `sourceedit` 指定功 `misctools` 能](/help/sites-administering/rich-text-editor.md#aboutplugins)。

>[!CAUTION]
>
>仔细使 `sourceedit` 用功能。 键入错误和／或不支持的功能可能会带来更多问题。

## 添加对其他HTML元素和属性的支持 {#adding-support-for-additional-html-elements-and-attributes}

要进一步扩展AEM的辅助功能，可以基于RTE(如 **Text** 和 **** Table组件)扩展现有组件，并添加其他元素和属性。

以下过程说明如何使用 **Caption****** 元素扩展Table组件，该元素向辅助型技术用户提供有关数据表的信息：

### 示例——将题注添加到表属性对话框 {#example-adding-the-caption-to-the-table-properties-dialog}

在的构造函数 `TablePropertiesDialog`中，添加一个用于编辑题注的附加文本输入字段。 请注 `itemId` 意，必须将 `caption` 其设置为（即DOM属性的名称）才能自动处理其内容。

在表 **中** ，必须显式地将属性设置为DOM元素或从DOM元素中删除该属性。 该值由对象中的对话框传 `config` 递。 请注意，应使用相应的方法设置／删除DOM属 `CQ.form.rte.Common` 性( `com` 这是浏览器实现的一个快捷方式 `CQ.form.rte.Common`)，以避免浏览器实现中的常见缺陷。

>[!NOTE]
>
>此过程仅适用于经典UI。

### 分步说明 {#step-by-step-instructions}

1. 启动CRXDE Lite。 例如： [http://localhost:4502/crx/de/](http://localhost:4502/crx/de/)
1. 复制:

   `/libs/cq/ui/widgets/source/widgets/form/rte/commands/Table.js`

   到:

   `/apps/cq/ui/widgets/source/widgets/form/rte/commands/Table.js`

   >[!NOTE]
   >
   >如果中间文件夹尚不存在，则可能需要创建中间文件夹。

1. 复制:

   `/libs/cq/ui/widgets/source/widgets/form/rte/plugins/TablePropertiesDialog.js`

   到:

   `/apps/cq/ui/widgets/source/widgets/form/rte/plugins/TablePropertiesDialog.js`.

1. 打开以下文件进行编辑（通过双击打开）:

   `/apps/cq/ui/widgets/source/widgets/form/rte/plugins/TablePropertiesDialog.js`

1. 在方法 `constructor` 中，在读取行之前：

   ```
   var dialogRef = this;
   ```

   添加以下代码：

   ```
   editItems.push({
       "itemId": "caption",
       "name": "caption",
       "xtype": "textfield",
       "fieldLabel": CQ.I18n.getMessage("Caption"),
       "value": (this.table && this.table.caption ? this.table.caption.textContent : "")
   });
   ```

1. 打开以下文件：

   `/apps/cq/ui/widgets/source/widgets/form/rte/commands/Table.js`.

1. 在方法的结尾添加以下代 `transferConfigToTable` 码：

   ```
   /**
    * Adds Caption Element
    */
   var captionElement; 
   if (dom.firstChild && dom.firstChild.tagName.toLowerCase() == "caption") 
   {
      captionElement = dom.firstChild;
   }
   if (config.caption)
   {
       var captionTextNode = document.createTextNode(config.caption)
       if (captionElement)
       {
          dom.replaceNode(captionElement.firstChild,captionTextNode); 
       } else
       {
           captionElement = document.createElement("caption");
           captionElement.appendChild(captionTextNode);
           if (dom.childNodes.length>0)
           {
              dom.insertBefore(captionElement, dom.firstChild);
           } else
           {
              dom.appendChild(captionElement);
           }
       }
   } else if (captionElement) 
   {
     dom.removeChild(captionElement);
   }
   ```

1. 使用“全部保 **存……”保存更改**

>[!NOTE]
>
>纯文本字段不是字幕元素值允许的唯一输入类型。 可使用通过其方法提供题注值的任何ExtJS `getValue()` 构件。
>
>要为其他元素和属性添加编辑功能，请确保以下两项：
>
>* 每 `itemId` 个对应字段的属性被设置为相应DOM属性(`TablePropertiesDialog`)的名称。
>* 该属性在DOM元素上显式设置和／或删除(`Table`)。


>[!MORELIKETHIS]
>
>* [WCAG 2.0快速指南](/help/managing/qg-wcag.md)
>* [创建可访问内容（WCAG 2.0符合性）](/help/sites-authoring/creating-accessible-content.md)

