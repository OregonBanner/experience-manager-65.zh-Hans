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
exl-id: 8b4d56d9-ba73-4eda-9773-3daaa9237abe
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '409'
ht-degree: 9%

---

# 排行榜功能{#leaderboard-feature}

## 简介 {#introduction}

`Leaderboard`组件提供了根据获得的分数（基本评分）或其专业知识（高级评分）对成员进行排名，从而了解成员在社区内的交互情况的能力。

在将排行榜组件包含到页面之前，必须配置[社区评分和徽章](/help/communities/implementing-scoring.md)。

文档的此部分描述：

* 将`Leaderboard`组件添加到[社区站点](/help/communities/overview.md#community-sites)。
* `Leaderboard`组件的配置设置。

### 向页面{#adding-a-leaderboard-to-a-page}添加排行榜

要在创作模式下向页面添加`Leaderboard`组件，请找到该组件

* `Communities / Leaderboard`

并将其拖动到页面上的位置。

有关必要信息，请访问[社区组件基础知识](/help/communities/basics.md)。

首次将组件放置在社区站点的页面上时，组件的显示方式如下：

![领导人](assets/leaderboard.png)

### 配置排行榜{#configuring-leaderboard}

选择要访问的已放置的`Leaderboard`组件，然后选择`Configure`图标以打开编辑对话框。

![configure-new](assets/configure-new.png)

![配置编组板](assets/configure-leaderboard.png)

#### “设置”选项卡{#settings-tab}

在&#x200B;**[!UICONTROL Settings]**&#x200B;选项卡下，指定显示与成员相关的信息：

* **显示名称**

   为展示板显示的描述性名称，反映为显示徽章和得分而选择的规则。
如果未输入任何内容，则默认值为`Leaderboard`。

* **徽章**

   如果选中此选项，则标记图标的列将包含在排行榜中。
默认为未选中。

* **徽章名称**

   如果选中此项，则标志名称的列将包含在排行榜中。
默认为未选中。

* **使用头像**

   如果选中此项，则会将成员的头像图像包含在排行榜中，旁边是其名称链接到其成员配置文件的位置。
默认为未选中。

#### “规则”选项卡{#rules-tab}

在&#x200B;**Rules**&#x200B;选项卡下，社区网站及其评分和标记规则

* **规则位置**

   （必需）配置评分/标记规则的位置。

* **评分规则**

   （必需）生成要显示的分数的特定规则。

* **徽章规则**

   （必需）生成要显示标记的特定规则。

* **显示限制**

   每页要显示的成员数。默认为10。

### 示例：参与者排行榜{#example-participants-leaderboard}

该排行榜会报告应用基本评分规则的结果。

排行榜组件配置：

* “设置”选项卡：

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

![参加者领导委员会](assets/participants-leaderboard.png)

### 示例：专家领导小组{#example-experts-leaderboard}

此排行榜会报告应用高级评分规则所产生的结果。

排行榜组件配置：

* “设置”选项卡：

   * 显示名称 = `Expertise Board`
   * `checked`:

      * 徽章
      * 使用头像

* “规则”选项卡：

   * 规则位置 = `/content/sites/<site name>/jcr:content`
   * 评分规则 = `/libs/settings/community/scoring/rules/adv-forums-scoring`
   * 徽章规则 = `/libs/settings/community/badging/rules/adv-forums-badging`
   * 显示限制 = `10`

![专家领导委员会](assets/experts-leaderboard.png)

### 附加信息 {#additional-information}

有关更多信息，请参阅[Ledroboard Essentials](/help/communities/leaderboard.md)页面，供开发人员使用。

[社区评分和徽章](/help/communities/implementing-scoring.md)页面上为管理员提供了创建规则的说明。
