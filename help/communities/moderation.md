---
title: 审核控制台
seo-title: 审核控制台
description: 如何访问审核控制台
seo-description: 如何访问审核控制台
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
source-wordcount: '2050'
ht-degree: 4%

---

# 审核控制台 {#moderation-console}

在AEM Communities中，管理员和社区审核者（分配为审核者的受信任社区成员）可以在创作和发布环境中批量审核社区内容[审核](/help/communities/moderate-ugc.md)。

管理员和社区审核者还可以在发布环境中执行[上下文内审核](/help/communities/in-context.md)。

所有[社区站点](/help/communities/sites-console.md)的功能是`Administration`菜单项，可供具有管理权限登录的用户使用。 `Administration`链接提供对审核控制台的访问权限。

从“审核”控制台中，管理员和社区审核者将有权访问所有用户生成的内容(UGC)，他们有权对其进行审核。 如果允许审核多个网站，则可以查看所有网站中的帖子或按选定的社区网站进行过滤。

有关更多详细信息，请访问[管理用户和用户组](/help/communities/users.md)。

审核控制台支持：

* 批量执行审核任务。
* 正在搜索UGC。
* 查看UGC详细信息。
* 查看UGC作者详细信息。

只有以管理员或` [moderator permissions](/help/communities/in-context.md#identifyingtrustedmembers)`的成员身份登录后，才能执行审核任务。

## 发布环境访问 {#publish-environment-access}

从已发布的社区站点访问审核控制台时，会通过管理链接，该链接在社区审核者登录时显示。

![publishweretail](assets/publishweretail.png)

通过选择管理链接，将显示审核控制台：

![moderation-console-publish](assets/moderation-console-publish.png)

## 创作环境访问 {#author-environment-access}

在创作环境中，访问审核控制台

* 从全局导航中，选择&#x200B;**[!UICONTROL Communities]** > **[!UICONTROL Moderation]**。

只有以管理员身份登录或以具有[审核者权限](/help/communities/in-context.md#identifyingtrustedmembers)的成员身份登录时，才能执行审核任务。 显示的唯一社区内容是允许登录的成员审核的社区内容。

>[!NOTE]
>
>仅当所选SRP实施公共存储时，发布环境中的UGC才会在创作时可见。 例如，默认情况下，存储为JSRP，它不是创作和发布的常用存储。 请参阅[社区内容存储](/help/communities/working-with-srp.md)。

![moderationconsoleauthor](assets/moderationconsoleauthor.png)

## 审核控制台UI {#moderation-console-ui}

将左侧导航边栏（在创作中显示，但在发布中不显示）放在一边，审核UI的主要区域如下：

* **[顶部导航栏](#top-navigation-bar)**
* **[工具栏](#toolbar)**
* **[内容区域](#content-area)**

### 顶部导航栏 {#top-navigation-bar}

对于所有控制台，顶部导航栏都是常量。 有关更多信息，请参阅[基本操作](/help/sites-authoring/basic-handling.md)。

### 工具栏 {#toolbar}

位于顶部导航栏下方的工具栏在左侧提供了以下切换开关：

* [过](/help/communities/moderation.md#filterrail)
滤器栏会打开一个边栏，供您选择过滤内容的属性。

位于顶部导航栏下方的工具栏在左侧提供了以下切换开关：

![托格勒施维奇](assets/toggleswitch.png)

[在选](/help/communities/moderation.md#filterrail)
择“搜索”时，过滤器栏会打开一个边栏，该边栏允许您选择过滤内容的属性。

![过滤器](assets/filterrail.png)

### 内容区域 {#content-area}

内容区域包含有关已发布的UGC的信息：

* 已发布UGC
* 成员名称
* 会员头像
* 帖子的位置。
* 发布时。
* 帖子的回复数。
* [](/help/communities/moderate-ugc.md#sentiment) 与帖子关联的情绪
* 如果已批准，则会显示复选标记。
* 如果存在附件，则显示平装夹。

>[!NOTE]
> 
>内容区域具有&#x200B;*无限滚动*，这意味着它允许您继续滚动直到内容结束。 即使在滚动时，工具栏仍会停留在内容区域上方的固定可见位置。

### 过滤器边栏 {#ootbfilters}

![开放过滤器边栏](assets/open-filterrail.png)

侧面板图标可打开过滤器边栏。 显示在内容区域左侧的过滤器边栏提供了不同的过滤器，每个过滤器对显示在内容区域中的引用UGC具有直接影响。

每个类别中的过滤器是&#x200B;**OR**&#39;d，不同类别中的过滤器是&#x200B;**AND**&#39;d。

例如，如果同时检查&#x200B;**问题**&#x200B;和&#x200B;**答案**，您将看到以下内容：**问题** *或***答案**。

但是，如果选中&#x200B;**Question**&#x200B;和&#x200B;**Pending**，您将只看到属于&#x200B;**Question**&#x200B;且为&#x200B;**Pending**&#x200B;的内容。

>[!NOTE]
>
>社区审核者可以为审核控制台UI中预定义的过滤器添加书签。 由于这些过滤器会附加到URL的末尾（作为查询字符串参数），审核者稍后可以返回到已添加书签的过滤器，并且还可以共享这些链接。

![searchicon](assets/searchicon.png)

打开过滤器边栏时，“搜索”图标可切换关闭侧面板。 但是，要关闭过滤器边栏并仅查看用户生成的内容，请单击搜索图标，然后选择仅内容选项。

#### 内容路径 {#content-path}

内容路径将显示的引用UGC限制为放置在指定内容存储库中的帖子。

![内容路径](assets/content-path.png)

#### 文本搜索 {#text-search}

文本搜索将引用的UGC限制为包含输入文本的帖子。

![文本搜索](assets/text-search.png)

#### 站点 {#site}

网站将引用的UGC显示给选定社区网站的帖子限制为。 如果未选中任何网站，则会显示对UGC的所有引用。

![站点面板](assets/site-panel.png)

>[!NOTE]
>
>当管理员访问批量审核控制台时，将显示对UGC的所有引用，包括未通过[站点创建向导](/help/communities/sites-console.md)创建的站点，如Geometrixx示例。
>
>当受信任的社区成员在发布时访问批量审核控制台时，只会显示对为其有权审核的社区站点创建的UGC的引用，并且可以使用站点过滤器进行过滤。

#### 内容类型 {#content-type}

内容类型将引用的UGC限制为显示给选定资源类型的帖子。 可以选择以下一种或多种类型。 如果未选择任何类型，则会显示所有类型。

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

* 以管理员身份登录到创作实例。
* 打开[Web控制台](https://localhost:4502/system/console/configMgr)。
* 找到`AEM Communities Moderation Dashboard Filters`。
* 选择要在编辑模式下打开的配置。
* 输入要筛选的组件的ResourceType:

   * 例如，要筛选包含的投票组件，请输入：

      `Voting=social/tally/components/hbs/voting`
   ![additional-contenttype](assets/additional-contenttype.png)

* 选择保存。
* 刷新“社区 — 审核”控制台。

结果会为`Content Type`筛选器组下的`Voting`提供一个新的可选筛选器。

选择该过滤器后，功能板的内容将显示与输入的任何资源类型匹配的UGC。

#### 状态 {#status}

状态将引用的UGC限制为显示给选定状态（可能是“待定”、“已批准”、“拒绝”或“已关闭”中的一个或多个，以及“为博客文章草稿”或“已计划”、“已回答或未回答问题”中的一个或多个）的帖子。 如果未选择任何内容，则会显示所有内容。

>[!NOTE]
>
>如果仅选择“未回答”状态，则审核者将看到除已回答问题之外的所有内容（适用于所有内容类型）。 这是因为在未回答的问题和其他内容（如论坛主题、博客文章或评论）中，不存在负责回答问题的属性。

![状态](assets/statuses.png)

#### 标记 {#flagging}

标记将所引用的UGC限制为显示给标记或隐藏的帖子。

标记某段内容后，它会一直标记，直到您再次选择&#x200B;**标记**&#x200B;按钮来取消该段内容的标记。 请注意，没有标记级别，如重要或后续操作。

![衰落](assets/flagging.png)

#### 成员 {#members}

成员将所引用的UGC显示的UGC限制为由输入的成员名称发布的UGC。

![成员](assets/members.png)

#### 发布于前一 {#posted-in-the-last}

在“最后”限制中发布引用的UGC显示给在最后一小时、一天、一周、一个月或一年发布的帖子。

![最近发布](assets/posted-last.png)

#### 情绪 {#sentiment}

[](/help/communities/moderate-ugc.md#sentiment) 情绪将引用的UGC限制为具有正面、负面或中性情绪值的帖子显示。

![情绪](assets/sentiment.png)

## 自定义过滤器 {#custom-filters}

除了[过滤器边栏](/help/communities/moderation.md#ootbfilters)中的现成过滤器之外，还可以将有关元数据的其他自定义过滤器添加到审核UI中。 开发人员可以使用Github中的示例代码来扩展现有的审核UI过滤器。

![custom-tag-filter](assets/custom-tag-filter.png)

Github上的[示例项目](https://github.com/Adobe-Marketing-Cloud/aem-communities-extensions/tree/main/aem-communities-moderation-filter)实施了标记过滤器，以根据特定标记是否应用于用户生成的内容来筛选UGC列表。 您可以按照示例代码为其他类似的UGC元数据字段构建类似过滤器。

要安装标记过滤器的示例，请执行以下操作：

1. 在AEM创作(`https://[aem-author]:4502/crx/packmgr/index.jsp`)实例和AEM发布(`https://[aem-publish]:4503/crx/packmgr/index.jsp`)实例上打开包管理器。
1. 从Github代码构建包`com.adobe.social.sample.moderation.filter.ui.apps-1.0-SNAPSHOT.zip`，并安装并启用该包。
1. 在AEM创作(`https://[aem-author]:4502/system/console/bundles`)实例和AEM发布(`https://[aem-publish]:4503/system/console/bundles`)实例上打开包控制台。
1. 从Github构建包(`[com](https://sample-moderation-filter.com/).adobe.social.sample.moderation.filter.core-1.0-SNAPSHOT.jar`)，并安装并启用该包。
1. 转到AEM创作(`https://[aem-author]:4502/crx/de/index.jsp#/apps/social/moderation/facets`)和AEM发布(`https://[aem-publish]:4502/crx/de/index.jsp#/apps/social/moderation/facets`)实例上的&#x200B;**/apps/social/moderation/facets**&#x200B;节点。
1. 添加具有`jcr:read`权限的技术用户&#x200B;**communities-utility-reader**。

要在现有社区网站上显示自定义过滤器，请执行以下操作：

1. 编辑现有审核页面`/content/we-retail/us/en/community/moderation/shell3/jcr:content/head/clientlibs.`的`Clientlibs`

   * 添加新类别`cq.social.hbs.moderation.v2.`

1. 转到 `/content/we-retail/us/en/community/moderation/shell3/jcr:content/rails/searchWell/items/filters.`

   * 设置为新组件`sling:resourceType = social/moderation/v2/filters.`

1. 转到 `/content/we-retail/us/en/community/moderation/shell3/jcr:content/views/content/items/modcontainer`.

   * 设置为新组件`sling:resourceType = social/moderation/v2/modcontainer`。

## 审核操作 {#moderation-actions}

[审核](/help/communities/moderate-ugc.md#moderation-actions) 操作可在内容区域中或查看内容详细信息时对一个或多个选择执行。

要批量审核帖子，请在内容区域中单击帖子上的选择(![selecticon](assets/selecticon.png))图标，当将鼠标悬停在帖子上时（桌面）会显示该图标，或者在帖子（移动设备）上按住手指。 通过此操作，您可以进入多选模式，现在只需单击即可选择要批量审核的后续帖子。 使用工具栏中显示的按钮对选定的帖子执行审核操作。 所有操作都将提示进行确认。

要审核内容区域中的单个帖子，请将鼠标悬停在该帖子上（桌面），或按住该帖子（移动设备）上的手指，以便在帖子上显示按钮。 对单个内容详细信息进行操作时，只有删除操作会提示进行确认。

### 审核多个帖子 {#moderating-multiple-posts}

通过单击帖子上的`Select`图标进入批量选择模式：

![选择图标](assets/select-icon.png)

要退出批量选择模式，请选择工具栏上的取消(x)图标：

可对多个帖子执行的审核操作包括：

* 拒绝
* 删除
* 关闭/重新打开帖子

仅当选择了多个帖子时，工具栏上才会显示允许这些操作的图标。

![批量审核](assets/bulkmoderate.png)

### 审核单个帖子 {#moderating-a-single-post}

在单选模式下，可以：

* 通过选择用户的名称查看用户详细信息。
* 通过选择指向帖子的链接，查看帖子的上下文关联。
* [回复](#reply)
* [允许](#allow)
* [拒绝](#deny)
* [删除](#delete)
* [关闭](#close)
* 查看[审核历史记录](#moderation-history)
* [查看详细信息](#viewdetails)

审核操作图标上方的卡片视图中显示的是帖子的文本，下面显示的是指示以下内容的数据：

* 如果有答复，则在答复数前加上。
* 已标记。
* 如果已批准。
* 发布UGC时。

![单选模式](assets/singleselectmode.png)

#### 回复 {#reply}

![回复](assets/reply.png)

处理单个帖子时，如果UGC类型支持回复并配置为允许回复，则会显示“回复”图标。

#### 允许 {#allow}

![允许](assets/allow.png)

处理单个帖子时，当该帖子被标记或拒绝时，将显示允许图标。 如果已标记，则选择允许将清除所有标记。

#### 拒绝 {#deny}

![拒绝](assets/deny.png)

**拒绝**&#x200B;审核操作仅适用于已审核的内容，除非在多选模式下，否则不会显示在未审核的内容上。

未审核的内容将始终获得批准。

已审核的内容最初进入“待定”状态，之后可修改为被批准或拒绝。

离开待定状态的内容永远无法返回到待定状态。 标记为已批准或已拒绝的内容可随时更改为其他状态。

#### 删除 {#delete}

![删除](assets/delete.png)

在单选或批量模式下，可以选择并删除项目。 删除操作会导致出现确认对话框。 删除后，这些项目会立即从内容区域中消失。 **删除UGC后，该UGC将从存储库中永久删除，以后将无法检索**。

#### 关闭 {#close}

![关闭](assets/close.png)

处理单个帖子时，如果UGC类型支持阻止该资源进一步发布的功能，则会显示“关闭”图标。

#### 审核历史记录 {#moderation-history}

![审核](assets/moderation.png)

处理单个帖子时，将鼠标悬停在该帖子上方时，将显示“审核历史记录”图标。 选择该图标将显示一个窗格，其中包含对UGC帖子采取的操作历史记录。

要返回到显示多个UGC帖子的内容区域，请选择视图详细信息窗格右上角的X。

例如：

![审核历史](assets/moderation-history.png)

#### 查看详细信息 {#view-detail}

![视图](assets/view.png)

使用单个帖子时，可以通过在详细模式下打开UGC来查看更多详细信息。

为此，请将鼠标悬停在帖子上以显示`View Detail`图标，然后选择该图标以显示包含帖子更多详细信息的面板。

要返回到显示多个UGC帖子的内容区域，请选择视图详细信息窗格右上角的X。

例如：

![view1](assets/view1.png)
