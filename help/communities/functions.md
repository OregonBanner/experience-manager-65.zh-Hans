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
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '2220'
ht-degree: 6%

---

# 社区功能{#community-functions}

社区体验中预期的功能类型是众所周知的。 社区功能作为社区功能提供。 本质上，它们是预连接的一个或多个页面，用于实施社区功能，该功能不仅需要在创作模式下将组件添加到页面。 它们是用于定义 [社区站点模板](/help/communities/sites.md) 社区站点的来源 [已创建](/help/communities/sites-console.md).

创建社区站点后，可以使用标准将内容添加到生成的页面 [AEM创作模式](/help/sites-authoring/editing-content.md). 可以在社区功能控制台中看到各种社区功能。

>[!NOTE]
>
>用于创建的控制台 [社区站点](/help/communities/sites-console.md)， [社区站点模板](/help/communities/sites.md)， [社区组模板](/help/communities/tools-groups.md)、和 [社区功能](/help/communities/functions.md) 仅供在创作环境中使用。

## 社区功能控制台 {#community-functions-console}

要在创作环境中访问社区功能控制台，请执行以下操作：

* 导航到 **[!UICONTROL 工具]** > **[!UICONTROL Communities]** > **[!UICONTROL 社区功能]**.

![社区功能](assets/community-functions.png)

## 预建函数 {#pre-built-functions}

以下简要介绍了AEM Communities提供的功能。 每个功能包括一个或多个AEM页面，这些页面包含相互连接在一起的Communities组件，这些组件可轻松合并到功能中 [社区站点模板](/help/communities/sites.md).

社区站点模板提供了社区站点的结构，包括登录、用户配置文件、通知、消息、站点菜单、搜索、主题设定和品牌推广功能。

### 标题和URL设置 {#title-and-url-settings}

**标题** 和 **URL** 是所有社区功能通用的属性。

将社区功能添加到社区站点模板或进行添加 [修改](/help/communities/sites-console.md#modifying-site-properties) 在社区站点的结构中，将打开函数的对话框，以便可以配置标题和URL。

#### 配置功能详细信息 {#configuration-function-details}

![title-url-details](assets/title-url-details.png)

* **标题**

  (*必填*)站点功能菜单中显示的文本

* **URL**

  (*必填*)用于生成URI的名称。 名称必须符合 [命名约定](/help/sites-developing/naming-conventions.md) 由AEM和JCR强制实施。

例如，使用通过以下方式创建的站点 [快速入门](/help/communities/getting-started.md) 教程，如果

* 标题=网页
* URL =页面

然后，指向该页面的URL为https://localhost:4503/content/sites/engage/en/page.html

该页面的菜单链接显示为：

![engage-page](assets/engage-page.png)

### 活动流功能 {#activity-stream-function}

活动流函数是一个页面，其中 [活动流组件](/help/communities/activities.md) 选定所有视图（所有活动、用户活动及其他）。 另请参阅 [Activity Stream Essentials](/help/communities/essentials-activities.md) 适用于开发人员。

添加到模板后，将打开以下对话框：

#### 配置功能详细信息 {#configuration-function-details-1}

![function-details](assets/function-details.png)

* [标题和URL设置](#title-and-url-settings)

* **显示“我的活动”视图**

  如果选择，则“活动”页面包括一个选项卡，该选项卡根据当前成员在社区内生成的活动进行筛选。 默认处于选中状态。

* **显示“全部活动”视图**

  如果选择，则“活动”页面包括一个选项卡，其中包含当前成员有权访问的社区内生成的所有活动。 默认处于选中状态。

* **显示“新闻信息源”视图**

  如果选择，活动页面将包含一个选项卡，该选项卡会根据当前成员所关注的活动进行筛选。 默认处于选中状态。

### 博客功能 {#blog-function}

博客功能是带有 [博客组件](/help/communities/blog-feature.md) 针对标记、文件上传、关注、成员自我编辑、投票和审核进行了配置。 另请参阅 [博客要点](/help/communities/blog-developer-basics.md) 适用于开发人员。

添加到模板后，将打开以下对话框：

![博客组件](assets/blog-component.png)

* [标题和URL设置](#title-and-url-settings)

* **允许拥有权限的成员**

  如果选中，则博客仅允许拥有权限的成员通过允许选择 [拥有权限的成员组](/help/communities/users.md#privileged-members-group). 如果未选择，则允许创建所有社区成员。 默认值为取消选中。

* **允许文件上传**

  如果选定此选项，则博客将允许成员上传文件。 默认处于选中状态。

* **允许主题回复**

  如果未选中，则博客允许对文章进行回复（评论），但不允许对评论进行回复。 默认处于选中状态。

* **允许专题内容**

  如果选定该属性，则会将博客标识为 [专题内容](/help/communities/featured.md). 默认处于选中状态。

### 日历功能 {#calendar-function}

日历功能是一个页面，其中 [日历组件](/help/communities/calendar.md) 配置为允许标记。 另请参阅 [日历要点](/help/communities/calendar-basics-for-developers.md) 适用于开发人员。

添加到模板后，将打开以下对话框：

![calendar-details](assets/calendar-details.png)

* [标题和URL设置](#title-and-url-settings)

* **允许固定**

  如果选定，论坛允许将主题回复固定到评论列表的开头。 默认处于选中状态。

* **允许拥有权限的成员**

  如果选中，则博客仅允许拥有权限的成员通过允许选择 [拥有权限的成员组](/help/communities/users.md#privileged-members-group). 如果未选择，则允许创建所有社区成员。 默认值为取消选中。

* **允许文件上传**

  如果选定此选项，则博客将允许成员上传文件。 默认处于选中状态。

* **允许主题回复**

  如果未选中，则博客允许对文章进行回复（评论），但不允许对评论进行回复。 默认处于选中状态。

* **允许专题内容**

  如果选择，其内容将标识为 [专题内容](/help/communities/featured.md). 默认处于选中状态。

### 专题内容功能 {#featured-content-function}

专题内容功能是一个页面，其中具有 [专题内容组件](/help/communities/featured.md) 配置为允许添加和删除评论。

每个组件可能允许或不允许使用特征内容功能(请参阅 [博客功能](#blog-function)， [日历功能](#calendar-function)， [论坛功能](#forum-function)， [构思功能](#ideation-function)、和 [问题与解答功能](#qna-function))。

添加到模板时，的唯一配置是 [标题和URL设置](#title-and-url-settings).

### 文件库功能 {#file-library-function}

文件库函数是一个页面，其中包含 [文件库组件](/help/communities/file-library.md) 配置为允许添加和删除评论。

添加到模板时，的唯一配置是 [标题和URL设置](#title-and-url-settings).

### 论坛功能 {#forum-function}

论坛功能是一个页面，其中包含 [论坛组件](/help/communities/forum.md) 针对标记、文件上传、关注、成员自我编辑、投票和审核进行了配置。

添加到模板后，将打开以下对话框：

#### 配置功能详细信息 {#configuration-function-details-2}

![forum-component1](assets/forum-component1.png)

* [标题和URL设置](#title-and-url-settings)

* **允许固定**

  如果选定，论坛允许将主题回复固定到评论列表的开头。 默认处于选中状态。

* **允许拥有权限的成员**

  如果选中，则论坛仅允许拥有权限的成员通过允许选择 [拥有权限的成员组](/help/communities/users.md#privileged-members-group). 如果未选择，则允许所有社区成员发帖。 默认值为取消选中。

* **允许文件上传**

  如果选中，论坛将允许成员上传文件。 默认处于选中状态。

* **允许主题回复**

  如果未选择此选项，则论坛允许对主题进行评论，但不允许对这些评论进行回复。 默认处于选中状态。

* **允许专题内容**

  如果选定该属性，组件的内容将标识为 [专题内容](/help/communities/featured.md). 默认处于选中状态。

### 组功能 {#groups-function}

>[!CAUTION]
>
>组功能必须 *非* 是 *第一或唯一* 在站点结构或社区站点模板中起作用。
>
>任何其他函数，如 [页面函数](#page-function)，必须先包含并列出。

“组”功能使社区成员能够在发布环境中的社区站点中创建子社区。

根据 [设置](/help/communities/sites-console.md#groupmanagement) 当“组”功能包含在 [社区站点模板](/help/communities/sites.md)，则这些组可以是公共的或私有的，并且可以配置一个或多个社区组模板，以便在实际创建社区组时（例如从发布环境）提供模板选择。 A [社区组模板](/help/communities/tools-groups.md) 指定为组页面（如论坛和日历）创建的Communities功能。

创建社区组时，会为新组动态创建成员组，成员可以分配给新组或加入新组。 有关更多信息，请参阅 [管理用户和用户组](/help/communities/users.md).

截止社区 [功能包1](/help/communities/deploy-communities.md#latestfeaturepack)，使用在创作环境中创建的社区组 [社区站点的组控制台](/help/communities/groups.md)、和可在启用时在发布环境中创建。

添加到模板后，将打开以下对话框：

![group-template-config](assets/group-template-config.png)

* [标题和URL设置](#title-and-url-settings)

* **选择组模板**

  一个下拉列表，允许选择一个或多个已启用的组模板，新社区组的未来创建者（在发布环境中）可以从中进行选择。

* **允许拥有权限的成员**

  如果选中，则论坛仅允许拥有权限的成员通过允许选择 [拥有权限的成员安全组](/help/communities/users.md#privileged-members-group). 如果未选择，则允许所有社区成员发帖。 默认值为取消选中。

* **允许发布创建**

  如果选择，则授权社区成员可以在发布环境中创建组。 如果取消选择，则只能从社区站点的“组”控制台在创作环境中创建新组（子社区）。
默认处于选中状态。

### 构思功能 {#ideation-function}

构思功能是一个具有构思功能的页面 [构思组件](/help/communities/ideation-feature.md).

添加到模板后，将打开以下对话框，其中指定了模板的默认“标题”和URL名称以及默认显示设置：

![构思函数](assets/ideation-function.png)

* [标题和URL设置](#title-and-url-settings)

* **允许拥有权限的成员**

  如果选中，则论坛仅允许拥有权限的成员通过允许选择 [拥有权限的成员安全组](/help/communities/users.md#privileged-members-group). 如果未选择，则允许所有社区成员发帖。 默认值为取消选中。

* **允许文件上传**

  如果选中，该想法包括成员上传文件的功能。 默认处于选中状态。

* **允许主题回复**

  如果未选择此构思，则允许对主题进行回复（评论），但不允许对评论进行回复。 默认处于选中状态。

* **允许专题内容**

  如果选择，其内容将标识为 [专题内容](/help/communities/featured.md). 默认处于选中状态。

### 排行榜功能 {#leaderboard-function}

排行榜功能是一页带有一个排行榜 [排行榜组件](/help/communities/enabling-leaderboard.md).

**注意**：排行榜组件需要进一步配置 *之后* 社区站点是从包含排行榜功能的社区模板创建的。 指定排行榜组件的 [规则](/help/communities/enabling-leaderboard.md#rules-tab)，具体取决于 [评分和徽章](/help/communities/implementing-scoring.md) 社区站点的。

添加到模板后，将打开以下对话框，其中指定了模板的默认“标题”和URL名称以及默认显示设置：

![排行榜 — 对话](assets/leaderboard-dialog.png)

* [标题和URL设置](#title-and-url-settings)

* **显示徽章**

  如果选择，则排行榜中将包含徽章图标列。
默认值为取消选中。

* **显示徽章名称**

  如果选择，则徽章名称的列将包含在排行榜中。
默认值为取消选中。

* **显示头像**

  如果选择该选项，则成员的头像图像将包含在排行榜中，位于其名称链接旁边，指向其成员配置文件。
默认值为取消选中。

### 页面功能 {#page-function}

页面功能会向社区站点添加一个空白页面，该页面与社区站点的功能（登录、菜单、通知、消息、主题设置和品牌推广）相链接。 使用将内容添加到页面 [标准AEM创作模式](/help/sites-authoring/editing-content.md).

添加到模板时，的唯一配置是 [标题和URL设置](#title-and-url-settings).

### 问题与解答功能 {#qna-function}

QnA函数是一个页面，其中包含 [问题与解答组件](/help/communities/working-with-qna.md) 针对标记、文件上传、关注、成员自我编辑、投票和审核进行了配置。

添加到模板后，该配置允许对拥有权限的成员进行限制：

![问题与解答 — 对话](assets/qna-dialog.png)

* [标题和URL设置](#title-and-url-settings)

* **允许固定**

  如果选定，论坛允许将主题回复固定到评论列表的开头。 默认处于选中状态。

* **允许拥有权限的成员**

  如果选中，问题与解答论坛仅允许拥有权限的成员通过选择 [拥有权限的成员组](/help/communities/users.md#privileged-members-group). 如果未选择，则允许所有社区成员发帖。 默认值为取消选中。

* **允许文件上传**

  如果选中，问题与解答论坛包括成员上传文件的功能。 默认处于选中状态。

* **允许主题回复**

  如果未选择，问题与解答论坛允许对已发布的问题进行评论（回答），但不允许对答案进行回复。 默认处于选中状态。

* **允许专题内容**

  如果选择，其内容将标识为 [专题内容](/help/communities/featured.md). 默认处于选中状态。

## 创建社区功能 {#create-community-function}

通过选择社区功能即可创建社区功能 `Create Community Function` 图标（位于“社区功能”控制台顶部）。 可以创建基于同一AEM Blueprint的多个函数，然后通过以创作编辑模式打开来进行唯一自定义。

![create-community-function](assets/create-community-function.png)

### 社区功能名称 {#community-function-name}

![function-name](assets/function-name.png)

在“社区功能名称”面板上，配置了名称、描述以及功能是启用还是禁用：

* **社区功能名称**

  用于显示和存储的函数名称。

* **社区功能描述**

  显示的函数描述。

* **已禁用/已启用**

  用于控制函数是否可引用的切换开关。

### AEM Blueprint {#aem-blueprint}

![aem-blueprint](assets/aem-blueprint.png)

在 `AEM Blueprint` 在面板中，可以选择Blueprint，它是社区功能的基础实施。

社区功能是一个微型站点，它包含一个或多个页面，预先布线以包含到社区站点中，包括登录、用户配置文件、通知、消息、站点菜单、搜索、主题设定和品牌推广功能。 创建函数后，可以 [打开函数](#open-community-function) 在作者编辑模式下，并自定义页面或组件设置。

由于社区功能是作为 [live copy](/help/sites-administering/msm.md#live-copies) 的 [Blueprint](/help/sites-administering/msm-livecopy.md#creatingablueprint)，则可以转出对函数所做的更改，该函数会影响从创建的所有社区站点页面。 [社区站点模板](/help/communities/sites.md) 或 [社区组模板](/help/communities/tools-groups.md) 包括函数。 也可以取消页面与其父Blueprint的关联，以进行页面级别的修改。

另请参阅 [多站点管理器](/help/sites-administering/msm.md).

### 缩略图 {#thumbnail}

![功能缩略图](assets/funtion-thumbnail.png)

在“缩略图”面板上，可以上传图像以在 [社区功能控制台](#community-functions-console).

## 打开社区功能 {#open-community-function}

![开放函数](assets/open-function.png)

选择 `Open Community Function` 图标以进入创作编辑模式，进而创作页面内容和修改功能组件的配置。

### 配置组件 {#configuring-components}

社区功能作为AEM Blueprint的Live Copy实施，其详细信息记录在 [多站点管理器](/help/sites-administering/msm.md).

您不仅可以创作页面内容，还可以配置组件。

如果在已创建的社区站点的页面上配置组件，则可能需要取消 [继承](/help/sites-administering/msm-livecopy.md#changing-live-copy-content) 以配置组件。 配置完成后，应重新建立继承。

有关配置详细信息，请访问 [Communities组件](/help/communities/author-communities.md) 供作者使用。

## 编辑社区功能 {#edit-community-function}

![edit-function](assets/edit-function.png)

选择 `Edit Community Function` 图标，使用与相同的面板编辑函数的属性 [创建社区功能](#create-community-function)，包括启用或禁用函数。
