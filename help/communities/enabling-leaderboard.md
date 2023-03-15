---
title: 排行榜功能
seo-title: Leaderboard Feature
description: 向页面添加排行榜组件
seo-description: Adding a Leaderboard component to a page
uuid: c4633919-75d3-4bc7-830c-ef9c28cc1cba
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 9045ce2e-a06d-4da5-9b83-56dd823007bb
docset: aem65
exl-id: 8b4d56d9-ba73-4eda-9773-3daaa9237abe
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '400'
ht-degree: 10%

---

# 排行榜功能 {#leaderboard-feature}

## 简介 {#introduction}

此 `Leaderboard` 通过根据获得的点数（基本评分）或其专业知识（高级评分）对成员进行排名，组件提供了解成员如何在社区内进行交互的能力。

在页面上包含排行榜组件之前，需要配置 [社区评分和徽章](/help/communities/implementing-scoring.md).

本文档的这一部分描述了：

* 添加 `Leaderboard` 组件到 [社区站点](/help/communities/overview.md#community-sites).
* 的配置设置 `Leaderboard` 组件。

### 将排行榜添加到页面 {#adding-a-leaderboard-to-a-page}

添加 `Leaderboard` 组件到创作模式下的页面，找到该组件

* `Communities / Leaderboard`

并将其拖动到页面上的适当位置。

有关必要信息，请访问 [社区组件基础知识](/help/communities/basics.md).

首次放置到社区站点的页面上时，以下是组件的显示方式：

![排行榜](assets/leaderboard.png)

### 配置排行榜 {#configuring-leaderboard}

选择已放置的 `Leaderboard` 组件以访问和选择 `Configure` 图标，打开“编辑”对话框。

![configure-new](assets/configure-new.png)

![configure-leaderboard](assets/configure-leaderboard.png)

#### “设置”选项卡 {#settings-tab}

在 **[!UICONTROL 设置]** 选项卡，指定与显示的成员相关的信息：

* **显示名称**

   为展示板显示的描述性名称，反映为显示徽章和分数而选择的规则。
默认为 `Leaderboard`如果未输入任何内容，则为。

* **徽章**

   如果选中，则排行榜中包含徽章图标列。
默认值为未选中。

* **徽章名称**

   如果选中，则排行榜中将包含徽章名称列。
默认值为未选中。

* **使用头像**

   如果选中，则成员的头像图像将包含在排行榜中，位于其名称链接旁边，指向其成员配置文件。
默认值为未选中。

#### “规则”选项卡 {#rules-tab}

在 **规则** 选项卡、社区站点及其评分和标记规则

* **规则位置**

   （必需）配置评分/徽章规则的位置。

* **评分规则**

   （必需）生成要显示的分数的特定规则。

* **徽章规则**

   （必需）生成要显示的徽章的特定规则。

* **显示限制**

   每页显示的成员数。默认为10。

### 示例：参与者排行榜 {#example-participants-leaderboard}

此排行榜报告应用基本评分规则的结果。

排行榜组件配置：

* 设置选项卡：

   * 显示名称 = `Participation Board`
   * `checked`:

      * 徽章
      * 徽章名称
      * 使用头像

* “规则”选项卡：

   * 规则位置 = `/content/sites/<site name>/jcr:content`
   * 评分规则 = `/libs/settings/community/scoring/rules/forums-scoring`
   * 徽章规则 = `/libs/settings/community/badging/rules//reference-badging`
   * 显示限制 = `10`

![参与者 — 排行榜](assets/participants-leaderboard.png)

### 示例：专家排行榜 {#example-experts-leaderboard}

此排行榜报告应用高级评分规则的结果。

排行榜组件配置：

* 设置选项卡：

   * 显示名称 = `Expertise Board`
   * `checked`:

      * 徽章
      * 使用头像

* “规则”选项卡：

   * 规则位置 = `/content/sites/<site name>/jcr:content`
   * 评分规则 = `/libs/settings/community/scoring/rules/adv-forums-scoring`
   * 徽章规则 = `/libs/settings/community/badging/rules/adv-forums-badging`
   * 显示限制 = `10`

![专家 — 排行榜](assets/experts-leaderboard.png)

### 附加信息 {#additional-information}

欲知更多信息，请访问 [排行榜要点](/help/communities/leaderboard.md) 适用于开发人员的页面。

有关创建规则的说明，请参见 [社区评分和徽章](/help/communities/implementing-scoring.md) 页面。
