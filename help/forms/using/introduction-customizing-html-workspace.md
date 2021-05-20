---
title: 自定义AEM表单工作区简介
seo-title: 自定义AEM表单工作区简介
description: 快速介绍，其中包含概念和技术信息，用于自定义LiveCycleAEM Forms工作区以进行流程管理。
seo-description: 快速介绍，其中包含概念和技术信息，用于自定义LiveCycleAEM Forms工作区以进行流程管理。
uuid: 38759071-e6b8-4976-8b06-909ad7a786cd
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 021c6606-8cd3-472c-a80b-b1bcace7e87f
docset: aem65
exl-id: b183d42f-343c-4acb-bc73-f80ad72e54df
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1786'
ht-degree: 0%

---

# 自定义AEM表单工作区{#introduction-to-customizing-aem-form-workspace}简介

AEM表单工作区提供了修改其界面的表示语义和功能的功能。 更改样式、布局、格式、品牌和核心功能的自定义类型如下所述。

![cu_customized_workspace_example](assets/cu_customized_workspace_example.png)

自定义工作区的示例

## 自定义类型{#types-of-customizations}

AEM Forms工作区支持各种自定义，以更新用户界面的布局、外观、功能等。 这些自定义涉及更新以下一项或多项：

* 用户界面的外观
* 使用语义自定义的功能
* 在其他应用程序中重用HTML组件

### 用户界面更改{#user-interface-changes}

您可以更改AEM Forms工作区的外观、布局和其他表示语义。 通过自定义CSS、HTML模板和JavaScript™文件来更改工作区。 所有默认文件都在默认安装中提供。

[AEM Forms工作区自定义的一般步骤](../../forms/using/generic-steps-html-workspace-customization.md)中介绍了最常用的步骤。 有关此类自定义的特定示例（包括详细步骤），请参阅本文末尾的相关文章。

#### 了解样式表{#understanding-the-style-sheet}

在自定义工作区之前，请熟悉AEM Forms提供的默认样式表，网址为/libs/ws/css/style.css。

要自定义工作区，建议您熟悉位于/libs/ws/css文件夹中的现有样式表style.css。 下面介绍了一些主要组件。

<table>
 <tbody>
  <tr>
   <th><p>CSS元素</p> </th>
   <th><p>修改了用户界面组件</p> </th>
  </tr>
  <tr>
   <td><p>#标题</p> </td>
   <td><p>AEM Forms工作区标题</p> </td>
  </tr>
  <tr>
   <td><p>.categoryList</p> </td>
   <td><p>类别列表</p> </td>
  </tr>
  <tr>
   <td><p>.categoryList .header</p> </td>
   <td><p>类别列表标题</p> </td>
  </tr>
  <tr>
   <td><p>.categories， .filters</p> </td>
   <td><p>类别列表下方的空格</p> </td>
  </tr>
  <tr>
   <td><p>.category， .filter</p> </td>
   <td><p>类别</p> </td>
  </tr>
  <tr>
   <td><p>.category:hover， .category.selected， .filter:hover， .filter.selected</p> </td>
   <td><p>选定类别和将鼠标悬停在类别样式上</p> </td>
  </tr>
  <tr>
   <td><p>categoryListBar .tool， categoryListBar .content</p> </td>
   <td><p>开始流程页（已关闭的类别列表）</p> </td>
  </tr>
  <tr>
   <td><p>filterListBar .tool、filterListBar .content</p> </td>
   <td><p>要执行的页面（已关闭的过滤器列表）</p> </td>
  </tr>
  <tr>
   <td><p>processNameListBar .tool、processNameListBar .content</p> </td>
   <td><p>跟踪页面（已关闭的进程名称列表）</p> </td>
  </tr>
  <tr>
   <td><p>.startPointList， .tasklist</p> </td>
   <td><p>起始点列表或任务列表</p> </td>
  </tr>
  <tr>
   <td><p>.startPointList .header， .tasklist .header</p> </td>
   <td><p>起始点列表或任务列表的标头</p> </td>
  </tr>
  <tr>
   <td><p>.startpoint.selected， .task.selected</p> </td>
   <td><p>所选起点或任务</p> </td>
  </tr>
  <tr>
   <td><p>.startpoint.selected .description， .task.selected .description</p> </td>
   <td><p>所选起点或任务的描述</p> </td>
  </tr>
  <tr>
   <td><p>#taskarea</p> </td>
   <td><p>任务区</p> </td>
  </tr>
  <tr>
   <td><p>#header .dropdown</p> </td>
   <td><p>标题中的用户下拉列表</p> </td>
  </tr>
  <tr>
   <td><p>.sortDrop dd ul</p> </td>
   <td><p>排序任务下拉列表</p> </td>
  </tr>
 </tbody>
</table>

#### CSS {#css}

AEM Forms工作区的外观借用了CSS的外观。 通过自定义CSS，您可以更改工作区的表示语义，如字体、颜色、品牌和布局。

CSS自定义的顶级步骤包括：

* 创建CSS文件。
* 向此CSS添加样式项。 请参阅了解CSS样式以了解更多信息。
* 在`html.jsp`中更新其引用。

有关执行这些自定义的确切步骤，请参阅[AEM Forms工作区自定义的一般步骤](../../forms/using/generic-steps-html-workspace-customization.md)。 AEM Forms工作区附带的CSS文件位于/libs/ws/css/。 对于与CSS相关的自定义设置，请使用[Ship Package](../../forms/using/introduction-customizing-html-workspace.md#p-crx-package-p)。 有关与CSS相关的自定义的特定示例，请参阅本文末尾的相关帮助主题。

#### 图像 {#image}

您可以自定义AEM Forms工作区，以添加用户的变形或添加组织的徽标。 对于这些自定义设置，请使用[发运包](../../forms/using/introduction-customizing-html-workspace.md#p-crx-package-p)。

对图像进行自定义的顶级步骤包括：

* 安装和配置WebDAV。
* 添加新图像。
* 添加与添加的图像对应的新样式。
* 链接到`html.jsp`文件中的新CSS文件。

要开始在AEM Forms工作区中自定义图像，请按照[AEM Forms工作区自定义的常规步骤](../../forms/using/generic-steps-html-workspace-customization.md)操作。 有关与图像相关的自定义的特定示例，请参阅本文末尾的相关帮助主题。

#### HTML模板{#html-template}

HTML模板有助于定义工作区用户界面的外观和布局。 通过更新默认HTML模板，您可以自定义布局默认用户界面。

对HTML模板进行自定义的顶级步骤包括：

* 在用户创建的文件夹中，复制所需的默认文件。
* 在用户定义的文件夹中添加新模板。
* 对复制的文件（如新模板的路径）进行相关更新。

有关此类自定义的特定示例，请参阅本文末尾提供的帮助主题。 根据要自定义的模板，在[发运包](../../forms/using/introduction-customizing-html-workspace.md#p-crx-package-p)或[开发包](../../forms/using/introduction-customizing-html-workspace.md#p-crx-package-p)之间进行选择。

### 语义变化{#semantic-changes}

要修改AEM Forms工作区功能，请更改JavaScript源代码。 核心功能的修改将标记为语义更改。 您可以修改作为AEM Forms工作区源代码一部分提供的模型、视图和模板。

要进行语义更改以修改AEM Forms工作区的功能，请执行以下顶级步骤：

* 在用户创建的文件夹中，复制相应的默认文件。
* 在用户定义的文件夹中添加新模型和视图。
* 进行相关更新，如更新默认JavaScript文件中新添加模型和视图的路径。
* 缩小资源包以优化性能。

有关源代码中组件的更多概念信息，请参阅[可重用组件描述](/help/forms/using/description-reusable-components.md)。 对于这些自定义设置，请使用开发包。

### 可重用组件{#reusable-components}

由于AEM Forms工作区是一款基于组件的软件，因此可以轻松自定义和重复使用。 您可以轻松地将工作区组件与Web应用程序相集成。

有关更多概念信息，请参阅[可重用组件描述](/help/forms/using/description-reusable-components.md)和有关使用组件的说明，请参阅[在Web应用程序中集成AEM Forms工作区组件](/help/forms/using/description-reusable-components.md)。

## 构建AEM Forms工作区代码{#building-html-workspace-code}

### SDK包{#sdk-package}

该包包含AEM Forms工作区的源代码。 该包位于`[LC root]\sdk\html-workspace\adobe-lc-workspace-src.zip`。

它主要用于自定义，因为它提供了生成以下内容的功能：

* 适用于发运、调试和开发配置文件的CRX包（在[CRX包](../../forms/using/introduction-customizing-html-workspace.md#p-crx-package-p)中提及）。
* 自定义代码的缩小版本（用于语义更改）。

#### WS内容{#ws-content}

* client-pkg:

   * src — 包含创建CRX节点所需的工件。
   * pom.xml — 为各种配置文件构建部署包的脚本WS-Deploy包

* client-html:

   * 程序集 — 包含脚本用于创建AEM Forms工作区SDK的zip.xml。
   * src/main/webapp -

      * css — 包含AEM Forms工作区的样式表。
      * 图像 — 包含在AEM Forms工作区中使用的图像。
      * js:

         * libs — 包含在AEM Forms工作区中使用的所有第三方库。
         * 许可证 — 包含HTML和JS文件的许可证以及用于为这些许可证添加前缀的代码，以添加到相应的源文件。
         * 缩小器 — 用于customizedJavaScript代码的组合、缩小和升级。
         * resourcejs_optimizer — 用于JavaScript源的组合、缩小和升级。
         * resource_generator — 用于生成register.js和modelcontrollerpath.js。
         * 运行时：

            * 初始值设定项 — 包含初始值设定项.js ，用于初始化AEM Forms工作区中使用的骨干视图和模型。
            * 模型 — 包含AEM Forms工作区中所有组件的骨干模型。
            * routes — 包含JavaScript文件和HTML文件，它们在AEM Forms工作区中加载开始进程、操作、跟踪和首选项。
            * 服务 — 包含在AEM Forms工作区中使用的service.js。 所有服务器调用均通过service.js进行。
            * 模板 — 包含所有模板，即AEM Forms工作区中所有视图的HTML文件。
            * util — 包含在AEM Forms工作区中使用的所有实用工具文件(javascript)。
            * 视图 — 包含AEM Forms工作区中所有组件的主干视图。
         * main.js
         * router.js
      * libs/ws:pdf.html和pluginPing.pdf用于在AEM Forms工作区中加载PDF forms，而WSNextAdapter.swf用于在AEM Forms工作区中加载SWF表单和指南。
      * 区域设置：

         * de-DE — 包含德语的translation.json。
         * en-US — 包含英语的translation.json。
         * fr-FR — 包含法语的translation.json。
         * ja-JP — 包含日语的translation.json。
         * html.jsp — 包含用于找出当前浏览器区域设置的代码。
      * html.jsp
      * GET.jsp




### CRX包{#crx-package}

CRX包可以部署在CRX™存储库上。 它位于`[LC root]\crx-repository\install\adobe-lc-workspace-pkg.zip`。

可以使用下面描述的三个配置文件构建此包。

| **个人资料** | **描述** | **使用** |
|---|---|---|
| 发运配置文件 | 此配置文件会使用缩小功能创建尽可能小的CRX包。 这个包最有效。 所有JavaScript™文件都会合并并缩小为一个JS文件。 | 当JS文件中不需要进行任何语义更改时，请使用此配置文件。 |
| 调试配置文件 | 此配置文件可创建中等效率的CRX包。 包的大小比使用“发运”配置文件创建的包的大小略大。 此包将大多数JavaScript文件合并到一个JS文件中。 | 使用此配置文件进行调试。 |
| 开发用户档案 | 此配置文件会创建尽可能大的CRX包。 所有JavaScript文件均可单独使用，因为它们位于SDK包中。 | 结合语义变化时使用此配置文件。 |

#### 发运配置文件{#ship-profile}

#### Command {#command}

* mvn clean -P在发送到客户端的源包的client-pkg文件夹上发运安装。
* 仅在64位JVM上执行发运配置文件命令。

#### WS内容{#ws-content-1}

* css — 包含style.css、ie.css和jquery-ui.css。
* 图像 — 包含所有图像。
* js:

   * libs:

      * require — 包含require.js。
      * jqueryui — 包含jquery.ui.datepicker.ja.js。
   * 运行时：

      * 模板 — 包含所有模板，即AEM Forms工作区中所有组件的HTML文件。
   * main.js（合并、缩小和缩小）。
   * registry.js



* libs:

   * ws — 包含pluginPing.pdf、pdf.html和WSNextAdapter.swf。

* 区域设置 — 包含.content.xml。
* 区域设置：

   * de-DE — 包含德语的translation.json。
   * en-US — 包含英语的translation.json。
   * fr-FR — 包含法语的translation.json。
   * ja-JP — 包含日语的translation.json。
   * html.jsp — 包含用于找出当前浏览器区域设置的代码。

* 索引 — 包含.content.xml
* 配置文件 — 包含offline.jsp。
* GET.jsp
* html.jsp
* content.xml
* _rep_policy.xml

#### 调试配置文件{#debug-profile}

#### Command {#command-1}

* mvn clean -P在client-pkg上安装调试
* 调试配置文件命令执行仅在64位JVM上工作。

#### WS内容{#ws-content-2}

* css — 包含style.css、ie.css和jquery-ui.css。
* 图像 — 包含所有图像。
* js:

   * libs:

      * require — 包含require.js。
      * jqueryui — 包含jquery.ui.datepicker.ja.js。
   * 运行时：

      * 模板 — 包含所有模板，即AEM Forms工作区中所有组件的HTML文件。
   * main.js（合并）。
   * registry.js



* libs:

   * ws — 包含pluginPing.pdf、pdf.html和WSNextAdapter.swf。

* 区域设置 — 包含.content.xml。
* 区域设置：

   * de-DE — 包含德语的translation.json。
   * en-US — 包含英语的translation.json。
   * fr-FR — 包含法语的translation.json。
   * ja-JP — 包含日语的translation.json。
   * html.jsp — 包含用于找出当前浏览器区域设置的代码。

* 索引 — 包含.content.xml
* 配置文件 — 包含offline.jsp。
* GET.jsp
* html.jsp
* content.xml
* _rep_policy.xml

#### 开发配置文件{#dev-profile}

#### 命令{#command-2}

mvn clean -P Dev在client-pkg上安装

#### WS内容{#ws-content-3}

* css — 包含style.css、ie.css和jquery-ui.css。
* 图像 — 包含所有图像。
* js:

   * libs — 包含在AEM Forms工作区中使用的所有库。
   * require — 包含require.js
   * jqueryui — 包含jquery.ui.datepicker.ja.js
   * 运行时：

      * 初始值设定项 — 包含初始值设定项.js和modelcontrollerpath.js。
      * 模型 — 包含AEM Forms工作区中所有组件的模型。
      * routes — 包含JavaScript文件和HTML文件，它们在AEM Forms工作区中加载开始进程、操作、跟踪和首选项。
      * 服务 — 包含在AEM Forms工作区中使用的service.js。
      * 模板 — 包含所有模板，即AEM Forms工作区中所有组件的HTML文件。
      * util — 包含在AEM Forms工作区中使用的所有实用工具文件(JavaScript)。
      * 视图 — 包含AEM Forms工作区中所有组件的视图。
   * main.js
   * registry.js
   * router.js


* libs:

   * ws — 包含pluginPing.pdf、pdf.html和WSNextAdapter.swf。

* 区域设置 — 包含.content.xml。
* 区域设置：

   * de-DE — 包含德语的translation.json。
   * en-US — 包含英语的translation.json。
   * fr-FR — 包含法语的translation.json。
   * ja-JP — 包含日语的translation.json。
   * html.jsp — 包含用于找出当前浏览器区域设置的代码。

* 索引 — 包含.content.xml
* 配置文件 — 包含offline.jsp。
* GET.jsp
* html.jsp
* content.xml
* _rep_policy.xml
