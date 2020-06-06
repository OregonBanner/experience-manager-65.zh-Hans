---
title: 排行榜功能
seo-title: 排行榜功能
description: 向页面添加排行榜组件
seo-description: 向页面添加排行榜组件
uuid: c4633919-75d3-4bc7-830c-ef9c28cc1cba
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 9045ce2e-a06d-4da5-9b83-56dd823007bb
docset: aem65
translation-type: tm+mt
source-git-commit: fb7d2a3cebda86fa4d91d2ea89ae459fa4b86fa0
workflow-type: tm+mt
source-wordcount: '409'
ht-degree: 9%

---


# 排行榜功能 {#leaderboard-feature}

## 简介 {#introduction}

该组 `Leaderboard` 件提供了通过根据所获得分（基本得分）或其专业知识（高级得分）对成员进行排名来了解成员在社区内交互情况的能力。

在将排行榜组件包含在页面之前，必须配置社 [区评分和标记](/help/communities/implementing-scoring.md)。

文档的本节介绍

* 将组件 `Leaderboard` 添加到社 [区站点](/help/communities/overview.md#community-sites)
* 组件的配置设 `Leaderboard` 置

### Adding a Leaderboard to a Page {#adding-a-leaderboard-to-a-page}

要在创作模 `Leaderboard` 式下将组件添加到页面，请找到该组件

* `Communities / Leaderboard`

并将其拖动到页面上的位置。

有关必要的信息，请访 [问社区组件基础](/help/communities/basics.md)。

首次放置到社区站点的页面时，组件的显示方式如下：

![chlimage_1-19](assets/chlimage_1-19.png)

### 配置通栏 {#configuring-leaderboard}

选择要访问的 `Leaderboard` 已放置组件，然后选择打 `Configure` 开编辑对话框的图标。

![chlimage_1-20](assets/chlimage_1-20.png) ![chlimage_1-21](assets/chlimage_1-21.png)

#### “设置”选项卡 {#settings-tab}

在“设 **置** ”选项卡下，指定显示与成员相关的信息：

* **显示名称**

   用于显示展示板的描述性名称，反映为显示标记和分数而选择的规则。
默认值 `Leaderboard`为，如果未输入。

* **徽章**

   如果选中此项，则在通栏中会包含标记图标的列。
默认为未选中。

* **徽章名称**

   如果选中，则标记名称的列将包括在通栏中。
默认为未选中。

* **使用头像**

   如果选中此项，则会员的头像图像将包含在排行榜中，位于其名称链接旁边，指向其成员用户档案。
默认为未选中。

#### “规则”选项卡 {#rules-tab}

在“规 **则** ”选项卡下，社区站点及其评分和徽章规则

* **规则位置**

   （必需）配置评分／徽章规则的位置。

* **评分规则**

   （必需）生成要显示的分数的特定规则。

* **徽章规则**

   （必需）生成要显示的徽章的特定规则。

* **显示限制**

   每页要显示的成员数。默认值为10。

### 示例： 参加者排行榜 {#example-participants-leaderboard}

此排行榜报告应用基本评分规则的结果。

通栏组件配置：

* 设置选项卡：

   * 显示名称 = `Participation Board`
   * `checked`:

      * 徽章
      * 徽章名称
      * 使用头像

* 规则选项卡：

   * 规则位置 = `/content/sites/<site name>/jcr:content`
   * 评分规则 = `/libs/settings/community/scoring/rules/forums-scoring`
   * 徽章规则 = `/libs/settings/community/badging/rules//reference-badging`
   * 显示限制 = `10`

![chlimage_1-22](assets/chlimage_1-22.png)

### 示例： 专家排行榜 {#example-experts-leaderboard}

此排行榜报告应用高级评分规则的结果。

通栏组件配置：

* 设置选项卡：

   * 显示名称 = `Expertise Board`
   * `checked`:

      * 徽章
      * 使用头像

* 规则选项卡：

   * 规则位置 = `/content/sites/<site name>/jcr:content`
   * 评分规则 = `/libs/settings/community/scoring/rules/adv-forums-scoring`
   * 徽章规则 = `/libs/settings/community/badging/rules/adv-forums-badging`
   * 显示限制 = `10`

![chlimage_1-23](assets/chlimage_1-23.png)

### 附加信息 {#additional-information}

有关更多信息，请参阅Legroid Essentials页 [面，供开发人员](/help/communities/leaderboard.md) 使用。

有关创建规则的说明，请参阅适用于管 [理员的“社区评分和标记](/help/communities/implementing-scoring.md) ”页面。
