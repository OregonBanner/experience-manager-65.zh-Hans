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
source-git-commit: 2fcd87cd1def7fc265ba40c83b50db86618f3b70
workflow-type: tm+mt
source-wordcount: '571'
ht-degree: 4%

---


# 使用社交标记云 {#using-social-tag-cloud}

## 简介 {#introduction}

该组 `Social Tag Cloud` 件会在发布内容时突出显示社区成员应用的标记。 这是一种识别热门话题并允许网站访客快速找到标记内容的方法。

要了解当前趋势的其他方法，请访问 [活动趋势](trends.md)。

此页文档组件 `Social Tag Cloud` 对话框设置并描述用户体验。

有关开发人员的详细信息，请 [参阅Tag Essentials](tag.md)。

See [Administering Tags](../../help/sites-administering/tags.md) for information about creating and managing tags, as well as to which content tags have been applied.

## 添加社交标记云 {#adding-a-social-tag-cloud}

要在创作 `Social Tag Cloud` 模式下将组件添加到页面，请使用组件浏览器 `Communities / Social Tag Cloud` 在应显示标记云的页面上查找并将其拖至适当位置。

有关必要的信息，请访 [问社区组件基础](basics.md)。

当包 [含所需的客户端库](tag.md#essentials-for-client-side) ，组件的显示 `Social Tag Cloud` 方式如下：

![社交标签](assets/social-tag.png)

## 配置社交标记云 {#configuring-social-tag-cloud}

选择要访问的 `Social Tag Cloud` 已放置组件，然后选择打 `Configure` 开编辑对话框的图标。

![配置](assets/configure-new.png)

在“社 **[!UICONTROL 交标记云]** ”选项卡下，指定要显示的标记，如果这些标记是活动链接，则指定页面的搜索结果位置：

![社交标签云](assets/social-tag-cloud.png)

* **[!UICONTROL 要显示的社交标]**&#x200B;记标识要显示的UGC标记。 下拉选项包括：

   * `From page and child pages`
   * `All tags`

   默认为， `From page and child pages`其中“页面”指以下 **的页** 面设置。

* **[!UICONTROL 页面]**

   (如果不是页 `All tags)` 面的UGC路径，则为必需。 如果留空，则默认为当前页面。

* **[!UICONTROL 标记上无链接]**

   如果选中，则标记将以纯文本形式显示在标记云中。 如果未选中，则标记将显示为活动链接，用于搜索应用该标记的所有内容。 默认为未选中，并 **[!UICONTROL 需要设置搜索结果]** 路径。

* **[!UICONTROL 搜索结果路径]**

   放置组件的页面的路 `Search Result` 径，配置为引用UGC，该UGC包括页面设置指定的 **UGC** 路径。

## 更改社交标记云的显示 {#change-display-of-social-tag-cloud}

要编辑社交标记云 **的显示**，请进 [入设计模式](../../help/sites-authoring/default-components-designmode.md) ，然后多次单击置入的 `Social Tag Cloud` 组件以打开一个包含其他选项卡的对话框。

使用社 **[!UICONTROL 交标记云（设计）选项卡]** ，指定标记的显示方式。 标记可以是简单标记、默认命名空间中的单个单词或分层分类：

![社交标签云设计](assets/social-tag-cloud-design.png)

* **[!UICONTROL 显示完整的标题路径]**

   如果选中，则显示父标记的标题和每个已应用标记的命名空间。

   例如：

   * 已选中: `Geometrixx Media: Gadgets / Cars`
   * 未选中: `Cars`

   简单的标签没有区别。

   默认为未选中。

* **[!UICONTROL 仅显示叶标记]**

   如果选中，则仅显示不包含其他标记的已应用标记。

   例如，给定的TagID为：

   `Geometrixx Media: Gadgets / Cars`

   可应用3个标记：

   `Geometrixx Media (the namespace)`、 `Gadgets`and `Cars`

   * 已检查：如果 `Cars` 应用，则只显示。
   * 未选中： `Geometrixx Media` 并 `Gadgets`且如果应 `Cars` 用，也会显示。

   简单的标签是叶标签。

   默认为未选中。

* **[!UICONTROL 链接模板]**

   当通过组件编辑对话框启用链接时，用于在标记云中显示链接的模板（默认模板除外）。

* **[!UICONTROL 所有标记相同尺寸]**

   如果选中此项，则标记云中的所有单词的样式相同。 如果不选中，则根据单词的用法设置不同的样式。 默认为未选中。

## 附加信息 {#additional-information}

有关更多信息，请参阅开发 [人员的“Tag](tag.md) Essentials”页面。

有关创 [建和管理标记的信息](tag-ugc.md) ，请参阅标记用户生成的内容(UGC)。
