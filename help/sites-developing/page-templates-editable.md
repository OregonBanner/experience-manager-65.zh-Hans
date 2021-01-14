---
title: 页面模板——可编辑
seo-title: 页面模板——可编辑
description: 已引入可编辑模板，允许非开发人员创建和编辑模板，提供模板，它们可以保留与从它们创建的任何页面的动态连接，并使页面组件更通用
seo-description: 已引入可编辑模板，允许非开发人员创建和编辑模板，提供模板，它们可以保留与从它们创建的任何页面的动态连接，并使页面组件更通用
uuid: 61791960-fdef-4e49-878a-11fdf1d4f0ab
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 1099cc44-de6d-499e-8b52-f2f5811ae086
docset: aem65
translation-type: tm+mt
source-git-commit: 149cdd00f745ad897f506434d7156b8147ef5bae
workflow-type: tm+mt
source-wordcount: '3285'
ht-degree: 8%

---


# 页面模板——可编辑{#page-templates-editable}

可编辑模板已引入：

* 允许专业作者[创建和编辑模板](/help/sites-authoring/templates.md)。

   * 此类专用作者称为&#x200B;**模板作者**
   * 模板作者必须是`template-authors`组的成员。

* 提供模板，它们可以保留与从它们创建的任何页面的动态连接。 这可确保模板的任何更改都反映在页面本身中。
* 使页面组件更加通用，这样无需自定义即可使用核心页面组件。

借助可编辑的模板，可在组件中隔离制作页面的部分内容。 您可以在UI中配置组件的必要组合，从而无需为每个页面变体开发新的页面组件。

>[!NOTE]
>
>[静态](/help/sites-developing/page-templates-static.md) 模板也可用。

本文档：

* 概述了如何创建可编辑的模板

   * 有关详细信息，请参阅[创建页面模板](/help/sites-authoring/templates.md)

* 描述创建可编辑模板所需的管理员／开发人员任务
* 描述可编辑模板的技术基础

此文档假定您已经熟悉创建和编辑模板。 请参阅创作文档[创建页面模板](/help/sites-authoring/templates.md)，其中详细介绍了模板作者可编辑模板的功能。

>[!NOTE]
>
>以下教程可能也会对在新项目中设置可编辑的页面模板感兴趣：
>[AEM Sites第2部分入门——创建基本页和模板](https://helpx.adobe.com/experience-manager/kt/sites/using/getting-started-wknd-tutorial-develop/part2.html)

## 创建新模板{#creating-a-new-template}

创建可编辑的模板主要由模板作者使用[模板控制台和模板编辑器](/help/sites-authoring/templates.md)来完成。 本节概述了此过程，并随后介绍了在技术层面发生的情况。

有关如何在AEM项目中使用可编辑模板的信息，请参阅[使用Lazybones](https://helpx.adobe.com/experience-manager/using/aem_lazybones.html)创建AEM项目。

创建新的可编辑模板时，您需要执行以下步骤：

1. 为模板](#template-folders)创建[文件夹。 这不是强制性的，但建议采用最佳实践。
1. 选择[模板类型](#template-type)。 复制此模板以创建[模板定义](#template-definitions)。

   >[!NOTE]
   >
   >现成提供模板类型选项。 如果需要，还可以[创建您自己的站点特定模板类型](/help/sites-developing/page-templates-editable.md#creating-template-types)。

1. 配置新模板的结构、内容策略、初始内容和布局。

   **结构**

   * 该结构允许您为模板定义组件和内容。
   * 不能在生成页面上移动在模板结构中定义的组件，也不能从任何生成页面中删除这些组件。

      * 如果要在We.Retail示例内容之外的自定义文件夹中创建模板，则可以选择Foundation Components或使用[核心组件](https://helpx.adobe.com/experience-manager/core-components/using/developing.html)。
   * 如果要使页面作者能够添加和删除组件，请在模板中添加段落系统。
   * 可以解锁组件，然后再将其锁定，以便定义初始内容。

   有关模板作者如何定义结构的详细信息，请参阅[创建页面模板](/help/sites-authoring/templates.md#editing-a-template-structure-template-author)。

   有关结构的技术详细信息，请参阅此文档中的[结构](/help/sites-developing/page-templates-editable.md#structure)。

   **策略**

   * 内容策略定义组件的设计属性。

      * 例如，可用的组件或最小/最大尺寸。
   * 这些属性适用于模板（和使用模板创建的页面）。

   有关模板作者如何定义策略的详细信息，请参阅[创建页面模板](/help/sites-authoring/templates.md#editing-a-template-structure-template-author)。

   有关策略的技术详细信息，请参阅此文档中的[内容策略](/help/sites-developing/page-templates-editable.md#content-policies)。

   **初始内容**

   * 初始内容定义首次根据模板创建页面时将显示的内容。
   * 初始内容随后可由页面作者编辑。

   有关模板作者如何定义结构的详细信息，请参阅[创建页面模板](/help/sites-authoring/templates.md#editing-a-template-initial-content-author)。

   有关初始内容的技术详细信息，请参阅此文档中的[初始内容](/help/sites-developing/page-templates-editable.md#initial-content)。

   **布局**

   * 您可以为各种设备定义模板布局。
   * 模板的响应式布局与页面创作时的响应式布局功能相同。

   有关模板作者如何定义模板布局的详细信息，请参阅[创建页面模板](/help/sites-authoring/templates.md#editing-a-template-layout-template-author)。

   有关模板布局的技术详细信息，请参阅此文档中的[布局](/help/sites-developing/page-templates-editable.md#layout)。

1. 启用模板，然后为特定内容树允许它。

   * 可以启用或禁用模板，以使其对页面作者可用或不可用。
   * 可以使模板可用于或不可用于某些页面分支。

   有关模板作者如何启用模板的详细信息，请参阅[创建页面模板](/help/sites-authoring/templates.md#enabling-and-allowing-a-template-template-author)。

   有关启用模板的技术详细信息，请参阅此文档中的[为Us](/help/sites-developing/page-templates-editable.md#enabling-and-allowing-a-template-for-use)e启用和允许模板

1. 使用它创建内容页面。

   * 使用静态模板和可编辑的模板创建新页面的过程没有明显的区别，也没有孰优孰劣之分。
   * 对于页面作者而言，该创建过程一目了然。

   有关页面作者如何使用模板创建页面的详细信息，请参阅[创建和组织页面](/help/sites-authoring/managing-pages.md#templates)。

   有关使用可编辑模板创建页面的技术详细信息，请参阅此文档中的[生成内容页面](/help/sites-developing/page-templates-editable.md#resultant-content-pages)。

>[!TIP]
>
>切勿在模板中输入任何需要国际化的信息。出于内部化目的，建议使用核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/get-started/localization.html)的[本地化功能。

>[!NOTE]
>
>模板是简化页面创建工作流程的强大工具。 但是，过多的模板可能会使作者不堪重负，并使页面创建变得混乱。 一个不错的经验法则是将模板数量保持在100以下。
>
>Adobe不建议具有1000个以上的模板，因为这可能会影响性能。

>[!NOTE]
>
>编辑器客户端库假定内容页面中存在`cq.shared`命名空间，如果不存在，则将导致JavaScript错误`Uncaught TypeError: Cannot read property 'shared' of undefined`。
>
>所有示例内容页面都包含`cq.shared`，因此基于这些页面的任何内容都会自动包含`cq.shared`。 但是，如果您决定从头开始创建您自己的内容页面而不基于示例内容，则必须确保包含`cq.shared`命名空间。
>
>有关详细信息，请参阅[使用客户端库](/help/sites-developing/clientlibs.md)。

## 模板文件夹{#template-folders}

要组织模板，您可以使用以下文件夹：

* **全局**
* 站点特定
您为组织模板而创建的站点特定文件夹是使用具有管理员权限的帐户创建的。

>[!NOTE]
>
>即使您可以嵌套文件夹，当用户在&#x200B;**模板**&#x200B;控制台中视图文件夹时，这些文件夹也会显示为平面结构。

在标准 AEM 实例中，“模板”控制台中已存在&#x200B;**全局**&#x200B;文件夹。此文件夹会保存默认模板，如果在当前文件夹中没有找到策略和/或模板类型，则此文件夹可以充当备用。您可以将默认模板添加到此文件夹或创建新文件夹（推荐）。

>[!NOTE]
>
>最好创建一个新文件夹来保存您的自定义模板，而不使用全局文件夹。

>[!CAUTION]
>
>文件夹必须由具有`admin`权限的用户创建。

模板类型和策略会按照以下优先顺序继承到所有文件夹：

1. 当前文件夹。
1. 当前文件夹的父级。
1. `/conf/global`
1. `/apps`
1. `/libs`

将创建所有允许条目的列表。 如果任何配置重叠(`path`/ `label`)，则只向用户显示最接近当前文件夹的实例。

要创建新文件夹，您可以执行以下操作之一：

* 以编程方式或通过CRXDE Lite
* 使用配置浏览器

## 使用CRXDE Lite{#using-crxde-lite}

1. 可以通过编程或CRXDE Lite为实例创建新文件夹（在/conf下）。

   必须使用以下结构：

   ```xml
   /conf
       <your-folder-name> [sling:Folder]
           settings [sling:Folder]
               wcm [cq:Page]
                   templates [cq:Page]
                   policies [cq:Page]
   ```

1. 然后，您可以在文件夹根节点上定义以下属性：

   `<your-folder-name> [sling:Folder]`

   名称: `jcr:title`

   * 类型: `String`

   * 值：要显示在&#x200B;**Templates**&#x200B;控制台中的标题（用于文件夹）。

1. 在&#x200B;*中，将*&#x200B;添加到标准创作权限和权限(例如，`content-authors`)，您现在需要为作者分配组并定义所需的访问权限(ACL)，以便在新文件夹中创建模板。

   `template-authors`组是需要分配的默认组。 有关详细信息，请参见下一节[ACL和组](/help/sites-developing/page-templates-editable.md#acls-and-groups)。

   有关管理和分配访问权限的完整详细信息，请参阅[访问权限管理](/help/sites-administering/user-group-ac-admin.md#access-right-management)。

### 使用配置浏览器{#using-the-configuration-browser}

1. 转至&#x200B;**全局导航** -> **工具** > **配置浏览器**。

   现有文件夹列在左侧，包括&#x200B;**global**&#x200B;文件夹。

1. 单击&#x200B;**创建**。
1. 在&#x200B;**创建配置**&#x200B;对话框中，需要配置以下字段：

   * **标题**:提供配置文件夹的标题
   * **可编辑模板**:勾号，允许在此文件夹内创建可编辑的模板

1. 单击&#x200B;**创建**

>[!NOTE]
>
>在配置浏览器中，如果您希望在此文件夹中创建模板，可以编辑全局文件夹并激活&#x200B;**可编辑模板**&#x200B;选项，但建议不要这样做。
>
>有关详细信息，请参阅[配置浏览器](/help/sites-administering/configurations.md)文档。

### ACL和组{#acls-and-groups}

在创建模板文件夹（通过CRXDE或使用配置浏览器）后，必须为模板文件夹的相应组定义ACL，以确保适当的安全性。

[We.Retail引用实现](/help/sites-developing/we-retail.md)的模板文件夹可以用作示例。

#### template-authors组{#the-template-authors-group}

`template-authors`组是用于管理模板访问权限的组，它标配AEM，但为空。 必须将用户添加到项目／站点的组。

>[!CAUTION]
>
>对于必须能够创建新模板的用户，`template-authors`组仅为&#x200B;**。
>
>编辑模板功能非常强大，如果不能正确编辑，现有模板就会损坏。 因此，该角色应集中并仅包括合格用户。

下表详细列出了进行模板编辑所需的权限。

<table>
 <tbody>
  <tr>
   <th>路径</th>
   <th>角色／组</th>
   <th>权限<br /> </th>
   <th>描述</th>
  </tr>
  <tr>
   <td rowspan="3"><code>/conf/&lt;<i>your-folder</i>&gt;/settings/wcm/templates</code></td>
   <td>模板作者<br /> </td>
   <td>读、写、复制</td>
   <td>在特定于站点的<code>/conf</code>空间中创建、读取、更新、删除和复制模板的模板作者</td>
  </tr>
  <tr>
   <td>匿名Web用户</td>
   <td>读</td>
   <td>匿名Web用户在呈现页面时必须阅读模板</td>
  </tr>
  <tr>
   <td>内容作者</td>
   <td>复制</td>
   <td>replicateContent作者在激活页面时需要激活页面的模板</td>
  </tr>
  <tr>
   <td rowspan="3"><code>/conf/&lt;<i>your-folder</i>&gt;/settings/wcm/policies</code></td>
   <td><code>Template Author</code></td>
   <td>读、写、复制</td>
   <td>在特定于站点的<code>/conf</code>空间中创建、读取、更新、删除和复制模板的模板作者</td>
  </tr>
  <tr>
   <td>匿名Web用户</td>
   <td>读</td>
   <td>匿名Web用户在呈现页面时必须阅读策略</td>
  </tr>
  <tr>
   <td>内容作者</td>
   <td>复制</td>
   <td>内容作者在激活页面时需要激活页面模板的策略</td>
  </tr>
  <tr>
   <td rowspan="2"><code>/conf/&lt;site&gt;/settings/template-types</code></td>
   <td>模板作者</td>
   <td>读</td>
   <td>模板作者根据预定义的模板类型之一创建新模板。</td>
  </tr>
  <tr>
   <td>匿名Web用户</td>
   <td>无</td>
   <td>匿名Web用户不能访问模板类型</td>
  </tr>
 </tbody>
</table>

此默认`template-authors`组仅涵盖项目设置，所有`template-authors`成员均可访问和创作所有模板。 对于更复杂的设置，在这些设置中，需要多个模板作者组才能单独访问模板，必须创建更多自定义模板作者组。 但是，模板作者组的权限将保持不变。

#### /conf/global {#legacy-templates-under-conf-global}下的旧版模板

模板不应再存储在`/conf/global`中，但是，对于某些旧版安装，此位置可能仍有模板。 只有在这种传统情况下，才应显式配置以下`/conf/global`路径。

<table>
 <tbody>
  <tr>
   <th>路径</th>
   <th>角色／组</th>
   <th>权限<br /> </th>
   <th>描述</th>
  </tr>
  <tr>
   <td rowspan="3"><code>/conf/global/settings/wcm/templates</code></td>
   <td>模板作者</td>
   <td>读、写、复制</td>
   <td>创建、读取、更新、删除和复制 <code>/conf/global</code></td>
  </tr>
  <tr>
   <td>匿名Web用户</td>
   <td>读</td>
   <td>匿名Web用户在呈现页面时必须阅读模板</td>
  </tr>
  <tr>
   <td>内容作者</td>
   <td>复制</td>
   <td>内容作者在激活页面时需要激活页面的模板</td>
  </tr>
  <tr>
   <td rowspan="3"><code>/conf/global/settings/wcm/policies</code></td>
   <td><code>Template Author</code></td>
   <td>读、写、复制</td>
   <td>创建、读取、更新、删除和复制 <code>/conf/global</code></td>
  </tr>
  <tr>
   <td>匿名Web用户</td>
   <td>读</td>
   <td>匿名Web用户在呈现页面时必须阅读策略</td>
  </tr>
  <tr>
   <td>内容作者</td>
   <td>复制</td>
   <td>内容作者在激活页面时需要激活页面模板的策略</td>
  </tr>
  <tr>
   <td rowspan="2"><code>/conf/global/settings/wcm/template-types</code></td>
   <td>模板作者</td>
   <td>读</td>
   <td>模板作者根据预定义的模板类型之一创建新模板</td>
  </tr>
  <tr>
   <td>匿名Web用户</td>
   <td>无</td>
   <td>匿名Web用户不能访问模板类型</td>
  </tr>
 </tbody>
</table>

## 模板类型{#template-type}

创建新模板时，您需要指定模板类型：

* 模板类型有效地为模板提供模板。 创建新模板时，将使用所选模板类型的结构和初始内容创建新模板。

   * 将复制模板类型以创建模板。
   * 复制完成后，模板与模板类型之间的唯一连接就是静态引用，供参考。

* 模板类型允许您定义：

   * 页面组件的资源类型。
   * 根节点的策略，它定义模板编辑器中允许的组件。
   * 建议在模板类型上为响应式网格和移动模拟器的设置定义断点。 这是可选的，因为配置也可以在单个模板上定义（请参阅[模板类型和移动设备组](/help/sites-developing/page-templates-editable.md#p-template-type-and-mobile-device-groups-br-p)）。

* AEM提供一些现成的模板类型选项，如HTML5页面和自适应表单页面。

   * 还提供了其他示例，作为[We.Retail](/help/sites-developing/we-retail.md)示例内容的一部分。

* 模板类型通常由开发人员定义。

现成模板类型存储在以下位置：

* `/libs/settings/wcm/template-types`

>[!CAUTION]
>
>不得更改`/libs`路径中的任何内容。 这是因为下次升级实例时，`/libs`的内容会被覆盖（应用修补程序或功能包时，可能会被覆盖）。

站点特定的模板类型应存储在以下可比位置：

* `/apps/settings/wcm/template-types`

自定义模板类型的定义应存储在用户定义的文件夹中（建议），或者存储在`global`中。 例如：

* `/conf/<my-folder-01>/<my-folder-02>/settings/wcm/template-types`
* `/conf/<my-folder>/settings/wcm/template-types`
* `/conf/global/settings/wcm/template-types`

>[!CAUTION]
>
>模板类型必须遵循正确的文件夹结构(即`/settings/wcm/...`)，否则将找不到模板类型。

### 模板类型和移动设备组{#template-type-and-mobile-device-groups-br}

用于可编辑模板的[设备组](/help/sites-developing/mobile.md#device-groups)（设置为属性`cq:deviceGroups`的相对路径）定义了在页面创作的[布局模式](/help/sites-authoring/responsive-layout.md)中哪些移动设备可用作模拟器。 此值可以设置为两个位置：

* 在可编辑的模板类型上
* 在可编辑的模板上

创建新的可编辑模板时，值会从模板类型复制到单个模板。 如果未在类型上设置值，则可以在模板上设置该值。 创建模板后，类型不再继承到模板。

>[!CAUTION]
>
>必须将`cq:deviceGroups`的值设置为相对路径（如`mobile/groups/responsive`），而不设置为绝对路径（如`/etc/mobile/groups/responsive`）。

>[!NOTE]
>
>对于[静态模板](/help/sites-developing/page-templates-static.md)，可以在站点的根位置设置`cq:deviceGroups`的值。
>
>对于可编辑的模板，此值现在存储在模板级别，而在页面根级别不受支持。

### 创建模板类型{#creating-template-types}

如果已创建可用作其他模板基础的模板，则可以将此模板复制为模板类型。

1. 按照此处](/help/sites-authoring/templates.md#creating-a-new-template-template-author)的说明创建任何可编辑模板[的模板，它将作为模板类型的基础。
1. 使用CRXDE Lite，将新创建的模板从`templates`节点复制到[template文件夹](/help/sites-developing/page-templates-editable.md#template-folders)下的`template-types`节点。
1. 从[template folder](/help/sites-developing/page-templates-editable.md#template-folders)下的`templates`节点中删除模板。
1. 在`template-types`节点下的模板副本中，删除所有`cq:template`和`cq:templateType` `jcr:content`属性。

您还可以根据GitHub提供的示例可编辑模板，开发您自己的模板类型。

GITHUB上的代码

您可以在GitHub上找到此页面的代码

* [在GitHub上打开aem-sites-example-custom-template-type项目](https://github.com/Adobe-Marketing-Cloud/aem-sites-example-custom-template-type)
* 将项目下载为[a ZIP文件](https://github.com/Adobe-Marketing-Cloud/aem-sites-example-custom-template-type/archive/master.zip)

## 模板定义{#template-definitions}

可编辑模板的定义存储在[用户定义的文件夹](/help/sites-developing/page-templates-editable.md#template-folders)（推荐）或`global`中。 例如：

* `/conf/<my-folder>/settings/wcm/templates`
* `/conf/<my-folder-01>/<my-folder-02>/settings/wcm/templates`
* `/conf/global/settings/wcm/templates`

模板的根节点类型为`cq:Template`，其骨架结构为：

```xml
<template-name>
  initial
    jcr:content
      root
        <component>
        ...
        <component>
  jcr:content
    @property status
  policies
    jcr:content
      root
        @property cq:policy
        <component>
          @property cq:policy
        ...
        <component>
          @property cq:policy
  structure
    jcr:content
      root
        <component>
        ...
        <component>
      cq:responsive
        breakpoints
  thumbnail.png
```

主要元素有：

* `<template-name>`

   * ` [initial](#initial-content)`
   * `jcr:content`
   * ` [structure](#structure)`
   * ` [policies](#policies)`
   * `thumbnail.png`

### jcr:content {#jcr-content}

此节点包含模板的属性：

* **名称**: `jcr:title`

* **名称**: `status`

   * ``**类型**: `String`

   * **值**: `draft`、 `enabled` 或  `disabled`

### 结构 {#structure}

定义生成页面的结构：

* 在创建新页面时与初始内容(`/initial`)合并。
* 对结构所做的更改将反映在使用模板创建的任何页面中。
* `root`(`structure/jcr:content/root`)节点定义将在生成页面中可用的组件列表。

   * 在模板结构中定义的组件不能移动到任何生成页面或从任何生成页面中删除。
   * 解锁组件后，`editable`属性将设置为`true`。

   * 解锁已包含内容的组件后，此内容将移至`initial`分支。

* `cq:responsive`节点保存响应式布局的定义。

### 初始内容 {#initial-content}

定义新页面在创建时将包含的初始内容：

* 包含复制到任何新页面的`jcr:content`节点。
* 创建新页面时与结构(`/structure`)合并。
* 如果初始内容在创建后发生更改，则不会更新任何现有页面。
* `root`节点包含一列表组件，用于定义在生成页面中可用的组件。
* 如果内容以结构模式添加到组件，并且该组件随后被解锁（反之亦然），则此内容将用作初始内容。

### 布局 {#layout}

在[编辑模板时，您可以定义布局](/help/sites-authoring/templates.md)，这使用标准响应式布局[，该布局也可以是[configured](/help/sites-administering/configuring-responsive-layout.md)。](/help/sites-authoring/responsive-layout.md)

### 内容策略{#content-policies}

内容（或设计）策略可定义组件的设计属性。例如，可用的组件或最小/最大尺寸。这些属性适用于模板（和使用模板创建的页面）。可以在模板编辑器中创建和选择内容策略。

* `root`节点上的属性`cq:policy`
   `/conf/<your-folder>/settings/wcm/templates/<your-template>/policies/jcr:content/root`
为页面的段落系统提供对内容策略的相对引用。

* 属性`cq:policy`位于`root`下的component-explicit节点上，提供指向各个组件的策略的链接。

* 实际策略定义存储在：
   `/conf/<your-folder>/settings/wcm/policies/wcm/foundation/components`

>[!NOTE]
>
>策略定义的路径取决于组件的路径。 `cq:policy` 保存对配置本身的相对引用。

>[!NOTE]
>
>从可编辑模板创建的页面不会优惠页面编辑器中的设计模式。
>
>可编辑模板的`policies`树的层次结构与静态模板的设计模式配置在以下位置相同：
>
>`/etc/designs/<my-site>/jcr:content/<component-name>`
>
>静态模板的设计模式配置是按页面组件定义的。

### 页面策略 {#page-policies}

页面策略允许您在模板或生成页面中为页面（主parsys）定义[内容策略](#content-policies)。

### 启用和允许使用{#enabling-and-allowing-a-template-for-use}模板

1. **启用模板**

   必须通过以下任一方式启用模板才能使用模板：

   * [从“模](/help/sites-authoring/templates.md#enablingatemplateauthor) 板”控制台启 **** 用模板。

   * 在`jcr:content`节点上设置状态属性。

      * 例如，在：
         `/conf/<your-folder>/settings/wcm/templates/<your-template>/jcr:content`

      * 定义属性：

         * 名称：状态
         * 类型：字符串
         * 值: `enabled`

1. **允许的模板**

   * [在子分支的相应页面或根页 **面的**](/help/sites-authoring/templates.md#allowing-a-template-author) 页面属性中定义允许的模板路径。
   * 设置属性：
      `cq:allowedTemplates`
在 
`jcr:content` 所需分支的节点。
   例如，值为：

   `/conf/<your-folder>/settings/wcm/templates/.*`

## 生成内容页{#resultant-content-pages}

从可编辑模板创建的页面：

* 使用从模板中的`structure`和`initial`合并的子树创建

* 具有对模板和模板类型中信息的引用。 这是通过具有以下属性的`jcr:content`节点实现的：

   * `cq:template`
提供对实际模板的动态参考；允许在实际页面上反映对模板所做的更改。

   * `cq:templateType`
提供对模板类型的引用。

![chlimage_1-71](assets/chlimage_1-71.png)

上图显示了模板、内容和组件之间如何相互关联：

* 控制器- `/content/<my-site>/<my-page>`
引用模板的生成页面。 内容控制整个过程。 根据定义，它访问相应的模板和组件。

* 配置- `/conf/<my-folder>/settings/wcm/templates/<my-template>`
[模板和相关内容策略](#template-definitions)定义页面配置。

* Model - OSGi bundles
[OSGI包](/help/sites-deploying/osgi-configuration-settings.md)实现该功能。

* 视图- `/apps/<my-site>/components`
在创作和发布环境上，内容由[组件](/help/sites-developing/components.md)呈现。

呈现页面时：

* **模板**:

   * 将引用其`jcr:content`节点的`cq:template`属性以访问与该页面对应的模板。

* **组件**:

   * 页面组件将模板的`structure/jcr:content`树与页面的`jcr:content`树合并。

   * 页面组件将仅允许作者编辑已标记为可编辑的模板结构的节点（以及任何子节点）。
   * 在页面上呈现组件时，该组件的相对路径将从`jcr:content`节点获取；随后将搜索模板`policies/jcr:content`节点下的同一路径。

      * 此节点的`cq:policy`属性指向实际的内容策略（即它包含该组件的设计配置）。

      * 这允许您拥有多个可重复使用相同内容策略配置的模板。
