---
title: 创建和组织页面
description: 本节介绍如何使用AEM创建和管理页面，以便您随后能够在这些页面上创建内容。
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
exl-id: bd2636d1-6f13-4c6c-b8cd-3bed9e83a101
source-git-commit: 5bdf42d1ce7b2126bfb2670049deec4b6eaedba2
workflow-type: tm+mt
source-wordcount: '1906'
ht-degree: 21%

---

# 创建和组织页面{#creating-and-organizing-pages}

本节将介绍如何使用Adobe Experience Manager (AEM)创建和管理页面，以便您随后可以 [创建内容](/help/sites-classic-ui-authoring/classic-page-author-edit-content.md) 在这些页面上。

>[!NOTE]
>
>您的帐户需要 [适当的访问权限](/help/sites-administering/security.md) 和 [权限](/help/sites-administering/security.md#permissions) 要对页面执行操作，例如创建、复制、移动、编辑、删除。
>
>如果您遇到任何问题，我们建议您与系统管理员联系。

## 组织您的网站 {#organizing-your-website}

作为作者，您需要在 AEM 内组织您的网站。这包括创建和命名您的内容页面，因此：

* 您可以在创作环境中轻松找到它们
* 您网站的访客可以轻松地在发布环境中浏览这些页面

您还可以使用[文件夹](#creating-a-new-folder)来帮助组织内容。

网站的结构可以视为 *树结构* 保存您的内容页面的存储库。 这些内容页面的名称用于组成URL，而标题在查看页面内容时显示。

下面显示了从Geometrixx站点中提取的内容；例如， `Triangle` 页面将被访问：

* 创作环境

  `http://localhost:4502/cf#/content/geometrixx/en/products/triangle.html`

* 发布环境

  `http://localhost:4503/content/geometrixx/en/products/triangle.html`

  根据实例的配置，使用 `/content` 在发布环境中可能是可选的。

```xml
  /content
    /geometrixx
      /en
        /toolbar...
        /products
          /triangle
            /overview
            /features
          /square...
          /circle...
          /...
        /...
      /fr...
      /de...
      /es...
      /...
    /...
```

此结构可以从网站控制台中查看，您可以将其用于 [在树结构中导航](/help/sites-classic-ui-authoring/author-env-basic-handling.md#main-pars-text-15).

![chlimage_1-151](assets/chlimage_1-151.png)

### 页面命名惯例 {#page-naming-conventions}

在创建新页面时，需填写以下两个关键字段：

* **[标题](#title)**：

   * 它会在控制台中向用户显示并在编辑中的页面内容顶部显示。
   * 此字段为必填字段。

* **[名称](#name)**：

   * 用于生成 URI。
   * 此字段的用户输入是可选的。如果未指定，名称会从标题派生。

创建新页面时，AEM将 [根据惯例验证页面名称](/help/sites-developing/naming-conventions.md) 由AEM和JCR强制实施。

根据UI，允许的实施和字符列表略有不同（触屏UI允许的实施和字符列表更加广泛），但允许的最低值为：

* &#39;a&#39;到&#39;z&#39;
* &#39;A&#39;到&#39;Z&#39;
* &#39;0&#39;到&#39;9&#39;
* _ （下划线）
* `-`（连字符/减号）

如果您希望确保这些字符被接受/使用(如果您需要有关允许的所有字符的完整详细信息，请参阅 [命名约定](/help/sites-developing/naming-conventions.md))。

#### 标题 {#title}

如果您在创建新页面时只提供一个页面&#x200B;**标题**，AEM 将从此字符串派生页面&#x200B;**名称**[，并依据 AEM 和 JCR 实行的惯例验证此名称](/help/sites-developing/naming-conventions.md)。在这两个UI中 **标题** 虽然将接受包含无效字符的字段，但派生的名称将替代无效字符。 例如：

| 标题 | 派生的名称 |
|---|---|
| Schön | schoen.html |
| SC%&amp;&amp;ast；c+ | sc---c-.html |

#### 名称 {#name}

如果您在创建新页面时提供页面&#x200B;**名称**，AEM 将[依据 AEM 和 JCR 实行的惯例验证此名称](/help/sites-developing/naming-conventions.md)。

在经典UI中，您 **无法输入无效字符** 在 **名称** 字段。

>[!NOTE]
>在触屏UI中，您 **无法提交无效字符** 在 **名称** 字段。 当 AEM 检测到无效字符时，此字段将会突出显示，并出现一条说明性消息以指示需要删除/替换的字符。

>[!NOTE]
>
>您应避免使用ISO-639-1定义的双字母代码，除非该代码是语言根。
>
>请参阅[准备翻译内容](/help/sites-administering/tc-prep.md)以了解更多信息。

### 模板 {#templates}

在 AEM 中，模板可指定特定类型的页面。模板将作为要创建的任何新页面的基础。

模板定义页面的结构，包括缩略图图像和其他属性。 例如，您可能会有产品页面、站点地图和联系信息的单独模板。模板包括各个[组件](#components)。

AEM 附带了一些现成的模板。所提供的模板取决于各个网站，而需要提供的信息（在创建新页面时）取决于所使用的UI。 关键的字段如下：

* **标题**
在生成的网页上显示的标题。

* **名称**
在命名页面时使用。

* **模板**
可在生成新页面时使用的模板列表。

### 组件 {#components}

组件是AEM提供的元素，用于添加特定类型的内容。AEM附带一系列现成的组件，可提供全面的功能；这些组件包括：

* 文本
* 图像
* 幻灯片放映
* 视频
* 更多内容

创建并打开页面后，您可以 [使用组件添加内容](/help/sites-classic-ui-authoring/classic-page-author-edit-content.md#insertinganewparagraph)，可从以下位置获取： [sidekick](/help/sites-classic-ui-authoring/classic-page-author-env-tools.md#sidekick).

## 管理页面 {#managing-pages}

### 创建新页面 {#creating-a-new-page}

除非提前为您创建了所有页面，否则在开始创建内容之前，您必须创建一个页面：

1. 从 **网站** 控制台中，选择要创建新页面的级别。

   在以下示例中，您在级别下创建页面 **产品**  — 显示在左窗格中；右窗格显示已存在于以下级别的页面 **产品**.

   ![screen_shot_2012-02-15at114413am](assets/screen_shot_2012-02-15at114413am.png)

1. 在 **新建……** 菜单（单击旁边的箭头） **新建……**)，选择 **新建页面……**. 此 **创建页面** 窗口打开。

   点击 **新建……** 它本身也可作为 **新建页面……** 选项。

1. 此 **创建页面** 通过对话框，您可以：

   * 提供 **标题**；向用户显示。
   * 提供 **名称**；用于生成URI。 如果未指定，则将从标题派生名称。

      * 如果您提供页面 **名称** 创建新页面时，AEM将 [根据惯例验证名称](/help/sites-developing/naming-conventions.md) 由AEM和JCR提供。
      * 在经典UI中，您 **无法输入无效字符** 在 **名称** 字段。

   * 单击要用于创建新页面的模板。

     模板用作新页面的基础；例如，确定内容页面的基本布局。

   >[!NOTE]
   >
   >请参阅[页面命名惯例](#page-naming-conventions)。

   创建新页面所需的最低信息是 **标题** 和所需的模板。

   ![screen_shot_2012-02-15at114845am](assets/screen_shot_2012-02-15at114845am.png)

   >[!NOTE]
   >
   >如果要在URL中使用Unicode字符，请设置别名( `sling:alias`)属性([页面属性](/help/sites-classic-ui-authoring/classic-page-author-edit-page-properties.md))。

1. 单击 **创建** 以创建页面。 您会返回 **网站** 控制台，您可以在此处查看新页面的条目。

   控制台提供有关页面的信息（例如，上次编辑该页面的时间以及由谁编辑），这些信息将在必要时进行更新。

   >[!NOTE]
   >
   >您也可以在编辑现有页面时创建页面。 使用**创建子页面**，从 **页面** 选项卡，将直接在正在编辑的页面下创建新页面。

### 打开页面进行编辑 {#opening-a-page-for-editing}

您可以打开要保留的页面 [已编辑](/help/sites-classic-ui-authoring/classic-page-author-edit-content.md#editing-a-component-content-and-properties) 通过以下几种方法之一：

* 从 **网站** 控制台，您可以 **双击** 用于打开以进行编辑的页面条目。

* 从 **网站** 控制台，您可以 **右键单击** （上下文菜单）页面项目，然后选择 **打开** 菜单。

* 打开页面后，您可以通过单击超链接来导航到网站中的其他页面（以进行编辑）。

### 复制和粘贴页面 {#copying-and-pasting-a-page}

在复制时，您可以复制：

* 单个页面
* 包含所有子页面的页面

1. 从 **网站** 控制台，选择要复制的页面。

   >[!NOTE]
   >
   >在此阶段，您要复制单个页面还是底层子页面无关。

1. 单击 **复制**.

1. 导航到新位置，然后单击：

   * **粘贴**  — 粘贴页面以及所有子页面
   * **Shift +粘贴**  — 仅粘贴选定的页面

   页面将粘贴到新位置。

   >[!NOTE]
   >
   >如果现有页面已经具有相同的名称，则页面名称可能会自动调整。

   >[!NOTE]
   >
   >您还可以使用 **复制页面** 从 **页面** 替他搭便车。 这将打开一个对话框，您可以在其中指定目标等。

### 移动或重命名页面 {#moving-or-renaming-page}

>[!NOTE]
>
>重命名页面也需遵循指定新页面名称时用到的[页面命名惯例](#page-naming-conventions)。

移动或重命名页面的过程相同。 通过相同的操作，您可以：

* 将页面移动到新位置
* 在同一位置重命名页面
* 将页面移动到新位置并同时重命名页面

AEM提供了将内部链接更新到要重命名或移动的页面的功能。 此操作非常灵活，可以一个页面一个页面地执行。

要移动或重命名页面，请执行以下操作：

1. 有多种方法可触发移动：

   * 从 **网站** 单击以选择页面，然后选择 **移动……**
   * 从 **网站** 控制台中，您还可以选择页面项目，然后 **右键单击** 并选择 **移动……**
   * 编辑页面时，您可以选择 **移动页面** 从 **页面** 替他搭便车。

1. 此 **移动** 窗口打开；您可以在此指定新位置和/或页面的新名称。

   ![screen_shot_2012-02-15at121336pm](assets/screen_shot_2012-02-15at121336pm.png)

   该页面还列出了引用正在移动的页面的任何页面。 根据引用页面的状态，您或许可以调整这些链接和/或重新发布页面。

1. 根据需要填写以下字段：

   * **目标**

     使用站点地图（通过下拉选择器提供）选择页面应移动到的位置。

     如果仅重命名页面，请忽略此字段。

   * **移动**

     指定要移动的页面 — 默认情况下通常会填充此页面，具体取决于您启动移动操作的方式和位置。

   * **重命名为**

     默认显示当前页面标签。 根据需要指定新页面标签。

   * **调整**

     更新列出的页面上指向已移动页面的链接：例如，如果页面A具有指向页面B的链接，AEM会调整页面A中的链接，以防您移动页面B。

     可以为每个单独引用页面选择/取消选择此选项。

   * **重新发布**

     重新发布引用页面；再次可以为每个页面选择此选项。

   >[!NOTE]
   >
   >如果页面已激活，则移动页面会自动取消激活该页面。 默认情况下，移动完成后将重新激活它，但可以通过取消选中 **重新发布** 中页面的字段 **移动** 窗口。

1. 单击 **移动**. 需要确认。 单击 **确定** 以确认。

   >[!NOTE]
   >
   >不会更新页面标题。

### 删除页面 {#deleting-a-page}

1. 您可以从各种位置删除页面：

   * 在 **网站** 单击以选择页面，然后右键单击并选择 **删除** 从生成的菜单中。
   * 在 **网站** 单击以选择页面，然后选择 **删除** 工具栏菜单中的。
   * 在sidekick中，使用 **页面** 选项卡以选择 **删除页面**  — 这将删除当前打开的页面。

1. 选择删除页面后，您必须确认请求 — 因为操作无法撤消。

   >[!NOTE]
   >
   >删除后，如果页面已发布，您可以恢复最新的（或特定的）版本，但如果进行了进一步修改，则此版本的内容可能与上一个版本不完全相同。 请参阅 [如何恢复页面](/help/sites-classic-ui-authoring/classic-page-author-work-with-versions.md#restoringpages) 以了解更多详细信息。

>[!NOTE]
>
>如果页面已经激活，则在删除前会自动将其停用。

### 锁定页面 {#locking-a-page}

您可以在控制台中或者在编辑单个页面时[锁定/解锁页面](/help/sites-classic-ui-authoring/classic-page-author-edit-content.md#locking-a-page)。有关锁定页面的信息也会同时显示在这两个位置。

### 创建新文件夹 {#creating-a-new-folder}

>[!NOTE]
>
>文件夹也需遵循在指定新文件夹名称时用到的[页面命名惯例](#page-naming-conventions)。

1. 打开 **网站** 控制台并导航到所需的位置。
1. 在 **新建……** 菜单（单击旁边的箭头） **新建……**)，选择 **新建文件夹……**.
1. 此 **创建文件夹** 此时将打开对话框。 您可在此输入&#x200B;**名称**&#x200B;和&#x200B;**标题**：

   ![chlimage_1-152](assets/chlimage_1-152.png)

1. 选择&#x200B;**创建**&#x200B;以创建文件夹。
