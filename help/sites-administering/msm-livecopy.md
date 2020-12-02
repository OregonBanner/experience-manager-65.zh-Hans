---
title: 创建和同步Live Copy
description: 了解如何创建和同步Live Copy。
translation-type: tm+mt
source-git-commit: 4755f33ed27bb876bfb70bab35d411d9b06788b0
workflow-type: tm+mt
source-wordcount: '4115'
ht-degree: 1%

---


# 创建和同步Live Copy{#creating-and-synchronizing-live-copies}

您可以从页面或蓝图配置创建Live Copy，然后可以管理继承和同步。

## 管理Blueprint配置{#managing-blueprint-configurations}

Blueprint配置标识要用作一个或多个Live Copy页面源的现有网站。

>[!NOTE]
>
>Blueprint配置允许您将内容更改推送到Live Copy。 请参阅[Live Copy - Source、Blueprint和Blueprint Configurations](/help/sites-administering/msm.md#source-blueprints-and-blueprint-configurations)。

创建Blueprint配置时，您将选择一个模板，它定义Blueprint的内部结构。 默认的蓝图模板假定源网站具有以下特征：

* 该网站有根页面。
* 根的直接子页面是网站的语言分支。 创建Live Copy时，语言会作为可选内容显示在副本中。
* 每个语言分支的根具有一个或多个子页面。 创建Live Copy时，子页面会作为可以包含在Live Copy中的章节显示。

>[!NOTE]
>
>不同的结构需要另一个蓝图模板。

创建Blueprint配置后，您配置以下属性：

* **名称**:蓝图配置的名称。
* **源路径**:用作源(blueprint)的站点的根页面的路径。
* **描述**. （可选）蓝图配置的说明。 描述显示在创建站点时要选择的蓝图配置列表中。

使用Blueprint配置时，您可以将其与转出配置关联，该转出配置确定如何同步源/Blueprint的Live Copy。 请参阅[指定要使用的转出配置](/help/sites-administering/msm-sync.md#specifying-the-rollout-configurations-to-use)。

### 创建Blueprint配置{#creating-a-blueprint-configuration}

要创建Blueprint配置，请执行以下操作：

1. [导](/help/sites-authoring/basic-handling.md#global-navigation) 航至“工 **** 具”菜单，然后选择“ **** 大小”菜单。
1. 选择&#x200B;**Blueprint**&#x200B;以打开&#x200B;**Blueprint Configurations**&#x200B;控制台：

   ![chlimage_1-209](assets/chlimage_1-209.png)

1. 选择&#x200B;**创建**。
1. 选择Blueprint模板，然后选择&#x200B;**Next**&#x200B;继续。
1. 选择要用作蓝图的源页面；然后&#x200B;**Next**&#x200B;继续。
1. 定义：

   * **标题**:蓝图的必填标题
   * **描述**:提供更多详细信息的可选描述。

1. **Create** 将根据您的规范创建Blueprint配置。

### 编辑或删除Blueprint配置{#editing-or-deleting-a-blueprint-configuration}

您可以编辑或删除现有的Blueprint配置：

1. [导](/help/sites-authoring/basic-handling.md#global-navigation) 航至“工 **** 具”菜单，然后选择“ **** 大小”菜单。
1. 选择&#x200B;**Blueprint**&#x200B;以打开&#x200B;**Blueprint Configurations**&#x200B;控制台：

   ![chlimage_1-210](assets/chlimage_1-210.png)

1. 选择所需的Blueprint配置——相应的操作将在工具栏中变为可用：

   * **属性**;您可以使用它来视图，然后编辑配置的属性。
   * **删除**

   ![chlimage_1-211](assets/chlimage_1-211.png)

## 创建 Live Copy {#creating-a-live-copy}

### 创建页面{#creating-a-live-copy-of-a-page}的Live Copy

您可以创建任何页面或分支的Live Copy。 创建Live Copy时，可以指定用于同步内容的转出配置：

* 所选转出配置将应用于Live Copy页面及其子页面。
* 如果未指定任何转出配置，MSM将确定要使用的转出配置。 请参阅[指定要使用的转出配置](/help/sites-administering/msm-sync.md#specifying-the-rollout-configurations-to-use)。

您可以创建任何页面的Live Copy:

* 由[blueprint配置](#creating-a-blueprint-configuration)引用的页面。
* 以及与配置无连接的页面。
* AEM还支持在其他Live Copy的页面中创建Live Copy。

唯一的区别在于，源／蓝图页面上的&#x200B;**Rollout**&#x200B;命令的可用性取决于源是否被蓝图配置引用：

* 如果从在Blueprint配置中引用的&#x200B;**为**&#x200B;的源页面创建Live Copy，则Rollout命令将在源/Blueprint页面上可用。
* 如果您从未在Blueprint配置中引用&#x200B;**的源页面创建Live Copy，则Rollout命令在源/Blueprint页面上将不可用。**

要创建Live Copy，请执行以下操作：

1. 在&#x200B;**站点**&#x200B;控制台中，选择&#x200B;**创建**，然后选择&#x200B;**Live Copy**。

   ![chlimage_1-212](assets/chlimage_1-212.png)

1. 选择源页面，然后单击或点按&#x200B;**下一步**。 例如：

   ![chlimage_1-213](assets/chlimage_1-213.png)

1. 指定Live Copy的目标路径（打开Live Copy的父文件夹／页面），然后单击或点按&#x200B;**下一步**。

   ![chlimage_1-214](assets/chlimage_1-214.png)

   >[!NOTE]
   >
   >目标路径不能在源路径中。

1. 输入：

   * a **页面的标题**。
   * **名称**，在URL中使用。

   ![chlimage_1-215](assets/chlimage_1-215.png)

1. 使用&#x200B;**排除子页面**&#x200B;复选框：

   * 已选择：仅创建选定页面的Live Copy（浅Live Copy）
   * 未选择：创建包含选定页面的所有子代的Live Copy（深层Live Copy）

1. （可选）要指定一个或多个用于Live Copy的转出配置，请使用&#x200B;**转出配置**&#x200B;下拉列表选择它们；选定的配置将显示在下拉选择器下。
1. 单击或点按&#x200B;**创建**。此时将显示一条确认消息，您可以从此处选择&#x200B;**打开**&#x200B;或&#x200B;**完成**。

### 从Blueprint配置{#creating-a-live-copy-of-a-site-from-a-blueprint-configuration}创建站点的Live Copy

使用Blueprint配置创建Live Copy，以基于Blueprint（源）内容创建站点。 从Blueprint配置创建Live Copy时，选择要复制的Blueprint源的一个或多个语言分支，然后从语言分支中选择要复制的章节。 请参阅[创建Blueprint配置](/help/sites-administering/msm-livecopy.md#creating-a-blueprint-configuration)。

如果在Live Copy中漏掉一些语言分支或章节，可以稍后添加；请参阅[在Live Copy中创建Live Copy（Blueprint配置）](#creating-a-live-copy-inside-a-live-copy-blueprint-configuration)。

>[!CAUTION]
>
>当蓝图源包含链接和引用，这些链接和引用目标了不同分支中的某个段落时，Live Copy页面中的目标不会更新，但仍指向原始目标。

创建站点时，请提供以下属性的值：

* **初始语言**:要包含在Live Copy中的Blueprint源的语言分支。
* **初始章节**:要包含在Live Copy中的Blueprint语言分支的子页面。
* **目标路径**:Live Copy站点的根页面的位置。
* **标题**:Live Copy站点的根页面的标题。
* **名称**:（可选）存储Live Copy根页面的JCR节点的名称。默认值基于标题。
* **站点所有者**:（可选）
* **Live Copy**:选择此选项可与源站点建立实时关系。如果不选择此选项，将创建Blueprint的副本，但随后不会与源同步。
* **转出配置**:（可选）选择一个或多个转出配置以用于同步Live Copy。默认情况下，转出配置从Blueprint继承；有关详细信息，请参阅[指定要使用的转出配置](/help/sites-administering/msm-sync.md#specifying-the-rollout-configurations-to-use)。

要从Blueprint配置创建站点的Live Copy，请执行以下操作：

1. 在&#x200B;**站点**&#x200B;控制台中，从下拉选择器中选择&#x200B;**创建**，然后选择&#x200B;**站点**。
1. 选择要用作Live Copy源的Blueprint配置，然后继续执行&#x200B;**Next**:

   ![chlimage_1-216](assets/chlimage_1-216.png)

1. 使用&#x200B;**初始语言**&#x200B;选择器指定Blueprint站点要用于Live Copy的语言。

   默认情况下，将选择所有可用语言。 要删除语言，请单击或点按该语言旁边显示的&#x200B;**X**。

   例如：

   ![chlimage_1-217](assets/chlimage_1-217.png)

1. 使用&#x200B;**初始章节**&#x200B;下拉框选择要包含在Live Copy中的Blueprint的各个部分。 同样，所有可用章节都默认包含在内，但可以删除。
1. 为其余属性提供值，然后选择&#x200B;**创建**。 在确认对话框中，选择&#x200B;**完成**&#x200B;以返回到&#x200B;**站点**&#x200B;控制台，或选择&#x200B;**打开站点**&#x200B;以打开站点的根页面。

### 在Live Copy中创建Live Copy（Blueprint配置）{#creating-a-live-copy-inside-a-live-copy-blueprint-configuration}

在现有Live Copy中创建Live Copy（使用Blueprint配置创建）时，可以插入最初创建Live Copy时未包含的任何语言副本或章节。

## 监视Live Copy {#monitoring-your-live-copy}

### 查看Live Copy的状态{#seeing-the-status-of-a-live-copy}

Live Copy页面的属性显示有关Live Copy的以下信息：

* **来源**:Live Copy页面的源页面。
* **状态**:Live Copy的同步状态。状态包括Live Copy是否与源同步，以及上次同步发生的时间以及执行同步的人员。
* **配置**:

   * 页面是否仍受Live Copy继承的约束。
   * 配置是否从父页面继承。
   * Live Copy使用的任何转出配置。

视图属性：

1. 在&#x200B;**站点**&#x200B;控制台中，选择Live Copy页面并打开属性。
1. 选择&#x200B;**Live Copy**&#x200B;选项卡。

   例如：

   ![chlimage_1-218](assets/chlimage_1-218.png)

   >[!NOTE]
   >
   >有关详细信息，另请参阅知识库文章[Live Copy状态消息——最新／绿色／同步](https://helpx.adobe.com/experience-manager/kb/livecopy-status-message---up-to-date-green-in-sync.html)。

### 查看Blueprint页面{#seeing-the-live-copies-of-a-blueprint-page}的Live Copy

Blueprint页面（在Blueprint配置中引用）为您提供了Live Copy页面的列表，这些页面使用当前(Blueprint)页面作为源。 使用此列表跟踪Live Copy。 该列表显示在[页面属性](/help/sites-authoring/editing-page-properties.md)的&#x200B;**Blueprint**&#x200B;选项卡上。

![chlimage_1-219](assets/chlimage_1-219.png)

## 正在同步Live Copy {#synchronizing-your-live-copy}

### Rolling Out a Blueprint {#rolling-out-a-blueprint}

展开蓝图页面，将内容更改推送到Live Copy。 **Rollout**&#x200B;操作执行使用[On Rollout](/help/sites-administering/msm-sync.md#rollout-triggers)触发器的转出配置。

>[!NOTE]
>
>如果在Blueprint分支和从属Live Copy分支中创建了具有相同页面名称的新页面，则可能会发生冲突。
>
>此类[冲突需要在转出](/help/sites-administering/msm-rollout-conflicts.md)时处理和解决。


#### 从页面属性{#rolling-out-a-blueprint-from-page-properties}中滚动Blueprint

1. 在&#x200B;**站点**&#x200B;控制台中，选择Blueprint中的页面并打开属性。
1. 打开&#x200B;**Blueprint**&#x200B;选项卡。
1. 选择&#x200B;**转出**。

   ![chlimage_1-220](assets/chlimage_1-220.png)

1. 指定页面和任何子页面，然后使用复选标记进行确认：

   ![chlimage_1-221](assets/chlimage_1-221.png)

1. 指定是否应立即执行转出作业(**Now**)或在其他日期／时间（**稍后**）。

   ![转出蓝图](assets/rollout-blueprint.png)

转出将作为异步作业处理，并可以在&#x200B;**全局导航** -> **工具** -> **操作** -> **作业**&#x200B;的&#x200B;[**仪表板中检查。](asynchronous-jobs.md#monitor-the-status-of-asynchronous-operations)**

>[!NOTE]
>
>异步转出处理需要AEM 6.5.3.0或更高版本。 在以前的版本中，页面会立即和同步处理。

#### 从参考边栏{#roll-out-a-blueprint-from-the-reference-rail}中展开Blueprint

1. 在&#x200B;**站点**&#x200B;控制台中，选择Blueprint中的页面，然后打开&#x200B;**[引用](/help/sites-authoring/basic-handling.md#references)**&#x200B;面板（从工具栏中）。
1. 从列表中选择&#x200B;**Blueprint**&#x200B;选项，以显示与此页面关联的Blueprint。
1. 从列表中选择所需的蓝图。
1. 单击或点按&#x200B;**转出**。
1. 系统将要求您确认转出的详细信息：

   * **转出范围**:

      指定范围是仅针对所选页面，还是应包括子页面。

   * **计划**：

      指定是立即执行转出作业(**Now**)还是在以后的日期／时间执行(**Later**)。

      ![chlimage_1-222](assets/rollout-live-copy.png)

1. 确认这些详细信息后，选择&#x200B;**转出**&#x200B;以执行操作。

转出将作为异步作业处理，并可以在&#x200B;**全局导航** -> **工具** -> **操作** -> **作业**&#x200B;的&#x200B;[**仪表板中检查。](asynchronous-jobs.md#monitor-the-status-of-asynchronous-operations)**

>[!NOTE]
>
>异步转出处理需要AEM 6.5.3.0或更高版本。 在以前的版本中，页面会立即同步处理，除非选中&#x200B;**后台转出**&#x200B;选项。

#### 从Live Copy概述{#roll-out-a-blueprint-from-the-live-copy-overview}中推出Blueprint

选择Blueprint页面后，[转出操作也可从Live Copy概述](/help/sites-administering/msm-livecopy-overview.md#using-the-live-copy-overview)中使用。

1. 打开[Live Copy概述](/help/sites-administering/msm-livecopy-overview.md#using-the-live-copy-overview)并选择Blueprint页面。
1. 从工具栏中选择&#x200B;**转出**。
1. 指定页面和任何子页面，然后使用复选标记进行确认：

   ![chlimage_1-223](assets/chlimage_1-223.png)

1. 指定是否应立即执行转出作业(**Now**)或在其他日期／时间（**稍后**）。

   ![转出蓝图](assets/rollout-blueprint.png)

转出将作为异步作业处理，并可以在&#x200B;**全局导航** -> **工具** -> **操作** -> **作业**&#x200B;的&#x200B;[**仪表板中检查。](asynchronous-jobs.md#monitor-the-status-of-asynchronous-operations)**

>[!NOTE]
>
>异步转出处理需要AEM 6.5.3.0或更高版本。 在以前的版本中，页面会立即和同步处理。

### 同步Live Copy {#synchronizing-a-live-copy}

同步Live Copy页面，将内容更改从源提取到Live Copy。

#### 从页面属性{#synchronize-a-live-copy-from-page-properties}同步Live Copy

同步Live Copy以从源将更改拉入Live Copy。

>[!NOTE]
>
>同步执行使用[On Rollout](/help/sites-administering/msm-sync.md#rollout-triggers)触发器的转出配置。

1. 在&#x200B;**站点**&#x200B;控制台中，选择Live Copy页面并打开属性。
1. 打开&#x200B;**Live Copy**&#x200B;选项卡。
1. 单击或点按&#x200B;**同步**。

   ![chlimage_1-224](assets/chlimage_1-224.png)

   将请求确认，使用&#x200B;**同步**&#x200B;继续。

#### 从Live Copy概述{#synchronize-a-live-copy-from-the-live-copy-overview}同步Live Copy

选择Live Copy页面后， Live Copy概述](/help/sites-administering/msm-livecopy-overview.md#using-the-live-copy-overview)中也提供了[同步操作。

1. 打开[Live Copy概述](/help/sites-administering/msm-livecopy-overview.md#using-the-live-copy-overview)并选择Live Copy页面。
1. 从工具栏中选择&#x200B;**同步**。
1. 指定是否要包括以下内容后，确认对话框中的&#x200B;**Rollout**&#x200B;操作：

   * **页面和子页面**
   * **仅页面**

   ![chlimage_1-225](assets/chlimage_1-225.png)

## 更改Live Copy内容{#changing-live-copy-content}

要更改Live Copy内容，您可以：

* 向页面添加段落。
* 通过中断任何页面或组件的Live Copy继承来更新现有内容。

>[!NOTE]
>
>如果您在Live Copy中手动创建新页面，则它是Live Copy的本地页面，这意味着它没有要附加的相应源页面。
>
>创建作为关系一部分的本地页面的最佳实践是在源中创建它并执行（深层）转出。 这将在本地创建页面作为Live Copy。

>[!NOTE]
>
>如果在Blueprint分支和从属Live Copy分支中创建了具有相同页面名称的新页面，则可能会发生冲突。
>
>此类[冲突需要在转出](/help/sites-administering/msm-rollout-conflicts.md)时处理和解决。


### 将组件添加到Live Copy页面{#adding-components-to-a-live-copy-page}

随时将组件添加到Live Copy页面。 Live Copy及其段落系统的继承状态无法控制您添加组件的能力。

当Live Copy页面与源页面同步时，添加的组件将保持不变。 另请参阅[更改Live Copy页面上的组件顺序](#changing-the-order-of-components-on-a-live-copy-page)。

>[!NOTE]
>
>本地对标记为容器的组件所做的更改不会被转出时Blueprint的内容覆盖。 有关详细信息，请参阅[MSM最佳实践](/help/sites-administering/msm-best-practices.md#components-and-container-synchronization)。

### 暂停页面{#suspending-inheritance-for-a-page}的继承

创建Live Copy时，Live Copy配置将保存在复制页面的根页面上。 根页面的所有子页面都继承Live Copy配置。 Live Copy页面上的组件也继承Live Copy配置。

您可以暂停Live Copy页面的Live Copy继承，以便更改页面属性和组件。 暂停继承时，页面属性和组件不再与源同步。

>[!NOTE]
>
>还可以从Live Copy](#detaching-a-live-copy)的蓝图中分离Live Copy[以删除所有连接。 “分离”(Detach)操作是永久的且不可撤消的。

#### 从页面属性{#suspending-inheritance-from-page-properties}挂起继承

要暂停页面上的继承，请执行以下操作：

1. 使用&#x200B;**Sites**&#x200B;控制台的&#x200B;**视图属性**&#x200B;命令或使用页面工具栏上的&#x200B;**页面信息**&#x200B;打开Live Copy页面的属性。
1. 单击或点按&#x200B;**Live Copy**&#x200B;选项卡。
1. 从工具栏中选择&#x200B;**暂停**。 然后，您可以选择以下任一选项：

   * **暂停**:仅限当前页面
   * **在子项中暂停**:当前页面以及任何子页面

1. 在确认对话框中选择&#x200B;**暂停**。

#### 暂停Live Copy的继承概述{#suspending-inheritance-from-the-live-copy-overview}

选择Live Copy页面后，Live Copy概述](/help/sites-administering/msm-livecopy-overview.md#using-the-live-copy-overview)中也提供了[暂停操作。

1. 打开[Live Copy概述](/help/sites-administering/msm-livecopy-overview.md#using-the-live-copy-overview)并选择Live Copy页面。
1. 从工具栏中选择&#x200B;**暂停**。
1. 从以下位置选择相应的选项：

   * **暂停**
   * **与子项一起暂停**

   ![chlimage_1-226](assets/chlimage_1-226.png)

1. 在&#x200B;**暂停Live Copy**&#x200B;对话框中确认&#x200B;**暂停**&#x200B;操作：

   ![chlimage_1-227](assets/chlimage_1-227.png)

### 恢复页面{#resuming-inheritance-for-a-page}的继承

暂停页面的Live Copy继承是临时操作。 暂停后，**恢复**&#x200B;动作变为可用，允许您恢复实时关系。

重新启用继承时，页面不会自动与源同步。 如果需要，您可以请求同步，可以执行以下任一操作：

* 在&#x200B;**恢复**/**恢复**&#x200B;对话框中；例如：

   ![chlimage_1-228](assets/chlimage_1-228.png)

* 在以后的阶段，手动选择同步操作。

>[!CAUTION]
>
>重新启用继承时，页面不会自动与源同步。 如果需要，您可以手动请求同步；在恢复或稍后恢复时。

#### 从页面属性{#resuming-inheritance-from-page-properties}恢复继承

一旦[挂起](#suspending-inheritance-from-page-properties),**恢复**&#x200B;操作就会出现在页面属性的工具栏中：

![chlimage_1-229](assets/chlimage_1-229.png)

选中后，将显示对话框。 您可以根据需要选择同步，然后确认操作。

#### 从Live Copy概述{#resume-a-live-copy-page-from-the-live-copy-overview}恢复Live Copy页面

选择Live Copy页面后，还可以从Live Copy概述](/help/sites-administering/msm-livecopy-overview.md#using-the-live-copy-overview)中执行[恢复操作。

1. 打开[Live Copy概述](/help/sites-administering/msm-livecopy-overview.md#using-the-live-copy-overview)并选择已挂起的Live Copy页面；将显示为&#x200B;**继承已取消**。
1. 从工具栏中选择&#x200B;**继续**。
1. 指示是否要在还原继承后同步页面，然后在&#x200B;**恢复Live Copy**&#x200B;对话框中确认&#x200B;**恢复**&#x200B;操作。

### 更改继承深度（浅／深）{#changing-inheritance-depth-shallow-deep}

在现有Live Copy上，可以更改页面深度；即是否包含子页面。

* 切换到浅Live Copy:

   * 将立即生效，不可逆。

      * 子页面与Live Copy显式分离。 如果撤消，则无法保留对子项的进一步修改。

      * 将删除任何子体`LiveRelationships`，即使存在嵌套`LiveCopies`。

* 切换到深层Live Copy:

   * 子页面保持不变。
   * 要查看交换机的效果，您可以进行转出，任何内容修改都会根据转出配置进行应用。

* 切换到浅Live Copy，然后返回深层：

   * （以前）浅层Live Copy的所有子项均被视为已手动创建，因此使用`[oldname]_msm_moved name`移走。

要指定或更改深度，请执行以下操作：

1. 使用&#x200B;**Sites**&#x200B;控制台的&#x200B;**视图属性**&#x200B;命令或使用页面工具栏上的&#x200B;**页面信息**&#x200B;打开Live Copy页面的属性。
1. 单击或点按&#x200B;**Live Copy**&#x200B;选项卡。
1. 在&#x200B;**配置**&#x200B;部分，根据是否包含子页面设置或清除&#x200B;**Live Copy继承**&#x200B;选项：

   * 选中——一个深层Live Copy（包含子页面）
   * 清除——浅层Live Copy（排除子页面）

   >[!CAUTION]
   >
   >切换到浅Live Copy将立即生效，并且不可撤消。
   >
   >有关详细信息，请参阅[Live Copy - Composition](/help/sites-administering/msm.md#live-copies-composition)。

1. 单击或点按&#x200B;**保存**&#x200B;以保留您的更新。

### 取消组件{#cancelling-inheritance-for-a-component}的继承

取消组件的Live Copy继承，以便组件不再与源组件同步。 如果需要，可以在以后启用继承。

>[!NOTE]
>
>重新启用继承时，组件不会自动与源同步。 如果需要，可以手动请求同步。

取消继承以更改组件内容或删除组件：

1. 单击或点按要取消继承的组件。

   ![chlimage_1-230](assets/chlimage_1-230.png)

1. 在组件工具栏上，单击或点按&#x200B;**取消继承**&#x200B;图标。

   ![图像](do-not-localize/chlimage_1-8.png)

1. 在“取消继承”对话框中，使用&#x200B;**Yes**&#x200B;确认操作。

   组件工具栏将更新为包含所有（适当）编辑命令。

### 为组件{#re-enabling-inheritance-for-a-component}重新启用继承

要为组件启用继承，请单击或点按组件工具栏上的&#x200B;**重新启用继承**&#x200B;图标。

![图像](do-not-localize/chlimage_1-9.png)

### 更改Live Copy页面{#changing-the-order-of-components-on-a-live-copy-page}上的组件顺序

如果Live Copy包含属于段落系统的组件，则该段落系统的继承遵循以下规则：

* 可修改继承段落系统中组件的顺序，即使已建立继承也是如此。
* 转出时，组件的顺序将从Blueprint中恢复。 如果在转出之前将新组件添加到Live Copy，则它们将与添加它们的组件一起重新排序。
* 如果取消段落系统的继承，则转出时将不恢复组件的顺序，并将保持Live Copy中的原样。

>[!NOTE]
>
>在段落系统上还原取消的继承时，组件&#x200B;**的顺序不会自动从蓝图中还原**。 如果需要，可以手动请求同步。

请按照以下过程取消段落系统的继承。

1. 打开Live Copy页面。
1. 将现有组件拖到页面上的新位置。
1. 在&#x200B;**取消继承**&#x200B;对话框中，使用&#x200B;**是**&#x200B;确认操作。

### 覆盖Live Copy页面{#overriding-properties-of-a-live-copy-page}的属性

默认情况下，Live Copy页面的页面属性会从源页面继承（且不可编辑）。

当需要更改Live Copy的属性值时，可以取消属性的继承。 链接图标指示已为属性启用继承。

![chlimage_1-231](assets/chlimage_1-231.png)

取消继承时，可以更改属性值。 断开链接图标表示继承已取消。

![chlimage_1-232](assets/chlimage_1-232.png)

如果需要，您以后可以重新为属性启用继承。

>[!NOTE]
>
>重新启用继承时，Live Copy页面属性不会自动与源属性同步。 如果需要，可以手动请求同步。

1. 使用页面工具栏上的&#x200B;**站点**&#x200B;控制台的&#x200B;**视图属性**&#x200B;选项或&#x200B;**页面信息**&#x200B;图标打开Live Copy页面的属性。
1. 要取消属性的继承，请单击或点按属性右侧显示的链接图标。

   ![图像](do-not-localize/chlimage_1-10.png)

1. 在&#x200B;**取消继承**&#x200B;确认对话框中，单击或点按&#x200B;**是**。

### 还原Live Copy页面{#revert-properties-of-a-live-copy-page}的属性

要为属性启用继承，请单击或点按属性旁边显示的&#x200B;**还原继承**&#x200B;图标。

![图像](do-not-localize/chlimage_1-11.png)

### 重置Live Copy页面{#resetting-a-live-copy-page}

将Live Copy页面重置为：

* 删除所有继承取消和
* 将页面返回到与源页面相同的状态。

重置会影响您对页面属性、段落系统和组件所做的更改。

#### 从页面属性{#reset-a-live-copy-page-from-the-page-properties}重置Live Copy页面

1. 在&#x200B;**站点**&#x200B;控制台中，选择Live Copy页面，然后选择&#x200B;**视图属性**。
1. 打开&#x200B;**Live Copy**&#x200B;选项卡。
1. 从工具栏中选择&#x200B;**重置**。

   ![chlimage_1-233](assets/chlimage_1-233.png)

1. 在&#x200B;**重置Live Copy**&#x200B;对话框中，使用&#x200B;**重置**&#x200B;进行确认。

#### 从Live Copy概述{#reset-a-live-copy-page-from-the-live-copy-overview}重置Live Copy页面

选择Live Copy页面后， Live Copy概述](/help/sites-administering/msm-livecopy-overview.md#using-the-live-copy-overview)中也提供[重置操作。

1. 打开[Live Copy概述](/help/sites-administering/msm-livecopy-overview.md#using-the-live-copy-overview)并选择Live Copy页面。
1. 从工具栏中选择&#x200B;**重置**。
1. 在&#x200B;**重置Live Copy**&#x200B;对话框中确认&#x200B;**重置**&#x200B;操作：

   ![chlimage_1-234](assets/chlimage_1-234.png)

## 将Live Copy页面与Blueprint页面{#comparing-a-live-copy-page-with-a-blueprint-page}进行比较

要跟踪您所做的更改，可以在&#x200B;**引用**&#x200B;中视图Blueprint页面，并将其与其Live Copy页面进行比较：

1. 在&#x200B;**站点**&#x200B;控制台中，[导航到Blueprint或Live Copy页面，然后选择它](/help/sites-authoring/basic-handling.md#viewing-and-selecting-resources)。
1. 打开&#x200B;**[引用](/help/sites-authoring/basic-handling.md#references)**&#x200B;面板并选择：

   * **Blueprint** （当选择Live Copy页面时）
   * **Live Copy** （当选择了Blueprint页面时）

1. 选择您的特定Live Copy，然后：

   * **与Blueprint比较** （当选择Live Copy页面时）
   * **与Live Copy比较** （当选择了Blueprint页面时）

   例如：

   ![chlimage_1-235](assets/chlimage_1-235.png)

1. 两个页面（Live Copy和Blueprint）将并排打开。

   有关使用此功能的完整信息，请参阅[页面差异](/help/sites-authoring/page-diff.md)。

## 分离Live Copy {#detaching-a-live-copy}

“分离”将永久删除Live Copy与其源／蓝图页面之间的Live关系。 所有与MSM相关的属性都会从Live Copy中删除，并且Live Copy页面会变为独立副本。

>[!CAUTION]
>
>在分离Live Copy后，不能恢复Live Relationship。
>
>要删除与以后重新启用的选项的Live Relationship，您可以[取消页面的Live Copy继承](#suspending-inheritance-for-a-page)。

使用&#x200B;**Detach**&#x200B;的树中的位置有含义：

* **在LiveCopy的根页面上分离**

   在Live Copy的根页面上执行此操作时，将删除Blueprint的所有页面与其Live Copy之间的Live关系。

   对Blueprint中的页面（原样）**的进一步更改不会**&#x200B;影响Live Copy（原样）。

* **在LiveCopy的子页面上分离**

   在Live Copy的子页面（或分支）上执行此操作时：

   * 该子页面（或分支）的实时关系将被删除
   * 而Live Copy分支中的（子）页面则被视为是手动创建的。

   *但是*，子页面仍受父分支的实时关系的约束，因此进一步转出Blueprint页面将同时满足以下两个条件：

   1. 重命名已分离的页面：

      * 这是因为MSM将它们视为手动创建的页面，这会导致冲突，因为它们的名称与其尝试创建的Live Copy页面相同。
   1. 使用原始名称创建新(Live Copy)页面，其中包含转出中的更改。

   >[!NOTE]
   >
   >请参阅[MSM转出冲突](/help/sites-administering/msm-rollout-conflicts.md)以了解此类情况的详细信息。

### 从页面属性{#detach-a-live-copy-page-from-the-page-properties}中分离Live Copy页面

分离Live Copy:

1. 在&#x200B;**站点**&#x200B;控制台中，选择Live Copy页面，然后单击或点按&#x200B;**视图属性**。
1. 打开&#x200B;**Live Copy**&#x200B;选项卡。
1. 在工具栏上，选择&#x200B;**分离**。

   ![chlimage_1-236](assets/chlimage_1-236.png)

1. 将显示确认对话框，选择&#x200B;**分离**&#x200B;以完成操作。

### 从Live Copy概述{#detach-a-live-copy-page-from-the-live-copy-overview}中分离Live Copy页面

选择Live Copy页面后，还可以从Live Copy概述](/help/sites-administering/msm-livecopy-overview.md#using-the-live-copy-overview)中执行[分离操作。

1. 打开[Live Copy概述](/help/sites-administering/msm-livecopy-overview.md#using-the-live-copy-overview)并选择Live Copy页面。
1. 从工具栏中选择&#x200B;**分离**。
1. 在&#x200B;**分离Live Copy**&#x200B;对话框中确认&#x200B;**分离**&#x200B;操作：

   ![chlimage_1-237](assets/chlimage_1-237.png)
