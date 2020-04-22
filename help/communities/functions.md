---
title: 社区功能
seo-title: 社区功能
description: 了解如何访问“社区功能”控制台
seo-description: 了解如何访问“社区功能”控制台
uuid: d3d70134-f318-4709-a673-b01a3467d980
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 91833914-b811-4355-a97d-e1a9cb7441f1
docset: aem65
translation-type: tm+mt
source-git-commit: 58a06c1a16c62bffad2893fbec0b32d2ce7267a7

---


# 社区功能{#community-functions}

社区体验中预期的功能类型众所周知。 社区功能可作为社区功能提供。 本质上，它们是预先连接的一个或多个页面，以实施社区功能，该功能不仅需要在创作模式下将组件添加到页面。 它们是用于定义从中创建社区站点的 [社区站点模板](/help/communities/sites.md) ，结构的构 [建块](/help/communities/sites-console.md)。

创建社区站点后，可以使用标准 [AEM创作模式将内容添加到生成的页面](/help/sites-authoring/editing-content.md)。 社区功能控制台中显示了各种社区功能。

>[!NOTE]
>
>社区站点的控制台、 [社区站点模板](/help/communities/sites-console.md)、社区组模板 [,](/help/communities/sites.md)以及社区功能的创建控制台仅 [](/help/communities/tools-groups.md)[](/help/communities/functions.md) 在创作环境中使用。


## 社区功能控制台 {#community-functions-console}

在创作环境中，要访问社区功能控制台，请执行以下操作：

* 从全局导航：“工 **[!UICONTROL 具]** ”>“ **[!UICONTROL 社区]** ” **[!UICONTROL >“社]**&#x200B;区功能”。

![chlimage_1-106](assets/chlimage_1-106.png)

## 预建函数 {#pre-built-functions}

以下是随AEM Communities提供的功能的简短说明。 每个功能都包括一个或多个AEM页面，其中包含连接到功能中的社区组件，该功能可轻松并入社 [区站点模板中](/help/communities/sites.md)。

社区站点模板为社区站点提供了结构，包括登录名、用户用户档案、通知、消息、站点菜单、搜索、主题和品牌功能。

### 标题和URL设置 {#title-and-url-settings}

**标题**和**URL **是所有社区功能通用的属性。

当将社区功能添加到社区站点模板或在修改社区站点的结 [构](/help/communities/sites-console.md#modifying-site-properties) 时添加社区功能时，将打开该功能的对话框，以便可以配置标题和URL。

#### 配置功能详细信息 {#configuration-function-details}

![chlimage_1-107](assets/chlimage_1-107.png)

* **标题**

   (必&#x200B;*需*)站点功能菜单中显示的文本

* **URL**

   (*必需*)用于生成URI的名称。 该名称必须符合AEM和JCR [实施的命](/help/sites-developing/naming-conventions.md) 名约定。

例如，使用根据入门教程创建的 [站点](/help/communities/getting-started.md) ，如果

* 标题=网页
* URL =页

然后，页面的URL为https://localhost:4503/content/sites/engage/en/page.html

页面的菜单链接显示为：

![chlimage_1-108](assets/chlimage_1-108.png)

### 活动流功能 {#activity-stream-function}

活动流函数是具有活动流组件的页面 [](/help/communities/activities.md) ，该组件选择了所有视图(所有活动、用户活动和以下内容)。 另请参 [阅活动Stream Essentials](/help/communities/essentials-activities.md) for developers。

添加到模板时，将打开以下对话框：

#### 配置功能详细信息 {#configuration-function-details-1}

![chlimage_1-109](assets/chlimage_1-109.png)

* [标题和URL设置](#title-and-url-settings)

* **显示“我的活动”视图**

   如果选择此选项，则活动页面将包含一个选项卡，该选项卡基于当前成员在社区中生成的活动。 默认为选中状态。

* **显示“全部活动”视图**

   如果选择此选项，则活动页面将包含一个选项卡，该选项卡包括当前成员有权访问的社区中生成的所有活动。 默认为选中状态。

* **显示“新闻信息源”视图**

   如果选择了此选项卡，则活动页面将包含一个选项卡，根据当前成员所遵循的过滤器活动将显示这些选项卡。 默认为选中状态。

### 指定任务功能 {#assignments-function}

任务功能是定义社区站点以用于启 [用的基本功能](/help/communities/overview.md#enablement-community)。 它允许向社区成员分配启用资源。 另请参 [阅Assignments Essentials](/help/communities/essentials-assignments.md) for developers。

此功能可作为Enablement Add-on的 [一个功能](/help/communities/enablement.md)。 Enablement Add-on需要额外的许可才能用于生产环境。

添加到模板时，唯一的配置是标题 [和URL设置](#title-and-url-settings)。

### 博客功能 {#blog-function}

博客功能是一个页面，其中配置了 [Blog组件](/help/communities/blog-feature.md) ，用于标记、文件上传、跟踪成员以进行自编辑、投票和审核。 另请参 [阅适用于开发人员的Blog Essentials](/help/communities/blog-developer-basics.md) 。

添加到模板时，将打开以下对话框：

![chlimage_1-110](assets/chlimage_1-110.png)

* [标题和URL设置](#title-and-url-settings)

* **允许拥有权限的成员**

   如果选中此选项，则博客仅允许特权成员通过允许选择特权成员组来 [创建文章](/help/communities/users.md#privileged-members-group)。 如果未选择，则允许所有社区成员进行创建。 取消选择默认值。

* **允许文件上传**

   如果选择此选项，则博客将允许成员上传文件。 默认为选中状态。

* **允许主题回复**

   如果未选择，博客将允许对文章的回复（评论），但不允许对评论的回复。 默认为选中状态。

* **允许专题内容**

   如果选择此选项，则博客将标识为特 [色内容](/help/communities/featured.md)。 默认为选中状态。

### 日历功能 {#calendar-function}

日历功能是一个页面，其“日历”组 [件配置为](/help/communities/calendar.md) “允许标记”。 另请参 [阅适用于开发人员的Calendar Essentials](/help/communities/calendar-basics-for-developers.md) 。

添加到模板时，将打开以下对话框：

![chlimage_1-111](assets/chlimage_1-111.png)

* [标题和URL设置](#title-and-url-settings)

* **允许固定**

   如果选择此选项，论坛将允许将主题回复固定到评论列表的开头。 默认为选中状态。

* **允许拥有权限的成员**

   如果选中此选项，则博客仅允许特权成员通过允许选择特权成员组来 [创建文章](/help/communities/users.md#privileged-members-group)。 如果未选择，则允许所有社区成员进行创建。 取消选择默认值。

* **允许文件上传**

   如果选择此选项，则博客将允许成员上传文件。 默认为选中状态。

* **允许主题回复**

   如果未选择，博客将允许对文章的回复（评论），但不允许对评论的回复。 默认为选中状态。

* **允许专题内容**

   如果选中，其内容将标识为特 [色内容](/help/communities/featured.md)。 默认为选中状态。

### 目录功能 {#catalog-function}

目录功能使Enablement Community成员能 [够浏览未分配给他们的Enablement](/help/communities/overview.md#enablement-community) Resources。 请参 [阅为开发人员添加标签](/help/communities/tag-resources.md) Enablement Resources [和Catalog Essentials](/help/communities/catalog-developer-essentials.md) 。

如果社区站点的所有属性设置为true，则所有目录中都会显示社区站点的所有 ` [Show in Catalog](/help/communities/resources.md)`支持资源和学习路径。 要明确包含资源和学习路径，必须对目录应 [用预过滤](/help/communities/catalog-developer-essentials.md#pre-filters) 。

添加到模板时，该配置允许指定用于配置向站点命名空间显示的标记过滤器的标记访客:

![Catalog函数](assets/catalog-function.png)

* [标题和URL设置](#title-and-url-settings)

* **选择所有命名空间**

   选定的标记命名空间定义哪些标记可供访客选择，以过滤目录中列出的启用资源的列表。
如果选择此选项，则允许为社区站点使用的所有标记命名空间均可用。
如果取消选择，则可以选择社区站点所允许的一个或多个命名空间。
默认为选中状态。

### 特色内容功能 {#featured-content-function}

特色内容功能是一个页面，其中配置了 [特色内容组件](/help/communities/featured.md) ，允许添加和删除评论。

可能允许或禁止按组件对内容进行功能(请参阅 [Blog Function](#blog-function)、 [Calendar Function](#calendar-function)、 [Forum Function](#forum-function)[](#ideation-function)[](#qna-function)、Ideation Function、A QnFunction)。

添加到模板时，唯一的配置是标题 [和URL设置](#title-and-url-settings)。

### 文件库功能 {#file-library-function}

文件库功能是一个页面，其中配置了 [“文件库”组件](/help/communities/file-library.md) ，允许添加和删除注释。

添加到模板时，唯一的配置是标题 [和URL设置](#title-and-url-settings)。

### 论坛功能 {#forum-function}

论坛功能是一个页面，其中的论坛组 [件配置为标记](/help/communities/forum.md) 、文件上传、跟踪成员以进行自编辑、投票和审核。

添加到模板时，将打开以下对话框：

#### 配置功能详细信息 {#configuration-function-details-2}

![chlimage_1-112](assets/chlimage_1-112.png)

* [标题和URL设置](#title-and-url-settings)

* **允许固定**

   如果选择此选项，论坛将允许将主题回复固定到评论列表的开头。 默认为选中状态。

* **允许拥有权限的成员**

   如果选择该选项，则论坛仅允许特权成员通过允许选择特权成员组来发 [布主题](/help/communities/users.md#privileged-members-group)。 如果未选择，则允许所有社区成员发布。 取消选择默认值。

* **允许文件上传**

   如果选择了此选项，则论坛将允许成员上传文件。 默认为选中状态。

* **允许主题回复**

   如果未选择，论坛将允许对主题进行评论，但不允许对这些评论进行回复。 默认为选中状态。

* **允许专题内容**

   如果选择此项，组件的内容将标识为特色 [内容](/help/communities/featured.md)。 默认为选中状态。

### 组函数 {#groups-function}

>[!CAUTION]
>
>组功能不能*是站点结构 *中或社区站点模板中的第* 一个或唯一功能。
>
>必须首先包含并列出任何其 [他函数](#page-function)，如页面函数。


组功能使社区成员能够在发布环境的社区站点内创建子社区。

根据 [设置](/help/communities/sites-console.md#groupmanagement) ，当“组”功能包含在社区站点模板中时 [](/help/communities/sites.md)，这些组可以是公共的或私有的，并且一个或多个社区组模板可以配置为在实际创建社区组时(例如，从发布环境)提供模板选择。 社 [区组模板](/help/communities/tools-groups.md) ，指定为组页面（如论坛和日历）创建的社区功能。

创建社区组后，会为新组动态创建成员组，可向其分配或加入成员。 For more information, see [Managing Users and User Groups](/help/communities/users.md).

自Communities功 [能包1起](/help/communities/deploy-communities.md#latestfeaturepack)，社区组在创作环境中使用 [Communities Sites的“组”控制台创建](/help/communities/groups.md)，并且在启用后可在发布环境中创建。

添加到模板时，将打开以下对话框：

![chlimage_1-113](assets/chlimage_1-113.png)

* [标题和URL设置](#title-and-url-settings)

* **选择组模板**

   允许选择一个或多个已启用的组模板的下拉框，新社区组(在发布环境中)的未来创建者可从中进行选择。

* **允许拥有权限的成员**

   如果选择该选项，则论坛仅允许特权成员通过允许选择特权成员安 [全组发布主题](/help/communities/users.md#privileged-members-group)。 如果未选择，则允许所有社区成员发布。 取消选择默认值。

* **允许发布创建**

   如果选择此选项，则授权社区成员可以在发布环境中创建组。 如果取消选择，则只能在创作环境中从“社区站点的组”控制台创建新组（子社区）。
默认为选中状态。

### 构思功能 {#ideation-function}

构思功能是一个包含一个构思组件的 [页面](/help/communities/ideation-feature.md)。

添加到模板时，将打开以下对话框，其中指定默认的标题和URL名称以及模板的默认显示设置：

![chlimage_1-114](assets/chlimage_1-114.png)

* [标题和URL设置](#title-and-url-settings)

* **允许拥有权限的成员**

   如果选择该选项，则论坛仅允许特权成员通过允许选择特权成员安 [全组发布主题](/help/communities/users.md#privileged-members-group)。 如果未选择，则允许所有社区成员发布。 取消选择默认值。

* **允许文件上传**

   如果选择此项，则该想法包括允许成员上传文件的功能。 默认为选中状态。

* **允许主题回复**

   如果未选择，则该构思允许对主题进行回复（评论），但不允许对评论进行回复。 默认为选中状态。

* **允许专题内容**

   如果选中，其内容将标识为特 [色内容](/help/communities/featured.md)。 默认为选中状态。

### 排行榜功能 {#leaderboard-function}

排行榜功能是包含一个“排行榜”组件的 [页面](/help/communities/enabling-leaderboard.md)。

**注意**:在从包含“排行榜”功能的社区模 *板创建社区站点后* ,“排行榜”组件需要进一步配置。 指定“排行榜”组件的 [规则](/help/communities/enabling-leaderboard.md#rules-tab)，具体取决于社区站点 [的得分和标记配](/help/communities/implementing-scoring.md) 置。

添加到模板时，将打开以下对话框，其中指定默认的标题和URL名称以及模板的默认显示设置：

![chlimage_1-115](assets/chlimage_1-115.png)

* [标题和URL设置](#title-and-url-settings)

* **显示徽章**

   如果选中此选项，则排行榜中会包含标记图标的列。
取消选择默认值。

* **显示徽章名称**

   如果选中此选项，则会在排行榜中包含标记名称的列。
取消选择默认值。

* **显示头像**

   如果选择此项，则会员的头像图像将包含在排行榜中，位于其名称链接旁边，指向其成员用户档案。
取消选择默认值。

### 页面功能 {#page-function}

页面功能会向社区站点添加一个空白页面，该页面已连接到社区站点的功能中：登录、菜单、通知、消息、主题和品牌。 内容将使用标准AEM创作模 [式添加到页面](/help/sites-authoring/editing-content.md)。

添加到模板时，唯一的配置是标题 [和URL设置](#title-and-url-settings)。

### 问题与解答功能 {#qna-function}

QnA函数是一个页面，其中配置了 [QnA组件](/help/communities/working-with-qna.md) ，用于标记、文件上传、跟踪、成员到自编辑、投票和协调。

添加到模板时，配置允许对特权成员进行限制：

![chlimage_1-116](assets/chlimage_1-116.png)

* [标题和URL设置](#title-and-url-settings)

* **允许固定**

   如果选择此选项，论坛将允许将主题回复固定到评论列表的开头。 默认为选中状态。

* **允许拥有权限的成员**

   如果选择了此选项，则问题与解答论坛仅允许特权成员通过选择特权成员组来发 [布问题](/help/communities/users.md#privileged-members-group)。 如果未选择，则允许所有社区成员发布。 取消选择默认值。

* **允许文件上传**

   如果选择了此选项，则问题与解答论坛将允许成员上传文件。 默认为选中状态。

* **允许主题回复**

   如果未选择，问题与解答论坛允许对已发布的问题进行评论（答案），但不允许回复答案。 默认为选中状态。

* **允许专题内容**

   如果选中，其内容将标识为特 [色内容](/help/communities/featured.md)。 默认为选中状态。

## 创建社区功能 {#create-community-function}

通过选择位于“社区功能”控制台顶部 `Create Community Function` 的图标，可以创建社区功能。 可以创建基于同一AEM Blueprint的多个函数，然后通过在创作编辑模式下打开来唯一自定义这些函数。

![chlimage_1-117](assets/chlimage_1-117.png)

### 社区功能名称 {#community-function-name}

![chlimage_1-118](assets/chlimage_1-118.png)

在“社区功能名称”面板上，将配置名称、说明以及是否启用或禁用该功能：

* **社区功能名称**

   用于显示和存储的函数名。

* **社区功能描述**

   显示的函数描述。

* **禁用／启用**

   控制函数是否可引用的切换开关。

### AEM Blueprint {#aem-blueprint}

![chlimage_1-119](assets/chlimage_1-119.png)

在面 `AEM Blueprint` 板上，可以选择作为社区功能底层实现的蓝图。

社区功能是一个微型网站，包括一个或多个页面，预先连接以包含在社区站点中，包括登录名、用户用户档案、通知、消息、站点菜单、搜索、主题和品牌功能。 创建该函数后，可以在创作编辑模 [式下打开该函数](#open-community-function) ，并自定义页面或组件设置。

由于社区功能是作为Blueprint的 [Live](/help/sites-administering/msm.md#live-copies) [Copy实现的，因此可以转出对函数所做的更改，该函数影响从社区站点模板创建的所有社区站点页面或包含该函数](/help/sites-administering/msm-livecopy.md#creatingablueprint)[](/help/communities/sites.md)[](/help/communities/tools-groups.md) 的社区组模板创建的所有社区站点页面。 还可以将页面与其父蓝图取消关联，以进行页面级别修改。

另请参阅 [多站点管理器](/help/sites-administering/msm.md)。

### 缩略图 {#thumbnail}

![chlimage_1-120](assets/chlimage_1-120.png)

在“缩略图”面板上，可以上传图像以在“社区功能”控 [制台中显示](#community-functions-console)。

## 打开社区功能 {#open-community-function}

![chlimage_1-121](assets/chlimage_1-121.png)

选择图 `Open Community Function` 标以进入创作编辑模式以创作页面内容和修改功能组件的配置。

### 配置组件 {#configuring-components}

社区功能将作为AEM Blueprint的Live Copy实施，其详细信息将在多站点管理器下 [进行说明](/help/sites-administering/msm.md)。

不仅可以创作页面内容，还可以配置组件。

如果在创建的社区站点的页面上配置组件，则可能需要取消继 [承](/help/sites-administering/msm-livecopy.md#changing-live-copy-content) ，才能配置组件。 完成配置后，应重新建立继承。

有关配置详细信息，请访 [问作者的社区组](/help/communities/author-communities.md) 件。

## 编辑社区功能 {#edit-community-function}

![chlimage_1-122](assets/chlimage_1-122.png)

选择图 `Edit Community Function` 标以使用与创建社区函数相同的面板编辑 [该函数的属性](#create-community-function)，包括启用或禁用该函数。
