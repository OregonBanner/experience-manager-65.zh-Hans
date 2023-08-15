---
title: 编辑页面内容
description: 使用可拖放到页面上的组件来添加内容。 然后，可以就地编辑、移动或删除这些内容。
uuid: e7b65ceb-263c-46f2-91e3-11dec3a016fa
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: de321869-ebf9-41a1-8203-e12bdb088678
docset: aem65
exl-id: e1b5aea0-983c-4e7b-9d35-d7beeee45dc7
source-git-commit: 50d29c967a675db92e077916fb4adef6d2d98a1a
workflow-type: tm+mt
source-wordcount: '1832'
ht-degree: 17%

---

# 编辑页面内容{#editing-page-content}

创建页面（新页面或者作为启动项或 Live Copy 的一部分）后，您可以编辑内容，以进行所需的更新。

内容使用可拖动到页面上的[组件](/help/sites-classic-ui-authoring/classic-page-author-default-components.md)（适用于内容类型）进行添加。然后，可以就地编辑、移动或删除这些内容。

>[!NOTE]
>
>您的帐户需要 [适当的访问权限](/help/sites-administering/security.md) 和 [权限](/help/sites-administering/security.md#permissions) 编辑页面；例如，添加、编辑或删除组件、注释、解锁。
>
>如果您遇到任何问题，我们建议您与系统管理员联系。

## Sidekick {#sidekick}

Sidekick是创作页面时的关键工具。 在创作页面时，它会浮动，因此始终可见。

提供了多个选项卡和图标，包括：

* 组件
* 页面
* 信息
* 版本控制
* 工作流
* 模式
* 基架
* ClientContext
* 网站

![chlimage_1-71](assets/chlimage_1-71.png)

它们提供了对多种功能的访问；包括：

* [选择组件](/help/sites-classic-ui-authoring/classic-page-author-env-tools.md#sidekick)
* [显示引用](/help/sites-classic-ui-authoring/classic-page-author-env-tools.md#showing-references)
* [访问审核日志](/help/sites-classic-ui-authoring/classic-page-author-env-tools.md#audit-log)
* [切换模式](/help/sites-classic-ui-authoring/classic-page-author-env-tools.md#page-modes)
* [创建](/help/sites-classic-ui-authoring/classic-page-author-work-with-versions.md#creating-a-new-version)， [正在恢复](/help/sites-classic-ui-authoring/classic-page-author-work-with-versions.md#restoring-a-page-version-from-sidekick) 和 [比较](/help/sites-classic-ui-authoring/classic-page-author-work-with-versions.md#comparing-with-a-previous-version) 版本

* [发布](/help/sites-classic-ui-authoring/classic-page-author-publish-pages.md#publishing-a-page)， [取消发布](/help/sites-classic-ui-authoring/classic-page-author-publish-pages.md#unpublishing-a-page) 页面

* [编辑页面属性](/help/sites-classic-ui-authoring/classic-page-author-edit-page-properties.md)

* [基架](/help/sites-authoring/scaffolding.md)

* [客户端上下文](/help/sites-administering/client-context.md)

## 插入组件 {#inserting-a-component}

### 插入组件 {#inserting-a-component-1}

打开页面后，您可以开始添加内容。 可通过添加组件（也称为段落）来实现这一点。

要插入新组件：

1. 有多种方法可用于选择要插入的段落类型：

   * 双击标记为的区域 **将组件或资源拖动到此处……** - **插入新组件** 工具栏打开。 选择元件并单击 **确定**.

   * 从浮动工具栏中拖动组件（称为sidekick）以插入新段落。
   * 右键单击现有段落并选择 **新建……**  — 插入新组件工具栏打开。 选择元件并单击 **确定**.

   ![screen_shot_2012-02-15at115605am](assets/screen_shot_2012-02-15at115605am.png)

1. 在副手和 **插入新组件** 工具栏您会看到可用组件（段落类型）的列表。 它们可以拆分为不同的部分（例如，常规、列等），可以根据需要展开这些部分。

   根据您的生产环境，这些选项可能会有所不同。 有关组件的完整详细信息，请参阅 [默认组件](/help/sites-classic-ui-authoring/classic-page-author-default-components.md).

1. 在页面上插入所需的组件。 然后双击该段落，将打开一个窗口，允许您配置段落并添加内容。

### 使用内容查找器插入组件 {#inserting-a-component-using-the-content-finder}

您还可以通过从以下位置拖动资产，向页面中添加新组件： [内容查找器](/help/sites-classic-ui-authoring/classic-page-author-env-tools.md#the-content-finder). 这将自动创建包含该资产的相应类型的新组件。

这适用于以下资产类型（某些资产取决于页面/段落系统）：

| 资产类型 | 结果组件类型 |
|---|---|
| 图像 | 图像 |
| 文档 | 下载 |
| 产品 | 产品 |
| 视频 | 闪光灯 |

>[!NOTE]
>
>可针对您的安装配置此行为。请参阅 [配置段落系统以便拖动资产可创建组件实例](/help/sites-developing/developing-components.md#configuring-a-paragraph-system-so-that-dragging-an-asset-creates-a-component-instance) 以了解更多详细信息。

要通过拖动以上某一资源类型创建组件，请执行以下操作：

1. 确保页面处于&#x200B;[**编辑**&#x200B;模式](/help/sites-classic-ui-authoring/classic-page-author-env-tools.md#page-modes)。
1. 打开 [内容查找器](/help/sites-classic-ui-authoring/classic-page-author-env-tools.md#the-content-finder).
1. 将所需的资源拖动到所需位置。此 [组件占位符](#componentplaceholder) 显示组件的放置位置。

   将在所需位置创建一个适合该资源类型的组件 — 该组件将包含选定的资源。

1. 根据需要[编辑](#editmovecopypastedelete)组件。

## 编辑组件（内容和属性） {#editing-a-component-content-and-properties}

要编辑现有段落，请执行下列操作之一：

* **双击** 打开该段落的链接。 您会看到与创建包含现有内容的段落时相同的窗口。 进行更改并单击 **确定**.

* **右键单击** 段落并单击 **编辑**.

* **单击** 在段落上单击两次（缓慢双击）以进入就地编辑模式。 您将能够直接编辑页面上的文本，而不是在对话框窗口中编辑。 在此模式下，将为您提供位于页面顶部的工具栏。 只需进行更改，更改将自动保存。

## 移动组件 {#moving-a-component}

要移动段落，请执行以下操作：

>[!NOTE]
>
>您也可以使用[剪切并粘贴](#cut-copy-paste-a-component)来移动组件。

1. 选择要移动的段落：

   ![screen_shot_2012-02-15at115855am](assets/screen_shot_2012-02-15at115855am.png)

1. 将段落拖动到新位置 — AEM使用绿色复选标记指示可以将段落移动到何处。 将其放在您想要的位置。
1. 此时会移动您的段落：

   ![screen_shot_2012-02-15at120030pm](assets/screen_shot_2012-02-15at120030pm.png)

## 删除组件 {#deleting-a-component}

要删除段落，请执行以下操作：

1. 选择段落并 **右键单击**：

   ![screen_shot_2012-02-15at120220pm](assets/screen_shot_2012-02-15at120220pm.png)

1. 选择 **删除** 菜单。 AEM WCM请求确认您要删除段落，因为此操作无法撤消。
1. 单击&#x200B;**确定**。

>[!NOTE]
>
>如果您已设置 [用户属性，显示全局编辑工具栏](/help/sites-classic-ui-authoring/author-env-user-props.md) 您还可以对段落执行某些操作，方法是使用 **复制**， **剪切**， **粘贴**， **删除** 按钮可用。
>
>各种 [键盘快捷键](/help/sites-classic-ui-authoring/classic-page-author-keyboard-shortcuts.md) 也提供。

## 剪切/复制/粘贴组件 {#cut-copy-paste-a-component}

作为时间 [删除组件](#deleting-a-component) 您可以使用上下文菜单复制、剪切和/或粘贴组件

>[!NOTE]
>
>如果您已设置 [用户属性，显示全局编辑工具栏](/help/sites-classic-ui-authoring/author-env-user-props.md) 您还可以对段落执行某些操作，方法是使用 **复制**， **剪切**， **粘贴**， **删除** 按钮可用。
>
>各种 [键盘快捷键](/help/sites-classic-ui-authoring/classic-page-author-keyboard-shortcuts.md) 也提供。

>[!NOTE]
>
>仅支持在同一页面中剪切、复制和粘贴内容。

## 继承组件 {#inherited-components}

继承组件可能是多种情况的产物，包括：

* [多站点管理](/help/sites-administering/msm.md)；也与 [基架](/help/sites-classic-ui-authoring/classic-feature-scaffolding.md#scaffolding-with-msm-inheritance).

* [启动次数](/help/sites-classic-ui-authoring/classic-launches.md) （当基于livecopy时）。
* 特定组件；例如Geometrixx中的继承段落系统。

您可以取消（随后也可以重新启用）继承。根据组件，可以从以下位置执行此操作：

1. **Live Copy**

   如果组件是livecopy或launch的一部分，则它由一个挂锁图标指示。 您可以单击挂锁取消继承。

   * 选择组件后，将显示挂锁图标；例如：

   ![chlimage_1-72](assets/chlimage_1-72.png)

   * 挂锁也显示在组件的对话框中；例如：

   ![chlimage_1-73](assets/chlimage_1-73.png)

1. **继承的段落系统**

   配置对话框。 例如，与Geometrixx中的继承段落系统一样：

   ![chlimage_1-74](assets/chlimage_1-74.png)

## 添加注释 {#adding-annotations}

[注释](/help/sites-classic-ui-authoring/classic-page-author-annotations.md) 允许其他作者提供关于您的内容的反馈。 这通常用于审阅和验证。

## 预览页面 {#previewing-pages}

Sidekick的底部边框中有两个对预览页面很重要的图标：

![副手的底部边框，水平行由七个图标组成。 行开头的两个图标（编辑图标和预览模式图标）分别由铅笔符号和放大镜符号表示。](do-not-localize/chlimage_1-5.png)

* 铅笔图标显示您当前处于编辑模式，您可以在其中添加、修改、移动或删除内容。

  ![铅笔符号指示的编辑图标。](do-not-localize/chlimage_1-6.png)

* 利用放大镜图标，可选择预览模式，在该模式下页面会显示在发布环境中（有时还需要刷新页面）：

  ![由放大镜符号指示的预览模式图标。](do-not-localize/chlimage_1-7.png)

  在预览模式下，Sidekick将被减少，单击向下箭头图标以返回编辑模式：

  ![以AEM为标题的栏，标题右侧显示一个编辑模式图标，该图标由向下箭头符号指示。](do-not-localize/chlimage_1-8.png)

## 查找并替换 {#find-replace}

要更大规模地编辑相同的短语a **[查找并替换](/help/sites-classic-ui-authoring/author-env-search.md#find-and-replace)** 菜单选项允许您在网站的部分中搜索和替换字符串的多个实例。

## 锁定页面 {#locking-a-page}

AEM允许您锁定页面，这样其他人就无法修改页面内容。 当您要对某个特定页面进行大量编辑，或者需要冻结页面一段时间时，此功能非常有用。

>[!CAUTION]
>
>锁定页面时应谨慎使用，因为只有锁定页面的人（或具有管理员权限的帐户）才能解锁页面。

锁定页面：

1. 在 **网站** 选项卡，选择要锁定的页面。
1. 双击页面以将其打开以进行编辑。
1. 在 **页面** Sidekick的选项卡，选择 **锁定页面**：

   ![screen_shot_2012-02-08at15750pm](assets/screen_shot_2012-02-08at15750pm.png)

   此时将显示一条消息，表明您的页面已被其他用户锁定。 此外，在 **网站** 控制台中，AEM WCM将页面显示为已锁定，并指示哪个用户已锁定该页面。

   ![screen_shot_2012-02-08at20657pm](assets/screen_shot_2012-02-08at20657pm.png)

## 解锁页面 {#unlocking-a-page}

要解锁页面，请执行以下操作：

1. 在 **网站** 选项卡，选择要解锁的页面。
1. 双击页面以将其打开。
1. 在 **页面** Sidekick的选项卡，选择 **解锁页面**.

## 撤消和重做页面编辑 {#undoing-and-redoing-page-edits}

当页面的内容框架具有焦点时，使用以下键盘快捷键：

* 撤消：Ctrl+Z (Windows)或Cmd+Z (Mac)
* 重做：Ctrl+Y (Windows)或Cmd+Y (Mac)

当您撤消或重做一个或多个段落的移除、添加或重新定位时，闪烁（默认行为）高亮显示将指示受影响的段落。

>[!NOTE]
>
>有关撤消和重做页面编辑时可执行操作的完整详细信息，请参阅[撤消和重做页面编辑 - 理论](#undoing-and-redoing-page-edits-the-theory)。

## 撤消和重做页面编辑 – 理论 {#undoing-and-redoing-page-edits-the-theory}

>[!NOTE]
>
>您的系统管理员可以 [配置撤消/重做功能的各个方面](/help/sites-administering/config-undo.md) 根据您实例的要求。

AEM会存储您执行的操作的历史记录以及执行操作的顺序。 因此，您可以按照执行顺序撤消多个操作。 然后，可以使用重做重新应用一个或多个操作。

如果选择了内容页面上的某个元素，则撤消和重做命令将应用于所选项目，如文本组件。

撤消和重做命令的行为与其他软件程序中的类似。 在做出内容决策时，可使用命令恢复网页的最新状态。 例如，如果您将文本段落移至页面上的其他位置，可以使用撤消命令移回该段落。如果随后再次决定移动段落，请使用重做命令。

>[!NOTE]
>
>您可以：
>
>* 重做操作，只要您在使用撤消后未进行任何页面编辑即可。
>* 撤消最多20个编辑操作（默认设置）。
>* 还使用 [键盘快捷键](/help/sites-classic-ui-authoring/classic-page-author-keyboard-shortcuts.md) 用于撤消和重做。
>

您可以对以下类型的页面更改使用撤消和重做：

* 添加、编辑、删除和移动段落
* 段落内容的就地编辑
* 在页面内复制、剪切和粘贴项目
* 跨页面复制、剪切和粘贴项目
* 添加、删除和更改文件和图像
* 添加、删除和更改注释和草图
* 对基架的更改
* 添加和删除引用
* 更改组件对话框中的属性值。

表单组件呈现的表单字段并不意味着在创作页面时指定值。 因此，“撤消”和“重做”命令不会影响您对这些类型组件的值所做的更改。 例如，无法撤消在下拉列表中选择值的操作。

>[!NOTE]
>
>对文件和图像的更改执行撤消和重做操作需要特殊的权限。此外，撤消文件和图像更改的历史记录至少会持续几个小时。 但在超过此时间后，将无法保证可以撤消这些更改。您的管理员可以提供权限并更改十小时的默认时间。
