---
title: 创作 — AEM中的环境和工具
description: AEM 的创作环境提供了各种可用于组织和编辑内容的机制.
uuid: 23a8aa93-b3d2-423b-b402-9e5f3f273d9a
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: f488ba79-5bda-46e9-9c15-9a8c3dbfa2ce
docset: aem65
exl-id: 3b3c118b-ca35-484b-a62e-7bec98953123
source-git-commit: bc1f0bd20804bbae78c7ea9a5209e183d6bbaaf3
workflow-type: tm+mt
source-wordcount: '2230'
ht-degree: 39%

---

# 创作 — 环境和工具{#authoring-the-environment-and-tools}

AEM 的创作环境提供了各种可用于组织和编辑内容的机制. 可以从各种控制台和页面编辑器访问提供的工具。

## 管理您的站点 {#managing-your-site}

此 **站点** 通过控制台，您可以使用标题栏、工具栏、操作图标（适用于所选资源）、痕迹导航以及辅助边栏（例如时间轴和引用）来导航和管理您的网站。

例如，列视图：

![ateat-01](assets/ateat-01.png)

## 编辑页面内容 {#editing-page-content}

您可以使用页面编辑器编辑页面。 例如：

`https://localhost:4502/editor.html/content/we-retail/us/en/equipment.html`

![ateat-02](assets/ateat-02.png)

>[!NOTE]
>
>首次打开页面进行编辑时，一系列幻灯片将为您提供这些功能的概览。
>
>您可以根据需要跳过导览，并通过从 **页面信息** 菜单。

## 访问帮助 {#accessing-help}

在编辑页面时，**帮助**&#x200B;可从以下位置访问：

* 此 [**页面信息**](/help/sites-authoring/editing-page-properties.md#page-properties) 选择器；这将显示幻灯片介绍（在您首次访问编辑器时显示）。
* 此 [配置](/help/sites-authoring/editing-content.md#edit-configure-copy-cut-delete-paste) 对话框（使用？） 图标)；这将显示上下文相关帮助。

更多 [控制台中提供了与帮助相关的资源](/help/sites-authoring/basic-handling.md#accessing-help).

## 组件浏览器 {#components-browser}

组件浏览器会显示可在当前页面上使用的所有组件。 可以将这些内容拖到相应的位置，然后进行编辑以添加您的内容。

组件浏览器是侧面板中的一个选项卡（侧面板中还有[资产浏览器](/help/sites-authoring/author-environment-tools.md#assets-browser)和[内容树](/help/sites-authoring/author-environment-tools.md#content-tree)）。要打开（或关闭）侧面板，请使用工具栏左上方的图标：

![ateat-03](assets/ateat-03.png)

打开侧面板时，它将从左侧滑开(选择 **组件** 选项卡（如有必要）。 打开时，您可以浏览页面可用的所有组件。

实际外观和操作取决于您所使用的设备类型：

>[!NOTE]
>
>当宽度小于1024像素时检测到移动设备。 对于小型桌面窗口也是如此。

* **移动设备(例如iPad)**

   组件浏览器完全覆盖正在编辑的页面。

   要将组件添加到页面，请按住所需的组件并将其向右移动，组件浏览器将关闭以再次显示页面 — 您可以在其中放置组件。

   ![ateat-04](assets/ateat-04.png)

* **桌面设备**

   组件浏览器将在窗口的左侧打开。

   要将组件添加到页面，请单击所需的组件，然后将其拖动到所需的位置。

   ![ateat-05](assets/ateat-05.png)

   组件由表示

   * 组件名称
   * 组件组（灰色）
   * 图标或缩写

      * 标准组件的图标是单色的。
      * 缩写始终是组件名称的前两个字符。

   从&#x200B;**组件**&#x200B;浏览器顶部的工具栏可以：

   * 按名称筛选组件。
   * 使用下拉选择框将显示内容限定为特定组。

   有关组件的更多详细说明，您可以单击或点按&#x200B;**组件**&#x200B;浏览器（如果可用）中组件旁边的信息图标。例如，对于&#x200B;**布局容器**：

   ![ateat-06](assets/ateat-06.png)

   有关可供您使用的组件的更多信息，请参阅[组件控制台](/help/sites-authoring/default-components-console.md)。

## 资产浏览器 {#assets-browser}

资产浏览器会显示所有 [资产](/help/assets/home.md) 这些资源可在当前页面上直接使用。

资产浏览器是侧面板中的一个选项卡，侧面板中还包含 [组件浏览](/help/sites-authoring/author-environment-tools.md#components-browser)r和 [内容树](/help/sites-authoring/author-environment-tools.md#content-tree). 要打开或关闭侧面板，请使用工具栏左上角的图标：

![ateat-03-1](assets/ateat-03-1.png)

打开侧面板时，它将从左侧滑开。根据需要选择&#x200B;**资产**&#x200B;选项卡。

![ateat-07](assets/ateat-07.png)

当资产浏览器打开时，您可以浏览页面可用的所有资产。 需要时可使用无限滚动来展开列表。

![ateat-08](assets/ateat-08.png)

要将资源添加到页面，请选择并拖动到所需的位置。 这可以是：

* 相应类型的现有组件。

   * 例如，可以将图像类型的资产拖动到图像组件上。

* 段落系统中用于创建相应类型新组件的[占位符](/help/sites-authoring/editing-content.md#component-placeholder)。

   * 例如，可以将图像类型的资产拖动到段落系统中，以创建图像组件。

>[!NOTE]
>
>这适用于特定资源和组件类型。 参见 [使用资产浏览器插入组件](/help/sites-authoring/editing-content.md#inserting-a-component-using-the-assets-browser) 了解更多详细信息。

在资源浏览器的顶部工具栏中，您可以通过以下方式筛选资源：

* 名称
* 路径
* 资产类型，如图像、手稿、文档、视频、页面、段落和产品
* 资产特征，如方向（纵向、横向、正方形）和样式（颜色、单色、灰度）

   * 仅适用于特定资源类型

实际外观和操作取决于您所使用的设备类型：

>[!NOTE]
>
>在宽度小于 1024 像素时将视为检测到移动设备，这种情况也可能出现在较小的桌面窗口中。

* **移动设备，如iPad**

   资产浏览器会完全覆盖正在编辑的页面。

   要将资源添加到页面，请触控并按住所需资源，然后将其向右移动 — 资源浏览器将关闭以再次显示页面，您可以在其中将资源添加到所需组件。

   ![ateat-09](assets/ateat-09.png)

* **桌面设备**

   将在窗口左侧打开资产浏览器。

   要将资源添加到页面，请单击所需的资源并将其拖动到所需的组件或位置。

   ![ateat-10](assets/ateat-10.png)

如果您需要快速更改资产，可以直接从资产浏览器启动[资产编辑器](/help/assets/manage-assets.md)，方法是单击资产名称旁边显示的编辑图标。

![](do-not-localize/screen_shot_2018-03-22at142448.png)

## 内容树 {#content-tree}

此 **内容树** 以层次结构概览页面上的所有组件，以便您一眼就能看到页面的构成方式。

内容树是侧面板中的一个选项卡（侧面板中还有组件和资产浏览器）。 要打开（或关闭）侧面板，请使用工具栏左上方的图标：

![](do-not-localize/screen_shot_2018-03-22at142042.png)

打开侧面板时，它将（从左侧）滑开。根据需要选择&#x200B;**内容树**&#x200B;选项卡。打开时，您可以看到页面或模板的树视图表示形式，以便更容易了解其内容是如何按层次结构构建的。 此外，在复杂的页面上，还可以更轻松地在页面的组件之间跳转。

![ateat-11](assets/ateat-11.png)

页面可以轻松地由许多相同类型的组件组成，因此内容（组件）树会在组件类型名称（黑色）之后显示描述性文本（灰色）。 描述性文本来自组件的常见属性，如标题或文本。

组件类型将以用户语言显示，而组件描述文本则来自页面语言。

单击组件旁边的V形标记将折叠或展开该级别。

![screen_shot_2018-03-22at142559](assets/screen_shot_2018-03-22at142559.png)

>[!NOTE]
>
>如果您正在浏览器宽度小于 1024 像素的移动设备上编辑页面，则内容树将不可用。

单击组件将在页面编辑器中突出显示组件。 可用的操作将取决于页面状态：

* 例如，基本页面：

   `https://localhost:4502/editor.html/content/we-retail/language-masters/en/equipment.html`

   ![ateat-12](assets/ateat-12.png)

   如果单击树中的组件可编辑，则名称右侧将显示扳手图标。 单击此图标将直接启动组件的“编辑”对话框。

   ![](do-not-localize/screen_shot_2018-03-22at142725.png)

* 或属于某个页面的某个页面 [活动副本](/help/sites-administering/msm.md)，其中组件继承自其他页面；例如：

   `https://localhost:4502/editor.html/content/we-retail/us/en/equipment.html`

   ![ateat-13](assets/ateat-13.png)

## 片段 – 关联的内容浏览器 {#fragments-associated-content-browser}

如果您的页面包含内容片段，那么您还可以访问[适用于关联内容的浏览器](/help/sites-authoring/content-fragments.md#using-associated-content)。

## 引用 {#references}

**引用** 显示选定页面的连接：

* Blueprint
* 启动项
* Live Copy
* 语言副本
* 传入链接
* 对引用组件的使用：借入和借出的内容
* 对产品页面的引用（从“商务 — 产品”控制台）

打开所需的控制台，然后导航到所需资源并使用以下方法打开&#x200B;**引用**：

![screen_shot_2018-03-22at153653](assets/screen_shot_2018-03-22at153653.png)

[选择您需要的资源](/help/sites-authoring/basic-handling.md#viewing-and-selecting-resources)以显示与该资源相关的引用类型列表：

![ateat-22](assets/ateat-22.png)

有关详细信息，请选择相应的参照类型。 在某些情况下，当您选择特定引用时，还可以执行其他操作，包括：

* **传入链接**，在选择特定链接后提供引用页面的页面列表，并可直接访问以&#x200B;**编辑**&#x200B;这些页面之一

* 使用&#x200B;**引用**&#x200B;组件的借入和借出内容的实例，您可以从此处导航至正在引用/引用的页面

* [对产品页面的引用](/help/commerce/cif-classic/administering/generic.md#showing-product-references) （可从“商务 — 产品”控制台中获取）
* [启动项](/help/sites-authoring/launches.md)，提供对相关启动项的访问权
* [Live Copy](/help/sites-administering/msm.md) 显示基于选定资源的所有 Live Copy 的路径。
* [Blueprint](/help/sites-administering/msm-best-practices.md)，提供详细信息和各种操作
* [语言副本](/help/sites-administering/tc-manage.md#creating-translation-projects-using-the-references-panel)，提供详细信息和各种操作

例如，可以修复“参照”元件中的破损参照：

![ateat-14](assets/ateat-14.png)

## 事件 – 时间线 {#events-timeline}

对于相应的资源（例如&#x200B;**站点**&#x200B;控制台中的页面或&#x200B;**资产**&#x200B;控制台中的资产），[可使用时间线显示任何选定项目上的近期活动](/help/sites-authoring/basic-handling.md#timeline)。

打开所需的控制台，然后导航到需要的资源并使用以下方法打开&#x200B;**时间线**：

![ateat-15](assets/ateat-15.png)

[选择您需要的资源](/help/sites-authoring/basic-handling.md#viewing-and-selecting-resources)，然后选择&#x200B;**显示全部**&#x200B;或&#x200B;**活动**，可列出对所选资源的所有近期操作：

![ateat-16](assets/ateat-16.png)

## 页面信息 {#page-information}

“页面信息”按钮（均衡器图标）会打开一个菜单，其中还提供有关上次编辑和上次发布的详细信息。 根据页面、其站点和您的实例的特性，可用的选项可能会更多，也可能会更少：

![ateat-17](assets/ateat-17.png)

* [打开属性](/help/sites-authoring/editing-page-properties.md)
* [转出页](/help/sites-administering/msm.md#msm-from-the-ui)
* [启动工作流](/help/sites-authoring/workflows-applying.md#starting-a-workflow-from-the-page-editor)
* [锁定页面](/help/sites-authoring/editing-content.md#locking-a-page)
* [发布页面](/help/sites-authoring/publishing-pages.md#main-pars-title-10)
* [取消发布页面](/help/sites-authoring/publishing-pages.md#main-pars-title-5)
* [编辑模板](/help/sites-authoring/templates.md)；当页面基于 [可编辑模板](/help/sites-authoring/templates.md#editable-and-static-templates)

* [以发布的形式查看](/help/sites-authoring/editing-content.md#view-as-published)
* 在Admin中查看；打开 [站点控制台](/help/sites-authoring/basic-handling.md#viewing-and-selecting-resources)
* [帮助](/help/sites-authoring/basic-handling.md#accessing-help)

例如，在适当的时候， **页面信息** 此外，还提供了以下选项：

* [提升启动项](/help/sites-authoring/launches-promoting.md) 如果页面是启动项，则为。
* [在经典用户界面中打开](/help/sites-authoring/select-ui.md#switching-to-classic-ui-when-editing-a-page) 如果此选项已 [由管理员启用](/help/sites-administering/enable-classic-ui-editor.md)

此外， **页面信息** 在适当的时候，可以提供对analytics和推荐的访问权限。

## 页面模式 {#page-modes}

在编辑页面时，有多种模式允许不同的操作：

* [编辑](/help/sites-authoring/editing-content.md)  — 编辑页面内容时使用的模式。
* [布局](/help/sites-authoring/responsive-layout.md) - 允许您创建和编辑依赖于设备的响应式布局（如果页面基于布局容器）

* [基架](/help/sites-authoring/scaffolding.md)  — 帮助您创建共享相同结构但内容不同的大量页面。
* [开发人员](/help/sites-developing/developer-mode.md)  — 允许您执行各种操作（需要权限）。 这包括检查页面及其组件的技术详细信息。

* [设计](/help/sites-authoring/default-components-designmode.md)  — 允许您启用/禁用要在页面上使用的组件，并配置组件的设计(如果页面基于 [静态模板](/help/sites-authoring/templates.md#editable-and-static-templates))。

* [定位](/help/sites-authoring/content-targeting-touch.md)  — 通过在所有渠道中进行定位和衡量来提高内容相关性。
* [Activity Map](/help/sites-authoring/page-analytics-using.md#analyticsvisiblefromthepageeditor)  — 显示页面的Analytics数据。

* [时间扭曲](/help/sites-authoring/working-with-page-versions.md#timewarp)  — 允许您查看特定时间点的页面状态。
* [Live Copy状态](/help/sites-authoring/editing-content.md#live-copy-status)  — 允许快速概述Live Copy状态以及哪些组件是/不是继承的。
* [预览](/help/sites-authoring/editing-content.md#previewing-pages) - 用于查看将在发布环境中显示的页面；或使用内容中的链接进行导航。

* [注释](/help/sites-authoring/annotations.md) - 用于在页面上添加或查看注释。

您可以使用右上角的图标访问这些模式。实际图标会因您当前所使用的模式而有所不同：

![ateat-18](assets/ateat-18.png)

>[!NOTE]
>
>* 根据页面的特性，某些模式可能不可用。
>* 访问某些模式需要适当的权限。
>* 由于空间限制，开发人员模式在移动设备上不可用。
>* 使用[键盘快捷键](/help/sites-authoring/page-authoring-keyboard-shortcuts.md) (`Ctrl-Shift-M`) 可以在&#x200B;**预览**&#x200B;模式和当前选定的模式（例如，**编辑**、**布局**&#x200B;等）之间切换。
>


## 路径选择 {#path-selection}

通常，在创作时，需要选择其他资源，例如定义指向其他页面或资源的链接或选择图像时。 要轻松选择路径， [路径字段](/help/sites-authoring/author-environment-tools.md#path-fields) 优惠自动完成和 [路径浏览器](/help/sites-authoring/author-environment-tools.md#path-browser) 允许进行更可靠的选择。

### 路径字段 {#path-fields}

此处用于说明的示例是图像组件。 有关使用和编辑组件的更多信息，请参阅 [用于页面创作的组件](/help/sites-authoring/default-components.md).

路径字段现在具有自动完成和前瞻功能，可更轻松地查找资源。

单击路径字段中的&#x200B;**打开选择对话框**&#x200B;按钮可打开[路径浏览器](/help/sites-authoring/author-environment-tools.md#path-browser)对话框，以查看更多详细选择选项。

![](do-not-localize/screen_shot_2018-03-22at154427.png)

或者您可以在路径字段中开始输入，AEM 将会在您输入的同时提供匹配的路径。

![ateat-19](assets/ateat-19.png)

### 路径浏览器 {#path-browser}

路径浏览器的组织方式与站点控制台的[列视图](/help/sites-authoring/basic-handling.md#column-view)相似，允许查看更多详细资源选择选项。

![screen_shot_2018-03-22at154521](assets/screen_shot_2018-03-22at154521.png)

* 选择资源后， **选择** 对话框右上角的按钮变为活动状态。 单击或点按以确认选择或 **取消** 以中止。
* 如果上下文允许选择多个资源，则选择某个资源也会激活“选择 **** ”按钮，但也会将选定资源的计数添加到窗口的右上角。 单击该 **数字旁边的** X可取消选择全部。
* 在树中导航时，您的位置会反映在对话框顶部的痕迹导航中。 这些痕迹导航还可用于在资源层次结构中快速跳转。
* 您可以随时使用对话框顶部的搜索字段。 单击 **X** 以清除搜索。
* 要缩小搜索范围，您可以显示过滤器选项并按特定路径筛选结果。

   ![ateat-21](assets/ateat-21.png)

## 键盘快捷键 {#keyboard-shortcuts}

可以使用各种[键盘快捷键](/help/sites-authoring/page-authoring-keyboard-shortcuts.md)。
