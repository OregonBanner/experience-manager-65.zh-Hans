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
translation-type: tm+mt
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '2110'
ht-degree: 3%

---


# 审核控制台{#moderation-console}

在AEM Communities，管理员和社区版主（指定为版主的受信任社区成员）可以从作者和发布环境中批量[审核社区内容](/help/communities/moderate-ugc.md)。

管理员和社区管理者还可以在发布环境中执行[上下文内协调](/help/communities/in-context.md)。

所有[社区站点](/help/communities/sites-console.md)的功能是一个`Administration`菜单项，用户可以使用管理权限登录。 `Administration`链接提供对审核控制台的访问。

从审核控制台中，管理员和社区审核者将有权访问其有权审核的所有用户生成的内容(UGC)。 如果允许审核多个站点，则可以跨所有站点视图帖子或按选定社区站点进行筛选。

有关详细信息，请访问[管理用户和用户组](/help/communities/users.md)。

审核控制台支持：

* 批量执行审核任务。
* 搜索UGC。
* 查看UGC详细信息。
* 查看UGC作者详细信息。

仅当以管理员或` [moderator permissions](/help/communities/in-context.md#identifyingtrustedmembers)`成员身份登录时，才能执行审核任务。

## 发布环境访问{#publish-environment-access}

从已发布的社区站点访问审核控制台是通过管理链接，当社区审核者登录时会显示该链接。

![publishweretail](assets/publishweretail.png)

通过选择“管理”链接，将显示“审核”控制台：

![仲裁控制台——发布](assets/moderation-console-publish.png)

## 作者环境访问{#author-environment-access}

在创作环境中，要访问审核控制台

* 在全局导航中，选择&#x200B;**[!UICONTROL Communities]** > **[!UICONTROL 仲裁]**。

仅当以管理员身份登录或以[审查方权限](/help/communities/in-context.md#identifyingtrustedmembers)的成员身份登录时，才能执行审核任务。 显示的唯一社区内容是允许登录成员审核的社区内容。

>[!NOTE]
>
>只有在所选SRP实现公共存储时，发布环境中的UGC才在作者中可见。 例如，默认存储为JSRP，它不是创作和发布的常用存储。 请参阅[社区内容存储](/help/communities/working-with-srp.md)。

![moderationconsoleauthor](assets/moderationconsoleauthor.png)

## 仲裁控制台UI {#moderation-console-ui}

除左侧导航边栏（在作者中显示，但在发布中不显示）外，协调UI具有以下主要区域：

* **[顶部导航栏](#top-navigation-bar)**
* **[工具栏](#toolbar)**
* **[内容区域](#content-area)**

### 顶部导航栏{#top-navigation-bar}

顶部导航栏对所有控制台都是常量。 有关详细信息，请参阅[基本操作](/help/sites-authoring/basic-handling.md)。

### 工具栏 {#toolbar}

工具栏位于顶部导航栏下方，在左侧提供以下切换开关：

* [筛](/help/communities/moderation.md#filterrail)
选栏会打开边栏，允许选择筛选内容的属性。

工具栏位于顶部导航栏下方，在左侧提供以下切换开关：

![雪巫](assets/toggleswitch.png)

[在选](/help/communities/moderation.md#filterrail)
择“搜索”时，过滤器栏会打开一个边栏，通过该边栏可以选择要过滤内容的属性。

![过滤器](assets/filterrail.png)

### 内容区域 {#content-area}

内容区域包含已发布UGC的信息：

* UGC已发布
* 成员名称
* 成员头像
* 帖子的位置。
* 发布时。
* 帖子的回复数。
* [与](/help/communities/moderate-ugc.md#sentiment) 帖子相关的情感
* 如果批准，则显示复选标记。
* 如果存在附件，则显示一个平装夹。

>[!NOTE]
> 
>内容区域具有&#x200B;*无限滚动*，这意味着它允许您继续滚动直到内容结束。 即使在滚动时，工具栏仍保留在内容区域上方的固定可见位置。

### 过滤器边栏{#ootbfilters}

![开放式滑轨](assets/open-filterrail.png)

侧面板图标可打开筛选器边栏。 显示在内容区域左侧的筛选器边栏提供不同的过滤器符，每个边栏对内容区域中显示的引用UGC有即时影响。

每个类别内的过滤器一起为&#x200B;**OR**&#39;d，不同类别内的过滤器一起为&#x200B;**AND**&#39;d。

例如，如果同时检查&#x200B;**问题**&#x200B;和&#x200B;**答案**，您将看到&#x200B;**问题** *或*&#x200B;和&#x200B;**答案**&#x200B;的内容。

但是，如果选中&#x200B;**问题**&#x200B;和&#x200B;**挂起**，您将只看到&#x200B;**问题**&#x200B;且是&#x200B;**挂起**&#x200B;的内容。

>[!NOTE]
>
>社区版主可以在审核控制台UI上为预定义的过滤器加书签。 当这些过滤器附加到URL的末尾(作为查询字符串参数)时，版主可以稍后返回已添加书签的过滤器，并共享这些链接。

![search图标](assets/searchicon.png)

当过滤器边栏打开时，“搜索”图标将切换侧面板关闭。 但是，要关闭筛选器边栏并仅视图用户生成的内容，请单击“搜索”图标，然后选择“仅限内容”选项。

#### 内容路径 {#content-path}

内容路径将所显示的引用UGC限制为放置在指定内容存储库中的帖子。

![内容路径](assets/content-path.png)

#### 文本搜索 {#text-search}

文本搜索将引用的UGC限制为包含输入文本的帖子显示。

![文本搜索](assets/text-search.png)

#### 站点 {#site}

站点将所引用的UGC显示限制为发布到所选社区站点。 如果未选中任何站点，则显示对UGC的所有引用。

![站点面板](assets/site-panel.png)

>[!NOTE]
>
>管理员访问批量审核控制台时，将显示对UGC的所有引用，包括未使用[站点创建向导](/help/communities/sites-console.md)创建的站点，如Geometrixx示例。
>
>当受信任的社区成员在发布时访问批量审核控制台时，只会显示对为该成员被授权审核的社区站点创建的UGC的引用，并且可以使用站点过滤器进行过滤。

#### 内容类型 {#content-type}

内容类型将引用的UGC显示限制为所选资源类型的帖子。 可选择以下一种或多种类型。 如果未选择任何类型，则显示所有类型。

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

#### 其他内容类型{#additional-content-types}

要添加要筛选的其他资源，请执行以下操作：

* 以管理员身份登录到您的创作实例。
* 打开[Web控制台](https://localhost:4502/system/console/configMgr)。
* 找到`AEM Communities Moderation Dashboard Filters`。
* 选择要在编辑模式下打开的配置。
* 输入要筛选的组件的ResourceType:

   * 例如，要筛选包含的投票组件，请输入：

      `Voting=social/tally/components/hbs/voting`
   ![additional-contenttype](assets/additional-contenttype.png)

* 选择保存。
* 刷新社区——审核控制台。

结果为`Content Type`过滤器组下的`Voting`提供了一个新的可选过滤器。

选择该过滤器后，仪表板的内容将显示与输入的任何资源类型相匹配的UGC。

#### 状态 {#status}

状态将引用的UGC限制为所选状态的帖子显示，这些帖子可能是一个或多个“待定”、“已批准”、“已拒绝”或“已关闭”，以及博客文章的“草稿”或“已预定”，以及“已回答或未回答问题”。 如果未选择任何内容，则显示所有内容。

>[!NOTE]
>
>如果仅选择“未回答”状态，则审查方将看到除已回答问题外的所有内容（适用于所有内容类型）。 之所以如此，是因为在未回答的问题和其他内容（如论坛主题、博客文章或评论）的情况下，不存在负责回答问题的属性。

![状态](assets/statuses.png)

#### 标记 {#flagging}

标记将引用的UGC显示限制为标记或隐藏的帖子。

标记某个内容后，它会一直被标记，直到您再次选择&#x200B;**标记**&#x200B;按钮取消标记该内容为止。 请注意，不存在标记级别，如重要或后续操作。

![衰](assets/flagging.png)

#### 成员 {#members}

成员将所引用的UGC显示为由输入的成员名称发布的UGC。

![成员](assets/members.png)

#### 发布于前一 {#posted-in-the-last}

在最后一个限制中发布引用的UGC显示在最后一小时、一天、一周、月或年内发布的帖子中。

![已过帐——上次](assets/posted-last.png)

#### 情绪 {#sentiment}

[感](/help/communities/moderate-ugc.md#sentiment) 情将引用的UGC限制为以正面、负面或中性的情绪值显示的帖子。

![情感](assets/sentiment.png)

## 自定义过滤器{#custom-filters}

除了[筛选器边栏](/help/communities/moderation.md#ootbfilters)中的开箱即用过滤器外，还可以将元数据的其他自定义过滤器添加到仲裁UI。 开发人员可以使用Github中的示例代码扩展现有的协调UI过滤器。

![custom-tag-filter](assets/custom-tag-filter.png)

Github上的[示例项目](https://github.com/Adobe-Marketing-Cloud/aem-communities-extensions/tree/main/aem-communities-moderation-filter)实现了标记过滤器，以根据特定标记是否应用于用户生成的内容来过滤UGC列表。 您可以按照示例代码，为其他类似的UGC元数据字段构建类似过滤器。

要安装“标记”过滤器的示例，请执行以下操作：

1. 打开AEM作者([https://[aem-author]:4502/crx/packmgr/index.jsp](https://aem65-communities-demo.corp.adobe.com:4502/crx/packmgr/index.jsp))实例和AEM发布([https://[aem-publish]:4503/crx/packmgr/index.jsp](https://aem65-communities-demo.corp.adobe.com:4502/crx/packmgr/index.jsp))实例上的包管理器。
1. 从Github代码构建包`com.adobe.social.sample.moderation.filter.ui.apps-1.0-SNAPSHOT.zip`，并安装并启用它。
1. 在AEM作者(`https://[aem-author]:4502/system/console/bundles`)实例和AEM发布(`https://[aem-publish]:4503/system/console/bundles`)实例上打开捆绑控制台。
1. 从Github构建包` [com](https://sample-moderation-filter.com/).adobe.social.sample.moderation.filter.core-1.0-SNAPSHOT.jar`，并安装并启用该包。
1. 转到AEM作者([https://[aem-author]:4502/crx/de/index.jsp#/apps/social/仲裁/facets](https://aem65-communities-demo.corp.adobe.com:4502/crx/de/index.jsp#/apps/social/moderation/facets))和AEM发布([https://[aem-publish]:4502/crx/de/index.jsp#/apps/social/仲裁/facets](https://aem65-communities-demo.corp.adobe.com:4502/crx/de/index.jsp#/apps/social/moderation/facets))实例上的&#x200B;**节点。**
1. 添加具有`jcr:read`权限的技术用户&#x200B;**communities-utility-reader**。

在现有社区站点上公开自定义过滤器:

1. 编辑现有审核页面`/content/we-retail/us/en/community/moderation/shell3/jcr:content/head/clientlibs.`的`Clientlibs`

   * 添加新类别`cq.social.hbs.moderation.v2.`

1. 转到 `/content/we-retail/us/en/community/moderation/shell3/jcr:content/rails/searchWell/items/filters.`

   * 设置为新组件`sling:resourceType = social/moderation/v2/filters.`

1. 转到 `/content/we-retail/us/en/community/moderation/shell3/jcr:content/views/content/items/modcontainer`.

   * 设置为新组件`sling:resourceType = social/moderation/v2/modcontainer`。

## 协调操作{#moderation-actions}

[在内](/help/communities/moderate-ugc.md#moderation-actions) 容区域中或查看内容详细信息时，对一个或多个选择执行协调操作扫描。

要批量审核帖子，请在内容区域中单击帖子上的“选择”(![selecticon](assets/selecticon.png))图标，当用鼠标（桌面）将指针悬停在帖子上时，该图标会显示在帖子上，或者用手指在帖子上（移动）。 通过执行此操作，您进入多选模式，现在只需单击即可选择要批量审核的后续帖子。 使用工具栏上显示的按钮对选定的帖子执行审核操作。 所有操作都将提示进行确认。

要审核内容区域中的单个帖子，请用鼠标（桌面）将鼠标悬停在该帖子上，或按住该帖子（移动）上的手指，使帖子上显示按钮。 在单个内容详细信息上操作时，只有删除操作会提示您进行确认。

### 协调多个帖子{#moderating-multiple-posts}

单击帖子上的`Select`图标，进入批量选择模式：

![select-icon](assets/select-icon.png)

要退出批量选择模式，请选择工具栏中的取消(x)图标：

可以对多个帖子执行的审核操作包括：

* 拒绝
* 删除
* 关闭／重新打开帖子

仅当选择多个帖子时，工具栏上才会显示允许这些操作的图标。

![bulverate](assets/bulkmoderate.png)

### 协调单个帖子{#moderating-a-single-post}

在单选模式下，可以：

* 视图用户详细信息，方法是选择用户名。
* 视图帖子的上下文，方法是选择指向帖子的链接。
* [回复](#reply)
* [允许](#allow)
* [拒绝](#deny)
* [删除](#delete)
* [关闭](#close)
* 视图[协调历史记录](#moderation-history)
* [查看详细信息](#viewdetails)

审核操作图标上方的卡片视图上显示帖子的文本，下面显示的数据表示：

* 如果有回复，则在回复数前加上。
* 如果已标记。
* 如果已获批准。
* UGC发布时。

![单选电模式](assets/singleselectmode.png)

#### 回复 {#reply}

![回复](assets/reply.png)

处理单个帖子时，如果UGC类型支持回复并配置为允许回复，则将显示回复图标。

#### 允许 {#allow}

![允许](assets/allow.png)

处理单个帖子时，当帖子已被标记或拒绝时，将显示“允许”图标。 如果已标记，则选择“允许”将清除所有标记。

#### 拒绝 {#deny}

![拒绝](assets/deny.png)

**拒绝**&#x200B;审核操作仅适用于已审核的内容，除多选模式外，未审核的内容上不显示该操作。

未审核的内容始终会得到批准。

已审核的内容最初进入“待定”状态，之后可修改为“已批准”或“已拒绝”。

离开待处理状态的内容永远不会返回到待处理状态。 标记为已批准或已拒绝的内容可随时更改为其他状态。

#### 删除 {#delete}

![删除](assets/delete.png)

在单选模式或批量模式下，可以选择项目并将其删除。 删除操作会生成确认对话框。 删除后，这些项目会立即从内容区域中消失。 **删除UGC后，它将从存储库中永久删除，以后将无法检索**。

#### 关闭 {#close}

![关闭](assets/close.png)

处理单个帖子时，如果UGC类型支持阻止该资源的进一步帖子的功能，则将显示“关闭”图标。

#### 审核历史记录 {#moderation-history}

![审核](assets/moderation.png)

处理单个帖子时，将鼠标悬停在其上方时将显示“审核历史记录”图标。 选择该图标将显示一个窗格，其中包含对UGC帖子所执行操作的历史记录。

要返回到显示多个UGC帖子的内容区域，请选择视图详细信息窗格右上角的X。

例如：

![协调历史](assets/moderation-history.png)

#### 查看详细信息 {#view-detail}

![视图](assets/view.png)

处理单个帖子时，可以在详细信息模式下打开UGC来查看更多详细信息。

为此，请将鼠标悬停在帖子上以显示`View Detail`图标，然后选择它以显示包含帖子更多详细信息的面板。

要返回到显示多个UGC帖子的内容区域，请选择视图详细信息窗格右上角的X。

例如：

![视图1](assets/view1.png)

