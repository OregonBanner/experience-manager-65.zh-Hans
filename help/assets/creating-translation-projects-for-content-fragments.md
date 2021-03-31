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
feature: 内容片段
role: 业务从业者，管理员
translation-type: tm+mt
source-git-commit: aec4530fa93eacd151ca069c2da5d1bc92408e10
workflow-type: tm+mt
source-wordcount: '992'
ht-degree: 0%

---


# 为内容片段{#creating-translation-projects-for-content-fragments}创建翻译项目

除资产外，Adobe Experience Manager(AEM)资产还支持[内容片段](/help/assets/content-fragments/content-fragments.md)（包括变量）的语言复制工作流。 在内容片段上运行语言副本工作流不需要任何其他优化。 在每个工作流中，都会发送整个内容片段以供翻译。

您可以在内容片段上运行的工作流类型与您为资产运行的工作流类型非常相似。 此外，每个工作流类型中的可用选项都与资产相应工作流类型下的可用选项相匹配。

您可以对内容片段运行以下类型的语言复制工作流:

**创建和翻译**

在此工作流中，要翻译的内容片段会被复制到要翻译的语言的语言的语言根目录。 此外，根据您选择的选项，系统会在“项目”控制台中为内容片段创建一个翻译项目。 根据设置，可以手动启动翻译项目，也可以允许在创建翻译项目后自动运行。

**更新语言副本**

更新或修改源内容片段时，相应的区域设置/语言特定内容片段需要重新编译。 更新语言副本工作流将翻译一组额外的内容片段并将其包含在针对特定区域设置的语言副本中。 在这种情况下，已翻译的内容片段将添加到已包含以前翻译的内容片段的目标文件夹。

## 创建和翻译工作流{#create-and-translate-workflow}

创建和翻译工作流包含以下选项。 与每个选项关联的过程步骤与与资产的相应选项关联的步骤类似。

* 仅创建结构：有关过程步骤，请参阅[仅为资产创建结构](translation-projects.md#create-structure-only)。
* 创建新翻译项目：有关过程步骤，请参阅[为资产](translation-projects.md#create-a-new-translation-project)创建新的翻译项目。
* 添加到现有翻译项目：有关过程步骤，请参阅[添加到资产的现有翻译项目](translation-projects.md#add-to-existing-translation-project)。

## 更新语言副本工作流{#update-language-copies-workflow}

更新语言副本工作流包含以下选项。 与每个选项关联的过程步骤与与资产的相应选项关联的步骤类似。

* 创建新翻译项目：有关过程步骤，请参阅[为资产](translation-projects.md#create-a-new-translation-project)创建新的翻译项目（更新工作流）。
* 添加到现有翻译项目：有关过程步骤，请参阅[添加到资产的现有翻译项目](translation-projects.md#add-to-existing-translation-project)（更新工作流）。

您还可以为片段创建临时语言副本，这与为资产创建临时副本的方式类似。 有关详细信息，请参阅[为资产创建临时语言副本](translation-projects.md#creating-temporary-language-copies)。

## 转换混合媒体片段{#translating-mixed-media-fragments}

AEM允许您翻译包含各种类型媒体资产和集合的内容片段。 如果您翻译包含内联资产的内容片段，则这些资产的已翻译副本会存储在目标语言根目录下。

如果内容片段包含集合，则集合中的资产将与内容片段一起进行翻译。 资产的已翻译副本存储在相应的目标语言根目录中，该目录位置与源资产在源语言根目录下的物理位置相匹配。

要能够翻译包含混合媒体的内容片段，请首先编辑默认翻译框架，以启用内联资产和与内容片段关联的集合的翻译。

1. 单击/点按AEM徽标，然后导航到&#x200B;**[!UICONTROL 工具>部署>Cloud Services]**。
1. 在&#x200B;**[!UICONTROL Adobe Marketing Cloud]**&#x200B;下找到&#x200B;**[!UICONTROL Translation Integration]**，然后单击/点按&#x200B;**[!UICONTROL 显示配置]**。

   ![chlimage_1-444](assets/chlimage_1-444.png)

1. 在可用配置的列表中，单击/点按&#x200B;**[!UICONTROL 默认配置（翻译集成配置）]**&#x200B;以打开&#x200B;**[!UICONTROL 默认配置]**&#x200B;页。

   ![chlimage_1-445](assets/chlimage_1-445.png)

1. 单击工具栏中的&#x200B;**[!UICONTROL 编辑]**&#x200B;以显示&#x200B;**[!UICONTROL 翻译配置]**&#x200B;对话框。

   ![chlimage_1-446](assets/chlimage_1-446.png)

1. 导航到&#x200B;**[!UICONTROL 资产]**&#x200B;选项卡，然后从&#x200B;**[!UICONTROL 转换内容片段资产]**&#x200B;列表中选择&#x200B;**[!UICONTROL 内联媒体资产和关联集合]**。 单击/点按&#x200B;**[!UICONTROL 确定]**&#x200B;以保存更改。

   ![chlimage_1-447](assets/chlimage_1-447.png)

1. 从英文根文件夹中，打开内容片段。

   ![chlimage_1-448](assets/chlimage_1-448.png)

1. 单击/点按&#x200B;**[!UICONTROL 插入资产]**&#x200B;图标。

   ![chlimage_1-449](assets/chlimage_1-449.png)

1. 将资产插入内容片段。

   ![将资产插入到内容片段](assets/column-view.png)

1. 单击/点按&#x200B;**[!UICONTROL 关联内容]**&#x200B;图标。

   ![chlimage_1-451](assets/chlimage_1-451.png)

1. 单击/点按&#x200B;**[!UICONTROL 关联内容]**。

   ![chlimage_1-452](assets/chlimage_1-452.png)

1. 选择一个集合并将其包含在内容片段中。 单击/点按&#x200B;**[!UICONTROL 保存]**。

   ![chlimage_1-453](assets/chlimage_1-453.png)

1. 选择内容片段，然后单击/点按&#x200B;**[!UICONTROL GlobalNav]**&#x200B;图标。
1. 从菜单中选择&#x200B;**[!UICONTROL 引用]**&#x200B;以显示&#x200B;**[!UICONTROL 引用]**&#x200B;窗格。

   ![chlimage_1-454](assets/chlimage_1-454.png)

1. 单击/点按&#x200B;**[!UICONTROL 副本]**&#x200B;下的&#x200B;**[!UICONTROL 语言副本]**&#x200B;以显示语言副本。

   ![chlimage_1-455](assets/chlimage_1-455.png)

1. 单击/点按面板底部的&#x200B;**[!UICONTROL 创建和翻译]**&#x200B;以显示&#x200B;**[!UICONTROL 创建和翻译]**&#x200B;对话框。

   ![chlimage_1-456](assets/chlimage_1-456.png)

1. 从&#x200B;**[!UICONTROL 目标语言]**&#x200B;列表中选择目标语言。

   ![chlimage_1-457](assets/chlimage_1-457.png)

1. 从&#x200B;**[!UICONTROL Project]**&#x200B;列表中选择翻译项目类型。

   ![chlimage_1-458](assets/chlimage_1-458.png)

1. 在&#x200B;**[!UICONTROL 项目标题]**&#x200B;框中指定项目标题，然后单击/点按&#x200B;**创建**。

   ![chlimage_1-459](assets/chlimage_1-459.png)

1. 导航到&#x200B;**[!UICONTROL Projects]**&#x200B;控制台，然后打开您创建的翻译项目的项目文件夹。

   ![chlimage_1-460](assets/chlimage_1-460.png)

1. 单击/点按项目拼贴以打开项目详细信息页面。

   ![chlimage_1-461](assets/chlimage_1-461.png)

1. 在翻译作业拼贴中，验证要翻译的资产数。
1. 从&#x200B;**[!UICONTROL 转换作业]**&#x200B;拼贴中，开始转换作业。

   ![chlimage_1-462](assets/chlimage_1-462.png)

1. 单击“翻译作业”拼贴底部的省略号以显示翻译作业的状态。

   ![chlimage_1-463](assets/chlimage_1-463.png)

1. 单击/点按内容片段以检查已翻译的关联资产的路径。

   ![chlimage_1-464](assets/chlimage_1-464.png)

1. 在“收藏集”控制台中查看收藏集的语言副本。

   ![chlimage_1-465](assets/chlimage_1-465.png)

   请注意，只翻译集合的内容。 集合本身不会翻译。

1. 导航到已转换的关联资产的路径。 请注意，已翻译的资产存储在目标语言根目录下。

   ![chlimage_1-466](assets/chlimage_1-466.png)

1. 导航到与内容片段一起转换的集合中的资产。 请注意，资产的已翻译副本会以适当的目标语言根存储。

   ![chlimage_1-467](assets/chlimage_1-467.png)

   >[!NOTE]
   >
   >将内容片段添加到现有项目或执行更新工作流的过程与资产的相应过程类似。 有关该等程序的指引，请参阅有关资产的程序。

