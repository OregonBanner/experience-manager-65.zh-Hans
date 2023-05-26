---
title: 审核控制台
seo-title: Moderation Console
description: 如何访问审核控制台
seo-description: How to access the Moderation console
uuid: d3b8a160-85b2-43f4-9891-5fafa8c48c5f
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 404582ab-bb4c-4775-9ae3-17356d376dca
docset: aem65
role: Admin
exl-id: 829da16a-4083-43c1-857d-f2666b363bfc
source-git-commit: 1d334c42088342954feb34f6179dc5b134f81bb8
workflow-type: tm+mt
source-wordcount: '2042'
ht-degree: 4%

---

# 审核控制台 {#moderation-console}

在AEM Communities中，批量 [社区内容的审核](/help/communities/moderate-ugc.md) 管理员和社区审查方（指定为审查方的受信任社区成员）可以在创作和发布环境中使用。

管理员和社区审查方也可以执行 [上下文审核](/help/communities/in-context.md) 在发布环境中。

所有功能 [社区站点](/help/communities/sites-console.md) 是 `Administration` 对具有管理权限登录的用户可用的菜单项。 此 `Administration` 链接提供对审核控制台的访问。

在“审阅”控制台中，管理员和社区审阅人将有权访问他们有权审阅的所有用户生成内容(UGC)。 如果允许审核多个网站，则可以查看所有网站上的帖子或按选定的社区网站进行筛选。

有关更多详细信息，请访问 [管理用户和用户组](/help/communities/users.md).

“审核”控制台支持：

* 正在批量执行审核任务。
* 正在搜索UGC。
* 查看UGC详细信息。
* 查看UGC作者详细信息。

仅当以管理员或以下成员身份登录时 ` [moderator permissions](/help/communities/in-context.md#identifyingtrustedmembers)`，可以执行审核任务。

## 发布环境访问权限 {#publish-environment-access}

通过社区审查方登录时显示的“管理”链接，可从已发布的社区站点访问审查控制台。

![publishweretail](assets/publishweretail.png)

通过选择“管理”链接，将显示“审核”控制台：

![moderation-console-publish](assets/moderation-console-publish.png)

## 创作环境访问权限 {#author-environment-access}

在创作环境中，访问“审核”控制台

* 在全局导航中，选择 **[!UICONTROL Communities]** > **[!UICONTROL 审核]**.

仅以管理员或会员身份登录时 [审查方权限](/help/communities/in-context.md#identifyingtrustedmembers)，可以执行审核任务。 显示的唯一社区内容是允许登录成员审核的内容。

>[!NOTE]
>
>仅当所选的SRP实现公用存储时，发布环境中的UGC才对作者可见。 例如，默认情况下，存储为JSRP，这不是创作和发布的常用存储。 参见 [社区内容存储](/help/communities/working-with-srp.md).

![moderationconsoleauthor](assets/moderationconsoleauthor.png)

## 审核控制台UI {#moderation-console-ui}

将左侧导航边栏放在一边（该边栏显示在创作实例上，但不显示在发布实例上），审核UI包含以下主要区域：

* **[顶部导航栏](#top-navigation-bar)**
* **[工具栏](#toolbar)**
* **[内容区域](#content-area)**

### 顶部导航栏 {#top-navigation-bar}

对于所有控制台，顶部导航栏都是固定的。 有关更多信息，请参阅 [基本处理](/help/sites-authoring/basic-handling.md).

### 工具栏 {#toolbar}

工具栏位于顶部导航栏的下方，在左侧提供以下切换开关：

* [筛选器边栏](/help/communities/moderation.md#filterrail)
打开边栏，允许您选择用于筛选内容的属性。

工具栏位于顶部导航栏的下方，在左侧提供以下切换开关：

![切换开关](assets/toggleswitch.png)

[筛选器边栏](/help/communities/moderation.md#filterrail)
在选择搜索时打开边栏，该边栏允许选择要筛选内容的属性。

![过滤边栏](assets/filterrail.png)

### 内容区域 {#content-area}

内容区域包含有关已发布UGC的信息：

* UGC已发布
* 成员名称
* 成员头像
* 帖子位置。
* 发布时间。
* 对帖子的回复数。
* [情绪](/help/communities/moderate-ugc.md#sentiment) 与帖子关联
* 如果批准，将显示复选标记。
* 如果有附件，则显示回形针。

>[!NOTE]
> 
>内容区域具有 *无限滚动*，这意味着您可以继续滚动，直到内容结束。 即使在滚动时，工具栏也会保留在内容区域上方的固定可见位置。

### 筛选器边栏 {#ootbfilters}

![开放式过滤边栏](assets/open-filterrail.png)

侧面板图标可打开过滤器边栏。 位于内容区域左侧的过滤器边栏提供了不同的过滤器，每个过滤器都会立即影响内容区域中显示的引用UGC。

每个类别中的过滤器包括 **或**&#39;d在一起，不同类别中的过滤器是 **和**&#39;d在一起。

例如，如果同时选中两者 **问题** 和 **答案**，您将看到以下内容之一 **问题** *或* 一个 **答案**.

但是，如果选中 **问题** 和 **待处理**，您只会看到 **问题** 和 **待处理**.

>[!NOTE]
>
>社区审查方可以在审查控制台UI上将预定义过滤器标记为书签。 由于这些过滤器会附加到URL的末尾（作为查询字符串参数），因此审查方可以稍后返回到已添加书签的过滤器，还可以共享这些链接。

![searchicon](assets/searchicon.png)

打开过滤器边栏时，搜索图标可切换关闭的侧面板。 但是，要关闭过滤器边栏并仅查看用户生成的内容，请单击“搜索”图标，然后选择“仅内容”选项。

#### 内容路径 {#content-path}

内容路径将显示的引用UGC限制为放置在指定内容存储库中的帖子。

![内容路径](assets/content-path.png)

#### 文本搜索 {#text-search}

文本搜索将引用的UGC显示限制为包含输入文本的帖子。

![text-search](assets/text-search.png)

#### 站点 {#site}

站点限制将引用的UGC显示给选定社区站点的帖子。 如果未选中任何站点，则会显示对UGC的所有引用。

![site-panel](assets/site-panel.png)

>[!NOTE]
>
>管理员访问批量审核控制台时，将显示对UGC的所有引用，包括未使用创建的站点 [站点创建向导](/help/communities/sites-console.md)，如Geometrixx示例。
>
>当受信任的社区成员在发布时访问批量审核控制台时，则仅显示对该成员有权审核的社区站点创建的UGC引用，并且可以使用站点过滤器进行筛选。

#### 内容类型 {#content-type}

内容类型将引用的UGC显示限制为所选资源类型的帖子。 可以选择以下一种或多种类型。 如果未选择任何类型，则会显示所有类型。

* **注释**
* **论坛 - 主题**
* **论坛回复**
* **问题与解答 - 问题**
* **问题与解答 - 回答**
* **博客文章**
* **博客评论**
* **日历事件**
* **日历注释**
* **文件库文件夹**
* **文件库文档**
* **构思**
* **构思评论**

![内容类型](assets/content-types.png)

#### 其他内容类型 {#additional-content-types}

要添加要筛选的其他资源，请执行以下操作：

* 以管理员身份登录创作实例。
* 打开 [Web控制台](https://localhost:4502/system/console/configMgr).
* 查找 `AEM Communities Moderation Dashboard Filters`.
* 选择要在编辑模式下打开的配置。
* 输入要筛选的组件的资源类型：

   * 例如，要筛选包含的投票组件，请输入：

      `Voting=social/tally/components/hbs/voting`
   ![additional-contenttype](assets/additional-contenttype.png)

* 选择保存。
* 刷新社区 — 审核控制台。

结果是一个新的可选过滤器 `Voting` 在 `Content Type` 筛选组。

选择该过滤器后，功能板的内容将显示与输入的任何资源类型匹配的UGC。

#### 状态 {#status}

状态将引用的UGC限制为仅显示选定状态的帖子，这些状态可以是“待处理”、“已批准”、“已拒绝”或“已关闭”中的一个或多个状态，以及草稿或博客文章预定状态，以及QnA问题的已应答或未应答状态。 如果未选择任何内容，则会显示所有内容。

>[!NOTE]
>
>如果仅选择“未回答”状态，版主将看到除已回答问题之外的所有内容（适用于所有内容类型）。 这是因为在未回答的问题和其他内容（如论坛主题、博客文章或评论）的情况下，不存在负责已回答问题的属性。

![状态](assets/statuses.png)

#### 标记 {#flagging}

标记会将引用的UGC显示限制为已标记或隐藏的帖子。

标记一段内容后，它将保持标记状态，直到您通过选择 **标志** 再次按下按钮。 请注意，没有标记级别，例如重要或跟进。

![标记](assets/flagging.png)

#### 成员 {#members}

成员限制将引用的UGC显示给按输入的成员名称过帐的UGC。

![成员](assets/members.png)

#### 发布于前一 {#posted-in-the-last}

发布在上次限制中引用的UGC显示为在过去小时、天、周、月或年所做的帖子。

![已发布 — 最后](assets/posted-last.png)

#### 情绪 {#sentiment}

[情绪](/help/communities/moderate-ugc.md#sentiment) 将引用的UGC限制为仅显示情绪值为正、负或中性的帖子。

![情绪](assets/sentiment.png)

## 自定义筛选条件 {#custom-filters}

除了开箱即用的过滤器 [筛选器边栏](/help/communities/moderation.md#ootbfilters)，可以向审核UI中添加其他关于元数据的自定义筛选器。 开发人员可以使用Github中的示例代码来扩展现有的审核UI过滤器。

![custom-tag-filter](assets/custom-tag-filter.png)

此 [示例项目](https://github.com/Adobe-Marketing-Cloud/aem-communities-extensions/tree/main/aem-communities-moderation-filter) 在Github上实现了标记过滤器，以根据特定标记是否应用于用户生成的内容来过滤UGC列表。 您可以遵循示例代码，并为其他类似的UGC元数据字段构建类似过滤器。

要安装“标记”过滤器的示例，请执行以下操作：

1. 在AEM创作中打开包管理器(`https://[aem-author]:4502/crx/packmgr/index.jsp`)实例和AEM发布(`https://[aem-publish]:4503/crx/packmgr/index.jsp`)实例。
1. 生成包 `com.adobe.social.sample.moderation.filter.ui.apps-1.0-SNAPSHOT.zip` 从Github代码中，安装并启用该代码。
1. 在AEM创作中打开包控制台( `https://[aem-author]:4502/system/console/bundles`)实例和AEM发布( `https://[aem-publish]:4503/system/console/bundles`)实例。
1. 生成包(`[com](https://sample-moderation-filter.com/).adobe.social.sample.moderation.filter.core-1.0-SNAPSHOT.jar`)，并安装和启用相同功能。
1. 转到 **/apps/social/moderation/facets** AEM作者上的节点(`https://[aem-author]:4502/crx/de/index.jsp#/apps/social/moderation/facets`)和AEM发布(`https://[aem-publish]:4502/crx/de/index.jsp#/apps/social/moderation/facets`)实例。
1. 添加技术用户 **communities-utility-reader** 替换为 `jcr:read` 权限。

要在现有社区网站上显示自定义筛选条件，请执行以下操作：

1. 编辑 `Clientlibs` 现有审核页面的 `/content/we-retail/us/en/community/moderation/shell3/jcr:content/head/clientlibs.`

   * 添加新类别 `cq.social.hbs.moderation.v2.`

1. 转到 `/content/we-retail/us/en/community/moderation/shell3/jcr:content/rails/searchWell/items/filters.`

   * 设置为新组件 `sling:resourceType = social/moderation/v2/filters.`

1. 转到 `/content/we-retail/us/en/community/moderation/shell3/jcr:content/views/content/items/modcontainer`.

   * 设置为新组件 `sling:resourceType = social/moderation/v2/modcontainer`.

## 审核操作 {#moderation-actions}

[审核操作](/help/communities/moderate-ugc.md#moderation-actions) 可以在内容区域或查看内容详细信息时执行一个或多个选择。

要批量审核帖子，请在内容区域中单击选择(![选择](assets/selecticon.png))图标，当鼠标悬停在帖子（桌面）上或按住手指在帖子（移动设备）上时，此图标会显示。 这样，您就可以进入多选模式，现在只需单击后续帖子即可批量审核这些帖子。 使用工具栏上显示的按钮对所选帖子执行审核操作。 所有操作都将提示进行确认。

要在内容区域中审核单个帖子，请使用鼠标（桌面）将鼠标悬停在该帖子上，或者按住帖子（移动设备）上的手指，以使按钮显示在帖子上。 对单个内容详细信息执行操作时，只有删除操作会提示进行确认。

### 审核多个帖子 {#moderating-multiple-posts}

通过单击 `Select` 帖子上的图标：

![选择图标](assets/select-icon.png)

要退出批量选择模式，请选择工具栏上的取消(x)图标：

可以对多个帖子执行的审核操作包括：

* 拒绝
* 删除
* 关闭/重新打开帖子

仅当选择多个帖子时，工具栏上才会显示允许这些操作的图标。

![批量处理](assets/bulkmoderate.png)

### 审核单个帖子 {#moderating-a-single-post}

在单选模式下，可以：

* 通过选择用户名查看用户详细信息。
* 通过选择指向帖子的链接来查看上下文中的帖子。
* [回复](#reply)
* [允许](#allow)
* [拒绝](#deny)
* [删除](#delete)
* [关闭](#close)
* 视图 [审核历史记录](#moderation-history)
* [查看详细信息](#viewdetails)

在信息卡视图上，审核操作图标上方是帖子文本，下方是指示以下内容的数据：

* 如果它有回复，则前有回复的数量。
* 如果已标记。
* 是否已批准。
* UGC发布的时间。

![singleselectmode](assets/singleselectmode.png)

#### 回复 {#reply}

![回复](assets/reply.png)

处理单个帖子时，如果UGC类型支持回复并配置为允许回复，则会显示“回复”图标。

#### 允许 {#allow}

![允许](assets/allow.png)

处理单个帖子时，当帖子被标记或拒绝时，将显示允许图标。 如果已标记，则选择“允许”将清除所有标记。

#### 拒绝 {#deny}

![拒绝](assets/deny.png)

此 **拒绝** 审核操作仅适用于已审核的内容，并且除多选模式外，不会显示在未审核内容上。

未经审核的内容始终获得批准。

已审核的内容最初进入待处理状态，以后可以修改为批准或拒绝。

离开待处理状态的内容无法返回到待处理状态。 标记为“已批准”或“已拒绝”的内容可以随时更改为其他状态。

#### 删除 {#delete}

![删除](assets/delete.png)

在单选或批量模式下，可以选择项目并将其删除。 删除操作会生成一个确认对话框。 删除后，这些项目会立即从内容区域中消失。 **删除UGC后，它将从存储库中永久删除，以后无法检索**.

#### 关闭 {#close}

![关闭](assets/close.png)

处理单个帖子时，如果UGC类型支持防止该资源出现更多帖子的功能，则会显示“关闭”图标。

#### 审核历史记录 {#moderation-history}

![审核](assets/moderation.png)

处理单个帖子时，将鼠标悬停在该帖子上时，将显示“审核历史记录”图标。 选择该图标将显示一个窗格，其中包含对UGC帖子采取的操作历史记录。

要返回到多个UGC帖子的内容区域显示，请选择视图详细信息窗格右上角的X。

例如：

![moderation-history](assets/moderation-history.png)

#### 查看详细信息 {#view-detail}

![视图](assets/view.png)

使用单个帖子时，可以通过在详细信息模式下打开UGC来查看更多详细信息。

为此，请将鼠标悬停在帖子上以显示 `View Detail` 图标并选择它以显示包含帖子更多详细信息的面板。

要返回到多个UGC帖子的内容区域显示，请选择视图详细信息窗格右上角的X。

例如：

![view1](assets/view1.png)
