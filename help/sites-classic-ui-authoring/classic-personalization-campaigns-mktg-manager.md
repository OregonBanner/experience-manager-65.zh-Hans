---
title: 使用营销活动管理器
seo-title: 使用营销活动管理器
description: 营销活动管理器 (MCM) 是一个控制台，可帮助您管理多渠道营销活动。使用此营销活动自动化软件，您可以管理您的所有品牌、营销活动和体验，以及相关的区段、列表、潜在客户和报表。
seo-description: 营销活动管理器 (MCM) 是一个控制台，可帮助您管理多渠道营销活动。使用此营销活动自动化软件，您可以管理您的所有品牌、营销活动和体验，以及相关的区段、列表、潜在客户和报表。
uuid: 63b817e4-34b9-42b8-845b-e0b7d9af3a96
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: 11ff8bb3-39eb-4f77-b3dc-720262fa7f3f
docset: aem65
translation-type: tm+mt
source-git-commit: dc1985c25c797f7b994f30195d0586f867f9b3ee

---


# 使用营销活动管理器{#working-with-the-marketing-campaign-manager}

在 AEM 中，营销活动管理器 (MCM) 是一个控制台，可帮助您管理多渠道营销活动。使用此营销活动自动化软件，您可以管理您的所有品牌、营销活动和体验，以及相关的区段、列表、潜在客户和报表。

可以从 AEM 中的多个位置访问 MCM；例如，通过欢迎屏幕、使用营销活动图标，或使用以下 URL：

`https://<hostname>:<port>/libs/mcm/content/admin.html`

例如：

`https://localhost:4502/libs/mcm/content/admin.html`

![screen_shot_2012-02-21at114636am](assets/screen_shot_2012-02-21at114636am.png)

从 MCM 您可以访问：

* **[功能板](#dashboard)**共分为四个窗格：

   * [列表](#lists)此窗格显示您已创建的列表，以及该列表中的潜在客户数量。在此窗格中，您可以直接创建新列表或导入潜在客户来创建新列表。选择特定列表将转到[列表](#lists)部分，其中显示了列表的详细信息。

   * [区段](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#anoverviewofsegmentation)此窗格显示您已定义的区段。区段表示拥有某些相同特征的访客群。选择特定的区段将打开区段定义页面。

   * [报表](/help/sites-administering/reporting.md)AEM 提供了不同报表，以帮助您分析和监视实例的状态。此 MCM 窗格列出了相应报表。选择报表将打开报表页面。

   * [营销活动](#campaigns)此窗格列出了您的营销活动体验，例如[新闻稿](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#newsletters)和 [Teaser](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#teasers)。

* **[潜在客户](#leads)**您可以在此处管理潜在客户。您可以创建或导入潜在客户、编辑各个潜在客户的特定细节，或者在不再需要时删除。还可以将潜在客户放入称为“列表”的不同组中。**注意：**Adobe 不打算进一步增强此功能。Adobe 的建议是[利用 Adobe Campaign 以及将其与 AEM 集成](/help/sites-administering/campaign.md)。

* **[列表](#lists)**您可以在此处管理（潜在客户）列表。**注意：**Adobe 不打算进一步增强此功能。Adobe 的建议是[利用 Adobe Campaign 以及将其与 AEM 集成](/help/sites-administering/campaign.md)。

* **[营销活动](#campaigns)**您可以在此处管理品牌、营销活动和体验。

## 功能板 {#dashboard}

功能板显示了四个窗格，分别为您提供了有关（潜在客户）列表、区段、报表和营销活动的概述。可以在此处访问这些内容的基本功能。

![mcm_dashboard](assets/mcm_dashboard.png)

### 潜在客户 {#leads}

>[!NOTE]
>
>Adobe 不打算进一步增强此功能（管理潜在客户）。
>Adobe 的建议是利用 [Adobe Campaign 以及将其与 AEM 集成](/help/sites-administering/campaign.md)。

在 AEM MCM 中，您可以组织和添加潜在客户，方法是手动输入，或导入逗号分隔的列表（例如邮寄列表）。生成潜在客户的其他方法包括新闻稿注册或社区注册（经配置后，它们可触发生成潜在客户的工作流程）。潜在客户通常会进行分类，并被放入列表中，便于您后期对整个列表执行操作（例如，向特定列表发出自定义电子邮件）。

在左边窗格的&#x200B;**潜在客户**&#x200B;下方，您可以创建、导入、编辑和删除您的潜在客户，然后按需要对其进行激活或取消激活。您可以将潜在客户添加到列表中，或查看它已经属于哪些列表。

>[!NOTE]
>
>有关特定任务的详细信息，请参阅[使用潜在客户](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#workingwithleads)。

![screen_shot_2012-02-21at114748am-1](assets/screen_shot_2012-02-21at114748am-1.png)

### 列表 {#lists}

>[!NOTE]
>
>Adobe 不打算进一步增强此功能（管理列表）。
>Adobe 的建议是利用 [Adobe Campaign 以及将其与 AEM 集成](/help/sites-administering/campaign.md)。

使用列表可将您的潜在客户组织到组中。借助列表，可以将市场营销活动定向到所选客户组，例如，可以向列表发送目标新闻稿。

在&#x200B;**列表**&#x200B;下，您可以通过创建、导入、编辑、合并和删除列表来管理您的列表，然后可以按需要对其进行激活或取消激活。您还可以查看该列表中的潜在客户、了解该列表是不是其他列表的成员或查看描述。

>[!NOTE]
>
>有关特定任务的详细信息，请参阅[使用列表](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#workingwithlists)。

![screen_shot_2012-02-21at124828pm-1](assets/screen_shot_2012-02-21at124828pm-1.png)

### 营销活动 {#campaigns}

>[!NOTE]
>
>有关特定任务的详细信息，请参阅 [Teaser 和战略](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#workingwithlists)、[设置您的营销活动](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#settingupyourcampaign)以及[新闻稿](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#newsletters)。

要访问现有营销活动，请在 MCM 中单击&#x200B;**营销活动**。

![screen_shot_2012-02-21at1106pm](assets/screen_shot_2012-02-21at11106pm.png)

* **在左侧窗格中**：列出了所有品牌和营销活动。单击一次品牌可以同时：

   * 在左边窗格中展开列表显示所有相关的营销活动；此列表还会显示每个营销活动的体验数量。
   * 在右侧窗格中打开品牌概述。

* **在右侧窗格中**：显示了每个品牌的图标（不会显示历史营销活动）。您可以双击这些图标打开品牌概述。

#### 品牌概述 {#brand-overview}

![mcm_brandoverview](assets/mcm_brandoverview.png)

您可以在此处：

* 查看此品牌的营销活动和体验的数量（数量在左边窗格显示）。
* 为此品牌&#x200B;**新建...**&#x200B;营销活动。

* 更改要查看的时间跨度；选择&#x200B;**周**、**月**&#x200B;或&#x200B;**季度**，使用箭头选择具体时段或返回到&#x200B;**今天**。

* （在右侧窗格中）选择一个营销活动可以：

   * 编辑&#x200B;**属性...**
   * **删除**&#x200B;营销活动。

* 打开营销活动概述（在右侧窗格中双击某个营销活动，或在左侧窗格中单击一次）。

#### 营销活动概述 {#campaign-overview}

对于每个营销活动提供有两种视图：

1. **日历视图**

   使用此图标：

   ![](do-not-localize/mcm_iconcalendarview.png)

   显示所有触点（灰色）列表，以及与此触点相关的体验（绿色）的水平时间表：

   ![mcm_banner_calendarview](assets/mcm_banner_calendarview.png)

   您可以在此处：

   * 使用箭头更改您要查看的时间跨度，或返回到&#x200B;**今天**。

   * 使用&#x200B;**添加触点...**&#x200B;来为现有的体验添加新触点。

   * 单击（右侧窗格中）的 Teaser 以设置&#x200B;**开启时间**&#x200B;和&#x200B;**结束时间**。

1. **列表视图**

   使用此图标：

   ![](do-not-localize/mcm_icon_listview.png)

   列出了所选营销活动的所有体验（如 teaser 和 newsletter）：

   ![mcm_banner_listview](assets/mcm_banner_listview.png)

   您可以在此处：

   * **创建**&#x200B;新……体验；例如，Adobe Target选件、Teaser和Newsletter。
   * **编辑**&#x200B;特定的 Teaser 页面或新闻稿的详细信息（也可以使用双击）。
   * 为特定的 Teaser 页面或新闻稿定义&#x200B;**属性...**。
   * **模拟**&#x200B;体验（Teaser 页面或新闻稿）的外观。当模拟的页面打开时，您可以打开 sidekick 以切换到该页面的编辑模式。

   * **分析...**&#x200B;为页面生成的展示次数。

   * **删除**&#x200B;项目（当不再需要它们时）。
   * **搜索**&#x200B;您的文本（将会搜索体验的“标题”字段）。
   * 使用&#x200B;**高级**&#x200B;搜索来对搜索应用过滤器。

### 模拟您的营销活动体验 {#simulating-your-campaign-experiences}

在 MCM 中，单击&#x200B;**营销活动**。确保列表视图处于激活状态，然后选择所需的营销活动体验，并单击“**模拟**”。触点（Teaser 或新闻稿页面）将会打开，以显示您选择的体验 - 与访客将会看到的内容相同。

![mcm_simulateexperience](assets/mcm_simulateexperience.png)

您还可以在此处打开 Sidekick（单击小的向下箭头）更改到编辑模式，以便更新页面。

### 分析您的营销活动体验 {#analyzing-your-campaign-experiences}

在 MCM 中，单击&#x200B;**营销活动**。确保列表视图处于激活状态，然后选择所需的营销活动体验，并选择&#x200B;**分析...**。将会显示一段时间内的页面展示图。

![mcm_campaignalyze](assets/mcm_campaignanalyze.png)
