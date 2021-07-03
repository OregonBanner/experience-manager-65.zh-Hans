---
title: 使用MSM重复使用资产
description: 在从派生并链接到父资产的多个页面/文件夹中使用资产。 资产与主副本保持同步，单击几下即可从父资产接收更新。
contentOwner: AG
mini-toc-levels: 1
role: User, Admin, Architect
feature: 资产管理，多站点管理器
exl-id: 4d0367c4-88aa-4aef-b23d-828609b0df09
source-git-commit: bb46b0301c61c07a8967d285ad7977514efbe7ab
workflow-type: tm+mt
source-wordcount: '3371'
ht-degree: 9%

---

# 使用MSM为[!DNL Assets]重用资产 {#reuse-assets-using-msm-for-assets}

[!DNL Adobe Experience Manager]中的多站点管理器(MSM)功能使用户能够重复使用一次创作的内容，并在多个Web位置中重复使用。 与MSM一样，数字资产也可用于[!DNL Assets]功能。 对[!DNL Assets]使用MSM，您可以：

* 只需创建一次资产，然后复制这些资产，以便在站点的其他区域中重复使用。
* 同步保留多个副本，并更新一次原始主副本，以将更改推送到子副本。
* 通过暂时或永久暂停父资产和子资产之间的链接来进行本地更改。

## 前提条件 {#prereq}

要将MSM用于[!DNL Assets]，请至少安装[!DNL Experience Manager] 6.5 Service Pack 1。 有关更多信息，请参阅[最新Service Pack的发行说明](/help/release-notes/sp-release-notes.md)。

## 了解优势和概念 {#concepts}

### 工作原理和优势 {#how-it-works-and-the-benefits}

要了解在多个Web位置中重复使用相同内容（文本和资产）的使用方案，请参阅[可能的MSM方案](/help/sites-administering/msm.md)。 [!DNL Experience Manager] 在原始资产及其链接的副本(称为Live Copy(LC))之间维护一个链接。维护的链接允许将集中的更改推送到多个Live Copy。 这样可以在消除管理重复副本的限制的同时，更快地进行更新。 变化的传播是无误的和集中的。 利用功能，可以腾出空间进行仅限于选定Live Copy的更新。 用户可以分离链接（即中断继承），并在下次更新主副本并转出更改时，进行不被覆盖的本地编辑。 可以对一些选定的元数据字段或整个资产进行分离。 它允许灵活地在本地更新最初从主副本继承的资产。

MSM会在源资产及其Live Copy之间维护实时关系，以便：

* 对源资产所做的更改也会应用（转出）到Live Copy，即Live Copy与源同步。
* 您可以通过暂停Live关系来更新Live Copy，也可以删除一些有限字段的继承。 对源的修改将不再应用于Live Copy。

### [!DNL Assets]术语的MSM术语表 {#glossary}

**来源：** 原始资产或文件夹。从中派生Live Copy的主副本。

**Live Copy:** 与其源同步的源资产/文件夹的副本。Live Copy可以是其他Live Copy的源。 请参阅如何创建LC。

**继承：** Live Copy资产/文件夹及其源之间的链接/引用，系统会使用它记住将更新发送到的位置。元数据字段的继承存在于粒度级别。 可以为选择性元数据字段删除继承，同时保留源与其Live Copy之间的实时关系。

**转出：** 将对源所做的修改推送到下游的Live Copy的操作。可以使用转出操作一次性更新一个或多个Live Copy。 请参阅转出。

**转出配置：** 用于确定同步哪些属性、同步方式和同步时间的规则。创建Live Copy时会应用这些配置；稍后可以编辑；和子项可以从其父资产继承转出配置。 对于[!DNL Assets]的MSM，请仅使用标准转出配置。 其他转出配置不适用于[!DNL Assets]的MSM。

**同步：** 除了转出之外，还执行了另一项操作，即通过将更新从源发送到Live Copy来在源副本与其Live Copy之间实现对等。将为特定Live Copy启动同步，并且该操作将从源中提取更改。 使用此操作，只能更新其中一个Live Copy。 请参阅同步操作。

**暂停：** 临时删除Live Copy及其源资产/文件夹之间的Live关系。你可以恢复关系。 请参阅暂停操作。

**恢复：** 恢复Live关系，以便Live Copy再次开始从源接收更新。请参阅恢复操作。

**重置：** 重置操作会通过覆盖任何本地更改，使Live Copy再次成为源的副本。它还会删除继承取消和重置所有元数据字段的继承。 要在将来进行本地修改，必须再次取消特定字段的继承。 请参阅对LC的本地修改。

**分离：** 不可撤消地删除Live Copy资产/文件夹的Live关系。分离操作后，Live Copy将永远无法从源接收更新，并且不再是Live Copy。 请参阅删除关系。

## 创建资产的Live Copy {#createlc}

要从一个或多个源资产或文件夹创建Live Copy，请执行以下任一操作：

* 方法1:选择源资产，然后单击顶部工具栏中的&#x200B;**[!UICONTROL 创建]** > **[!UICONTROL Live Copy]** 。
* 方法2:在[!DNL Experience Manager]用户界面中，单击界面右上角的&#x200B;**[!UICONTROL 创建]** > **[!UICONTROL Live Copy]**。

您可以一次创建资产或文件夹的Live Copy。 您可以创建从资产或作为Live Copy本身的文件夹派生的Live Copy。 用例不支持内容片段(CF)。 尝试创建其Live Copy时，CF会按原样复制，而不与任何关系。 复制的CF是及时的快照，在更新原始CF时不会更新。

要使用第一种方法创建Live Copy，请执行以下步骤：

1. 选择源资产或文件夹。 在工具栏中，单击&#x200B;**[!UICONTROL 创建]** > **[!UICONTROL Live Copy]**。

   ![从界面创建Live  [!DNL Experience Manager] Copy](assets/create_lc1.png)

   *图：从界面创建 [!DNL Experience Manager] Live Copy。*

1. 选择目标文件夹。 单击&#x200B;**[!UICONTROL 下一步]**。
1. 提供标题和名称。 资产没有子项。 创建文件夹的Live Copy时，您可以选择包含或排除子项。
1. 选择转出配置。 单击&#x200B;**[!UICONTROL 创建]**。

要使用第二种方法创建Live Copy，请执行以下步骤：

1. 在[!DNL Experience Manager]界面的右上角，单击&#x200B;**[!UICONTROL 创建]** > **[!UICONTROL Live Copy]**。

   ![从界面创建Live  [!DNL Experience Manager] Copy](assets/create_lc2.png)

   *图：从界面创建 [!DNL Experience Manager] Live Copy。*

1. 选择源资产或文件夹。 单击&#x200B;**[!UICONTROL 下一步]**。
1. 选择目标文件夹。 单击&#x200B;**[!UICONTROL 下一步]**。
1. 提供标题和名称。 资产没有子项。 创建文件夹的Live Copy时，您可以选择包含或排除子项。
1. 选择转出配置。 单击&#x200B;**[!UICONTROL 创建]**。

>[!NOTE]
>
>移动源或Live Copy时，这些关系会保留。 删除Live Copy后，这些关系将被删除。

## 查看源和Live Copy的各种属性和状态 {#properties}

您可以从[!DNL Experience Manager]用户界面的各个区域查看Live Copy的信息和与MSM相关的状态，如关系、同步、转出等。

以下两种方法适用于资产和文件夹：

* 选择Live Copy资产，并在其“属性”页面中查找相应信息。
* 选择源文件夹，并从[!UICONTROL Live Copy控制台]中查找每个Live Copy的详细信息。

>[!TIP]
>
>要检查几个单独的Live Copy的状态，请使用第一个方法检查&#x200B;**[!UICONTROL Properties]**&#x200B;页面。 要检查多个Live Copy的状态，请使用第二种方法检查&#x200B;**[!UICONTROL 关系状态]**&#x200B;页面。

### Live Copy的信息和状态 {#statuslcasset}

要检查Live Copy资产或文件夹的信息和状态，请执行以下步骤。

1. 选择Live Copy资产或文件夹。 单击工具栏中的&#x200B;**[!UICONTROL 属性]**。 或者，使用键盘快捷键`p`。
1. 单击&#x200B;**[!UICONTROL Live Copy]**。 您可以检查源的路径、暂停状态、同步状态、上次转出日期以及执行上次转出的用户。

   ![Live Copy信息和状态显示在“属性”的控制台中](assets/lcfolder_info_properties.png)

   *图：Live Copy信息和状态。*

1. 如果子资产借用Live Copy配置，则可以启用或禁用。

1. 您可以选择Live Copy的选项，以从父项继承转出配置或更改配置。

### 文件夹所有Live Copy的信息和状态 {#status-lc-folder}

[!DNL Experience Manager] 提供了一个控制台，用于检查源文件夹所有Live Copy的状态。此控制台显示所有子资产的状态。

1. 选择源文件夹。 单击工具栏中的&#x200B;**[!UICONTROL 属性]**。 或者，使用键盘快捷键`p`。
1. 单击 **[!UICONTROL Live Copy 源]**。要打开控制台，请单击 **[!UICONTROL Live Copy 概述]**。此功能板提供所有子资产的顶级状态。

   ![在源的Live Copy控制台中查看Live Copy的状态](assets/livecopy-statuses.png)

   *图：在源的Live Copy控制台中 [!UICONTROL 查看Live ] Copy的状态。*

1. 要查看 Live Copy 文件夹中每个资产的详细信息，请选择一个资产，然后单击工具栏中的&#x200B;**[!UICONTROL 关系状态]**。

   ![文件夹中Live Copy子资产的详细信息和状态](assets/livecopy_relationship_status.png)

   文件夹中Live Copy子资产的详细信息和状态

>[!TIP]
>
>您可以快速查看其他文件夹的Live Copy状态，而无需浏览太多。 从&#x200B;**[!UICONTROL Live Copy概述]**&#x200B;界面的中上部更改文件夹。

### 从源的“引用”边栏中快速执行操作 {#refrailsource}

对于源资产或文件夹，您可以看到以下信息，并直接从“引用”边栏中执行以下操作：

* 请参阅Live Copy的路径。
* 在[!DNL Experience Manager]用户界面中打开或显示特定Live Copy。
* 将更新同步到特定Live Copy。
* 暂停关系或更改特定Live Copy的转出配置。
* 访问Live Copy概述控制台。

选择源资产或文件夹，打开左边栏，然后单击&#x200B;**[!UICONTROL 引用]**。 或者，选择一个资产或文件夹，然后使用键盘快捷键 `Alt + 4`。

![所选源的“引用”边栏中可用的操作和信息](assets/referencerail_source.png)

*图：所选源的“引用”边栏中可用的操作和信息。*

对于特定的Live Copy，单击&#x200B;**[!UICONTROL 编辑Live Copy]**&#x200B;以暂停关系或更改转出配置。

![对于特定的Live Copy，在选择源资产时，可以从引用边栏访问暂停关系或更改转出配置的选项](assets/referencerail_editlc_options.png)

*图：暂停关系或更改特定Live Copy的转出配置。*

### Live Copy的“引用”边栏中的快速操作 {#ref-rail-lc}

对于Live Copy资产或文件夹，您可以看到以下信息，并直接从“引用”边栏中执行以下操作：

* 查看源的路径。
* 在[!DNL Experience Manager]用户界面中打开或显示特定Live Copy。
* 推出更新。

选择 Live Copy 资产或文件夹，打开左边栏，然后单击&#x200B;**[!UICONTROL 引用]**。或者，选择一个资产或文件夹，然后使用键盘快捷键 `Alt + 4`。

![所选 Live Copy 的“引用”边栏中的可用操作](assets/referencerail_livecopy.png)

*图：所选Live Copy的“引用”边栏中可用的操作。*

## 将修改从源传播到Live Copy {#rolloutsync}

修改源后，可以使用同步操作或转出操作将更改传播到Live Copy。 要了解这两个操作之间的差异，请参阅[术语表](#glossary)。

### 转出操作 {#rollout}

您可以从源资产启动转出操作，并更新所有或几个选定的Live Copy。

1. 选择Live Copy资产或文件夹。 单击工具栏中的&#x200B;**[!UICONTROL 属性]**。 或者，使用键盘快捷键`p`。
1. 单击 **[!UICONTROL Live Copy 源]**。单击工具栏中的&#x200B;**[!UICONTROL 转出]**。
1. 选择要更新的Live Copy。 单击&#x200B;**[!UICONTROL 转出]**。
1. 要转出对子资产所做的更新，请选择&#x200B;**[!UICONTROL 转出源和所有子资产]**。

   ![将源的修改转出到几个或所有Live Copy](assets/livecopy_rollout_page.png)

   *图：将源的修改转出到几个或所有Live Copy。*

>[!NOTE]
>
>在源资产中所做的修改将仅转出到直接相关的Live Copy。 如果Live Copy是从其他Live Copy派生的，则修改不会转出到派生的Live Copy。

或者，您也可以在选择特定的Live Copy后，从引用边栏中启动转出操作。 有关更多信息，请参阅Live Copy的“引用”边栏中的[快速操作](#ref-rail-lc)。 在此转出方法中，只更新选定的Live Copy及其子项（可选）。

![将源的修改转出到选定的Live Copy](assets/livecopy_rollout_dialog.png)

*图：将源的修改转出到选定的Live Copy。*

### 关于同步操作 {#about-sync}

同步操作仅将源中的修改提取到选定的Live Copy。 同步操作会尊重并维护在取消继承后完成的本地修改。 不会覆盖本地修改，并且取消的继承也不会重新建立。 您可以通过三种方式启动同步操作。

| 在[!DNL Experience Manager]接口中的位置 | 使用时间和原因 | 使用方法 |
|---|---|---|
|  引用边栏 | 已选择源时快速同步。 | 请参阅[源的“引用”边栏中的快速操作](#refrailsource) |
| [!UICONTROL 属性]页面中的工具栏 | 在已打开Live Copy属性时启动同步。 | 请参阅[同步Live Copy](#sync-lc) |
| [!UICONTROL Live Copy概述控] 制台 | 选择源文件夹或[!UICONTROL Live Copy概述]控制台已打开时，可快速同步多个资产（不一定是全部）。 每次为一个资产启动同步操作，但这是一次为多个资产同步的更快方式。 | 请参阅[对Live Copy文件夹中许多资产执行的操作](#bulk-actions) |

### 同步Live Copy {#sync-lc}

要开始同步操作，请打开Live **[!UICONTROL Copy的]** “属性”页，单击 **[!UICONTROL Live Copy]** ，然后单击工具栏中所需的操作。

要查看与同步操作相关的状态和信息，请参 [阅Live Copy的信息和状态](#statuslcasset) ，以 [及文件夹所有Live Copy的信息和状态](#status-lc-folder)。

![同步操作会提取对源所做的更改](assets/livecopy_sync.png)

*图：同步操作会提取对源所做的更改。*

>[!NOTE]
>
>如果关系暂停，则同步操作在工具栏中不可用。 虽然同步操作在引用边栏中可用，但即使成功转出后，修改也不会传播。

## 暂停和恢复关系 {#suspend-resume}

您可以暂时暂停关系，以阻止Live Copy接收对源资产或文件夹所做的修改。 还可以恢复Live Copy的关系，以开始从源接收修改。

要暂停或继续，请打 **[!UICONTROL 开Live Copy的]** “属性”页面，单击 **[!UICONTROL Live Copy]** ，然后从工具栏中单击所需的操作。

或者，您也可以从 **[!UICONTROL Live Copy 概述]**&#x200B;控制台快速暂停或恢复 Live Copy 文件夹中多个资产的关系。请参阅[对 Live Copy 文件夹中的许多资产执行操作](#bulk-actions)。

## 对Live Copy进行本地修改 {#local-mods}

Live Copy是创建时原始源的副本。 Live Copy的元数据值继承自源。 元数据字段单独维护与源资产相应字段的继承。

但是，您可以灵活地对Live Copy进行本地修改，以更改一些选定的属性。 要进行本地修改，请取消所需属性的继承。 取消一个或多个元数据字段的继承后，资产的实时关系和其他元数据字段的继承将保留。 任何同步或转出不会覆盖本地修改。 为此，请打开Live Copy资产的&#x200B;**[!UICONTROL 属性]**&#x200B;页面，单击元数据字段旁边的&#x200B;**[!UICONTROL 取消继承]**&#x200B;选项。

您可以撤消所有本地修改并将资产还原到其源的状态。 可撤消且立即重置操作将覆盖所有本地修改，并重新建立所有元数据字段的继承。 要还原，请从Live Copy资产的&#x200B;**[!UICONTROL 属性]**&#x200B;页面中，单击工具栏中的&#x200B;**[!UICONTROL 重置]** 。

![重置操作会覆盖本地编辑，并部分将Live Copy的源引入其中。](assets/livecopy_reset.png)

*图：重置操作会覆盖本地编辑，并部分将Live Copy的源引入其中。*

## 删除实时关系 {#detach}

您可以使用“分离”操作完全删除源与Live Copy之间的关系。 分离后，Live Copy将成为独立的资产或文件夹。 在分离后立即在[!DNL Experience Manager]界面中显示为新资产。 要从Live Copy的源中分离Live Copy，请执行以下步骤。

1. 选择Live Copy资产或文件夹。 单击工具栏中的&#x200B;**[!UICONTROL 属性]**。 或者，使用键盘快捷键`p`。

1. 单击&#x200B;**[!UICONTROL Live Copy]**。 单击工具栏中的&#x200B;**[!UICONTROL Detach]**。 在显示的对话框中，单击&#x200B;**[!UICONTROL Detach]**。

   ![“分离”操作会完全删除源副本和Live Copy之间的关系](assets/livecopy_detach.png)

   *图：“分离”操作会完全删除源副本与Live Copy之间的关系。*

   >[!CAUTION]
   >
   >在对话框中单击&#x200B;**[!UICONTROL Detach]**&#x200B;后，该关系会立即删除。 无法通过单击“属性”页面上的&#x200B;**[!UICONTROL 取消]**&#x200B;来撤消该操作。

或者，您也可以从&#x200B;**[!UICONTROL Live Copy概述]**&#x200B;控制台中快速分离Live Copy文件夹中的多个资产。 请参阅[对 Live Copy 文件夹中的许多资产执行操作](#bulk-actions)。

## Live Copy文件夹中的批量操作 {#bulk-actions}

如果您在Live Copy文件夹中包含多个资产，则对每个资产启动操作可能会非常繁琐。 您可以从[!UICONTROL Live Copy控制台]快速对许多资产启动基本操作。 上述方法可继续用于单个资产。

1. 选择源文件夹。 单击工具栏中的&#x200B;**[!UICONTROL 属性]**。 或者，使用键盘快捷键`p`。
1. 单击 **[!UICONTROL Live Copy 源]**。要打开控制台，请单击 **[!UICONTROL Live Copy 概述]**。
1. 在此功能板中，从 Live Copy 文件夹中选择 Live Copy 资产。单击工具栏中的所需操作。可用的操作有&#x200B;**[!UICONTROL 同步]**、**[!UICONTROL 重置]**、**[!UICONTROL 暂停]**&#x200B;和&#x200B;**[!UICONTROL 分离]**。您可以对任意数量的Live Copy文件夹中与选定源文件夹存在Live关系的任何资产快速启动这些操作。

   ![从Live Copy概述控制台轻松更新Live Copy文件夹中的许多资产](assets/livecopyconsole_update_many_assets.png)

   *图：从Live Copy概述控制台轻松更新Live Copy文件夹 [!UICONTROL 中的许] 多资产。*

## 为[!DNL Assets]扩展MSM {#extend-api}

[!DNL Experience Manager] 用于使用MSM Java API扩展功能。对于[!DNL Assets]，扩展的工作方式与与用于[!DNL Sites]的MSM相同。 有关详细信息，请参阅[扩展MSM](/help/sites-developing/extending-msm.md)以及以下内容，以了解有关特定任务的信息：

* [API概述](/help/sites-developing/extending-msm.md#overview-of-the-java-api)
* [创建同步操作](/help/sites-developing/extending-msm.md#creating-a-new-synchronization-action)
* [创建转出配置](/help/sites-developing/extending-msm.md#creating-a-new-rollout-configuration)
* [创建并使用一个简单的LiveActionFactory类](/help/sites-developing/extending-msm.md#creating-and-using-a-simple-liveactionfactory-class)

>[!NOTE]
>
>* [!DNL Sites]的MSM中的Blueprint在MSM中称为[!DNL Assets]的Live Copy源。
>* 对于[!DNL Assets],MSM不支持删除创建站点向导中的章节步骤。
>* 对于[!DNL Assets],MSM不支持在页面属性（触屏UI）上配置MSM锁定。


## 资产管理任务对Live Copy的影响 {#manage-assets}

Live Copy和源是可在一定程度上作为数字资产进行管理的资产或文件夹。 [!DNL Experience Manager]中的某些资产管理任务对Live Copy具有特定影响。

* 复制Live Copy时，会创建一个与第一个Live Copy具有相同源的Live Copy资产。
* 移动源或其Live Copy时，Live关系会保留。
* “编辑”操作不适用于Live Copy资产。 如果Live Copy的源本身是Live Copy，则编辑操作不适用于它。
* 签出操作不适用于Live Copy资产。
* 对于源文件夹，可使用创建审核任务的选项。
* 在列表视图和列视图中查看资产列表时，Live Copy资产或文件夹会针对该资产显示“Live Copy”。 它可帮助您轻松识别文件夹中的Live Copy。

## 比较[!DNL Assets]和[!DNL Sites]的MSM {#comparison}

在更多情况下，[!DNL Assets]的MSM与站点功能的MSM行为相匹配。 需要注意的一些关键区别是：

* [!DNL Sites]的MSM中的Blueprint在MSM中称为[!DNL Assets]的Live Copy源。
* 在站点中，您可以比较Blueprint及其Live Copy，但是在[!DNL Assets]中无法将源与其Live Copy进行比较。
* 无法在[!DNL Assets]中编辑Live Copy。
* 网站通常有子项，但[!DNL Assets]没有子项。 创建单个资产的Live Copy时，不显示包含或排除子项的选项。
* 对于[!DNL Assets],MSM不支持删除创建站点向导中的章节步骤。
* 对于[!DNL Assets],MSM不支持在页面属性（触屏UI）上配置MSM锁定。
* 对于[!DNL Assets]的MSM，请仅使用&#x200B;**[!UICONTROL 标准转出配置]**。 其他转出配置不适用于[!DNL Assets]的MSM。

## 最佳实践 {#best-practices}

MSM的一些最佳实践包括：

* 在开始实施之前，规划资产和内容流的父子关系。

## [!DNL Assets]的MSM限制和已知问题 {#limitations}

以下是[!DNL Assets]的MSM限制。

* 用例不支持内容片段(CF)。 尝试创建其Live Copy时，CF会按原样复制，而不与任何关系。 复制的CF是及时的快照，在更新原始CF时不会更新。

* 启用元数据写回后，MSM无法工作。 写回时，继承会中断。
