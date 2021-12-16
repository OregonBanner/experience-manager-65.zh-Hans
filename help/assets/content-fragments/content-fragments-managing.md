---
title: 管理内容片段
description: 了解如何使用AEM控制台来管理您的Assets内容片段（无头内容的基础）。
feature: Content Fragments
role: User
exl-id: 25c91a85-06ff-4666-a809-46778a689e25
source-git-commit: 20d46a7c37663dac36e6af9582d569a7f782eab7
workflow-type: tm+mt
source-wordcount: '1727'
ht-degree: 9%

---

# 管理内容片段 {#managing-content-fragments}

了解如何使用AEM控制台来管理您的Assets内容片段（无头内容的基础）。

在定义 [内容片段模型](#creating-a-content-model) 您可以使用这些 [创建内容片段](#creating-a-content-fragment).

的 [内容片段编辑器](#opening-the-fragment-editor) 提供各种 [模式](#modes-in-the-content-fragment-editor) 要使您能够：

* [编辑内容](#editing-the-content-of-your-fragment) 和 [管理变量](#creating-and-managing-variations-within-your-fragment)
* [在片段中添加批注](/help/assets/content-fragments/content-fragments-variations.md#annotating-a-content-fragment)
* [将内容与片段关联](#associating-content-with-your-fragment)
* [配置元数据](#viewing-and-editing-the-metadata-properties-of-your-fragment)
* [查看结构树](/help/assets/content-fragments/content-fragments-structure-tree.md)
* [预览JSON表示形式](/help/assets/content-fragments/content-fragments-json-preview.md)


>[!NOTE]
>
>可以使用内容片段：
>
>* 创作页面时；请参阅 [使用内容片段进行页面创作](/help/sites-authoring/content-fragments.md).
>* 表示 [通过GraphQL使用内容片段交付无头内容](/help/assets/content-fragments/content-fragments-graphql.md).


>[!NOTE]
>
>内容片段存储为 **资产**，因此主要从 **资产** 控制台。

## 创建内容片段 {#creating-content-fragments}

### 创建内容模型 {#creating-a-content-model}

[内容片段模型](/help/assets/content-fragments/content-fragments-models.md) 可在使用结构化内容创建内容片段之前启用和创建。

### 创建内容片段 {#creating-a-content-fragment}

创建内容片段的方法是：

1. 导航到要 **创建片段** 的Assets文件夹。
1. 选择 **创建**，然后选择 **内容片段** ，以打开向导。
1. 向导的第一步要求您指定新片段的基础。

   * [模型](/help/assets/content-fragments/content-fragments-models.md)  — 用于创建需要结构化内容的片段；例如， **冒险** 模型

      * 将显示所有可用的模型。

   选择后，使用 **下一个** 以继续。

   ![片段基础](assets/cfm-managing-01.png)

1. 在属性 **步骤中** ，指定：

   * **基本**

      * **标题**

         片段标题。

         强制.

      * **描述**

      * **标记**
   * **高级**

      * **名称**

         名称；将用于形成URL。

         强制；将自动从标题派生，但可以更新。


1. 选 **择创建** ，以完成操作，然后打开片段 **进行编辑** ，或返回控制台并执行完 **成**。

   >[!NOTE]
   >在 **列表** 的模式下，您可以更新 **查看设置** 启用 **内容片段模型** 列。

## 资产控制台中内容片段的操作 {#actions-for-a-content-fragment-assets-console}

在 **资产** 控制台为您的内容片段提供了一系列操作，包括：

* 工具栏中；选择片段后，所有适当的操作都可用。
* 作为 [快速操作](/help/sites-authoring/basic-handling.md#quick-actions);可用于单个片段卡的操作子集。

![操作](assets/cfm-managing-02.png)

选择片段以显示包含适用操作的工具栏：

* **下载**

   * 将片段另存为ZIP文件；您可以定义是否包含元素、变量、元数据。

* **创建**
* **签出**
* **属性**

   * 用于查看和/或编辑片段的元数据。

* **编辑**

   * 允许您 [打开片段以编辑内容](/help/assets/content-fragments/content-fragments-variations.md) 元素、变量、关联内容和元数据。

* **管理标记**
* **目标收藏集**
* **复制** (和 **粘贴**)
* **移动**
* **快速发布**
* **管理发布**
* **删除**

>[!NOTE]
>
>其中很多是 [资产的标准操作](/help/assets/manage-assets.md) 和/或 [AEM桌面应用程序](https://helpx.adobe.com/cn/experience-manager/desktop-app/aem-desktop-app.html).

## 打开片段编辑器 {#opening-the-fragment-editor}

要打开片段进行编辑，请执行以下操作：

>[!CAUTION]
>
>要编辑内容片段，您需要 [相应的权限](/help/sites-developing/customizing-content-fragments.md#asset-permissions). 如果您遇到问题，请联系您的系统管理员。

>[!CAUTION]
>
>要编辑内容片段，您需要相应的权限。 如果您遇到问题，请联系您的系统管理员。

1. 使用 **资产** 控制台以导航到内容片段的位置。
1. 通过以下任一方式打开片段进行编辑：

   * 单击/点按片段或片段链接（这取决于控制台视图）。
   * 选择片段，然后 **编辑** 中。

1. 将打开片段编辑器。 根据需要进行更改：

   ![片段编辑器](assets/cfm-managing-03.png)

1. 进行更改后，请使用 **保存**, **保存并关闭** 或 **关闭** 。

   >[!NOTE]
   >
   >**保存并关闭** 可通过 **保存** 下拉列表。

   >[!NOTE]
   >
   >两者兼有 **保存并关闭** 和 **关闭** 将退出编辑器 — 请参阅 [保存、关闭和版本](#save-close-and-versions) 有关各种选项如何对内容片段进行操作的完整信息。

## 内容片段编辑器中的模式和操作 {#modes-actions-content-fragment-editor}

内容片段编辑器中提供了多种模式和操作。

### 内容片段编辑器中的模式 {#modes-in-the-content-fragment-editor}

使用侧面板中的图标在各种模式中导航：

* 变体： [编辑内容](#editing-the-content-of-your-fragment) 和 [管理变量](#creating-and-managing-variations-within-your-fragment)

* [注释](/help/assets/content-fragments/content-fragments-variations.md#annotating-a-content-fragment)
* [关联的内容](#associating-content-with-your-fragment)
* [元数据](#viewing-and-editing-the-metadata-properties-of-your-fragment)
* [结构树](/help/assets/content-fragments/content-fragments-structure-tree.md)
* [预览](/help/assets/content-fragments/content-fragments-json-preview.md)

![模式](assets/cfm-managing-04.png)

### 内容片段编辑器中的工具栏操作 {#toolbar-actions-in-the-content-fragment-editor}

顶部工具栏中的某些功能可以从多种模式使用：

![模式](assets/cfm-managing-top-toolbar.png)

* 当内容页面上已引用片段时，将显示一条消息。 您可以 **关闭** 消息。

* 可以使用隐藏/显示侧面板 **切换侧面板** 图标。

* 在片段名称下，您可以看到 [内容片段模型](/help/assets/content-fragments/content-fragments-models.md) 用于创建当前片段：

   * 该名称还是一个将打开模型编辑器的链接。

* 查看片段的状态；例如，有关创建、修改或发布时间的信息。

* **保存** 提供对 **保存并关闭** 选项。

* 三个圆点(**...**)下拉列表提供了对其他操作的访问权限：
   * **更新页面引用**
      * 这会更新任何页面引用。
   * **[快速发布](#publishing-and-referencing-a-fragment)**
   * **[管理发布](#publishing-and-referencing-a-fragment)**

<!--
* See the status of the fragment; for example, information about when it was created, modified or published. The status is also color-coded:

  * **New**: grey
  * **Draft**: blue
  * **Published**: green
  * **Modified**: orange
  * **Deactivated**: red
-->

<!--
This updates any page references and ensures that the Dispatcher is flushed as required. 
-->

## 保存、关闭和版本 {#save-close-and-versions}

>[!NOTE]
>
>版本也可以 [从时间轴创建、比较和还原](/help/assets/content-fragments/content-fragments-managing.md#timeline-for-content-fragments).

编辑器具有各种选项：

* **保存** 和 **保存并关闭**

   * **保存** 将保存最新更改并保留在编辑器中。
   * **保存并关闭** 将保存最新更改并退出编辑器。

   >[!CAUTION]
   >
   >要编辑内容片段，您需要 [相应的权限](/help/sites-developing/customizing-content-fragments.md#asset-permissions). 如果您遇到问题，请联系您的系统管理员。

   >[!NOTE]
   >
   >在保存之前，可以保留在编辑器中并进行一系列更改。

   >[!CAUTION]
   >
   >除了仅保存您的更改外，这些操作还会更新任何引用，并确保Dispatcher按需要刷新。 这些更改可能需要一些时间才能处理。 因此，对于大型/复杂/重载系统，性能可能会受到影响。
   >
   >在使用 **保存并关闭** 然后快速重新进入片段编辑器以进行并保存进一步的更改。

* **关闭**

   将退出编辑器，而不保存最新更改(即自上次 **保存**)。

在编辑内容片段时，AEM会自动创建版本，以确保在您取消更改(使用 **关闭** （不保存）：

1. 打开内容片段以编辑AEM时，会检查是否存在基于Cookie的令牌，以指示 *编辑会话* 存在：

   1. 如果找到令牌，则该片段将被视为现有编辑会话的一部分。
   2. 如果令牌为 *not* 可用，用户便开始编辑内容，并创建一个版本，并将此新编辑会话的令牌发送到客户端，客户端将保存在Cookie中。

2. 当 *活动* 编辑会话时，每600秒会自动保存一次所编辑的内容（默认）。

   >[!NOTE]
   >
   >可使用 `/conf` 机制。
   >
   >默认值，请参阅：
   >  `/libs/settings/dam/cfm/jcr:content/autoSaveInterval`

3. 如果用户取消编辑，则会恢复在编辑会话开始时创建的版本，并删除令牌以结束编辑会话。
4. 如果用户选择 **保存** 进行编辑后，将保留更新的元素/变体，并删除令牌以结束编辑会话。

## 编辑片段的内容 {#editing-the-content-of-your-fragment}

打开片段后，您可以使用 [变体](/help/assets/content-fragments/content-fragments-variations.md) 选项卡来创作内容。

## 创建和管理片段中的变量 {#creating-and-managing-variations-within-your-fragment}

创建主控内容后，即可创建和管理 [变体](/help/assets/content-fragments/content-fragments-variations.md) 内容的一部分。

## 将内容与片段关联 {#associating-content-with-your-fragment}

您还可以 [关联内容](/help/assets/content-fragments/content-fragments-assoc-content.md) 片段。 这提供了一个连接，以便在将资产（即图像）添加到内容页面时，可以（可选）与片段一起使用资产（即图像）。

## 查看和编辑片段的元数据（属性） {#viewing-and-editing-the-metadata-properties-of-your-fragment}

您可以使用 [元数据](/help/assets/content-fragments/content-fragments-metadata.md) 选项卡。

## 内容片段的时间轴 {#timeline-for-content-fragments}

除了标准选项外， [时间轴](/help/assets/manage-assets.md#timeline) 提供特定于内容片段的信息和操作：

* 查看有关版本、注释和批注的信息
* 版本操作

   * **[还原到此版本](#reverting-to-a-version)** （选择现有片段，然后选择特定版本）

   * **[与当前比较](#comparing-fragment-versions)** （选择现有片段，然后选择特定版本）

   * 添加 **标签** 和/或 **注释** （选择现有片段，然后选择特定版本）

   * **另存为版本** （选择现有片段，然后选择时间轴底部的向上箭头）

* 注释操作

   * **删除**

>[!NOTE]
评论包括：
* 所有资产的标准功能
* 在时间轴中制造
* 与片段资产相关

注释（适用于内容片段）包括：
* 在片段编辑器中输入
* 特定于片段中选定的文本区段


例如：

![时间线](assets/cfm-managing-05.png)

## 比较片段版本 {#comparing-fragment-versions}

的 **与当前比较** 操作可从 [时间轴](/help/assets/content-fragments/content-fragments-managing.md#timeline-for-content-fragments) 选择特定版本后，才会将其删除。

此时将打开：

* the **当前** （最新）版本（左）

* 所选版本 **v&lt;*x.y*>** （右）

它们将并排显示，其中：

* 任何差异都会突出显示

   * 已删除的文本 — 红色
   * 插入的文本 — 绿色
   * 替换文本 — 蓝色

* 全屏图标允许您自行打开任一版本；然后切换回并行视图
* 您可以 **还原** 到特定版本
* **完成** 将返回控制台

>[!NOTE]
比较片段时无法编辑片段内容。

![比较](assets/cfm-managing-06.png)

## 还原到某个版本  {#reverting-to-a-version}

您可以还原到片段的特定版本：

* 直接从 [时间轴](/help/assets/content-fragments/content-fragments-managing.md#timeline-for-content-fragments).

   选择所需的版本，然后 **还原到此版本** 操作。

* While [将版本与当前版本进行比较](/help/assets/content-fragments/content-fragments-managing.md#comparing-fragment-versions) 您可以 **还原** 到所选版本。

## 发布和引用片段 {#publishing-and-referencing-a-fragment}

>[!CAUTION]
如果您的片段基于模型，则应确保 [模型已发布](/help/assets/content-fragments/content-fragments-models.md#publishing-a-content-fragment-model).
如果发布的内容片段的模型尚未发布，则会显示一个选择列表来指示该情况，并且模型将随该片段一起发布。

必须发布内容片段才能在发布环境中使用。 它们可以发布：

* 创建后；使用 [“资产”控制台中可用的操作](#actions-for-a-content-fragment-assets-console).
* 从 [内容片段编辑器](#toolbar-actions-in-the-content-fragment-editor).
* 当您 [发布使用片段的页面](/help/sites-authoring/content-fragments.md#publishing);片段将在页面引用中列出。

>[!CAUTION]
发布和/或引用片段后，当作者打开片段进行再次编辑时，AEM将显示警告。 这是为了警告，对片段所做的更改也会影响引用的页面。

## 删除片段 {#deleting-a-fragment}

要删除片段，请执行以下操作：

1. 在 **资产** 控制台导航到内容片段的位置。
2. 选择片段。

   >[!NOTE]
   的 **删除** 操作不可用作快速操作。

3. 选择 **删除** 中。
4. 确认 **删除** 操作。

   >[!CAUTION]
   如果片段已在页面中被引用，您将看到一条警告消息，需要您确认是否继续执行&#x200B;**强制删除**。片段及其内容片段组件将从任何内容页面中删除。
