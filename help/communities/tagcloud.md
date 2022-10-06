---
title: 使用Social标签云
seo-title: Using Social Tag Cloud
description: 向页面添加Social标签云组件
seo-description: Adding a Social Tag Cloud component to a page
uuid: 8c400030-976c-457a-bb5f-e473909647a9
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 23a5a65e-774d-4789-9659-09e8be0c2bcd
exl-id: 56af5362-78de-4308-8958-63a45e8573cc
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '558'
ht-degree: 5%

---

# 使用Social标签云 {#using-social-tag-cloud}

## 简介 {#introduction}

的 `Social Tag Cloud` 组件会突出显示在发布内容时由社区成员应用的标记。 它是识别趋势主题并允许网站访客快速找到标记内容的方法。

要获取确定当前趋势的另一种方法，请访问 [活动趋势](trends.md).

本页记录了 `Social Tag Cloud` 组件对话框设置，并描述用户体验。

有关开发人员的详细信息，请参阅 [标记要点](tag.md).

请参阅 [管理标记](../../help/sites-administering/tags.md) 有关创建和管理标记以及已对哪些内容应用标记的信息。

## 添加Social标签云 {#adding-a-social-tag-cloud}

添加 `Social Tag Cloud` 组件添加到创作模式下的页面，可使用组件浏览器找到 `Communities / Social Tag Cloud` 并将其拖动到应显示标记云的页面上。

有关必要信息，请访问 [社区组件基础知识](basics.md).

当 [所需的客户端库](tag.md#essentials-for-client-side) 包含，这是 `Social Tag Cloud` 组件将显示：

![social-tag](assets/social-tag.png)

## 配置Social标签云 {#configuring-social-tag-cloud}

选择已放置的 `Social Tag Cloud` 要访问和选择的组件 `Configure` 图标，打开编辑对话框。

![配置](assets/configure-new.png)

在 **[!UICONTROL Social标签云]** 选项卡，指定要显示的标记，如果标记是活动链接，则指定搜索结果页面的位置：

![social-tag-cloud](assets/social-tag-cloud.png)

* **[!UICONTROL 要显示的Social标签]**
识别要显示的UGC标记。 下拉选项包括：

   * `From page and child pages`
   * `All tags`

   默认值为 `From page and child pages`，其中“页面”是指 **页面** 设置。

* **[!UICONTROL 页面]**

   (如果不需要，则为必需 `All tags)` 页面的UGC路径。 如果留空，则默认为当前页面。

* **[!UICONTROL 标记上无链接]**

   如果选中此项，则标记将以纯文本形式显示在标记云中。 如果未选中，则标记将显示为活动链接，用于搜索应用了该标记的所有内容。 默认设置为未选中，并要求 **[!UICONTROL 搜索结果路径]** 设置。

* **[!UICONTROL 搜索结果路径]**

   页面的路径，其中 `Search Result` 组件已放置，配置为引用UGC，该UGC包含由 **页面** 设置。

## 更改Social标签云的显示 {#change-display-of-social-tag-cloud}

编辑 **Social标签云**，输入 [设计模式](../../help/sites-authoring/default-components-designmode.md) 并双击已放置的 `Social Tag Cloud` 组件来打开一个包含其他选项卡的对话框。

使用 **[!UICONTROL Social标签云（设计）]** 选项卡，指定标记的显示方式。 标记可以是简单的标记、默认命名空间中的单个词，或分层分类：

![social-tag-cloud-design](assets/social-tag-cloud-design.png)

* **[!UICONTROL 显示完整的标题路径]**

   如果选中，则显示父标记的标题以及每个已应用标记的命名空间。

   例如：

   * 已选中: `Geometrixx Media: Gadgets / Cars`
   * 未选中: `Cars`

   简单的标记没有区别。

   默认为未选中。

* **[!UICONTROL 仅显示叶标记]**

   如果选中此选项，则仅显示已应用的不包含其他标记的标记。

   例如，假定TagID为：

   `Geometrixx Media: Gadgets / Cars`

   有3个标记可应用：

   `Geometrixx Media (the namespace)`, `Gadgets`, 和 `Cars`

   * 已选中：仅 `Cars` 将显示（如果应用）。
   * 未选中： `Geometrixx Media` 和 `Gadgets`以及 `Cars` 将显示（如果应用）。

   简单的标签是叶标签。

   默认为未选中。

* **[!UICONTROL 链接模板]**

   当通过组件编辑对话框启用链接时，用于在标记云中显示链接的模板（默认值除外）。

* **[!UICONTROL 所有标记相同尺寸]**

   如果选中此选项，则标记云中的所有词语的样式均相同。 如果未选中，则根据词语的用法设置不同的样式。 默认为未选中。

## 附加信息 {#additional-information}

有关 [标记要点](tag.md) 页面。

请参阅 [标记用户生成的内容](tag-ugc.md) (UGC)以了解有关创建和管理标记的信息。
