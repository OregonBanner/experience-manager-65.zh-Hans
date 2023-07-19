---
title: 使用营销活动经理
seo-title: Working with the Marketing Campaign Manager
description: 营销活动管理器(MCM)是一个控制台，可帮助您管理多渠道营销活动。 借助此营销自动化软件，您可以管理所有品牌、营销活动和体验以及相关区段、列表、潜在客户和报表。
seo-description: The Marketing Campaign Manager (MCM) is a console that helps you manage multi-channel campaigns. With this marketing automation software you can manage all your brands, campaigns and experiences together with the related segments, lists, leads, and reports.
uuid: 63b817e4-34b9-42b8-845b-e0b7d9af3a96
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: 11ff8bb3-39eb-4f77-b3dc-720262fa7f3f
docset: aem65
exl-id: 0e13112b-d9df-4ba6-bd73-431c87890b79
source-git-commit: 259f257964829b65bb71b5a46583997581a91a4e
workflow-type: tm+mt
source-wordcount: '1180'
ht-degree: 1%

---

# 使用营销活动经理{#working-with-the-marketing-campaign-manager}

在AEM中，营销活动管理器(MCM)是一个控制台，可帮助您管理多渠道营销活动。 借助此营销自动化软件，您可以管理所有品牌、营销活动和体验以及相关区段、列表、潜在客户和报表。

可以从AEM中的各个位置访问MCM；例如，欢迎屏幕，使用促销活动图标或通过URL访问：

`https://<hostname>:<port>/libs/mcm/content/admin.html`

例如：

`https://localhost:4502/libs/mcm/content/admin.html`

![screen_shot_2012-02-21at114636am](assets/screen_shot_2012-02-21at114636am.png)

从MCM可以访问：

* **[仪表板](#dashboard)**
这分为四个窗格：

   * [列表](#lists)
此窗格显示您已创建的列表以及该列表中的潜在客户数量。 从该窗格中，您可以直接创建新列表或导入潜在客户以创建新列表。
选择特定列表后，您将转到 [列表](#lists) 部分显示列表的详细信息。

   * [区段](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#anoverviewofsegmentation)
此窗格显示已定义的区段。 通过区段，可表示共享特定特征的访客集合的特征。
选择特定区段将打开区段定义页面。

   * [报告](/help/sites-administering/reporting.md)
AEM提供不同的报告，以帮助您分析和监控实例的状态。 此MCM窗格列出了报告。
选择报告将打开报告页面。

   * [营销活动](#campaigns)
此窗格列出了您的营销活动体验，例如 [快讯](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#newsletters) 和 [Teasers](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#teasers).

* **[潜在客户](#leads)**
在这里，您可以管理您的潜在客户。 您可以创建或导入潜在客户，编辑单个潜在客户的特定详细信息，或者在不再需要时删除。 您还可以将潜在客户放入不同的组（称为“列表”）。 **注意：** Adobe不打算进一步增强此功能。
建议为 [利用Adobe Campaign以及与AEM的集成](/help/sites-administering/campaign.md).

* **[列表](#lists)**
您可以在此处管理您的（潜在客户）列表。**注意：** Adobe不打算进一步增强此功能。
建议为 [利用Adobe Campaign以及与AEM的集成](/help/sites-administering/campaign.md).

* **[营销活动](#campaigns)**
在这里，您可以管理您的品牌、营销活动和体验。

## 仪表板 {#dashboard}

仪表板显示四个窗格，这些窗格概述了您的列表（潜在客户）、区段、报表和促销活动。 此处还提供了对这些基本功能的访问权限。

![mcm_dashboard](assets/mcm_dashboard.png)

### 潜在客户 {#leads}

>[!NOTE]
>
>Adobe不打算进一步增强此功能（管理潜在客户）。
>建议利用 [Adobe Campaign和与AEM的集成](/help/sites-administering/campaign.md).

在AEM MCM中，您可以通过手动输入潜在客户或导入逗号分隔的列表（例如，邮件列表）来组织和添加潜在客户。 生成潜在客户的其他方法来自新闻稿注册或社区注册（如果配置，这些方法可能会触发填充潜在客户的工作流）。 商机通常会分类并放入列表中，以便您稍后可以对整个列表执行操作；例如，向特定列表发送自定义电子邮件。

下 **潜在客户** 在左窗格中，您可以创建、导入、编辑和删除潜在客户，然后根据需要激活或停用。 您可以将潜在客户添加到列表中，或查看它已经属于哪些列表。

>[!NOTE]
>
>参见 [使用潜在客户](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#workingwithleads) 以了解有关特定任务的详细信息。

![screen_shot_2012-02-21at114748am-1](assets/screen_shot_2012-02-21at114748am-1.png)

### 列表 {#lists}

>[!NOTE]
>
>Adobe不打算进一步增强此功能（管理列表）。
>建议利用 [Adobe Campaign和与AEM的集成](/help/sites-administering/campaign.md).

列表可让您将潜在客户组织到组中。 通过列表，您可以将营销活动定位到选定的用户组；例如，您可以将定向的新闻稿发送到列表。

下 **列表**，您可以通过创建、导入、编辑、合并和删除列表来管理列表，然后根据需要激活或取消激活这些列表。 您还可以查看该列表中的潜在客户，查看该列表是否是另一个列表的成员，或查看说明。

>[!NOTE]
>
>参见 [使用列表](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#workingwithlists) 以了解有关特定任务的详细信息。

![screen_shot_2012-02-21at124828pm-1](assets/screen_shot_2012-02-21at124828pm-1.png)

### 营销活动 {#campaigns}

>[!NOTE]
>
>参见 [Teaser和策略](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#workingwithlists)， [设置活动](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#settingupyourcampaign) 和 [快讯](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#newsletters) 以了解有关特定任务的详细信息。

要访问现有营销活动，请在MCM中单击 **营销活动**.

![screen_shot_2012-02-21at11106pm](assets/screen_shot_2012-02-21at11106pm.png)

* **在左窗格中**：有一个包含所有品牌和营销策划的列表。
单击一个品牌将同时执行以下操作：

   * 展开列表以在左侧窗格中显示所有相关营销活动；此列表还显示每个营销活动中存在的体验数量。
   * 在右侧窗格中打开品牌概述。

* **在右窗格中**：显示每个品牌的图标（不显示历史促销活动）。
您可以双击这些项目以打开品牌概述。

#### 品牌概述 {#brand-overview}

![mcm_brandoverview](assets/mcm_brandoverview.png)

从此处，您可以：

* 查看此品牌存在的营销活动和体验的数量（左侧窗格中显示的数量）。
* 创建 **新建……** 营销活动。

* 更改正在查看的时间范围；选择 **周**， **月** 或 **季度**，使用箭头选择特定期间或返回到 **今天**.

* 选择营销策划（在右窗格中）以：

   * 编辑 **属性……**
   * **删除** 营销活动。

* 打开营销活动概述（双击右窗格中的营销活动，或单击左窗格中的营销活动）。

#### Campaign概述 {#campaign-overview}

对于各个营销活动，有两个视图可用：

1. **日历视图**

   使用图标：

   ![日历视图](do-not-localize/mcm_iconcalendarview.png)

   这会显示所有接触点（灰色）的列表，其中包含连接到该接触点的体验的水平时间范围（绿色）：

   ![mcm_banner_calendarview](assets/mcm_banner_calendarview.png)

   从此处，您可以：

   * 使用箭头更改您查看的时间范围，或返回到 **今天**.

   * 使用 **添加接触点……** 为现有体验添加新接触点。

   * 单击右窗格中的Teaser以设置 **准时** 和 **关闭时间**.

1. **列表视图**

   使用图标：

   ![列表视图](do-not-localize/mcm_icon_listview.png)

   这将列出选定营销活动的所有体验（例如，Teaser和新闻稿）：

   ![mcm_banner_listview](assets/mcm_banner_listview.png)

   从此处，您可以：

   * 创建 **新建……** 体验；例如，Adobe Target优惠、Teaser和新闻稿。
   * **编辑** 特定Teaser页面或新闻稿的详细信息（也可以使用双击）。
   * 定义 **属性……** 特定Teaser页面或新闻稿。
   * **模拟** 体验（Teaser页面或新闻稿）的外观。
当模拟页面打开时，您可以打开sidekick以切换到该页面的编辑模式。

   * **分析……** 为页面生成的展示次数。

   * **删除** 不再需要的项目。
   * **搜索** （将搜索体验的“标题”字段）。
   * 使用 **高级** 搜索以将过滤器应用于搜索。

### 模拟您的营销活动体验 {#simulating-your-campaign-experiences}

在MCM中，单击 **营销活动**. 确保列表视图处于活动状态，然后选择所需的营销活动体验并单击 **模拟**. 将打开接触点（Teaser或新闻稿页面）以显示您选择的体验 — 访客将看到该体验。

![mcm_simulateexperience](assets/mcm_simulateexperience.png)

在此处，您还可以打开sidekick（单击向下小箭头）以更改为更新页面的编辑模式。

### 分析您的Campaign体验 {#analyzing-your-campaign-experiences}

在MCM中，单击 **营销活动**. 确保列表视图处于活动状态，然后选择所需的营销活动体验并选择 **分析……**. 此时将显示一段时间的页面展示次数图表。

![mcm_campaignanalyze](assets/mcm_campaignanalyze.png)
