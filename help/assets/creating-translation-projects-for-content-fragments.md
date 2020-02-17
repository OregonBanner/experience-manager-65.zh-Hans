---
title: 为内容片段创建翻译项目
seo-title: 为内容片段创建翻译项目
description: 了解如何翻译内容片段。
seo-description: 了解如何翻译内容片段。
uuid: 23176e70-4003-453c-af25-6499a5ed3f6d
contentOwner: heimoz
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: managing-assets
content-type: reference
discoiquuid: d2decc31-a04b-4a8e-bb19-65f21cf7107e
translation-type: tm+mt
source-git-commit: 48fd5ddb386d69795291e560fa7b21da6edf5979

---


# 为内容片段创建翻译项目 {#creating-translation-projects-for-content-fragments}

除了资产外，Adobe Experience Manager(AEM)资产还支持内容片段（包括变量）的语 [言复制工作流](content-fragments.md) 。 在内容片段上运行语言副本工作流不需要任何其他优化。 在每个工作流中，将发送整个内容片段以进行翻译。

您可以在内容片段上运行的工作流类型与您为资产运行的工作流类型完全相同。 此外，每个工作流类型中的可用选项与资产相应工作流类型下的可用选项相匹配。

您可以在内容片段上运行以下类型的语言复制工作流：

**创建和翻译**

在此工作流中，要翻译的内容片段将复制到要翻译的语言的语言的语言根目录中。 此外，根据您选择的选项，将在“项目”控制台中为内容片段创建一个翻译项目。 根据设置，可以手动启动翻译项目，也可以允许翻译项目在创建后立即自动运行。

**更新语言副本**

更新或修改源内容片段时，相应的区域设置／语言特定内容片段需要重新编译。 更新语言副本工作流程转换另一组内容片段，并将其包含在特定区域设置的语言副本中。 在这种情况下，已翻译的内容片段将添加到已包含先前已翻译的内容片段的目标文件夹。

## 创建和翻译工作流 {#create-and-translate-workflow}

创建和翻译工作流包含以下选项。 与每个选项关联的过程步骤与与与资产的相应选项关联的步骤类似。

* 仅创建结构：有关过程步骤，请参阅 [仅为资产创建结构](translation-projects.md#create-structure-only)。
* 创建新翻译项目：有关过程步骤，请参 [阅为资产创建新的翻译项目](translation-projects.md#create-a-new-translation-project)。
* 添加到现有翻译项目：有关过程步骤，请参 [阅添加到资产的现有翻译项目](translation-projects.md#add-to-existing-translation-project)。

## 更新语言副本工作流 {#update-language-copies-workflow}

更新语言副本工作流包含以下选项。 与每个选项关联的过程步骤与与与资产的相应选项关联的步骤类似。

* 创建新翻译项目：有关过程步骤，请参 [阅为资产创建新的翻译项目](translation-projects.md#create-a-new-translation-project) （更新工作流）。
* 添加到现有翻译项目：有关过程步骤，请参 [阅添加到资产的现有翻译项目](translation-projects.md#add-to-existing-translation-project) （更新工作流）。

您还可以为片段创建临时语言副本，这与为资产创建临时副本的方式类似。 有关详细信息，请 [参阅为资产创建临时语言副本](translation-projects.md#creating-temporary-language-copies)。

## 翻译混合媒体片段 {#translating-mixed-media-fragments}

AEM允许您翻译包含各种类型的媒体资产和集合的内容片段。 如果您翻译包含内联资产的内容片段，则这些资产的翻译后副本将存储在目标语言根目录下。

如果内容片段包括集合，则集合中的资产将与内容片段一起翻译。 资产的已翻译副本存储在相应的目标语言根目录下，该目录位置与源资产在源语言根目录下的物理位置相匹配。

要能够翻译包含混合媒体的内容片段，请首先编辑默认的翻译框架，以启用与内容片段关联的内联资产和集合的翻译。

1. 单击／点按AEM徽标，然后导航到工 **[!UICONTROL 具>部署>云服务]**。
1. 在 **[!UICONTROL Adobe Marketing cloud下找到]****[!UICONTROL 翻译集成]**，然后单击／点按 **[!UICONTROL 显示配置]**。

   ![chlimage_1-444](assets/chlimage_1-444.png)

1. 从可用配置列表中，单击／点按默 **[!UICONTROL 认配置（翻译集成配置）]** ，以打开“默 **[!UICONTROL 认配置”页]** 。

   ![chlimage_1-445](assets/chlimage_1-445.png)

1. 单击工 **[!UICONTROL 具栏中的]** “编辑”以显示“翻译配 **[!UICONTROL 置”对话框]** 。

   ![chlimage_1-446](assets/chlimage_1-446.png)

1. 导航到“资 **[!UICONTROL 产]** ”选项卡，然后从“转 **[!UICONTROL 换内容片段资产”列表中选择“内联媒]** 体资产和关联的集合 **** ”。 Click/tap **[!UICONTROL OK]** to save the changes.

   ![chlimage_1-447](assets/chlimage_1-447.png)

1. 从英文根文件夹中，打开内容片段。

   ![chlimage_1-448](assets/chlimage_1-448.png)

1. 单击／点按插入 **[!UICONTROL 资产图标]** 。

   ![chlimage_1-449](assets/chlimage_1-449.png)

1. 将资产插入内容片段。

   ![将资产插入内容片段](assets/column-view.png)

1. 单击／点按关联 **[!UICONTROL 内容图标]** 。

   ![chlimage_1-451](assets/chlimage_1-451.png)

1. 单击／点按关 **[!UICONTROL 联内容]**。

   ![chlimage_1-452](assets/chlimage_1-452.png)

1. 选择一个集合并将其包含在内容片段中。 Click/tap **[!UICONTROL Save]**.

   ![chlimage_1-453](assets/chlimage_1-453.png)

1. 选择内容片段，然后单击／点按 **[!UICONTROL GlobalNav]** 图标。
1. 从菜 **[!UICONTROL 单中选择]** “引用”(References **[!UICONTROL )以显示“]** 引用”(References)窗格。

   ![chlimage_1-454](assets/chlimage_1-454.png)

1. 单击／点按 **[!UICONTROL 副本下的]****[!UICONTROL 语言副本]** ，以显示语言副本。

   ![chlimage_1-455](assets/chlimage_1-455.png)

1. 单击／点按 **[!UICONTROL 面板底部的创建和翻译]** ，以显示创建和翻 **[!UICONTROL 译对话框]** 。

   ![chlimage_1-456](assets/chlimage_1-456.png)

1. 从“目标语言”列表中选 **[!UICONTROL 择目标语言]** 。

   ![chlimage_1-457](assets/chlimage_1-457.png)

1. 从“项目”列表中选择翻译项 **[!UICONTROL 目类]** 型。

   ![chlimage_1-458](assets/chlimage_1-458.png)

1. 在“项目标题”框中指定项 **[!UICONTROL 目的标题]** ，然后单击／点按 **创建**。

   ![chlimage_1-459](assets/chlimage_1-459.png)

1. 导航到“项 **[!UICONTROL 目]** ”控制台，然后打开您创建的翻译项目的项目文件夹。

   ![chlimage_1-460](assets/chlimage_1-460.png)

1. 单击／点按项目拼贴以打开项目详细信息页面。

   ![chlimage_1-461](assets/chlimage_1-461.png)

1. 从翻译作业拼贴中，验证要翻译的资产数。
1. 从翻译作 **[!UICONTROL 业拼贴中]** ，启动翻译作业。

   ![chlimage_1-462](assets/chlimage_1-462.png)

1. 单击翻译作业拼贴底部的省略号以显示翻译作业的状态。

   ![chlimage_1-463](assets/chlimage_1-463.png)

1. 单击／点按内容片段以检查已翻译的关联资产的路径。

   ![chlimage_1-464](assets/chlimage_1-464.png)

1. 在“收藏集”控制台中查看收藏集的语言副本。

   ![chlimage_1-465](assets/chlimage_1-465.png)

   请注意，只有集合的内容是翻译的。 集合本身不进行翻译。

1. 导航到已翻译的关联资产的路径。 请注意，已翻译的资产存储在目标语言根目录下。

   ![chlimage_1-466](assets/chlimage_1-466.png)

1. 导航到与内容片段一起翻译的集合中的资产。 请注意，资产的已翻译副本存储在相应的目标语言根目录下。

   ![chlimage_1-467](assets/chlimage_1-467.png)

   >[!NOTE]
   >
   >将内容片段添加到现有项目或执行更新工作流的过程与资产的相应过程类似。 有关这些程序的指导，请参阅资产描述的程序。

