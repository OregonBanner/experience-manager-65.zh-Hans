---
title: 使用社交标记云
seo-title: 使用社交标记云
description: 将社交标记云组件添加到页面
seo-description: 将社交标记云组件添加到页面
uuid: 8c400030-976c-457a-bb5f-e473909647a9
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 23a5a65e-774d-4789-9659-09e8be0c2bcd
translation-type: tm+mt
source-git-commit: 77d00c1d6e94b257aa0533ca88b5f9a12dba0054

---


# 使用社交标记云 {#using-social-tag-cloud}

## 简介 {#introduction}

该组 `Social Tag Cloud` 件突出显示在发布内容时由社区成员应用的标记。 这是一种识别热门话题并允许网站访客快速定位标记内容的方法。

要了解当前趋势的其他方法，请访问 [活动趋势](trends.md)。

此页文档了组 `Social Tag Cloud` 件对话框设置并描述了用户体验。

有关开发人员的详细信息，请参 [阅Tag Essentials](tag.md)。

See [Administering Tags](../../help/sites-administering/tags.md) for information about creating and managing tags, as well as to which content tags have been applied.

## 添加社交标记云 {#adding-a-social-tag-cloud}

要在创作模 `Social Tag Cloud` 式下将组件添加到页面，请使用组件浏览器在应显示标记云的页面上 `Communities / Social Tag Cloud` 查找并将其拖动到相应位置。

有关必要的信息，请访 [问社区组件基础](basics.md)。

当包含 [所需的客户端库时](tag.md#essentials-for-client-side) ，组件的显示方式 `Social Tag Cloud` 如下：

![chlimage_1-303](assets/chlimage_1-303.png)

## 配置社交标记云 {#configuring-social-tag-cloud}

选择要访问 `Social Tag Cloud` 的已放置组件，然后选择打 `Configure` 开编辑对话框的图标。

![chlimage_1-304](assets/chlimage_1-304.png)

在“社 **[!UICONTROL 交标记云”选项卡下]** ，指定要显示的标记以及（如果标记是活动链接）搜索结果页面的位置：

![chlimage_1-305](assets/chlimage_1-305.png)

* **[!UICONTROL 要显示的社交标记]**&#x200B;标识要显示的UGC标记。 下拉选项包括：

   * `From page and child pages`
   * `All tags`
   默认为 `From page and child pages`，其中“页面”指以下的 **页面** 。

* **[!UICONTROL 页面]**

   (如果不是， `All tags)` 则为必需)页面的UGC路径。 如果保留为空，则默认为当前页面。

* **[!UICONTROL 标记上无链接]**

   如果选中此项，则标记将作为纯文本显示在标记云中。 如果未选中，则标记将显示为活动链接，这些链接将搜索应用该标记的所有内容。 默认为未选中，并需 **[!UICONTROL 要设置搜索结果路径]** 。

* **[!UICONTROL 搜索结果路径]**

   放置组件的页面的路径， `Search Result` 配置为引用UGC，该路径包括页面设置指定的UGC **路径** 。

## 更改社交标记云的显示 {#change-display-of-social-tag-cloud}

要编辑 **Social Tag Cloud的显示**，请进入设计模式 [，然后多次单击置入的组件以打开一个包含其他选项卡的](../../help/sites-authoring/default-components-designmode.md)`Social Tag Cloud` 对话框。

使用 **[!UICONTROL Social Tag Cloud(Design)选项卡]** ，指定显示标记的方式。 标记可以是简单标记、默认命名空间中的单个单词或分层分类：

![chlimage_1-306](assets/chlimage_1-306.png)

* **[!UICONTROL 显示完整的标题路径]**

   如果选中此项，则显示父标记的标题和每个已应用标记的命名空间。

   例如：

   * 已选中: `Geometrixx Media: Gadgets / Cars`
   * 未选中: `Cars`
   简单的标签没有区别。

   默认为未选中。

* **[!UICONTROL 仅显示叶标记]**

   如果选中此项，则仅显示不包含其他标记的已应用标记。

   例如，给定的TagID为：

   `Geometrixx Media: Gadgets / Cars`

   可以应用3个标记：

   `Geometrixx Media (the namespace)`, `Gadgets`and `Cars`

   * 已选中：如果应 `Cars` 用，则仅显示。
   * 未选中：并 `Geometrixx Media` 且如 `Gadgets`果应用， `Cars` 也将显示。
   简单的标签是叶标签。

   默认为未选中。

* **[!UICONTROL 链接模板]**

   当通过组件编辑对话框启用链接时，用于在标记云中显示链接的模板（默认模板除外）。

* **[!UICONTROL 所有标记相同尺寸]**

   如果选中此项，则标记云中的所有单词的样式都相同。 如果未选中，则根据单词的使用情况设置不同的样式。 默认为未选中。

## 附加信息 {#additional-information}

有关更多信息，请参阅面向开 [发人员的Tag Essentials](tag.md) （标记基本工具）页面。

有关创 [建和管理标记的信息，请参阅标记用户生成的内容](tag-ugc.md) (UGC)。
