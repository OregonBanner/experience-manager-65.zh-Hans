---
title: 社区功能
seo-title: Community Functions
description: 了解如何访问社区功能控制台
seo-description: Learn how to access the Community Functions console
uuid: d3d70134-f318-4709-a673-b01a3467d980
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 91833914-b811-4355-a97d-e1a9cb7441f1
docset: aem65
role: Admin
exl-id: 2395c895-c611-43ac-abb6-c2bc4b4a41f4
source-git-commit: 4dbbcc41757843d3b2d5a3bbb2656ef587e83d2c
workflow-type: tm+mt
source-wordcount: '2224'
ht-degree: 6%

---

# 社区功能{#community-functions}

社区体验预期的功能类型已广为人知。 社区功能可作为社区功能提供。 本质上说，它们是预先布线的一个或多个页面，用于实施社区功能，该功能不仅需要在创作模式下向页面添加组件，还需要其他功能。 它们是用于定义 [社区站点模板](/help/communities/sites.md) 社区站点所在的位置 [已创建](/help/communities/sites-console.md).

创建社区站点后，可以使用标准 [AEM创作模式](/help/sites-authoring/editing-content.md). 社区功能控制台中显示了各种社区功能。

>[!NOTE]
>
>用于创建 [社区站点](/help/communities/sites-console.md), [社区网站模板](/help/communities/sites.md), [社区组模板](/help/communities/tools-groups.md)和 [社区功能](/help/communities/functions.md) 只能在创作环境中使用。

## 社区功能控制台 {#community-functions-console}

要在创作环境中访问社区功能控制台，请执行以下操作：

* 导航到 **[!UICONTROL 工具]** > **[!UICONTROL 社区]** > **[!UICONTROL 社区功能]**.

![社区功能](assets/community-functions.png)

## 预建函数 {#pre-built-functions}

以下是随AEM Communities一起提供的功能的简要描述。 每个函数都包括一个或多个包含社区组件的AEM页面，这些组件连接在一个功能中，可轻松融入到 [社区站点模板](/help/communities/sites.md).

社区站点模板为社区站点提供了结构，包括登录、用户配置文件、通知、消息、站点菜单、搜索、主题和品牌功能。

### 标题和URL设置 {#title-and-url-settings}

**标题** 和 **URL** 是所有社区功能的通用属性。

将社区功能添加到社区站点模板或在 [修改](/help/communities/sites-console.md#modifying-site-properties) 社区站点的结构中，将打开函数对话框，以便可以配置标题和URL。

#### 配置功能详细信息 {#configuration-function-details}

![title-url-details](assets/title-url-details.png)

* **标题**

   (*必需*)网站功能菜单中显示的文本

* **URL**

   (*必需*)用于生成URI的名称。 名称必须符合 [命名约定](/help/sites-developing/naming-conventions.md) 由AEM和JCR强加。

例如，使用通过以下内容创建的网站： [快速入门](/help/communities/getting-started.md) 教程，如果

* 标题=网页
* URL = page

然后，该页面的URL是https://localhost:4503/content/sites/engage/en/page.html

并且页面的菜单链接显示为：

![参与页面](assets/engage-page.png)

### 活动流功能 {#activity-stream-function}

活动流函数是一个 [活动流组件](/help/communities/activities.md) 选定所有视图（所有活动、用户活动及后续活动）。 另请参阅 [活动流要点](/help/communities/essentials-activities.md) 适用于开发人员。

添加到模板后，将打开以下对话框：

#### 配置功能详细信息 {#configuration-function-details-1}

![函数详细信息](assets/function-details.png)

* [标题和URL设置](#title-and-url-settings)

* **显示“我的活动”视图**

   如果选中此选项，则“活动”页面会包含一个选项卡，该选项卡会根据当前成员在社区中生成的活动筛选活动。 已选中默认值。

* **显示“全部活动”视图**

   如果选中此选项，则“活动”页面将包含一个选项卡，其中包含在当前成员有权访问的社区中生成的所有活动。 已选中默认值。

* **显示“新闻信息源”视图**

   如果已选择，则“活动”页面会包含一个选项卡，该选项卡会根据当前成员所关注的活动筛选活动。 已选中默认值。

### 博客功能 {#blog-function}

博客函数是 [博客组件](/help/communities/blog-feature.md) 配置了标记、文件上传、后续、成员自行编辑、投票和审核功能。 另请参阅 [博客要点](/help/communities/blog-developer-basics.md) 适用于开发人员。

添加到模板后，将打开以下对话框：

![博客组件](assets/blog-component.png)

* [标题和URL设置](#title-and-url-settings)

* **允许拥有权限的成员**

   如果选中，则博客仅允许特权成员通过允许选择 [特权成员组](/help/communities/users.md#privileged-members-group). 如果未选择，则允许所有社区成员创建。 取消选择默认值。

* **允许文件上传**

   如果已选择，则博客将包含成员上传文件的功能。 已选中默认值。

* **允许主题回复**

   如果未选择，博客将允许对文章进行回复（评论），但不允许对评论进行回复。 已选中默认值。

* **允许专题内容**

   如果选择，则会将博客标识为 [特色内容](/help/communities/featured.md). 已选中默认值。

### 日历功能 {#calendar-function}

日历函数是 [日历组件](/help/communities/calendar.md) 配置为允许标记。 另请参阅 [日历要点](/help/communities/calendar-basics-for-developers.md) 适用于开发人员。

添加到模板后，将打开以下对话框：

![日历详细信息](assets/calendar-details.png)

* [标题和URL设置](#title-and-url-settings)

* **允许固定**

   如果选中，论坛允许将主题回复固定到评论列表的开头。 已选中默认值。

* **允许拥有权限的成员**

   如果选中，则博客仅允许特权成员通过允许选择 [特权成员组](/help/communities/users.md#privileged-members-group). 如果未选择，则允许所有社区成员创建。 取消选择默认值。

* **允许文件上传**

   如果已选择，则博客将包含成员上传文件的功能。 已选中默认值。

* **允许主题回复**

   如果未选择，博客将允许对文章进行回复（评论），但不允许对评论进行回复。 已选中默认值。

* **允许专题内容**

   如果选择，则其内容将标识为 [特色内容](/help/communities/featured.md). 已选中默认值。

### 特色内容功能 {#featured-content-function}

特色内容功能是一个 [特色内容组件](/help/communities/featured.md) 配置为允许添加和删除注释。

每个组件可能允许或禁止功能显示内容(请参阅 [博客功能](#blog-function), [日历函数](#calendar-function), [论坛功能](#forum-function), [构思函数](#ideation-function)和 [问题解答函数](#qna-function))。

添加到模板后，唯一的配置是 [标题和URL设置](#title-and-url-settings).

### 文件库功能 {#file-library-function}

文件库函数是 [文件库组件](/help/communities/file-library.md) 配置为允许添加和删除注释。

添加到模板后，唯一的配置是 [标题和URL设置](#title-and-url-settings).

### 论坛功能 {#forum-function}

论坛函数是一个 [论坛组件](/help/communities/forum.md) 配置了标记、文件上传、后续、成员自行编辑、投票和审核功能。

添加到模板后，将打开以下对话框：

#### 配置功能详细信息 {#configuration-function-details-2}

![forum-component1](assets/forum-component1.png)

* [标题和URL设置](#title-and-url-settings)

* **允许固定**

   如果选中，论坛允许将主题回复固定到评论列表的开头。 已选中默认值。

* **允许拥有权限的成员**

   如果选择，则论坛仅允许特权成员通过选择 [特权成员组](/help/communities/users.md#privileged-members-group). 如果未选择，则允许所有社区成员发布内容。 取消选择默认值。

* **允许文件上传**

   如果选中，论坛将包括成员上传文件的功能。 已选中默认值。

* **允许主题回复**

   如果未选择，论坛将允许对主题进行评论，但不允许对这些评论进行回复。 已选中默认值。

* **允许专题内容**

   如果已选择，则组件的内容将标识为 [特色内容](/help/communities/featured.md). 已选中默认值。

### 组函数 {#groups-function}

>[!CAUTION]
>
>组函数必须 *not* be *第一，也是唯一* 功能。
>
>任何其他函数，例如 [页面函数](#page-function)，必须先包含并列出。

群组功能允许社区成员在发布环境中的社区站点内创建子社区。

取决于 [设置](/help/communities/sites-console.md#groupmanagement) 组函数包含在 [社区站点模板](/help/communities/sites.md)，则这些组可以是公共的或私有的，并且一个或多个社区组模板可配置为在实际创建社区组时（例如从发布环境）提供模板选项。 A [社区组模板](/help/communities/tools-groups.md) 指定为群组页面创建的社区功能，如论坛和日历。

创建社区组后，会为新组动态创建成员组，可以将成员分配或加入到新组中。 有关更多信息，请参阅 [管理用户和用户组](/help/communities/users.md).

截至社区 [功能包1](/help/communities/deploy-communities.md#latestfeaturepack)，则可使用 [“社区站点”的“组”控制台](/help/communities/groups.md)，且可以在启用后在发布环境中创建。

添加到模板后，将打开以下对话框：

![group-template-config](assets/group-template-config.png)

* [标题和URL设置](#title-and-url-settings)

* **选择组模板**

   允许选择一个或多个已启用的组模板的下拉列表，新社区组（在发布环境中）的未来创建者可以从中选择一个或多个已启用的组模板。

* **允许拥有权限的成员**

   如果选择，则论坛仅允许特权成员通过选择 [特权成员安全组](/help/communities/users.md#privileged-members-group). 如果未选择，则允许所有社区成员发布内容。 取消选择默认值。

* **允许发布创建**

   如果已选择，则授权的社区成员可以在发布环境中创建组。 如果取消选择，则只能在创作环境中从社区站点的组控制台创建新组（子社区）。
已选中默认值。

### 构思功能 {#ideation-function}

构思函数是一个包含 [构思组件](/help/communities/ideation-feature.md).

添加到模板后，将打开以下对话框，其中指定了模板的默认标题和URL名称以及默认的显示设置：

![想象函数](assets/ideation-function.png)

* [标题和URL设置](#title-and-url-settings)

* **允许拥有权限的成员**

   如果选择，则论坛仅允许特权成员通过选择 [特权成员安全组](/help/communities/users.md#privileged-members-group). 如果未选择，则允许所有社区成员发布内容。 取消选择默认值。

* **允许文件上传**

   如果选择，则构思包括让成员上传文件的功能。 已选中默认值。

* **允许主题回复**

   如果未选择，则允许对主题进行回复（评论），但不允许对评论进行回复。 已选中默认值。

* **允许专题内容**

   如果选择，则其内容将标识为 [特色内容](/help/communities/featured.md). 已选中默认值。

### 排行榜功能 {#leaderboard-function}

排行榜功能是一个包含 [排行榜部分](/help/communities/enabling-leaderboard.md).

**注意**:领导板组件需要进一步配置 *after* 社区站点是从包含领导板功能的社区模板创建的。 指定排行榜组件的 [规则](/help/communities/enabling-leaderboard.md#rules-tab)，具体取决于配置 [评分和徽章](/help/communities/implementing-scoring.md) （用于社区站点）。

添加到模板后，将打开以下对话框，其中指定了模板的默认标题和URL名称以及默认的显示设置：

![排行榜对话](assets/leaderboard-dialog.png)

* [标题和URL设置](#title-and-url-settings)

* **显示徽章**

   如果选中此选项，则标记图标的列将包含在排行榜中。
取消选择默认值。

* **显示徽章名称**

   如果选中，则标记名称的列将包含在排行榜中。
取消选择默认值。

* **显示头像**

   如果选择，则会将成员的头像图像包含在排行榜中，位于其成员用户档案的名称链接旁边。
取消选择默认值。

### 页面功能 {#page-function}

页面功能可向社区站点添加一个与社区站点功能连接的空白页面：登录、菜单、通知、消息、主题和品牌策略。 使用 [标准AEM创作模式](/help/sites-authoring/editing-content.md).

添加到模板后，唯一的配置是 [标题和URL设置](#title-and-url-settings).

### 问题与解答功能 {#qna-function}

问题解答函数是一个 [问题解答组件](/help/communities/working-with-qna.md) 配置了标记、文件上传、后续、成员自行编辑、投票和审核功能。

添加到模板后，配置允许对特权成员进行限制：

![qna-dialog](assets/qna-dialog.png)

* [标题和URL设置](#title-and-url-settings)

* **允许固定**

   如果选中，论坛允许将主题回复固定到评论列表的开头。 已选中默认值。

* **允许拥有权限的成员**

   如果选择，则QnA论坛仅允许特权成员通过选择 [特权成员组](/help/communities/users.md#privileged-members-group). 如果未选择，则允许所有社区成员发布内容。 取消选择默认值。

* **允许文件上传**

   如果已选择，则问题解答论坛将包含成员上传文件的功能。 已选中默认值。

* **允许主题回复**

   如果未选择，问题解答论坛允许对已发布的问题进行评论（回答），但不允许对答案进行回复。 已选中默认值。

* **允许专题内容**

   如果选择，则其内容将标识为 [特色内容](/help/communities/featured.md). 已选中默认值。

## 创建社区功能 {#create-community-function}

通过选择 `Create Community Function` 图标。 可以创建基于同一AEM Blueprint的多个函数，然后通过在创作编辑模式下打开来进行唯一自定义。

![创建社区功能](assets/create-community-function.png)

### 社区功能名称 {#community-function-name}

![function-name](assets/function-name.png)

在“社区函数名称”面板上，配置了函数的名称、说明以及是启用还是禁用该函数：

* **社区功能名称**

   用于显示和存储的函数名称。

* **社区功能描述**

   显示的函数描述。

* **已禁用/已启用**

   控制函数是否可引用的切换开关。

### AEM Blueprint {#aem-blueprint}

![aem-blueprint](assets/aem-blueprint.png)

在 `AEM Blueprint` ，则可以选择作为社区功能底层实现的Blueprint。

社区功能是一个微型网站，包括一个或多个页面，可预先连接到社区网站中，包括登录、用户档案、通知、消息、网站菜单、搜索、主题和品牌策略功能。 创建函数后，可以 [打开函数](#open-community-function) 在创作编辑模式下，自定义页面或组件设置。

由于社区功能是作为 [live copy](/help/sites-administering/msm.md#live-copies) a [Blueprint](/help/sites-administering/msm-livecopy.md#creatingablueprint)，则可以转出对函数所做的更改，该函数会影响从中创建的所有社区网站页面 [社区站点模板](/help/communities/sites.md) 或 [社区组模板](/help/communities/tools-groups.md) 包含函数。 也可以将页面与其父Blueprint取消关联，以进行页面级别的修改。

另请参阅 [多站点管理器](/help/sites-administering/msm.md).

### 缩略图 {#thumbnail}

![函数 — 缩略图](assets/funtion-thumbnail.png)

在“缩略图”面板上，可以上传图像以在 [社区功能控制台](#community-functions-console).

## 打开社区功能 {#open-community-function}

![open-function](assets/open-function.png)

选择 `Open Community Function` 图标，以进入创作编辑模式以创作页面内容和修改功能组件的配置。

### 配置组件 {#configuring-components}

社区功能作为AEM Blueprint的Live Copy实施，其详细信息记录在 [多站点管理器](/help/sites-administering/msm.md).

不仅可以创作页面内容，还可以配置组件。

如果在已创建社区站点的页面上配置组件，则可能需要取消 [继承](/help/sites-administering/msm-livecopy.md#changing-live-copy-content) 以配置组件。 配置完成后，应重新建立继承。

有关配置详细信息，请访问 [社区组件](/help/communities/author-communities.md) 作者。

## 编辑社区功能 {#edit-community-function}

![edit-function](assets/edit-function.png)

选择 `Edit Community Function` 图标，以使用与 [创建社区功能](#create-community-function)，包括启用或禁用函数。
