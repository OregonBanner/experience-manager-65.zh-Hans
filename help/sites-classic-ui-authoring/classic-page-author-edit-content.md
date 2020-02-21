---
title: 编辑页面内容
seo-title: 编辑页面内容
description: 内容使用可拖动到页面上的组件进行添加。然后，可以就地编辑、移动或删除这些内容。
seo-description: 内容使用可拖动到页面上的组件进行添加。然后，可以就地编辑、移动或删除这些内容。
uuid: e7b65ceb-263c-46f2-91e3-11dec3a016fa
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: de321869-ebf9-41a1-8203-e12bdb088678
docset: aem65
translation-type: tm+mt
source-git-commit: 71b1301faf3ea3d881bcbf34eac101f3ed5c514c

---


# 编辑页面内容{#editing-page-content}

创建页面（新页面或者作为启动项或 Live Copy 的一部分）后，您可以编辑内容，以进行所需的更新。

内容使用可拖动到页面上的[组件](/help/sites-classic-ui-authoring/classic-page-author-default-components.md)（适用于内容类型）进行添加。然后，可以就地编辑、移动或删除这些内容。

>[!NOTE]
>
>要编辑页面，您的帐户必须拥有[适当的访问权利](/help/sites-administering/security.md)和[权限](/help/sites-administering/security.md#permissions)；例如，在添加、编辑或删除组件，添加注释以及执行解锁等操作时。
>
>如果您遇到任何问题，我们建议您与系统管理员联系。

## Sidekick {#sidekick}

在创作页面时，Sidekick 是一项重要工具。创作页面时 Sidekick 将处于浮动状态，所以始终可见。

可用的一些选项卡和图标包括：

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

这些对象提供了丰富的功能，包括：

* [选择组件](/help/sites-classic-ui-authoring/classic-page-author-env-tools.md#sidekick)
* [显示引用](/help/sites-classic-ui-authoring/classic-page-author-env-tools.md#showing-references)
* [访问审查日志](/help/sites-classic-ui-authoring/classic-page-author-env-tools.md#audit-log)
* [切换模式](/help/sites-classic-ui-authoring/classic-page-author-env-tools.md#page-modes)
* [创建](/help/sites-classic-ui-authoring/classic-page-author-work-with-versions.md#creating-a-new-version)、[恢复](/help/sites-classic-ui-authoring/classic-page-author-work-with-versions.md#restoring-a-page-version-from-sidekick)和[比较](/help/sites-classic-ui-authoring/classic-page-author-work-with-versions.md#comparing-with-a-previous-version)版本

* [发布](/help/sites-classic-ui-authoring/classic-page-author-publish-pages.md#publishing-a-page)和[取消发布](/help/sites-classic-ui-authoring/classic-page-author-publish-pages.md#unpublishing-a-page)页面

* [编辑页面属性](/help/sites-classic-ui-authoring/classic-page-author-edit-page-properties.md)

* [基架](/help/sites-authoring/scaffolding.md)

* [客户端上下文](/help/sites-administering/client-context.md)

## 插入组件 {#inserting-a-component}

### 插入组件 {#inserting-a-component-1}

打开页面后，便可开始添加内容。可通过添加组件（也叫做段落）实现。

要插入新组件，请执行以下操作：

1. 可通过若干种方法来选择要插入的段落类型：

   * 双击标有&#x200B;**将组件或资产拖动到此处...** 的区域 - **插入新组件**&#x200B;工具栏将会打开。选择一个组件并单击“**确定**”。

   * 从浮动的工具栏（称为 Sidekick）中拖动组件，以插入新段落。
   * 右键单击现有段落并选择“**新建...**”-“插入新组件”工具栏将会打开。选择一个组件并单击“**确定**”。
   ![screen_shot_2012-02-15at115605am](assets/screen_shot_2012-02-15at115605am.png)

1. 在 Sidekick 和&#x200B;**插入新组件**&#x200B;工具栏中，您会看到可用组件（段落类型）的列表。这些段落类型可能划分为不同部分（例如，“常规”、“列”等），可根据需要展开这些部分。

   根据生产环境的差异，这些选项可能会有所不同。有关组件的完整详细信息，请参阅[默认组件](/help/sites-classic-ui-authoring/classic-page-author-default-components.md)。

1. 在页面中插入所需组件。然后双击段落，此时将打开一个窗口，在此可以配置段落和添加内容。

### 使用内容查找器插入组件 {#inserting-a-component-using-the-content-finder}

您还可以通过从[内容查找器](/help/sites-classic-ui-authoring/classic-page-author-env-tools.md#the-content-finder)拖动资产来向页面添加新组件。这将自动创建包含资产的相应类型新组件。

此操作适用于以下资产类型（其中一些类型取决于页面/段落系统）：

| 资产类型 | 生成的组件类型 |
|---|---|
| 图像 | 图像 |
| 文档 | 下载 |
| 产品 | 产品 |
| 视频 | Flash |

>[!NOTE]
>
>可针对您的安装配置此行为。有关更多详细信息，请参阅[配置段落系统以便可通过拖动资产创建组件实例](/help/sites-developing/developing-components.md#configuring-a-paragraph-system-so-that-dragging-an-asset-creates-a-component-instance)。

要通过拖动以上某一资产类型创建组件，请执行以下操作：

1. 确保页面处于[**编辑&#x200B;**模式](/help/sites-classic-ui-authoring/classic-page-author-env-tools.md#page-modes)。
1. 打开[内容查找器](/help/sites-classic-ui-authoring/classic-page-author-env-tools.md#the-content-finder)。
1. 将所需的资产拖动到所需位置。[组件占位符](#componentplaceholder)显示组件在放置时将占据的位置。

   此时将在所需位置创建与该资产类型对应的组件 - 组件将包含选定的资产。

1. 根据需要[编辑](#editmovecopypastedelete)组件。

## 编辑组件（内容和属性） {#editing-a-component-content-and-properties}

要编辑现有段落，请执行以下操作之一：

* **双击**&#x200B;段落以将其打开。您会看到与使用现有内容创建段落时相同的窗口。进行更改并单击&#x200B;**确定**。

* **右键单击**&#x200B;段落并单击&#x200B;**编辑**。

* **单击**&#x200B;段落两次（缓慢双击）以进入就地编辑模式。您将能够直接在页面上编辑文本，而不是在对话框窗口中编辑。在此模式中，将在页面顶部提供一个工具栏。只需进行更改即可，系统将自动保存这些更改。

## 移动组件 {#moving-a-component}

要移动段落，请执行以下操作：

>[!NOTE]
>
>您也可以使用[剪切并粘贴](#cut-copy-paste-a-component)来移动组件。

1. 选择要移动的段落：

   ![screen_shot_2012-02-15at115855am](assets/screen_shot_2012-02-15at115855am.png)

1. 将段落拖至新位置 - AEM 用绿色选中标记指示可将段落移至的位置。将其拖动到所需位置。
1. 您的段落将被移动：

   ![screen_shot_2012-02-15at120030pm](assets/screen_shot_2012-02-15at120030pm.png)

## 删除组件 {#deleting-a-component}

要删除段落，请执行以下操作：

1. 选择段落并&#x200B;**单击鼠标右键**：

   ![screen_shot_2012-02-15at120220pm](assets/screen_shot_2012-02-15at120220pm.png)

1. 从菜单中选择&#x200B;**删除**。由于此操作无法撤消，因此 AEM WCM 会请您确认要删除段落。
1. 单击&#x200B;**确定**。

>[!NOTE]
>
>如果已经[将“用户属性”设置为显示“全局编辑工具栏”](/help/sites-classic-ui-authoring/author-env-user-props.md)，则还可以使用提供的&#x200B;**复制**、**剪切**、**粘贴**&#x200B;和&#x200B;**删除**&#x200B;按钮对段落执行某些操作。
>
>也可以使用各种[键盘快捷键](/help/sites-classic-ui-authoring/classic-page-author-keyboard-shortcuts.md)。

## 剪切/复制/粘贴组件 {#cut-copy-paste-a-component}

与[删除组件](#deleting-a-component)时一样，您可以使用上下文菜单复制、剪切和/或粘贴组件。

>[!NOTE]
>
>如果已经[将“用户属性”设置为显示“全局编辑工具栏”](/help/sites-classic-ui-authoring/author-env-user-props.md)，则还可以使用提供的&#x200B;**复制**、**剪切**、**粘贴**&#x200B;和&#x200B;**删除**&#x200B;按钮对段落执行某些操作。
>
>也可以使用各种[键盘快捷键](/help/sites-classic-ui-authoring/classic-page-author-keyboard-shortcuts.md)。

>[!NOTE]
>
>仅在同一页面内支持剪切、复制和粘贴内容。

## 继承组件 {#inherited-components}

继承组件可能是多种情况的产物，包括：

* [多站点管理](/help/sites-administering/msm.md)；还与[基架](/help/sites-classic-ui-authoring/classic-feature-scaffolding.md#scaffolding-with-msm-inheritance)相结合。

* [启动项](/help/sites-classic-ui-authoring/classic-launches.md)（当基于 Live Copy 时）。
* 特定组件；例如 Geometrixx 中的“继承的段落系统”。

您可以取消（随后也可以重新启用）继承。根据具体的组件，可从以下位置执行此操作：

1. **Live Copy**

   如果某个组件是 Live Copy 或启动项的一部分，则会由一个挂锁图标进行指示。单击挂锁图标可取消继承。

   * 选择组件后，将会显示挂锁图标；例如：
   ![chlimage_1-72](assets/chlimage_1-72.png)

   * 挂锁图标也会显示在组件的对话框中；例如：
   ![chlimage_1-73](assets/chlimage_1-73.png)

1. **继承的段落系统**

   配置对话框。例如，Geometrixx 中的“继承的段落系统”：

   ![chlimage_1-74](assets/chlimage_1-74.png)

## 添加注释 {#adding-annotations}

[注释](/help/sites-classic-ui-authoring/classic-page-author-annotations.md)允许其他作者对内容提出反馈。该功能通常作审核和验证之用。

## 预览页面 {#previewing-pages}

Sidekick 的底部边框中有两个对于预览页面很重要的图标：

![](do-not-localize/chlimage_1-5.png)

* 铅笔图标表示您目前处于编辑模式下，可以添加、修改、移动或删除内容。

   ![](do-not-localize/chlimage_1-6.png)

* 放大镜图标允许您选择预览模式，在该模式下页面的显示效果与其在发布环境中显示的效果一致（有时候还需要刷新页面）：

   ![](do-not-localize/chlimage_1-7.png)

   在预览模式下 Sidekick 将会简化显示，单击向下箭头图标可返回编辑模式：

   ![](do-not-localize/chlimage_1-8.png)

## 查找并替换 {#find-replace}

如果要对同一个短语执行较大规模的编辑，通过&#x200B;**[查找并替换](/help/sites-classic-ui-authoring/author-env-search.md#find-and-replace)**菜单选项，可在网站的某一部分中搜索并替换某一字符串的多个实例。

## 锁定页面 {#locking-a-page}

AEM 允许您锁定页面，以便其他人无法修改页面内容。当您对某个特定页面做出大量修改，或者需要冻结页面一段时间时，此功能非常有用。

>[!CAUTION]
>
>锁定页面时需要注意的是，只有锁定该页面的人（或者具有管理员权限的帐户）才能对其进行解锁。

要锁定页面，请执行以下操作：

1. 在&#x200B;**网站**&#x200B;选项卡中，选择您要锁定的页面。
1. 双击该页面以将其打开进行编辑。
1. 在 Sidekick 的&#x200B;**页面**&#x200B;选项卡中，选择&#x200B;**锁定页面**：

   ![screen_shot_2012-02-08at15750pm](assets/screen_shot_2012-02-08at15750pm.png)

   此时将显示一条消息，提示已对其他用户锁定您的页面。此外，在&#x200B;**网站**&#x200B;控制台的右侧窗格中，AEM WCM 会将页面显示为锁定状态并指明锁定页面的用户。

   ![screen_shot_2012-02-08at20657pm](assets/screen_shot_2012-02-08at20657pm.png)

## 解锁页面 {#unlocking-a-page}

要解锁页面，请执行以下操作：

1. 在&#x200B;**网站**&#x200B;选项卡中，选择您要解锁的页面。
1. 双击该页面以将其打开。
1. 在 Sidekick 的&#x200B;**页面**&#x200B;选项卡中，选择&#x200B;**解锁页面**。

## 撤消和重做页面编辑 {#undoing-and-redoing-page-edits}

如果页面的内容边框处于焦点状态，请使用以下键盘快捷键：

* 撤消：Ctrl+Z (Windows) 或 Cmd+Z (Mac)
* 重做：Ctrl+Y (Windows) 或 Cmd+Y (Mac)

当您对一个或多个段落的删除、添加或迁移操作执行撤消或重做时，受影响的段落会闪烁加亮显示（默认行为）。

>[!NOTE]
>
>有关撤消和重做页面编辑时可执行操作的完整详细信息，请参阅[撤消和重做页面编辑 - 理论](#undoing-and-redoing-page-edits-the-theory)。

## 撤消和重做页面编辑 - 理论 {#undoing-and-redoing-page-edits-the-theory}

>[!NOTE]
>
>系统管理员可以根据您实例的要求，[配置撤消/重做功能的各个方面](/help/sites-administering/config-undo.md)。

AEM 会按照您执行操作的顺序来存储这些操作的历史记录。所以，您可以按照执行时的顺序撤消多个操作。然后，您可以使用重做来重新应用一个或多个操作。

如果内容页面上的某个元素处于选中状态，则撤消和重做命令将应用于这个选中的项（如文本组件）。

撤消和重做命令的行为与其他软件程序中的类似。使用这些命令可在您做出内容决策时恢复网页的近期状态。例如，如果您将文本段落移至页面上的其他位置，可以使用撤消命令移回该段落。如果您随后又决定移动该段落，请使用重做命令。

>[!NOTE]
>
>您可以：
>
>* 只要您在执行撤消操作之后没有进行任何页面编辑，就可以执行重做操作。
>* 最多可撤消 20 次编辑操作（默认设置）。
>* 也可以使用[键盘快捷键](/help/sites-classic-ui-authoring/classic-page-author-keyboard-shortcuts.md)执行撤消和重做操作。
>



您可以对以下类型的页面更改使用撤消和重做：

* 添加、编辑、删除和移动段落
* 段落内容的就地编辑
* 在页面内复制、剪切和粘贴项目
* 跨页面复制、剪切和粘贴项目
* 添加、删除以及更改文件和图像
* 添加、删除以及更改注释和设计
* Scaffold 的更改
* 添加和删除引用
* 在组件对话框中更改属性值。

呈现表单组件的表单字段不表示在创作页面时指定了值。因此，撤消和重做命令不会影响您对这些类型的组件值所进行的更改。例如，您不能撤消选中下拉列表中的某个值。

>[!NOTE]
>
>对文件和图像的更改执行撤消和重做操作需要特殊的权限。另外，文件和图像更改的撤消历史记录至少可以保留 10 个小时。但在超过此时间后，将无法保证可以撤消这些更改。您的管理员可以提供权限并更改 10 个小时的默认保留时间。
