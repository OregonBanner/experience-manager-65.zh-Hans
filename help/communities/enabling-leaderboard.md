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
source-git-commit: 6720d5a0fdf1facc0b10011ec306dffbb31f4ac5
workflow-type: tm+mt
source-wordcount: '409'
ht-degree: 9%

---


# 排行榜功能{#leaderboard-feature}

## 简介 {#introduction}

`Leaderboard`组件提供了通过根据所获得分（基本得分）或其专业知识（高级得分）对成员进行排名来了解成员在社区内交互情况的能力。

在将排行榜组件包含在页面之前，必须配置[社区评分和标记](/help/communities/implementing-scoring.md)。

文档的本节介绍：

* 将`Leaderboard`组件添加到[社区站点](/help/communities/overview.md#community-sites)。
* `Leaderboard`组件的配置设置。

### 向页面{#adding-a-leaderboard-to-a-page}添加排行榜

要在创作模式下将`Leaderboard`组件添加到页面，请找到该组件

* `Communities / Leaderboard`

并将其拖动到页面上的位置。

有关必要的信息，请访问[社区组件基础知识](/help/communities/basics.md)。

首次放置到社区站点的页面时，组件的显示方式如下：

![chlimage_1-8](assets/chlimage_1-8.png)

### 配置通栏{#configuring-leaderboard}

选择要访问的已放置`Leaderboard`组件，然后选择打开编辑对话框的`Configure`图标。

![chlimage_1-9](assets/chlimage_1-9.png)

![chlimage_1-10](assets/chlimage_1-10.png)

#### 设置选项卡{#settings-tab}

在&#x200B;**[!UICONTROL 设置]**&#x200B;选项卡下，指定显示与成员相关的信息：

* **显示名称**

   用于显示展示板的描述性名称，反映为显示标记和分数而选择的规则。
默认值为`Leaderboard`（如果未输入任何内容）。

* **徽章**

   如果选中此项，则在通栏中会包含标记图标的列。
默认为未选中。

* **徽章名称**

   如果选中，则标记名称的列将包括在通栏中。
默认为未选中。

* **使用头像**

   如果选中此项，则会员的头像图像将包含在排行榜中，位于其名称链接旁边，指向其成员用户档案。
默认为未选中。

#### 规则选项卡{#rules-tab}

在&#x200B;**规则**&#x200B;选项卡下，社区站点及其评分和徽章规则

* **规则位置**

   （必需）配置评分／徽章规则的位置。

* **评分规则**

   （必需）生成要显示的分数的特定规则。

* **徽章规则**

   （必需）生成要显示的徽章的特定规则。

* **显示限制**

   每页要显示的成员数。默认值为10。

### 示例：参加者排行榜{#example-participants-leaderboard}

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

![chlimage_1-11](assets/chlimage_1-11.png)

### 示例：专家排行榜{#example-experts-leaderboard}

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

![chlimage_1-12](assets/chlimage_1-12.png)

### 附加信息 {#additional-information}

有关开发人员的详细信息，请参阅[Legrobard Essentials](/help/communities/leaderboard.md)页面。

管理员的[社区评分和标记](/help/communities/implementing-scoring.md)页面上提供了有关创建规则的说明。
