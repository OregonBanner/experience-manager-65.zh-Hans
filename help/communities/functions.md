---
title: 社区功能
seo-title: 社区功能
description: 了解如何访问社区功能控制台
seo-description: 了解如何访问社区功能控制台
uuid: d3d70134-f318-4709-a673-b01a3467d980
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 91833914-b811-4355-a97d-e1a9cb7441f1
docset: aem65
role: Administrator
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '2459'
ht-degree: 6%

---


# 社区功能{#community-functions}

社区体验预期的功能类型众所周知。 社区功能可作为社区功能提供。 本质上，它们是预先连接的一个或多个页面，用于实现社区功能，该功能不仅需要在创作模式下向页面添加组件。 它们是用于定义[社区站点模板](/help/communities/sites.md)的结构的构造块，从中创建了[社区站点](/help/communities/sites-console.md)。

创建社区站点后，可以使用标准[AEM创作模式](/help/sites-authoring/editing-content.md)将内容添加到生成的页面。 社区功能控制台中显示了各种社区功能。

>[!NOTE]
>
>创建[社区站点](/help/communities/sites-console.md)、[社区站点模板](/help/communities/sites.md)、[社区组模板](/help/communities/tools-groups.md)和[社区功能](/help/communities/functions.md)的控制台仅供创作环境使用。

## 社区功能控制台{#community-functions-console}

要访问创作环境中的社区功能控制台，请执行以下操作：

* 导航到&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 社区]** > **[!UICONTROL 社区功能]**。

![社区功能](assets/community-functions.png)

## 预建函数{#pre-built-functions}

以下是随AEM Communities提供的功能的简要说明。 每个功能都包括一个或多个AEM页面，其中包含将Communities组件连接在一起的功能，该功能可轻松并入到[社区站点模板](/help/communities/sites.md)中。

社区站点模板为社区站点提供结构，包括登录、用户用户档案、通知、消息、站点菜单、搜索、主题和品牌功能。

### 标题和URL设置{#title-and-url-settings}

**标** 题和 **** URL是所有社区功能的通用属性。

在[修改](/help/communities/sites-console.md#modifying-site-properties)社区站点结构时，将社区功能添加到社区站点模板或添加社区功能时，将打开该功能的对话框，以便可以配置标题和URL。

#### 配置功能详细信息 {#configuration-function-details}

![title-url-details](assets/title-url-details.png)

* **标题**

   （*必需*）站点功能菜单中显示的文本

* **URL**

   （*必需*）用于生成URI的名称。 该名称必须符合AEM和JCR实施的[命名约定](/help/sites-developing/naming-conventions.md)。

例如，使用从[入门](/help/communities/getting-started.md)教程中创建的站点(如果

* 标题=网页
* URL =页面

然后，页面的URL为https://localhost:4503/content/sites/engage/en/page.html

并且页面的菜单链接显示为：

![参与页面](assets/engage-page.png)

### 活动流功能 {#activity-stream-function}

活动流函数是具有[活动流组件](/help/communities/activities.md)的页面，其中选择了所有视图(所有活动、用户活动和以下)。 另请参阅[活动 Stream Essentials](/help/communities/essentials-activities.md)，以供开发人员使用。

添加到模板时，将打开以下对话框：

#### 配置功能详细信息 {#configuration-function-details-1}

![function-details](assets/function-details.png)

* [标题和URL设置](#title-and-url-settings)

* **显示“我的活动”视图**

   如果选中，“活动”页面将包含一个选项卡，该选项卡基于当前成员在社区中生成的活动进行过滤器。 已选择默认值。

* **显示“全部活动”视图**

   如果选中，“活动”页面将包含一个选项卡，其中包括当前成员有权访问的社区中生成的所有活动。 已选择默认值。

* **显示“新闻信息源”视图**

   如果选中，活动页面将包含一个选项卡，根据当前成员正在进行的过滤器活动。 已选择默认值。

### 指定任务功能 {#assignments-function}

赋值函数是定义[社区站点以启用](/help/communities/overview.md#enablement-community)的基本功能。 它允许向社区成员分配启用资源。 另请参阅[Assignments Essentials](/help/communities/essentials-assignments.md)，以供开发人员使用。

此函数可作为[enablement add-on](/help/communities/enablement.md)的一个功能使用。 Enablement Add-on需要额外的许可才能用于生产环境。

添加到模板时，唯一的配置是[标题和URL设置](#title-and-url-settings)。

### 博客功能 {#blog-function}

博客函数是具有[Blog组件](/help/communities/blog-feature.md)的页面，该组件配置为标记、文件上载、跟踪成员以进行自编辑、投票和审核。 另请参阅[Blog Essentials](/help/communities/blog-developer-basics.md)，以供开发人员使用。

添加到模板时，将打开以下对话框：

![blog-component](assets/blog-component.png)

* [标题和URL设置](#title-and-url-settings)

* **允许拥有权限的成员**

   如果选择，则博客仅允许特权成员通过允许选择[特权成员组](/help/communities/users.md#privileged-members-group)来创建文章。 如果未选择，则允许所有社区成员进行创建。 “默认”为取消选择状态。

* **允许文件上传**

   如果选中，博客将允许成员上传文件。 已选择默认值。

* **允许主题回复**

   如果未选择，博客将允许对文章的回复（评论），但不允许对评论的回复。 已选择默认值。

* **允许专题内容**

   如果选择，则博客将标识为[特色内容](/help/communities/featured.md)。 已选择默认值。

### 日历功能 {#calendar-function}

日历函数是具有[日历组件](/help/communities/calendar.md)的页面，配置为允许标记。 另请参阅[Calendar Essentials](/help/communities/calendar-basics-for-developers.md)，以供开发人员使用。

添加到模板时，将打开以下对话框：

![calendar-details](assets/calendar-details.png)

* [标题和URL设置](#title-and-url-settings)

* **允许固定**

   如果选中，论坛允许将主题回复固定到评论列表的开头。 已选择默认值。

* **允许拥有权限的成员**

   如果选择，则博客仅允许特权成员通过允许选择[特权成员组](/help/communities/users.md#privileged-members-group)来创建文章。 如果未选择，则允许所有社区成员进行创建。 “默认”为取消选择状态。

* **允许文件上传**

   如果选中，博客将允许成员上传文件。 已选择默认值。

* **允许主题回复**

   如果未选择，博客将允许对文章的回复（评论），但不允许对评论的回复。 已选择默认值。

* **允许专题内容**

   如果选择，则其内容标识为[特色内容](/help/communities/featured.md)。 已选择默认值。

### 目录功能 {#catalog-function}

目录功能允许[enablement community](/help/communities/overview.md#enablement-community)成员浏览未分配给他们的启用资源。 请参阅[为开发人员标记Enablement Resources](/help/communities/tag-resources.md)和[Catalog Essentials](/help/communities/catalog-developer-essentials.md)。

如果社区站点的属性` [Show in Catalog](/help/communities/resources.md)`设置为true，则所有目录中会显示社区站点的所有启用资源和学习路径。 要显式包含资源和学习路径，必须将[pre-filter](/help/communities/catalog-developer-essentials.md#pre-filters)应用到目录。

当添加到模板时，配置允许指定用于配置向站点命名空间显示的标记过滤器的标记访客:

![目录函数](assets/catalog-function.png)

* [标题和URL设置](#title-and-url-settings)

* **选择所有命名空间**

   所选标记命名空间定义哪些标记可供访客选择，以过滤目录中列出的启用资源的列表。
如果选中此选项，则社区站点允许的所有标记命名空间均可用。
如果取消选择，则可以选择社区站点所允许的一个或多个命名空间。
已选择默认值。

### 特色内容函数{#featured-content-function}

特色内容功能是一个页面，其中配置了[特色内容组件](/help/communities/featured.md)，以允许添加和删除评论。

每个组件可允许或禁止功能内容（请参阅[博客函数](#blog-function)、[日历函数](#calendar-function)、[论坛函数](#forum-function)、[标识函数](#ideation-function)和[QnA函数](#qna-function)）。

添加到模板时，唯一的配置是[标题和URL设置](#title-and-url-settings)。

### 文件库功能 {#file-library-function}

文件库函数是一个页面，其中[文件库组件](/help/communities/file-library.md)配置为允许添加和删除注释。

添加到模板时，唯一的配置是[标题和URL设置](#title-and-url-settings)。

### 论坛功能 {#forum-function}

论坛功能是一个页面，其[论坛组件](/help/communities/forum.md)配置为标记、文件上载、跟踪、成员自编辑、投票和审核。

添加到模板时，将打开以下对话框：

#### 配置功能详细信息 {#configuration-function-details-2}

![forum-component1](assets/forum-component1.png)

* [标题和URL设置](#title-and-url-settings)

* **允许固定**

   如果选中，论坛允许将主题回复固定到评论列表的开头。 已选择默认值。

* **允许拥有权限的成员**

   如果选择，则论坛仅允许特权成员通过允许选择[特权成员组](/help/communities/users.md#privileged-members-group)来发布主题。 如果未选择，则允许所有社区成员发布内容。 “默认”为取消选择状态。

* **允许文件上传**

   如果选择，论坛将允许成员上传文件。 已选择默认值。

* **允许主题回复**

   如果未选择，论坛将允许对某个主题进行评论，但不允许对这些评论进行回复。 已选择默认值。

* **允许专题内容**

   如果选择，则组件的内容将标识为[特色内容](/help/communities/featured.md)。 已选择默认值。

### 组函数{#groups-function}

>[!CAUTION]
>
>组函数必须&#x200B;*不*&#x200B;是站点结构或社区站点模板中的&#x200B;*或唯一*&#x200B;函数。
>
>必须首先包含并列出任何其他函数，如[页函数](#page-function)。

组功能使社区成员能够在发布环境的社区站点内创建子社区。

根据[设置](/help/communities/sites-console.md#groupmanagement)在[社区站点模板](/help/communities/sites.md)中包含“组”功能时，这些组可以是公共的或私有的，并且一个或多个社区组模板可配置为在实际创建社区组时(例如从发布环境)提供模板选择。 [社区组模板](/help/communities/tools-groups.md)指定为组页面（如论坛和日历）创建哪些社区功能。

创建社区组时，会为新组动态创建成员组，可向其分配或加入成员。 有关详细信息，请参阅[管理用户和用户组](/help/communities/users.md)。

自Communities [功能包1](/help/communities/deploy-communities.md#latestfeaturepack)起，社区组在创作环境中使用[Communities Sites的组控制台](/help/communities/groups.md)创建，在启用后可在发布环境中创建。

添加到模板时，将打开以下对话框：

![group-template-config](assets/group-template-config.png)

* [标题和URL设置](#title-and-url-settings)

* **选择组模板**

   允许选择一个或多个已启用的组模板的下拉列表，新社区组(在发布环境中)的将来创建者可以从中选择这些模板。

* **允许拥有权限的成员**

   如果选择，则论坛仅允许特权成员通过允许选择[特权成员安全组](/help/communities/users.md#privileged-members-group)来发布主题。 如果未选择，则允许所有社区成员发布内容。 “默认”为取消选择状态。

* **允许发布创建**

   如果选中，授权社区成员可以在发布环境中创建组。 如果取消选择，则只能在创作环境中从“社区站点的组”控制台创建新组（子社区）。
已选择默认值。

### 构思功能 {#ideation-function}

标识函数是包含一个[标识组件](/help/communities/ideation-feature.md)的页面。

添加到模板时，将打开以下对话框，其中指定模板的默认标题和URL名称以及默认显示设置：

![视觉函数](assets/ideation-function.png)

* [标题和URL设置](#title-and-url-settings)

* **允许拥有权限的成员**

   如果选择，则论坛仅允许特权成员通过允许选择[特权成员安全组](/help/communities/users.md#privileged-members-group)来发布主题。 如果未选择，则允许所有社区成员发布内容。 “默认”为取消选择状态。

* **允许文件上传**

   如果选中，则该想法包括让成员上传文件的功能。 已选择默认值。

* **允许主题回复**

   如果未选择，则该想法允许对主题进行回复（评论），但不允许对评论进行回复。 已选择默认值。

* **允许专题内容**

   如果选择，则其内容标识为[特色内容](/help/communities/featured.md)。 已选择默认值。

### 排行榜功能 {#leaderboard-function}

通栏功能是包含一个[通栏组件](/help/communities/enabling-leaderboard.md)的页面。

**注意**:在从包含排行榜功能的社 ** 区模板创建社区站点后，排行榜组件需要进一步配置。指定排行榜组件的[规则](/help/communities/enabling-leaderboard.md#rules-tab)，具体取决于社区站点的[评分和标记](/help/communities/implementing-scoring.md)的配置。

添加到模板时，将打开以下对话框，其中指定模板的默认标题和URL名称以及默认显示设置：

![排行榜对话](assets/leaderboard-dialog.png)

* [标题和URL设置](#title-and-url-settings)

* **显示徽章**

   如果选中此项，则排行榜中将包含标记图标的列。
“默认”为取消选择状态。

* **显示徽章名称**

   如果选中，则排行榜中将包含徽章名称的列。
“默认”为取消选择状态。

* **显示头像**

   如果选择，则会员的头像图像将包含在排行榜中，位于其名称链接旁边，指向其成员用户档案。
“默认”为取消选择状态。

### 页面功能 {#page-function}

页面功能会向社区站点添加一个空白页面，该页面会连接到社区站点的功能中：登录、菜单、通知、消息、主题和品牌。 使用[标准AEM创作模式](/help/sites-authoring/editing-content.md)将内容添加到页面。

添加到模板时，唯一的配置是[标题和URL设置](#title-and-url-settings)。

### 问题与解答功能 {#qna-function}

QnA函数是一个具有[QnA组件](/help/communities/working-with-qna.md)的页面，该组件配置为标记、文件上载、跟踪成员以进行自编辑、投票和审核。

当添加到模板时，配置允许对特权成员进行限制：

![qna-dialog](assets/qna-dialog.png)

* [标题和URL设置](#title-and-url-settings)

* **允许固定**

   如果选中，论坛允许将主题回复固定到评论列表的开头。 已选择默认值。

* **允许拥有权限的成员**

   如果选择，则QnA论坛仅允许特权成员通过允许选择[特权成员组](/help/communities/users.md#privileged-members-group)来发布问题。 如果未选择，则允许所有社区成员发布内容。 “默认”为取消选择状态。

* **允许文件上传**

   如果选中此选项，则“问题与答案”论坛可让成员上传文件。 已选择默认值。

* **允许主题回复**

   如果未选择，则QnA论坛允许对已发布的问题进行评论（回答），但不允许对答案进行答复。 已选择默认值。

* **允许专题内容**

   如果选择，则其内容标识为[特色内容](/help/communities/featured.md)。 已选择默认值。

## 创建社区功能 {#create-community-function}

通过选择位于“社区功能”控制台顶部的`Create Community Function`图标，可以创建社区功能。 可以创建基于相同AEM Blueprint的多个函数，然后通过在作者编辑模式下打开进行唯一自定义。

![create-community-function](assets/create-community-function.png)

### 社区功能名称 {#community-function-name}

![function-name](assets/function-name.png)

在“社区功能名称”面板上，将配置名称、说明以及是否启用了该功能：

* **社区功能名称**

   用于显示和存储的函数名。

* **社区功能描述**

   用于显示的函数描述。

* **已禁用/已启用**

   控制函数是否可引用的切换开关。

### AEM Blueprint {#aem-blueprint}

![aem-blueprint](assets/aem-blueprint.png)

在`AEM Blueprint`面板上，可以选择作为社区函数基础实现的蓝图。

社区功能是一个微型网站，包括一个或多个页面，预先连接以包含在社区网站中，包括登录名、用户用户档案、通知、消息、站点菜单、搜索、主题和品牌功能。 创建函数后，可以在作者编辑模式下[打开函数](#open-community-function)并自定义页面或组件设置。

由于社区函数是作为[blueprint](/help/sites-administering/msm-livecopy.md#creatingablueprint)的[live copy](/help/sites-administering/msm.md#live-copies)实现的，因此可以转出对影响从包含该函数的[社区站点模板](/help/communities/sites.md)或[社区组模板](/help/communities/tools-groups.md)创建的所有社区站点页面的函数所做的更改。 还可以将页面与其父Blueprint取消关联以进行页面级别修改。

另请参阅[多站点管理器](/help/sites-administering/msm.md)。

### 缩略图 {#thumbnail}

![函数缩览图](assets/funtion-thumbnail.png)

在“缩略图”面板上，可以上传图像以在[社区功能控制台](#community-functions-console)中显示。

## 打开社区功能 {#open-community-function}

![开放函数](assets/open-function.png)

选择`Open Community Function`图标以进入创作编辑模式，以创作页面内容并修改功能组件的配置。

### 配置组件 {#configuring-components}

社区功能将作为AEM Blueprint的Live Copy实施，其详细信息将记录在[多站点管理器](/help/sites-administering/msm.md)下。

不仅可以创作页面内容，还可以配置组件。

如果在创建的社区站点的页面上配置组件，则可能需要取消[继承](/help/sites-administering/msm-livecopy.md#changing-live-copy-content)来配置组件。 配置完成后，应重新建立继承。

有关配置详细信息，请访问作者的[社区组件](/help/communities/author-communities.md)。

## 编辑社区功能 {#edit-community-function}

![edit-function](assets/edit-function.png)

选择`Edit Community Function`图标以使用与创建社区函数](#create-community-function)相同的面板编辑函数的属性，包括启用或禁用该函数。[
