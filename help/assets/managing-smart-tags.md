---
title: 管理智能标记和搜索
description: 更新或删除不准确的智能标记，以提高标记的相关性
contentOwner: AG
translation-type: tm+mt
source-git-commit: 566add37d6dd7efe22a99fc234ca42878f050aee
workflow-type: tm+mt
source-wordcount: '448'
ht-degree: 0%

---


# 管理智能标记和搜索 {#manage-smart-tags-and-searches}

<!--
TBD: This article should be merged into a new, uber article for Smart Tags. Delete this article then. Cloud service article is merged.
-->

您可以创建智能标记来删除可能分配给您的品牌图像的任何不准确标记，以便只显示最相关的标记。

调节智能标签还可确保图像显示在最相关标签的搜索结果中，从而帮助优化基于标签的图像搜索。 从根本上说，它有助于消除不相关图像在搜索结果中出现的可能性。

您还可以为标记分配更高的等级，以提高其与图像的相关性。 提升图像的标记可提高当基于特定标记执行搜索时在搜索结果中出现图像的可能性。

1. 在“全局搜索”框中，根据标记搜索资产。
1. 检查搜索结果以识别与搜索不相关的图像。
1. 选择图像，然后单击工 **[!UICONTROL 具栏中的]** “管理标记”。
1. 从“管 **[!UICONTROL 理标记]** ”页面检查标记。 如果不希望根据特定标记搜索图像，请选择该标记，然后单击工 **[!UICONTROL 具栏]** 中的删除。 或者，单 `X` 击标签旁边显示的符号。
1. 要为标记分配更高的等级，请选择标记，然后单 **[!UICONTROL 击工]** 具栏中的提升。 您提升的标记将移到“标记 **[!UICONTROL ”部]** 分。
1. Click **[!UICONTROL Save]**, and then click **[!UICONTROL OK]** to close the Success dialog.
1. 导航到图像的属性页面。 请注意，您提升的标记具有较高的相关性，因此在搜索结果中显示得更高。

## 通过智能标记了解Experience Manager搜索结果 {#understandsearch}

默认情况下，Experience Manager搜索将搜索词与子句 `AND` 组合。 使用智能标记不会更改此默认行为。 使用智能标记可添加 `OR` 一个附加子句，以在应用智能标记中查找任何搜索词。 For example, consider searching for `woman running`. 默认情况下， `woman` 元数据 `running` 中仅包含关键字的资产不会显示在搜索结果中。 但是，在此类搜索查询中， `woman` 会显 `running` 示带有或使用智能标记的资产。 搜索结果是，

* 元数据 `woman` 中 `running` 包含和关键字的资产。

* 使用任一关键字标记的资产智能。

首先显示与元数据字段中所有搜索词匹配的搜索结果，然后显示与智能标记中任何搜索词匹配的搜索结果。 在上例中，搜索结果的近似显示顺序为：

1. 的匹配 `woman running` 项。
1. 智能标 `woman running` 记中的匹配项。
1. 智能标 `woman` 签的 `running` 匹配项或匹配项。
