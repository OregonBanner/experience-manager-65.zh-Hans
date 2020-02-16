---
title: 创建和同步Live Copy
seo-title: 创建和同步Live Copy
description: 了解如何创建和同步Live Copy。
seo-description: 了解如何创建和同步Live Copy。
uuid: f6f410d4-8c72-48b7-a217-afd6076b512d
contentOwner: Alison Heimoz
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: site-features
content-type: reference
discoiquuid: 161b591b-5871-4b5f-9c63-823b6e67b1fd
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 创建和同步Live Copy{#creating-and-synchronizing-live-copies}

您可以从页面或Blueprint配置创建Live Copy，然后可以管理继承和同步。

## 管理Blueprint配置 {#managing-blueprint-configurations}

Blueprint配置标识要用作一个或多个Live copy页面源的现有网站。

>[!NOTE]
>
>Blueprint配置允许您将内容更改推送到Live Copy。 请参 [阅Live Copy —— 源、Blueprint和Blueprint配置](/help/sites-administering/msm.md#source-blueprints-and-blueprint-configurations)。

在创建Blueprint配置时，您会选择一个模板，该模板定义Blueprint的内部结构。 默认的Blueprint模板假定源网站具有以下特征：

* 网站有根页面。
* 根的直接子页面是网站的语言分支。 创建Live copy时，语言会作为可选内容显示，以包含在副本中。
* 每个语言分支的根具有一个或多个子页面。 创建Live copy时，子页面会作为可包含在Live copy中的章节显示。

>[!NOTE]
>
>不同的结构需要另一个Blueprint模板。

在创建Blueprint配置后，可配置以下属性：

* **名称**:Blueprint配置的名称。
* **源路径**:用作源的站点的根页面的路径(blueprint)。
* **描述**. （可选）Blueprint配置的说明。 描述显示在创建站点时要从中选择的Blueprint配置列表中。

使用Blueprint配置时，您可以将其与转出配置关联，该转出配置确定如何同步源/Blueprint的Live Copy。 See [Specifying the Rollout Configurations To Use](/help/sites-administering/msm-sync.md#specifying-the-rollout-configurations-to-use).

### 创建Blueprint配置 {#creating-a-blueprint-configuration}

要创建Blueprint配置，请执行以下操作：

1. [导览至](/help/sites-authoring/basic-handling.md#global-navigation) “工 **具** ”菜单，然后选择“ **站点** ”菜单。
1. 选择 **Blueprint** ，打开 **Blueprint配置控制台** :

   ![chlimage_1-209](assets/chlimage_1-209.png)

1. 选择&#x200B;**创建**。
1. 选择Blueprint模板，然后选择 **下一步** 以继续。
1. 选择要用作Blueprint的源页面；然 **后继** 续。
1. 定义：

   * **标题**:蓝图的必填标题
   * **说明**:提供更多详细信息的可选说明。

1. **创建** 将根据您的规范创建Blueprint配置。

### 编辑或删除Blueprint配置 {#editing-or-deleting-a-blueprint-configuration}

您可以编辑或删除现有的Blueprint配置：

1. [导览至](/help/sites-authoring/basic-handling.md#global-navigation) “工 **具** ”菜单，然后选择“ **站点** ”菜单。
1. 选择 **Blueprint** ，打开 **Blueprint配置控制台** :

   ![chlimage_1-210](assets/chlimage_1-210.png)

1. 选择所需的Blueprint配置——相应的操作将在工具栏中变为可用：

   * **属性**;您可以使用它查看和编辑配置的属性。
   * **删除**
   ![chlimage_1-211](assets/chlimage_1-211.png)

## 创建 Live Copy {#creating-a-live-copy}

### 创建页面的Live Copy {#creating-a-live-copy-of-a-page}

您可以创建任何页面或分支的Live Copy。 创建Live Copy时，可指定用于同步内容的转出配置：

* 选定的转出配置适用于Live copy页面及其子页面。
* 如果未指定任何转出配置，则MSM将确定要使用的转出配置。 请参 [阅指定要使用的转出配置](/help/sites-administering/msm-sync.md#specifying-the-rollout-configurations-to-use)。

您可以创建任何页面的Live Copy:

* 页面是由Blueprint配置引 [用的](#creating-a-blueprint-configuration),
* 以及与配置无连接的页面。
* AEM还支持在其他Live copy页面中创建Live Copy。

唯一的区别是，源/ **Blueprint页面上的Rollout** 命令的可用性取决于源是否被Blueprint配置引用：

* 如果从在Blueprint配置中引用的源页面 **创建** Live Copy，则Rollout命令将在源/Blueprint页面上可用。
* 如果从未在Blueprint配置中引用的源页面 **创建** Live Copy，则Rollout命令在源/Blueprint页面上将不可用。

要创建Live Copy，请执行以下操作：

1. 在站点控 **制台** ，选择 **创建**, **然后选择Live Copy**。

   ![chlimage_1-212](assets/chlimage_1-212.png)

1. 选择源页面，然后单击或点按下 **一步**。 例如：

   ![chlimage_1-213](assets/chlimage_1-213.png)

1. 指定Live Copy的目标路径（打开Live Copy的父文件夹／页面），然后单击或点按下 **一步**。

   ![chlimage_1-214](assets/chlimage_1-214.png)

   >[!NOTE]
   >
   >目标路径不能位于源路径中。

1. 输入：

   * 页 **面的标** 题。
   * 一 **个名称**，在URL中使用。
   ![chlimage_1-215](assets/chlimage_1-215.png)

1. 使用“ **排除子页面** ”复选框：

   * 已选择：仅创建选定页面的Live Copy（浅层Live Copy）
   * 未选择：创建包含选定页面的所有子代（深层Live Copy）的Live Copy

1. （可选）要指定一个或多个用于Live copy的转出配置，请使用“转出配置”( **Rollout Configs** )下拉列表选择它们；选定的配置将显示在下拉选择器下方。
1. 单击或点按&#x200B;**创建**。此时将显示一条确认消息，您可以从此处选择“打 **开** ”或“ **完成**”。

### 从Blueprint配置创建站点的Live Copy {#creating-a-live-copy-of-a-site-from-a-blueprint-configuration}

使用Blueprint配置创建Live Copy，以基于Blueprint（源）内容创建站点。 从Blueprint配置创建Live Copy时，选择要复制的Blueprint源的一个或多个语言分支，然后从语言分支中选择要复制的章节。 请参 [阅创建Blueprint配置](/help/sites-administering/msm-livecopy.md#creating-a-blueprint-configuration)。

如果在Live copy中忽略了某些语言分支或章节，可以稍后添加它们；请参 [阅在Live copy中创建Live Copy（Blueprint配置）](#creating-a-live-copy-inside-a-live-copy-blueprint-configuration)。

>[!CAUTION]
>
>当Blueprint源包含链接和引用，这些链接和引用以其他分支中的某个段落为目标时，Live copy页面中的目标不会更新，但仍会指向原始目标。

创建站点时，请为以下属性提供值：

* **初始语言**:要包含在Live copy中的Blueprint源的语言分支。
* **初始章节**:要包含在Live copy中的Blueprint语言分支的子页面。
* **目标路径**:Live copy站点的根页面的位置。
* **标题**:Live copy站点的根页面的标题。
* **名称**:（可选）存储Live copy根页面的JCR节点的名称。 默认值基于标题。
* **站点所有者**:（可选）
* **Live Copy**:选择此选项可与源站点建立实时关系。 如果不选择此选项，则将创建Blueprint的副本，但随后不会与源同步。
* **转出配置**:（可选）选择一个或多个转出配置以用于同步Live Copy。 默认情况下，转出配置从Blueprint继承；有关更 [多详细信息，请参阅指定要使用的转出配置](/help/sites-administering/msm-sync.md#specifying-the-rollout-configurations-to-use) 。

要从Blueprint配置创建站点的Live Copy，请执行以下操作：

1. 在“站 **点** ”控制台中，选 **择创建**, **** 然后从下拉选择器中选择站点。
1. 选择要用作Live copy源的Blueprint配置，然后继续执行下 **一步**:

   ![chlimage_1-216](assets/chlimage_1-216.png)

1. 使用“ **初始语言** ”选择器指定Live copy要使用的Blueprint站点的语言。

   默认情况下，将选择所有可用语言。 要删除语言，请单击或点按 **X** ，该语言旁边显示。

   例如：

   ![chlimage_1-217](assets/chlimage_1-217.png)

1. 使用“ **初始章节** ”下拉菜单选择要包含在Live copy中的Blueprint部分。 同样，所有可用章节在默认情况下都包含在内，但可以删除。
1. 为其余属性提供值，然后选择“创 **建”**。 在确认对话框中，选 **择完成** ，以返回到站点控制台，或选择 **打开站点****** ，以打开站点的根页面。

### 在Live copy中创建Live Copy（Blueprint配置） {#creating-a-live-copy-inside-a-live-copy-blueprint-configuration}

在现有Live Copy（使用Blueprint配置创建）中创建Live Copy时，可以插入最初创建Live copy时未包含的任何语言副本或章节。

## 监视Live Copy {#monitoring-your-live-copy}

### 查看Live copy的状态 {#seeing-the-status-of-a-live-copy}

Live copy页面的属性显示有关Live copy的以下信息：

* **来源**:Live copy页面的源页面。
* **状态**:Live Copy的同步状态。 状态包括Live copy是否与源保持最新，以及上次同步的时间和执行同步的人员。
* **配置**:

   * 页面是否仍受Live copy继承的约束。
   * 配置是否从父页面继承。
   * Live copy使用的任何转出配置。

要查看属性，请执行以下操作：

1. 在“站 **点** ”控制台中，选择Live copy页面并打开属性。
1. Select the **Live Copy** tab.

   例如：

   ![chlimage_1-218](assets/chlimage_1-218.png)

   >[!NOTE]
   >
   >有关详细信息，另请参阅知识库文章 [Live copy状态消息——最新／绿色／同步](https://helpx.adobe.com/experience-manager/kb/livecopy-status-message---up-to-date-green-in-sync.html)。

### 查看Blueprint页面的Live Copy {#seeing-the-live-copies-of-a-blueprint-page}

Blueprint页面（在Blueprint配置中引用）为您提供了一个Live copy页面列表，该列表使用当前(Blueprint)页面作为源。 使用此列表跟踪Live Copy。 该列表显示在页面属 **性的** “Blueprint”选 [项卡上](/help/sites-authoring/editing-page-properties.md)。

![chlimage_1-219](assets/chlimage_1-219.png)

## 同步Live Copy {#synchronizing-your-live-copy}

### 展示蓝图 {#rolling-out-a-blueprint}

推出Blueprint页面，将内容更改推送到Live Copy。 Rollout **(转出**[)操作执行使用On Rollout（转出）触发器](/help/sites-administering/msm-sync.md#rollout-triggers) 的转出配置。

>[!NOTE]
>
>如果在Blueprint分支和从属Live Copy分支中都创建了具有相同页面名称的新页面，则可能会发生冲突。
>
>此类 [冲突需要在转出时进行处理和解决](/help/sites-administering/msm-rollout-conflicts.md)。


#### 从页面属性中展开Blueprint {#rolling-out-a-blueprint-from-page-properties}

1. 在“站 **点** ”控制台中，选择Blueprint中的页面并打开属性。
1. Open the **Blueprint** tab.
1. 选择 **转出**。

   ![chlimage_1-220](assets/chlimage_1-220.png)

1. 指定页面和任何子页面，然后使用复选标记进行确认：

   ![chlimage_1-221](assets/chlimage_1-221.png)

#### 从参考边栏中展开Blueprint {#roll-out-a-blueprint-from-the-reference-rail}

1. 在“站 **点** ”控制台中，选择Blueprint中的页面，然后打开“引用” **[](/help/sites-authoring/basic-handling.md#references)**面板（从工具栏中）。
1. 从列表中选择 **Blueprint** 选项，以显示与此页面关联的Blueprint。
1. 从列表中选择所需的Blueprint。
1. Click or tap **Rollout**.
1. 系统将要求您确认转出的详细信息：

   * **转出范围**:

      指定范围是仅针对所选页面，还是应包括子页面。

   * **背景转出**:

      如果涉及许多页面／子页面，则可以将转出作为后台任务运行。
   ![chlimage_1-222](assets/chlimage_1-222.png)

1. 确认这些详细信息后，选择 **转出** ，以执行该操作。

#### 从Live copy概述中推出Blueprint {#roll-out-a-blueprint-from-the-live-copy-overview}

选择 [Blueprint页面后](/help/sites-administering/msm-livecopy-overview.md#using-the-live-copy-overview),Live copy概述中也提供了转出操作。

1. 打开Live [Copy概述](/help/sites-administering/msm-livecopy-overview.md#using-the-live-copy-overview) ，然后选择Blueprint页面。
1. Select **Rollout** from the toolbar.
1. 指定页面和任何子页面，然后使用复选标记进行确认：

   ![chlimage_1-223](assets/chlimage_1-223.png)

### 同步Live Copy {#synchronizing-a-live-copy}

同步Live copy页面，将内容更改从源提取到Live Copy。

#### 从页面属性同步Live Copy {#synchronize-a-live-copy-from-page-properties}

同步Live Copy以将更改从源拉到Live Copy。

>[!NOTE]
>
>同步会执行使用“转出时”触发 [器的转出配置](/help/sites-administering/msm-sync.md#rollout-triggers) 。

1. 在“站 **点** ”控制台中，选择Live copy页面并打开属性。
1. Open the **Live Copy** tab.
1. Click or tap **Synchronize**.

   ![chlimage_1-224](assets/chlimage_1-224.png)

   将请求确认，使用 **同步** 以继续。

#### 从Live copy概述同步Live Copy {#synchronize-a-live-copy-from-the-live-copy-overview}

选择 [Live copy页面后](/help/sites-administering/msm-livecopy-overview.md#using-the-live-copy-overview),Live copy概述中也可以执行同步操作。

1. 打开Live [Copy概述](/help/sites-administering/msm-livecopy-overview.md#using-the-live-copy-overview) ，然后选择Live copy页面。
1. Select **Synchronize** from the toolbar.
1. 指定是否 **要包括** :

   * **页面和子页面**
   * **仅页面**
   ![chlimage_1-225](assets/chlimage_1-225.png)

## 更改Live copy内容 {#changing-live-copy-content}

要更改Live copy内容，您可以：

* 向页面添加反弹。
* 通过中断任何页面或组件的Live copy继承来更新现有内容。

>[!NOTE]
>
>如果您在Live copy中手动创建新页面，则该页面是Live copy的本地页面，这意味着它没有要附加到的相应源页面。
>
>创建属于关系的本地页面的最佳实践是在源中创建它并执行（深层）转出。 这将在本地创建页面作为Live Copy。

>[!NOTE]
>
>如果在Blueprint分支和从属Live Copy分支中都创建了具有相同页面名称的新页面，则可能会发生冲突。
>
>此类 [冲突需要在转出时进行处理和解决](/help/sites-administering/msm-rollout-conflicts.md)。


### 将组件添加到Live copy页面 {#adding-components-to-a-live-copy-page}

随时将组件添加到Live copy页面。 Live copy及其段落系统的继承状态无法控制您添加组件的能力。

当Live copy页面与源页面同步时，添加的组件将保持不变。 另请参 [阅更改Live copy页面上的组件顺序](#changing-the-order-of-components-on-a-live-copy-page)。

>[!NOTE]
>
>对标记为容器的组件进行的本地更改不会被转出时Blueprint的内容覆盖。 See [MSM Best Practices](/help/sites-administering/msm-best-practices.md#components-and-container-synchronization) for more information.

### 暂停页面继承 {#suspending-inheritance-for-a-page}

创建Live Copy时，Live copy配置将保存在复制页面的根页面上。 根页面的所有子页面都继承Live copy配置。 Live copy页面上的组件也继承了Live copy配置。

您可以暂停Live copy页面的Live copy继承，以便更改页面属性和组件。 暂停继承时，页面属性和组件不再与源同步。

>[!NOTE]
>
>您还可以将 [Live Copy从其Blueprint中分离](#detaching-a-live-copy) ，以删除所有连接。 “分离”(Detach)操作是永久的且不可撤消的。

#### 暂停页面属性的继承 {#suspending-inheritance-from-page-properties}

要暂停页面上的继承，请执行以下操作：

1. 使用“站点”控制台的“查看属性 **”命令或使用页面工具栏上的“页** 面信息” **，打开Live Copy页面的属性****** 。
1. 单击或点按 **Live Copy选项卡** 。
1. Select **Suspend** from the toolbar. 然后，您可以选择以下任一选项：

   * **暂停**:仅限当前页面
   * **暂停子项**:当前页面以及任何子页面

1. 在确 **认对话框上** ，选择暂停。

#### 暂停Live copy的继承概述 {#suspending-inheritance-from-the-live-copy-overview}

选 [择Live copy页面后](/help/sites-administering/msm-livecopy-overview.md#using-the-live-copy-overview),Live copy概述中也可以执行暂停操作。

1. 打开Live [Copy概述](/help/sites-administering/msm-livecopy-overview.md#using-the-live-copy-overview) ，然后选择Live copy页面。
1. Select **Suspend** from the toolbar.
1. 从以下位置选择相应的选项：

   * **暂停**
   * **暂停（含子项）**
   ![chlimage_1-226](assets/chlimage_1-226.png)

1. 在**暂 **停Live Copy** **对话框中确认暂停操作：

   ![chlimage_1-227](assets/chlimage_1-227.png)

### 恢复页面继承 {#resuming-inheritance-for-a-page}

暂停页面的Live copy继承是一个临时操作。 暂停后，“继 **续** ”(Resume)操作变为可用，允许您恢复实时关系。

重新启用继承后，页面不会自动与源同步。 如果需要同步，您可以请求以下任一方式：

* 在“恢 **复**/恢&#x200B;**复”对话框中** ;例如：

   ![chlimage_1-228](assets/chlimage_1-228.png)

* 在稍后阶段，手动选择同步操作。

>[!CAUTION]
>
>重新启用继承后，页面不会自动与源同步。 如果需要，您可以手动请求同步；在恢复或稍后恢复时。

#### 从页面属性恢复继承 {#resuming-inheritance-from-page-properties}

暂停 [后](#suspending-inheritance-from-page-properties) ,“继 **续** ”动作将变为页面属性的工具栏：

![chlimage_1-229](assets/chlimage_1-229.png)

选择后，将显示对话框。 您可以根据需要选择同步，然后确认操作。

#### 从Live copy概述恢复Live copy页面 {#resume-a-live-copy-page-from-the-live-copy-overview}

选择 [Live copy页面后](/help/sites-administering/msm-livecopy-overview.md#using-the-live-copy-overview)，还可以从Live copy概述中执行恢复操作。

1. 打开 [Live copy概述](/help/sites-administering/msm-livecopy-overview.md#using-the-live-copy-overview) ，然后选择已挂起的Live copy页面；将显示为继承 **已取消**。
1. Select **Resume** from the toolbar.
1. 指示是否要在还原继承后同步页面，然后在“继续 **Live Copy** ” **对话框中确认“继续”操作。

### 更改继承深度（浅／深） {#changing-inheritance-depth-shallow-deep}

在现有Live Copy上，您可以更改页面深度；即是否包含子页面。

* 切换到浅层Live Copy:

   * 将立即生效，并且是不可逆的。

      * 子页面与Live copy显式分离。 如果撤消，则无法保留对子项的进一步修改。
   * 将删除任何子 `LiveRelationships` 体，即使嵌套也是如此 `LiveCopies`。


* 切换到深层Live Copy:

   * 子页面保持不变。
   * 要查看交换机的效果，您可以进行转出，任何内容修改都会根据转出配置进行应用。

* 切换到浅层Live Copy，然后返回深层：

   * （以前）浅层Live Copy的所有子项都会被视为是手动创建的，因此会使用移动 `[oldname]_msm_moved name`。

要指定或更改深度，请执行以下操作：

1. 使用“站点”控制台的“查看属性 **”命令或使用页面工具栏上的“页** 面信息” **，打开Live Copy页面的属性****** 。
1. 单击或点按 **Live Copy选项卡** 。
1. 在“配 **置** ”部分中，根据是否包含子页 **** 面，设置或清除Live Copy继承选项：

   * 选中——深层Live Copy（包含子页面）
   * clear —— 浅层Live Copy（不包括子页面）
   >[!CAUTION]
   >
   >切换到浅层Live Copy将立即生效，并且是不可逆的。
   >
   >有关详 [细信息，请参阅Live Copy —— 合成](/help/sites-administering/msm.md#live-copies-composition) 。

1. 单击或点按保 **存** ，以保留您的更新。

### 取消组件的继承 {#cancelling-inheritance-for-a-component}

取消组件的Live copy继承，以便组件不再与源组件同步。 如果需要，您可以在以后的点启用继承。

>[!NOTE]
>
>当您重新启用继承时，组件不会自动与源同步。 如果需要，可以手动请求同步。

取消继承以更改组件内容或删除组件：

1. 单击或点按要取消继承的组件。

   ![chlimage_1-230](assets/chlimage_1-230.png)

1. 在组件工具栏中，单击或点按取消继 **承图标** 。

   ![](do-not-localize/chlimage_1-8.png)

1. 在“取消继承”对话框中，用“是”确认 **操作**。

   组件工具栏将更新以包含所有（相应的）编辑命令。

### 为组件重新启用继承 {#re-enabling-inheritance-for-a-component}

要为组件启用继承，请单击或点按组件 **工具栏上的重新启用继承** 图标。

![](do-not-localize/chlimage_1-9.png)

### 更改Live copy页面上的组件顺序 {#changing-the-order-of-components-on-a-live-copy-page}

如果Live copy包含属于段落系统的组件，则段落系统的继承遵循以下规则：

* 可以修改继承段落系统中组件的顺序，即使已建立继承也是如此。
* 转出时，将从Blueprint中恢复组件的顺序。 如果在转出之前将新组件添加到Live Copy，则它们将与添加它们的组件一起重新排序。
* 如果取消段落系统的继承，则转出时将不恢复组件的顺序，并将保留在Live Copy中。

>[!NOTE]
>
>在段落系统上还原取消的继承时，组件的顺序 **不会从Blueprint中自动恢复** 。 如果需要，可以手动请求同步。

请按照以下过程取消段落系统的继承。

1. 打开Live copy页面。
1. 将现有组件拖动到页面上的新位置。
1. 在“取 **消继承** ”对话框中，用“是”确认 **操作**。

### 覆盖Live copy页面的属性 {#overriding-properties-of-a-live-copy-page}

默认情况下，Live copy页面的页面属性会从源页面继承（并且不可编辑）。

当您需要更改Live copy的属性值时，可以取消属性的继承。 链接图标指示已为属性启用继承。

![chlimage_1-231](assets/chlimage_1-231.png)

取消继承时，可以更改属性值。 断开链接图标表示继承已取消。

![chlimage_1-232](assets/chlimage_1-232.png)

您以后可以根据需要为属性重新启用继承。

>[!NOTE]
>
>重新启用继承后，Live Copy页面属性不会自动与源属性同步。 如果需要，可以手动请求同步。

1. 使用“站点”控制台的“查看属性”选项或 **页面工具栏上的“页面信息****”图标，打开Live Copy****** 页面的属性。
1. 要取消属性的继承，请单击或点按属性右侧显示的链接图标。

   ![](do-not-localize/chlimage_1-10.png)

1. 在取消继 **承确认对话框中** ，单击或点按 **是**。

### 还原Live copy页面的属性 {#revert-properties-of-a-live-copy-page}

要为属性启用继承，请单击或点按属 **性旁边显示的“恢复继承** ”图标。

![](do-not-localize/chlimage_1-11.png)

### 重置Live copy页面 {#resetting-a-live-copy-page}

将Live copy页面重置为：

* 删除所有继承取消和
* 将页面返回到与源页面相同的状态。

重置会影响您对页面属性、段落系统和组件所做的更改。

#### 从页面属性重置Live copy页面 {#reset-a-live-copy-page-from-the-page-properties}

1. 在“站 **点** ”控制台中，选择Live Copy页面，然后选择查看 **属性**。
1. Open the **Live Copy** tab.
1. Select **Reset** from the toolbar.

   ![chlimage_1-233](assets/chlimage_1-233.png)

1. 在“重 **置Live Copy** ”对话框中，使用“重置 **”确认**。

#### 从Live copy概述重置Live copy页面 {#reset-a-live-copy-page-from-the-live-copy-overview}

选 [择Live copy页面后](/help/sites-administering/msm-livecopy-overview.md#using-the-live-copy-overview),Live copy概述中也提供重置操作。

1. 打开Live [Copy概述](/help/sites-administering/msm-livecopy-overview.md#using-the-live-copy-overview) ，然后选择Live copy页面。
1. Select **Reset** from the toolbar.
1. 在重置 **Live Copy** 对话框中确 **认重置操作** :

   ![chlimage_1-234](assets/chlimage_1-234.png)

## 将Live copy页面与Blueprint页面进行比较 {#comparing-a-live-copy-page-with-a-blueprint-page}

要跟踪所做的更改，您可以在引用中查看Blueprint页 **面** ，并将其与其Live copy页面进行比较：

1. 在“站 **点** ”控制台 [中，导航到Blueprint或Live Copy页面并选择它](/help/sites-authoring/basic-handling.md#viewing-and-selecting-resources)。
1. Open the **[References](/help/sites-authoring/basic-handling.md#references)**panel and select:

   * **Blueprint** （当选择Live Copy页面时）
   * **Live Copy** （当选择Blueprint页面时）

1. 选择您的特定Live Copy，然后：

   * **与Blueprint比较** （当选择Live copy页面时）
   * **与Live Copy比较** （当选择了Blueprint页面时）
   例如：

   ![chlimage_1-235](assets/chlimage_1-235.png)

1. 两个页面（Live Copy和Blueprint）将并排打开。

   有关使用此功能的完整信息，请参阅[页面差异](/help/sites-authoring/page-diff.md)。

## 分离Live Copy {#detaching-a-live-copy}

“分离”将永久删除Live copy与其源/Blueprint页面之间的Live关系。 所有与MSM相关的属性都将从Live copy中删除，并且Live copy页面将变为独立副本。

>[!CAUTION]
>
>在分离Live copy后，不能恢复Live Relation。
>
>要删除Live Relationship（以后重新启用它）选项，可以取 [消页面的Live copy继承](#suspending-inheritance-for-a-page) 。

在使用“分离”的树内的位置上会显示 **含义**:

* **在LiveCopy的根页面上分离**

   在Live Copy的根页面上执行此操作时，它会删除Blueprint的所有页面与其Live copy之间的Live关系。

   对Blueprint中页面的进一步更改（原样） **不会** （原样）影响Live Copy。

* **在LiveCopy的子页面上分离**

   在Live Copy的子页面（或分支）上执行此操作时：

   * 该子页面（或分支）的实时关系将被删除
   * 而Live copy分支中的（子）页面则被视为已手动创建。
   *但是*，子页面仍受父分支的实时关系的约束，因此进一步转出Blueprint页面将同时执行以下操作：

   1. 重命名已分离的页面：

      * 这是因为MSM将它们视为手动创建的页面，这会导致冲突，因为它们的名称与其尝试创建的Live copy页面相同。
   1. 使用原始名称创建新的(Live Copy)页面，其中包含转出中的更改。
   >[!NOTE]
   >
   >有关 [此类情况的详细信息](/help/sites-administering/msm-rollout-conflicts.md) ，请参阅MSM转出冲突。

### 从页面属性中分离Live copy页面 {#detach-a-live-copy-page-from-the-page-properties}

分离Live Copy:

1. 在“站 **点** ”控制台中，选择Live copy页面，然后单击或点按查看 **属性**。
1. Open the **Live Copy** tab.
1. 在工具栏中，选择“ **分离**”。

   ![chlimage_1-236](assets/chlimage_1-236.png)

1. 此时将显示确认对话框，选择 **分离** ，以完成操作。

### 从Live copy概述中分离Live copy页面 {#detach-a-live-copy-page-from-the-live-copy-overview}

选择 [Live copy页面后](/help/sites-administering/msm-livecopy-overview.md#using-the-live-copy-overview),Live copy概述中也可以执行分离操作。

1. 打开Live [Copy概述](/help/sites-administering/msm-livecopy-overview.md#using-the-live-copy-overview) ，然后选择Live copy页面。
1. Select **Detach** from the toolbar.
1. 在“分离 **Live Copy** ”对话框中确 **认“分离”操作** :

   ![chlimage_1-237](assets/chlimage_1-237.png)

