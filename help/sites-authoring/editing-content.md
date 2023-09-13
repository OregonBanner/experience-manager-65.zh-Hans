---
title: 编辑页面内容
description: 创建页面后，您可以编辑内容以进行所需的更新。
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
docset: aem65
exl-id: d5cf4478-51e4-4ca8-b3f8-6d7caed7d515
source-git-commit: 474a726058b141985f52a0faec6161a34be1e9dc
workflow-type: tm+mt
source-wordcount: '3016'
ht-degree: 49%

---

# 编辑页面内容{#editing-page-content}

创建页面（新页面或者作为启动项或Live Copy的一部分）后，您可以编辑内容以进行所需的更新。

内容使用可拖动到页面上的[组件](/help/sites-authoring/default-components-console.md)（适用于内容类型）进行添加。然后，可以就地编辑、移动或删除这些内容。

>[!NOTE]
>
>您的帐户需要 [适当的访问权限](/help/sites-administering/security.md) 和 [权限](/help/sites-administering/security.md#permissions) 以编辑页面。
>
>如果您遇到任何问题，Adobe建议您与系统管理员联系。

>[!NOTE]
>
>如果您的页面、模板或两者都进行了适当设置，则可以使用 [响应式布局](/help/sites-authoring/responsive-layout.md) 编辑时。

>[!NOTE]
>
>在&#x200B;**编辑**&#x200B;模式下，内容中的链接是可见的，但是&#x200B;**不可访问**。如果您要使用内容中的链接进行导航，请使用[预览模式](#previewingpagestouchoptimizedui)。

## 页面工具栏 {#page-toolbar}

根据页面配置，用户可以通过页面工具栏访问相应的功能。

![页面工具栏](assets/screen_shot_2018-03-22at111338.png)

工具栏允许访问许多选项。根据您当前的上下文和配置，某些选项可能不可用。

* **切换侧面板**

  打开/关闭侧面板，其中包含[资源浏览器](/help/sites-authoring/author-environment-tools.md#assets-browser)、[组件浏览器](/help/sites-authoring/author-environment-tools.md#components-browser)和[内容树](/help/sites-authoring/author-environment-tools.md#content-tree)。

  ![切换侧面板](do-not-localize/screen_shot_2018-03-22at111425.png)

* **页面信息**

  它提供对 [页面信息](/help/sites-authoring/author-environment-tools.md#page-information) 菜单，其中包含页面详细信息和可在页面上执行的操作，包括查看和编辑页面信息、查看页面属性以及发布/取消发布页面。

  ![页面信息](do-not-localize/screen_shot_2018-03-22at111437.png)

* **模拟器**

  切换[模拟器工具栏](/help/sites-authoring/responsive-layout.md#selecting-a-device-to-emulate)，它用于在其他设备上模拟页面的外观。它在布局模式下会自动切换。

  ![模拟器](do-not-localize/screen_shot_2018-03-22at111442.png)

* **ContextHub**

  打开 [上下文中心](/help/sites-authoring/ch-previewing.md). 仅在预览模式下可用。

  ![上下文中心](assets/screen_shot_2018-03-22at111543.png)

* **页面标题**

  它是纯信息性的。

  ![页面标题](assets/screen_shot_2018-03-22at111554.png)

* **模式选择器**

  它显示当前 [模式](/help/sites-authoring/author-environment-tools.md#page-modes) 并允许您选择其他模式，如编辑、布局、时间扭曲或定位。

  ![模式选择器](assets/chlimage_1-120.png)

* **预览**

  启用[预览模式](/help/sites-authoring/editing-content.md#preview-mode)。这将显示发布时显示的页面。

  ![预览模式](assets/chlimage_1-121.png)

* **批注**

  它允许您添加 [注释](/help/sites-authoring/annotations.md) 查看页面时跳转到页面。 在第一个批注之后，图标会切换到一个数字，指示页面上的批注数量。

  ![批注](do-not-localize/screen_shot_2018-03-22at111638.png)

### 状态通知 {#status-notification}

如果页面是一个[工作流](/help/sites-authoring/workflows.md)或多个工作流的一部分，则在编辑该页面时，将在屏幕顶部的通知栏中显示此信息。

![工作流通知](assets/screen_shot_2018-03-22at111739.png)

>[!NOTE]
>
>状态栏仅对具有相应权限的用户帐户可见。

通知会列出正在针对页面运行的工作流。如果用户参与了当前工作流步骤，还可以使用[影响工作流状态](/help/sites-authoring/workflows-participating.md)和获取更多工作流相关信息的选项，例如：

* **完成**  — 打开 **完成工作项目** 对话框

* **委派**  — 打开 **完成工作项目** 对话框

* **查看详细信息** - 打开工作流的&#x200B;**详细信息**&#x200B;窗口

通过通知栏完成和委派工作流步骤，与以下情况一样 [参与工作流](/help/sites-authoring/workflows-participating.md) 从“通知”收件箱中。

如果页面从属于多个工作流，则在通知的右侧端将显示工作流的数量，并且还提供有箭头按钮以允许您滚动浏览工作流。

![工作流数量通知](assets/chlimage_1-122.png)

## 组件占位符 {#component-placeholder}

组件占位符是一个指示器，用于显示组件在放置时占据的位置 - 在您当前悬停鼠标的组件上方显示。

* 将组件添加到页面时（从组件浏览器拖动）：

  ![添加新组件](assets/screen_shot_2018-03-22at111928.png)

* 移动现有组件时：

  ![移动现有组件](assets/screen_shot_2018-03-22at112445.png)

## 插入组件 {#inserting-a-component}

### 使用组件浏览器插入组件 {#inserting-a-component-from-the-components-browser}

您可以使用添加组件 [组件浏览器](/help/sites-authoring/author-environment-tools.md#components-browser). [组件占位符](#component-placeholder)显示组件的位置：

1. 确保页面处于&#x200B;[**编辑**&#x200B;模式](/help/sites-authoring/author-environment-tools.md#page-modes)。
1. 打开[组件浏览器](/help/sites-authoring/author-environment-tools.md#components-browser)。
1. 将所需的组件拖动到[所需位置](#component-placeholder)。

1. [编辑](#editmovecopypastedelete)组件。

>[!NOTE]
>
>在移动设备上，组件浏览器会填充整个屏幕。 开始拖动组件后，浏览器将关闭以再次显示页面，以便您可以放置组件。

### 使用段落系统插入组件 {#inserting-a-component-from-the-paragraph-system}

您可以使用添加组件 **将组件拖动到此处** 框的文字输入框：

1. 确保页面处于&#x200B;[**编辑**&#x200B;模式](/help/sites-authoring/author-environment-tools.md#page-modes)。
1. 有两种方法可以从段落系统中选择和添加组件：

   * 从现有组件的工具栏或&#x200B;**将组件拖动到此处**&#x200B;框中选择&#x200B;**插入组件**&#x200B;选项 (+)。

   ![插入组件选择](assets/screen_shot_2018-03-22at112536.png)

   * 如果您使用的是桌面设备，则可以双击 **将组件拖动到此处** 盒子。

   此 **插入新组件** 对话框打开，允许您选择所需的组件：

   ![插入新组件](assets/screen_shot_2018-03-22at112650.png)

1. 选定的组件会添加到页面底部。根据需要[编辑](#editmovecopypastedelete)组件。

### 使用资源浏览器插入组件 {#inserting-a-component-using-the-assets-browser}

您还可以通过从以下位置拖动资产，将组件添加到页面： [资产浏览器](/help/sites-authoring/author-environment-tools.md#assets-browser). 这会自动创建相应类型的组件（并包含资产）。

这适用于以下资产类型（某些资产类型取决于页面/段落系统）：

<table>
 <tbody>
  <tr>
   <th><strong>资产类型</strong></th>
   <th><strong>结果组件类型</strong></th>
  </tr>
  <tr>
   <td>图像</td>
   <td>图像</td>
  </tr>
  <tr>
   <td>文档</td>
   <td>下载</td>
  </tr>
  <tr>
   <td>产品</td>
   <td>产品</td>
  </tr>
  <tr>
   <td>视频</td>
   <td>闪光灯</td>
  </tr>
  <tr>
   <td>内容片段</td>
   <td>内容片段<br /> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>可针对您的安装配置此行为。请参阅 [配置段落系统以便拖动资产可创建组件实例](/help/sites-developing/developing-components.md#configuring-a-paragraph-system-so-that-dragging-an-asset-creates-a-component-instance) 以了解更多详细信息。

要通过拖动以上某一资源类型创建组件，请执行以下操作：

1. 确保页面处于&#x200B;[**编辑**&#x200B;模式](/help/sites-authoring/author-environment-tools.md#page-modes)。
1. 打开[资源浏览器](/help/sites-authoring/author-environment-tools.md#assets-browser)。
1. 将所需的资源拖动到所需位置。[组件占位符](#component-placeholder)显示组件的位置。

   此时会在所需位置创建与该资源类型对应的组件 - 组件包含选定的资源。

1. [编辑](#editmovecopypastedelete) 组件（如有必要）。

>[!NOTE]
>
>在移动设备上，资产浏览器会填充整个屏幕。 开始拖动资产时，浏览器将关闭以再次显示页面，以便您可以放置资产。

在浏览资产时，如果您发现必须对资产进行快速更改，请单击资产名称旁边的编辑图标以开始 [资产编辑器](/help/assets/manage-assets.md).

![编辑图标](assets/screen_shot_2018-03-22at112735.png)

## 编辑/配置/复制/剪切/删除/粘贴 {#edit-configure-copy-cut-delete-paste}

选择组件会打开工具栏。 这提供了对可对组件执行的各种操作的访问权限。

用户实际可用的操作会根据相应的情况来显示，此处并未介绍所有这些操作。

![组件工具栏选项](assets/screen_shot_2018-03-22at112909.png)

* **编辑**

  [根据组件类型](/help/sites-authoring/default-components.md)，这将允许您[编辑组件的内容。](#edit-content)通常会提供一个工具栏。

  ![编辑](do-not-localize/screen_shot_2018-03-22at112936.png)

* **配置**

  [取决于组件类型](/help/sites-authoring/default-components.md) 这使您可以编辑和配置组件的属性。 通常会打开一个对话框。

  ![配置](do-not-localize/screen_shot_2018-03-22at112955.png)

* **复制**

  这会将组件复制到剪贴板。 粘贴后，原始组件将保留。

  ![复制](do-not-localize/screen_shot_2018-03-22at113000.png)

* **剪切**

  这会将组件复制到剪贴板。 粘贴操作完成后，原始组件会被移除。

  ![剪切](assets/screen_shot_2018-03-22at113007.png)

* **删除**

  这将从包含您确认的页面中删除组件。

  ![删除](do-not-localize/screen_shot_2018-03-22at113012.png)

* **插入组件**

  这将打开对话框，您可以 [添加组件](/help/sites-authoring/editing-content.md#inserting-a-component-from-the-paragraph-system).

  ![插入组件](do-not-localize/screen_shot_2018-03-22at113017.png)

* **粘贴**

  此操作可将组件从剪贴板粘贴到页面。 原稿是否保留取决于您使用的是复制还是剪切。

   * 您可以粘贴到同一页面或其他页面。
   * 粘贴的项目会被粘贴到选择粘贴操作时所在的项目上方。
   * 仅当剪贴板上有内容时，才会显示“粘贴”操作。

  ![粘贴](assets/screen_shot_2018-03-22at113553.png)

  >[!NOTE]
  >
  >如果粘贴到剪切/复制操作之前已打开的其他页面，则必须刷新该页面才能看到粘贴的内容。

* **组**

  此操作让您一次选择多个组件。在桌面设备上&#x200B;**按住 Ctrl 并单击**&#x200B;或&#x200B;**按住 Command 并单击**&#x200B;可实现同样的操作。

  ![组](do-not-localize/screen_shot_2018-03-22at113240.png)

* **父项**

  此项让您选择选定组件的父组件。

  ![父项](assets/screen_shot_2018-03-22at113028.png)

* **布局**

  让您修改选定组件的[布局](/help/sites-authoring/editing-content.md#edit-component-layout)。此操作仅适用于选定组件，而不会激活整个页面的[布局模式](/help/sites-authoring/author-environment-tools.md#page-modes)。

  ![布局](do-not-localize/screen_shot_2018-03-22at113044.png)

* **转换为体验片段变量**

  这让您能够创建 [体验片段](/help/sites-authoring/experience-fragments.md) 或将它添加到现有的体验片段中。

  ![转换为体验片段变量](do-not-localize/screen_shot_2018-03-22at113033.png)

## 编辑（内容） {#edit-content}

在组件中添加或编辑内容的方法有两种：

* 打开[组件编辑对话框](#component-edit-dialog)。
* 通过从资源浏览器中[拖放资源](#draganddropintocomponent)来直接添加内容。

### 组件编辑对话框 {#component-edit-dialog}

您可以打开组件以使用组件工具栏 [的编辑（铅笔）图标编辑内容](#edit-configure-copy-cut-delete-paste)。

确切的编辑选项取决于组件。 对于某些组件， [所有操作仅在全屏模式下可用](#edit-content-full-screen-mode). 例如：

* [文本组件](/help/sites-authoring/rich-text-editor.md#main-pars-title-24)

  ![文本组件](assets/screen_shot_2018-03-22at120215.png)

* 图像组件

  ![图像组件](assets/screen_shot_2018-03-22at120252.png)

  >[!NOTE]
  >
  >无法对空的图像组件执行编辑操作。
  >
  >
  >[拖动或上传图像（使用“配置”）](/help/sites-authoring/default-components-foundation.md#image) 然后才能开始编辑。

* 图像组件 - 全屏

  [进入图像组件的全屏模式](/help/sites-authoring/editing-content.md#edit-content-full-screen-mode) ，可以留出更多空间来编辑图像，并显示额外的编辑选项，如“启动映射”和“重 **置缩放”******。此外，全屏模式还允许选择裁剪预设。

  ![图像组件全屏](assets/screen_shot_2018-03-22at120529.png)

* 由多个基本组件构建的组件，例如 [文本与图像基础组件](/help/sites-authoring/default-components-foundation.md#text-image)，首先要求您确认所需的编辑选项集：

  ![组件编辑选项](assets/chlimage_1-123.png)

### 将资源拖放到组件中 {#drag-and-drop-assets-into-component}

对于特定的组件类型，您可以将资产直接从资产浏览器拖放到组件中来更新内容：

| **资产类型** | **组件类型** |
|---|---|
| 图像 | 图像 |
| 文档 | 下载 |
| 产品 | 产品 |
| 视频 | 闪光灯 |
| 内容片段 | 内容片段 |

## 编辑（内容）全屏模式 {#edit-content-full-screen-mode}

对于所有组件，都可以通过以下图标进入（和退出）全屏模式：

![编辑全屏模式](do-not-localize/chlimage_1-20.png)

例如，**文本**&#x200B;组件：

![文本编辑器](assets/screen_shot_2018-03-22at121616.png)

>[!NOTE]
>
>对于某些组件，全屏模式比基本的就地编辑器具有更多的可用选项。

## 移动组件 {#moving-a-component}

要移动段落组件，请执行以下操作：

1. 通过点按住或单击并按住来选择要移动的段落。
1. 将段落拖到新位置。AEM 指示该段落可以存放的位置。将其放在您想要的位置。

   ![移动段落组件](assets/screen_shot_2018-03-22at121821.png)

1. 此时会移动您的段落。

>[!NOTE]
>
>您也可以使用[剪切并粘贴](/help/sites-authoring/editing-content.md#edit-configure-copy-cut-delete-paste)来移动组件。

## 编辑组件布局 {#edit-component-layout}

无需反复从编辑切换到 [布局模式](/help/sites-authoring/responsive-layout.md) 要调整组件，可以选择 **布局** 用于组件更改该组件布局的操作。 由于不必离开编辑模式，这节省了时间。

1. 当在 **编辑** 在站点控制台的模式下，选择某个组件会显示该组件的工具栏。

   ![表单中的编辑模式](assets/screen_shot_2018-03-22at133756.png)

   单击或点按 **布局** 操作，以便您可以调整组件的布局。

   ![组件工具栏](do-not-localize/chlimage_1-21.png)

1. 在选择“布局”操作后：

   * 将显示用于调整组件大小的手柄。
   * 在屏幕的顶部将显示模拟器工具栏。
   * 在组件工具栏中将显示布局操作而不是标准编辑操作。

   ![在多个设备上预览表单](assets/screen_shot_2018-03-22at133843.png)

   此时，您便可以像在[布局模式](/help/sites-authoring/responsive-layout.md#defining-layouts-layout-mode)中一样修改组件布局。

1. 进行必要的布局更改后，单击 **关闭** 在组件操作菜单中，停止修改组件的布局。 组件的工具栏会返回到其正常的编辑状态。

   ![关闭](do-not-localize/screen_shot_2018-03-22at133920.png)

>[!NOTE]
>
>“布局”操作仅限用于选定的组件。例如，如果您正在编辑一个组件的布局，然后选择另一个组件，则将为新选择的组件显示标准编辑工具栏（而非布局工具栏）。 调整大小手柄和模拟器工具栏消失。
>
>如果必须编辑页面的整体布局，并且会影响多个组件，请切换到 [布局模式](/help/sites-authoring/responsive-layout.md).

## 继承组件 {#inherited-components}

继承组件可能是多种情况的产物，包括：

* [多站点管理](/help/sites-administering/msm.md)
* [启动项](/help/sites-authoring/launches.md)（当基于 Live Copy 时）。
* 特定组件，例如Geometrixx中的继承段落系统。

您可以取消（随后也可以重新启用）继承。根据组件，可以从以下位置执行此操作：

* **Live Copy**

  如果组件位于Live Copy或启动项的一部分（基于Live Copy）的页面上，则为组件工具栏。 例如：

  ![Live Copy](assets/screen_shot_2018-03-22at134339.png)

  取消继承选项可用：

  ![取消继承](do-not-localize/screen_shot_2018-03-22at134406.png)

  或者，如果已取消，则重新启用继承：

  ![重新启用继承](do-not-localize/screen_shot_2018-03-22at134417.png)

  转出操作也在Blueprint或Live Copy源中可用：

  ![转出](do-not-localize/screen_shot_2018-03-22at134516.png)

* **继承的段落系统**

  配置对话框。 例如，与继承的段落系统一样：

  ![继承的段落系统](assets/chlimage_1-124.png)

## 编辑页面模板 {#editing-the-page-template}

如果页面基于 [可编辑模板](/help/sites-authoring/templates.md#editable-and-static-templates)，您可以轻松切换到 [模板编辑器](/help/sites-authoring/templates.md#editing-templates-template-authors) 通过选择 **编辑模板** 在 [“页面信息”菜单](/help/sites-authoring/author-environment-tools.md#page-information).

如果页面基于 [静态模板](/help/sites-authoring/templates.md#editable-and-static-templates)，您可以切换到 [设计模式](/help/sites-authoring/default-components-designmode.md) 使用 [页面模式选择器](/help/sites-authoring/author-environment-tools.md#page-modes) 工具栏上的来启用/禁用要在页面上使用的组件。

在[列视图](/help/sites-authoring/basic-handling.md#column-view)或[列表视图](/help/sites-authoring/basic-handling.md#list-view)中选择页面时，您可以轻松查看该页面所基于的模板。

## Live Copy 状态 {#live-copy-status}

[“Live Copy 状态”页面模式](/help/sites-authoring/author-environment-tools.md#page-modes)允许快速查看 Live Copy 状态以及继承/未继承的组件。

* 绿色边框：已继承
* 粉色边框：继承已取消

例如：

![Live Copy继承状态](assets/screen_shot_2018-03-22at134820.png)

## 添加注释 {#adding-annotations}

[注释](/help/sites-authoring/annotations.md)允许审核者和其他作者对内容提出反馈。该功能通常作审核和验证之用。

## 预览页面 {#previewing-pages}

可通过以下两个选项预览页面：

* [预览模式](#preview-mode) - 快速就地预览

* [查看已发布的项目](#view-as-published) - 在新选项卡中打开页面的完整预览

>[!NOTE]
>
>* 链接会在内容中显示，但在“编辑”模式下无法访问。
>* 如果您希望使用链接进行导航，请使用任一预览选项。
>* 使用[键盘快捷键](/help/sites-authoring/keyboard-shortcuts.md) `Ctrl-Shift-M` 可在预览和最后选择的模式之间切换。
>

>[!NOTE]
>
>这两个选项均可设置WCM模式Cookie。

### 预览模式 {#preview-mode}

编辑内容时，您可以使用预览来预览页面 [模式](/help/sites-authoring/author-environment-tools.md#page-modes). 利用此模式，可执行以下操作：

* 隐藏各种编辑机制，以便您可以快速查看页面在发布时的显示方式。
* 使用链接进行导航。
* 确实如此 **非** 刷新页面内容。

进行创作时，可以使用页面编辑器右上角的图标进入预览模式：

![预览](assets/chlimage_1-125.png)

### 以发布的形式查看 {#view-as-published}

**查看已发布的项目**&#x200B;选项可从[页面信息](/help/sites-authoring/author-environment-tools.md#page-information)菜单中获取。这将在新选项卡中打开页面，刷新内容，并会在发布时显示该页面。

## 锁定页面 {#locking-a-page}

AEM允许您锁定页面，这样其他人就无法修改页面内容。 当您要对某个特定页面进行大量编辑，或者必须冻结页面一段时间时，此功能非常有用。

可以通过以下任一方式锁定页面：

* **Sites**&#x200B;控制台

   1. 在[选择模式](/help/sites-authoring/basic-handling.md#viewing-and-selecting-resources)中选择页面。
   1. 选择锁定图标。

  ![“锁定”图标](assets/screen_shot_2018-03-22at134928.png)

* **页面编辑器**

   1. 要打开菜单，请选择 **页面信息** 图标。
   1. 选择&#x200B;**锁定页面**&#x200B;选项。

锁定后，控制台视图信息便会更新；编辑时，工具栏中会出现锁定符号。

![锁定符号](assets/screen_shot_2018-03-22at135010.png)

>[!CAUTION]
>
>在以下情况下可以执行锁定页面 [模拟用户](/help/sites-administering/security.md#impersonating-another-user). 但是，以这种方式锁定的页面只能由被模拟的用户或管理员用户解锁。
>
>无法通过模拟锁定页面的用户的身份来解锁页面。

## 解锁页面 {#unlocking-a-page}

解锁页面的过程类似于 [锁定页面](#locking-a-page). 锁定页面后，锁定选项将被替换为解锁操作。

“页面信息”菜单会将&#x200B;**解锁**&#x200B;列为一个选项，并且 Sites 控制台中的“锁定”图标会被替换为&#x200B;**解锁**&#x200B;图标。

![解锁](assets/screen_shot_2018-03-22at134942.png)

>[!CAUTION]
>
>在以下情况下可以执行锁定页面 [模拟用户](/help/sites-administering/security.md#impersonating-another-user). 但是，以这种方式锁定的页面只能由被模拟的用户或管理员用户解锁。
>
>无法通过模拟锁定页面的用户的身份来解锁页面。

## 撤消和重做页面编辑 {#undoing-and-redoing-page-edits}

您可以通过以下图标撤消或重做某项操作。 在适当的时候，这些内容会显示在工具栏中：

![“撤消”和“重做”](do-not-localize/screen_shot_2018-03-23at093614.png)

>[!NOTE]
>
>也可使用[键盘快捷键](/help/sites-authoring/page-authoring-keyboard-shortcuts.md) `Ctrl-Z` 撤消页面编辑操作。
>
>也可使用键盘快捷键 `Ctrl-Y` 重做页面编辑操作。

>[!NOTE]
>
>有关撤消和重做页面编辑时可执行操作的完整详细信息，请参阅[撤消和重做页面编辑 - 理论](#undoing-and-redoing-page-edits-the-theory)。

## 撤消和重做页面编辑 – 理论 {#undoing-and-redoing-page-edits-the-theory}

>[!NOTE]
>
>您的系统管理员可以 [配置撤消/重做功能的各个方面](/help/sites-administering/config-undo.md) 根据您实例的要求。

AEM会存储您执行的操作的历史记录以及执行操作的顺序。 这项功能意味着您可以按照执行顺序撤消多个操作，并在必要时重做它们，以重新应用一个或多个操作。

如果选择了内容页面上的某个元素（例如文本组件），则撤消和重做命令将适用于选定的项目。

撤消和重做命令的行为与其他软件程序中的类似。 在您决定内容时，可使用命令恢复网页的最近状态。 例如，如果您将文本段落移至页面上的其他位置，可以使用撤消命令移回该段落。如果您稍后又认定之前的位置更好，可使用重做命令“撤消之前的撤消操作”。

>[!NOTE]
>
>您可以：
>
>* 只要您在执行撤消操作之后没有进行任何页面编辑，就可以执行重做操作。
>* 最多可撤消 20 次编辑操作（默认设置）。
>* 也可以使用[键盘快捷键](/help/sites-authoring/page-authoring-keyboard-shortcuts.md)执行撤消和重做操作。
>

您可以对以下类型的页面更改使用“撤消”和“重做”：

* 添加、编辑、删除和移动段落
* 段落内容的就地编辑
* 在页面内复制、剪切和粘贴项目

表单组件呈现的表单字段并不意味着在创作页面时指定值。 因此，“撤消”和“重做”命令不会影响您对这些类型组件的值所做的更改。 例如，无法撤消在下拉列表中选择值的操作。

>[!NOTE]
>
>对文件和图像的更改执行撤消和重做操作需要特殊的权限。

>[!NOTE]
>
>对文件和图像进行更改的历史记录将保留至少 10 个小时。然而，在这段时间之后，改变的逆转并非板上钉钉。 您的管理员可以更改 10 个小时的默认保留时间。
